# 🧠 Build a "Quote of the Day" Web App with Random Quotes, Images & Twitter Sharing

What if you could build an inspiring "Quote of the Day" app in just under an hour? One that fetches fresh quotes from a free API, looks beautiful, and even lets users share or save quotes?

Let’s do exactly that. 💡

---

## 🔥 Features We’ll Build

✅ Fetch random quote using FreeAPI

✅ Display quote + author

✅ “New Quote” button to fetch another one

✅ Copy to clipboard

✅ Share on Twitter

✅ Random background image

✅ Export the quote block as an image (Bonus!)

---

## 📡 The API We’ll Use

**FreeAPI (No Auth Required)**

- **Endpoint:**
    
    `GET https://api.freeapi.app/api/v1/public/quotes/quote/random`
    
- **Docs:**
    
    https://freeapi.hashnode.space/api-guide/apireference/getARandomQuote
    

Sample response:

```json
{
  "data": {
    "quoteText": "Life is what happens when you're busy making other plans.",
    "quoteAuthor": "John Lennon"
  }
}

```

---

## 🧱 Folder Structure

```
📂 quote-app/
│
├── index.html
├── styles.css
└── script.js

```

---

## 🧩 Step 1: HTML Markup

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Quote of the Day</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <div id="quote-box">
    <p id="quote">Loading...</p>
    <p id="author"></p>

    <div class="buttons">
      <button id="new-quote">✨ New Quote</button>
      <button id="copy">📋 Copy</button>
      <button id="tweet">🐦 Tweet</button>
      <button id="export">📥 Export</button>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>

```

---

## 🎨 Step 2: CSS Styling

```css
/* styles.css */
body {
  font-family: 'Georgia', serif;
  margin: 0;
  padding: 0;
  height: 100vh;
  background-size: cover;
  background-position: center;
  display: flex;
  align-items: center;
  justify-content: center;
}

#quote-box {
  background: rgba(255, 255, 255, 0.85);
  padding: 2rem;
  max-width: 600px;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 5px 20px rgba(0,0,0,0.2);
}

#quote {
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

#author {
  font-style: italic;
  color: #555;
}

.buttons button {
  margin: 0.5rem;
  padding: 0.5rem 1rem;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  background: #333;
  color: #fff;
}

```

---

## 🚀 Step 3: JavaScript Logic

```
// script.js
const quoteEl = document.getElementById('quote');
const authorEl = document.getElementById('author');
const newBtn = document.getElementById('new-quote');
const copyBtn = document.getElementById('copy');
const tweetBtn = document.getElementById('tweet');
const exportBtn = document.getElementById('export');
const quoteBox = document.getElementById('quote-box');

const backgrounds = [
  'https://source.unsplash.com/1600x900/?nature,water',
  'https://source.unsplash.com/1600x900/?sunset',
  'https://source.unsplash.com/1600x900/?stars',
  'https://source.unsplash.com/1600x900/?abstract',
];

function getRandomBackground() {
  document.body.style.backgroundImage = `url(${backgrounds[Math.floor(Math.random() * backgrounds.length)]})`;
}

async function fetchQuote() {
  const res = await fetch('https://api.freeapi.app/api/v1/public/quotes/quote/random');
  const data = await res.json();
  const quote = data.data;
  quoteEl.innerText = `“${quote.quoteText}”`;
  authorEl.innerText = `– ${quote.quoteAuthor || "Unknown"}`;
  getRandomBackground();
}

// Copy to clipboard
copyBtn.addEventListener('click', () => {
  const text = `${quoteEl.innerText} ${authorEl.innerText}`;
  navigator.clipboard.writeText(text).then(() => alert("Copied!"));
});

// Tweet it
tweetBtn.addEventListener('click', () => {
  const tweet = `${quoteEl.innerText} ${authorEl.innerText}`;
  const url = `https://twitter.com/intent/tweet?text=${encodeURIComponent(tweet)}`;
  window.open(url, '_blank');
});

// Export to image
exportBtn.addEventListener('click', async () => {
  const html2canvas = (await import('https://cdn.skypack.dev/html2canvas')).default;
  html2canvas(quoteBox).then(canvas => {
    const link = document.createElement('a');
    link.download = 'quote.png';
    link.href = canvas.toDataURL();
    link.click();
  });
});

newBtn.addEventListener('click', fetchQuote);

// Initial quote on load
fetchQuote();

```

---

## 🖼️ Bonus: Export as Image

We used [html2canvas](https://html2canvas.hertzen.com/) via Skypack to convert the quote box to an image and let users download it as PNG.

```bash
npm install html2canvas  # if using locally

```

---

## 📊 App Flow Diagram

```
User loads app
       ↓
Quote fetched from FreeAPI
       ↓
Displayed with author + new background
       ↓
User:
↳ Clicks "New" → fetches again
↳ Clicks "Copy" → clipboard
↳ Clicks "Tweet" → opens Twitter
↳ Clicks "Export" → downloads PNG

```

---

## 🧠 What You Learned

- Working with public REST APIs
- DOM manipulation and event listeners
- Copying to clipboard using `navigator.clipboard`
- Sharing on Twitter via intent URL
- Exporting DOM elements as images with `html2canvas`
- Changing backgrounds dynamically

---

## 🌟 Final Thoughts

This project is perfect for:

- 💬 Daily quote dashboards
- 📱 Shareable content creators
- 🧘 Mood + reflection apps
- 🚀 Beginner projects to impress recruiters

Try hosting it on **GitHub Pages**, **Netlify**, or **Vercel** in minutes.