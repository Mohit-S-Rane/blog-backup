# 📁 Working with File Systems in Node.js – Read, Write, Upload Like a Pro

Ever wondered how servers read a file or save uploaded documents from a user? In Node.js, it’s all possible using the built-in **`fs` module** and a little help from **Multer** for uploads.

Let’s explore how to **read, write, and upload files** like a backend wizard—with simple code examples and real-world analogies.

---

## 📦 The `fs` Module – Node’s Built-in File Manager

The `fs` (short for File System) module lets Node.js interact with your system’s files. Think of it like Node’s personal hard-drive assistant.

To use it:

```
const fs = require('fs');

```

---

## 📖 Reading a File – Synchronously vs Asynchronously

### 📚 Synchronous: Blocking Style

Reads the file and **waits** until it's done. The rest of the code **pauses**.

```
const data = fs.readFileSync('hello.txt', 'utf8');
console.log(data);

```

🛑 **Problem**: If reading a large file, the whole server halts.

---

### 🏃 Asynchronous: Non-blocking Style

Reads the file **without blocking** other code. Great for performance.

```
fs.readFile('hello.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

```

✅ **Best Practice**: Always prefer async for scalable apps.

---

## ✍️ Writing to a File – Save Like a Boss

### Asynchronous Write

```
fs.writeFile('output.txt', 'Hello from Node!', (err) => {
  if (err) throw err;
  console.log('File saved!');
});

```

📂 It will **create the file** if it doesn’t exist or **overwrite** it if it does.

---

## 📥 Uploading Files in Express with Multer

When users upload profile pictures, PDFs, or documents, we need to **accept**, **store**, and sometimes **serve** those files back.

That’s where **Multer** comes in.

```bash
npm install multer

```

### 🔧 Setup Multer

```
const express = require('express');
const multer = require('multer');
const app = express();

const upload = multer({ dest: 'uploads/' }); // folder to save files

```

### 👨‍💻 File Upload Route

```
app.post('/upload', upload.single('myFile'), (req, res) => {
  console.log(req.file);
  res.send('File uploaded successfully!');
});

```

🔎 `req.file` contains info like name, size, and path.

---

## 🖼️ Serving Uploaded Files

You can serve uploaded files using Express's static middleware:

```
app.use('/uploads', express.static('uploads'));

```

Now files can be accessed at:

```
http://localhost:3000/uploads/filename.jpg

```

---

## 📊 Diagram Idea: File Upload Flow

```
Client → [POST /upload]
          ↓
     Multer handles file
          ↓
     Stored in /uploads/
          ↓
   Server responds: “Success!”

```

---

## 💡 Streams vs Buffers – Bonus Nerd Tip

For **large files**, using **streams** is better than reading the whole file into memory.

```
const readStream = fs.createReadStream('bigfile.txt');
readStream.pipe(process.stdout);

```

🔁 This reads in **chunks**, improving performance and memory use.

---

## 🛠️ Full Working Example: Upload & Save

Here’s a basic app to upload files and store them:

```
const express = require('express');
const multer = require('multer');
const path = require('path');

const app = express();
const port = 3000;

// Setup destination and file renaming
const storage = multer.diskStorage({
  destination: 'uploads/',
  filename: (req, file, cb) => {
    cb(null, Date.now() + path.extname(file.originalname)); // timestamped name
  }
});

const upload = multer({ storage });

app.post('/upload', upload.single('file'), (req, res) => {
  res.send(`Uploaded file saved as ${req.file.filename}`);
});

app.use('/uploads', express.static('uploads'));

app.listen(port, () => console.log(`Server running on http://localhost:${port}`));

```

Now try uploading a file via Postman or a frontend form. 🎉

---

## 🧠 Final Thoughts

Node.js makes file handling a breeze—whether you’re:

- Reading configs,
- Logging data to files,
- Letting users upload resumes or receipts.

By using the `fs` module and Multer, you can confidently build features that interact with the real file system.

---

## 📁 Summary Table

| Task | Tool Used | Example |
| --- | --- | --- |
| Read file | `fs.readFile` | `fs.readFile('file.txt')` |
| Write file | `fs.writeFile` | `fs.writeFile('log.txt')` |
| Upload file | `Multer` | `upload.single('file')` |
| Serve files | `express.static` | `app.use('/uploads', express.static)` |

---
