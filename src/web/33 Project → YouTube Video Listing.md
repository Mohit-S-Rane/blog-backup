# 🎬 Build a YouTube Video Listing Page with FreeAPI and JavaScript

Ever wanted to build your own **YouTube-style** video grid? Imagine a page that fetches real videos, shows thumbnails, titles, channel names, and even lets you search—all using a **public API**!

Let’s create that today 👇

---

## 🚧 What Are We Building?

A simple YouTube video explorer using:

✅ Public API (FreeAPI YouTube endpoint)

✅ Grid UI like YouTube

✅ Thumbnails, titles, channels

✅ Click to open videos on YouTube

✅ Search bar with instant frontend filtering

✅ All using plain **HTML + CSS + JavaScript**

---

## 🔗 API We’ll Use

**Endpoint:**

```
GET https://api.freeapi.app/api/v1/public/youtube/videos

```

**Docs:**

https://freeapi.hashnode.space/api-guide/apireference/getYoutubeVideos

No auth key needed. Just fetch and go!

---

## 📁 File Structure

```
📂 youtube-app/
│
├── index.html
├── styles.css
└── script.js

```

---

## 🧱 Step 1: HTML Skeleton

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>YouTube Video Listing</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <h1>🎬 YouTube Explorer</h1>

  <input type="text" id="search" placeholder="Search videos..." />

  <div id="video-grid" class="grid"></div>

  <script src="script.js"></script>
</body>
</html>

```

---

## 🎨 Step 2: CSS for Grid UI

```css
/* styles.css */
body {
  font-family: sans-serif;
  padding: 1rem;
  background-color: #f9f9f9;
}

h1 {
  text-align: center;
}

#search {
  width: 100%;
  max-width: 400px;
  padding: 0.5rem;
  margin: 1rem auto;
  display: block;
  font-size: 1rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
}

.video-card {
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 0 5px rgba(0,0,0,0.1);
  cursor: pointer;
  transition: transform 0.2s ease;
}

.video-card:hover {
  transform: scale(1.03);
}

.thumbnail {
  width: 100%;
  height: 150px;
  object-fit: cover;
}

.info {
  padding: 0.5rem;
}

.title {
  font-weight: bold;
  margin: 0.5rem 0;
}

.channel {
  color: gray;
  font-size: 0.9rem;
}

```

---

## 🚀 Step 3: JavaScript to Fetch & Display Videos

```
// script.js
const API_URL = 'https://api.freeapi.app/api/v1/public/youtube/videos';
let allVideos = [];

async function fetchVideos() {
  try {
    const res = await fetch(API_URL);
    const data = await res.json();
    allVideos = data.data || [];
    renderVideos(allVideos);
  } catch (err) {
    console.error("Failed to fetch videos:", err);
  }
}

function renderVideos(videos) {
  const grid = document.getElementById('video-grid');
  grid.innerHTML = "";

  videos.forEach(video => {
    const card = document.createElement('div');
    card.className = 'video-card';
    card.innerHTML = `
      <img class="thumbnail" src="${video.snippet.thumbnails.medium.url}" alt="${video.snippet.title}" />
      <div class="info">
        <div class="title">${video.snippet.title}</div>
        <div class="channel">${video.snippet.channelTitle}</div>
      </div>
    `;
    card.addEventListener('click', () => {
      window.open(`https://www.youtube.com/watch?v=${video.id.videoId}`, '_blank');
    });

    grid.appendChild(card);
  });
}

```

---

## 🔍 Step 4: Frontend Search Functionality

We’re not making another API call here. We’ll just **filter the already-fetched videos**.

```
document.getElementById('search').addEventListener('input', (e) => {
  const term = e.target.value.toLowerCase();
  const filtered = allVideos.filter(video =>
    video.snippet.title.toLowerCase().includes(term) ||
    video.snippet.channelTitle.toLowerCase().includes(term)
  );
  renderVideos(filtered);
});

```

---

## 🖼️ Example Result (UI Preview)

```
[ 🎬 YouTube Explorer ]

[ 🔍 Search Bar ]

[ Thumbnail ]  [ Thumbnail ]  [ Thumbnail ]
[ Title     ]  [ Title     ]  [ Title     ]
[ Channel   ]  [ Channel   ]  [ Channel   ]

```

---

## 📌 Pro Tips

- ✅ Preload a loading spinner while fetching.
- ✅ Debounce the search input for performance.
- ✅ Add dark mode toggle 🌙
- ✅ Enhance with pagination (bonus)

---

## 📊 Diagram: App Flow

```
User opens app
       ↓
Fetch videos from FreeAPI
       ↓
Render grid cards with thumbnails
       ↓
User types in search bar
       ↓
Frontend filters & re-renders cards
       ↓
User clicks → open YouTube video in new tab

```

---

## 🧠 What You’ve Learned

- Fetching from a public API
- Rendering dynamic UI using JavaScript
- Filtering data on the frontend
- Designing responsive grid layouts

---

## 🚀 Wrap-up

This project is great for beginners and intermediate devs alike. You build a **real-world app** with:

✅ API usage

✅ UI rendering

✅ Frontend search

✅ Clean UX

💡 Bonus: You can repurpose the layout for image galleries, news feeds, or portfolios!