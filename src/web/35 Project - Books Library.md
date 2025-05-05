# 📚 Build a Dynamic Books Library with JavaScript and FreeAPI (No Backend Needed)

Have you ever wanted to create a sleek, searchable online book library using just HTML, CSS, and JavaScript?

In this tutorial, we’ll build a full-featured **Books Library web app** using [FreeAPI.app](https://freeapi.hashnode.space/api-guide/apireference/getBooks), complete with:

✅ Grid/List view toggle

✅ Search + Sort by title/date

✅ Pagination

✅ Detailed book previews

✅ Responsive UI

> ⚠️ Note: This app is for display purposes only. Downloading or sharing copyrighted content is strictly prohibited.
> 

---

## 🔧 Tech Stack

- **HTML** for structure
- **CSS** for styling
- **JavaScript** for fetching & rendering data
- **FreeAPI.app** for fetching book data

---

## 🚀 API Reference

- Endpoint:
    
    `GET https://api.freeapi.app/api/v1/public/books?page=1&limit=20`
    
- Documentation:
    
    https://freeapi.hashnode.space/api-guide/apireference/getBooks
    

Example response:

```json
{
  "data": [
    {
      "title": "The Hobbit",
      "authors": ["J.R.R. Tolkien"],
      "publisher": "HarperCollins",
      "publishedDate": "1995-07-01",
      "thumbnail": "https://...",
      "infoLink": "https://books.google.com/..."
    }
  ],
  "total": 1200,
  "page": 1,
  "limit": 20
}

```

---

## 🧱 Folder Structure

```
📂 books-library/
│
├── index.html
├── styles.css
└── script.js

```

---

## 🧩 Step 1: Basic HTML

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Books Library</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <div class="top-bar">
    <input type="text" id="search" placeholder="Search by title or author..." />
    <select id="sort">
      <option value="">Sort By</option>
      <option value="title">Title A-Z</option>
      <option value="date">Published Date</option>
    </select>
    <button id="toggleView">🔁 Toggle View</button>
  </div>

  <div id="book-list" class="grid-view"></div>
  <div id="loading">Loading more books...</div>

  <script src="script.js"></script>
</body>
</html>

```

---

## 🎨 Step 2: CSS Styling

```css
/* styles.css */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 1rem;
  background: #f9f9f9;
}

.top-bar {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
}

#book-list.grid-view {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 1rem;
}

#book-list.list-view {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.book-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 1px 5px rgba(0,0,0,0.1);
  display: flex;
  flex-direction: column;
  cursor: pointer;
}

.book-card img {
  max-width: 100%;
  height: 200px;
  object-fit: contain;
}

.book-info {
  margin-top: 0.5rem;
}

#loading {
  text-align: center;
  padding: 2rem;
  display: none;
}

```

---

## ⚙️ Step 3: JavaScript Logic

```
// script.js
const bookList = document.getElementById("book-list");
const searchInput = document.getElementById("search");
const sortSelect = document.getElementById("sort");
const toggleViewBtn = document.getElementById("toggleView");
const loading = document.getElementById("loading");

let books = [];
let page = 1;
let limit = 20;
let isLoading = false;
let currentView = "grid";

// Fetch books from API
async function fetchBooks() {
  if (isLoading) return;
  isLoading = true;
  loading.style.display = "block";

  const res = await fetch(`https://api.freeapi.app/api/v1/public/books?page=${page}&limit=${limit}`);
  const data = await res.json();

  books = books.concat(data.data);
  renderBooks(books);
  page++;
  isLoading = false;
  loading.style.display = "none";
}

// Render books
function renderBooks(list) {
  bookList.innerHTML = "";

  const filtered = filterAndSortBooks(list);

  filtered.forEach(book => {
    const card = document.createElement("div");
    card.className = "book-card";
    card.onclick = () => window.open(book.infoLink, "_blank");

    card.innerHTML = `
      <img src="${book.thumbnail || 'https://via.placeholder.com/150'}" alt="${book.title}" />
      <div class="book-info">
        <h4>${book.title}</h4>
        <p><strong>Author:</strong> ${book.authors?.join(", ") || "N/A"}</p>
        <p><strong>Publisher:</strong> ${book.publisher || "N/A"}</p>
        <p><strong>Date:</strong> ${book.publishedDate || "N/A"}</p>
      </div>
    `;

    bookList.appendChild(card);
  });

  bookList.className = currentView === "grid" ? "grid-view" : "list-view";
}

// Filter and sort books
function filterAndSortBooks(list) {
  let filtered = [...list];

  const query = searchInput.value.toLowerCase();
  if (query) {
    filtered = filtered.filter(book =>
      book.title.toLowerCase().includes(query) ||
      (book.authors?.join(" ").toLowerCase().includes(query))
    );
  }

  const sortBy = sortSelect.value;
  if (sortBy === "title") {
    filtered.sort((a, b) => a.title.localeCompare(b.title));
  } else if (sortBy === "date") {
    filtered.sort((a, b) => new Date(b.publishedDate) - new Date(a.publishedDate));
  }

  return filtered;
}

// Toggle between list and grid
toggleViewBtn.addEventListener("click", () => {
  currentView = currentView === "grid" ? "list" : "grid";
  renderBooks(books);
});

// Search + Sort listeners
searchInput.addEventListener("input", () => renderBooks(books));
sortSelect.addEventListener("change", () => renderBooks(books));

// Infinite Scroll
window.addEventListener("scroll", () => {
  if (window.innerHeight + window.scrollY >= document.body.offsetHeight - 100) {
    fetchBooks();
  }
});

// Initial load
fetchBooks();

```

---

## 🧠 What You’ll Learn

- Working with **public APIs**
- DOM manipulation with dynamic data
- Grid vs List UI toggle using JavaScript
- Search & sort logic implementation
- Pagination using **infinite scroll**
- Opening dynamic external links (`infoLink`)

---

## 🖼 App Flow Diagram

```
User visits → Fetch books → Render cards → Scroll → Fetch more
                 ↓
 Search / Sort filters applied in real-time
                 ↓
 Click on book → Opens detailed page (infoLink)

```

---

## 📣 Final Thoughts

This **Books Library** app is a great beginner-to-intermediate project to sharpen your frontend skills:

- Clean UI logic ✅
- Works on real-world API ✅
- Search, sort, pagination ✅
- Bonus UI enhancements possible (dark mode, favorites, etc.)

Host it on GitHub Pages or Netlify, and share it in your portfolio or community!

---

## 🪄 Want More Projects Like This?

Ask me to help you with:

- Firebase version to save favorite books
- React version using `useEffect` and `useState`
- Bookshelf animation with CSS
- Bookmarking books in `localStorage`

Happy Coding! 🧠✨