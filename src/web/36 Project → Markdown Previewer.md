# ✍️ Build a Real-Time Markdown Previewer with JavaScript and Marked.js

Ever wondered how README files on GitHub turn plain text into nicely formatted documentation?

In this fun and interactive project, you'll **build your own live Markdown Previewer** using **just HTML, CSS, and JavaScript** — no backend needed!

You’ll learn:

- How to use Markdown syntax and parse it
- Real-time DOM updates
- Basic input handling and text transformation
- Working with third-party libraries like [`marked.js`](https://marked.js.org/)

---

## 💡 What You’ll Build

A simple **Markdown Editor** on the left, and a **Live Preview** on the right — just like GitHub or StackOverflow.

📌 Features:

- Markdown typing with live preview
- Support for headings, bold, italics, links, lists
- Reset button to clear editor
- Bonus: Syntax-highlighted code blocks 🧠

![](https://marked.js.org/demo/images/demo.png)

---

## 🧰 Tech Stack

- **HTML** – Structure
- **CSS** – Styling
- **JavaScript** – Dynamic rendering
- [**Marked.js**](https://marked.js.org/) – Markdown parser (no backend needed)

---

## 🧱 File Structure

```
📁 markdown-previewer/
├── index.html
├── styles.css
└── script.js

```

---

## 🧩 Step 1: HTML Setup

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Markdown Previewer</title>
  <link rel="stylesheet" href="styles.css" />
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
</head>
<body>
  <div class="container">
    <div class="editor">
      <h2>Markdown Editor</h2>
      <textarea id="markdown-input" placeholder="Type your markdown here..."></textarea>
      <button id="reset-btn">🧹 Clear</button>
    </div>
    <div class="preview">
      <h2>Live Preview</h2>
      <div id="markdown-preview"></div>
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
  font-family: sans-serif;
  margin: 0;
  padding: 0;
  background: #f5f5f5;
}

.container {
  display: flex;
  height: 100vh;
}

.editor, .preview {
  width: 50%;
  padding: 1rem;
  box-sizing: border-box;
  overflow-y: auto;
}

textarea {
  width: 100%;
  height: 80vh;
  padding: 1rem;
  font-size: 16px;
  border-radius: 8px;
  border: 1px solid #ccc;
  resize: vertical;
}

#markdown-preview {
  padding: 1rem;
  background: white;
  border-radius: 8px;
  border: 1px solid #ddd;
  min-height: 80vh;
}

#reset-btn {
  margin-top: 0.5rem;
  padding: 0.5rem 1rem;
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

```

---

## ⚙️ Step 3: JavaScript Logic

```
// script.js
const input = document.getElementById("markdown-input");
const preview = document.getElementById("markdown-preview");
const resetBtn = document.getElementById("reset-btn");

// Configure marked.js
marked.setOptions({
  breaks: true,
  gfm: true,
  highlight: function (code, lang) {
    return hljs.highlightAuto(code).value;
  }
});

// Update preview on input
input.addEventListener("input", () => {
  preview.innerHTML = marked.parse(input.value);
});

// Clear input
resetBtn.addEventListener("click", () => {
  input.value = "";
  preview.innerHTML = "";
});

// Set default text
input.value = `# Welcome to Markdown Previewer

## Features
- **Bold**
- *Italic*
- [Link](https://example.com)
- \`Inline code\`
\`\`\`js
function greet() {
  console.log("Hello Markdown!");
}
\`\`\`
`;

preview.innerHTML = marked.parse(input.value);

```

---

## ✨ Bonus: Syntax Highlighting with Highlight.js

To support code highlighting, add this to your `index.html`:

```html
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/styles/github.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/highlight.min.js"></script>

```

---

## 📚 Supported Markdown Syntax

| Markdown | Example | Rendered Output |
| --- | --- | --- |
| `# Heading 1` | `# My Title` | My Title |
| Bold | `**Bold Text**` | **Bold Text** |
| Italic | `*Italic Text*` | *Italic Text* |
| Link | `[OpenAI](https://openai.com)` | [OpenAI](https://openai.com/) |
| List | `- Item 1\n- Item 2` | • Item 1• Item 2 |
| Code Block | ```js console.log()``` | Highlighted code block |

---

## 🧠 Learning Outcomes

- How to use a **JavaScript markdown parser** (`marked`)
- Real-time **input to output rendering**
- How to dynamically **update the DOM**
- Bonus: Working with **external libraries** for syntax highlighting

---

## 📸 Diagram – App Flow

```
User types Markdown → JavaScript parses it using marked.js → Output rendered as HTML in real-time

```

---

## 🌍 Live Demos You Can Try

- [DigitalOcean Markdown Demo](https://www.digitalocean.com/community/markdown)
- [Marked.js Demo](https://marked.js.org/demo/)

---

## 🧪 Challenge Yourself

After building this, try adding:

- 🌓 **Dark mode**
- 💾 Save & load previous markdown from `localStorage`
- 💻 Export the preview to PDF or image
- 📤 Drag & drop .md file support

---

## ✅ Final Thoughts

This **Markdown Previewer** is a fantastic beginner project for:

- Practicing **user input handling**
- Learning how to process and **render Markdown**
- Using powerful open-source libraries
- Building beautiful UI with live feedback ✨

You can deploy this on **GitHub Pages**, **Netlify**, or **Vercel**, and include it proudly in your dev portfolio! 💼