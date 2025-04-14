# 🔧 RESTful API Design – Building Clean APIs with Express.js

Ever wonder how apps like Instagram or Zomato talk to their servers? That magic happens through something called a **RESTful API**—a system that lets the frontend (what you see) talk to the backend (the server) in a clean, structured way.

And the best part? With **Express.js**, building one is surprisingly simple.

Let’s build a REST API from scratch using a real-world example—**users**—and see how HTTP methods like `GET`, `POST`, `PUT`, and `DELETE` map to actions we do every day.

---

## 🚪 What is a RESTful API?

REST stands for **Representational State Transfer**—but don’t worry about the name. Just think of it like a set of rules for how your app should talk to a server.

RESTful APIs use standard HTTP methods to perform **CRUD operations**:

| CRUD Action | HTTP Method | Meaning |
| --- | --- | --- |
| Create | POST | Add a new user |
| Read | GET | Get user(s) |
| Update | PUT | Update a user |
| Delete | DELETE | Remove a user |

📊 **Diagram Idea:**

> A table showing the four CRUD operations mapped to HTTP methods and example routes (e.g., /users, /users/:id)
> 

---

## 🗂️ Project Structure for Clean API Design

Here’s how you might structure a simple Express API:

```
project/
├── routes/
│   └── users.js
├── controllers/
│   └── usersController.js
├── app.js

```

This keeps your routes, logic, and app setup nicely separated.

---

## 👤 Let’s Build: A REST API for “Users”

Imagine you’re building an app where you manage users. Here’s how the API would look using Express.js.

### Step 1: Set up Express

```
// app.js
const express = require('express');
const app = express();
const userRoutes = require('./routes/users');

app.use(express.json()); // For parsing JSON
app.use('/users', userRoutes);

app.listen(3000, () => {
  console.log("Server is running on port 3000");
});

```

---

### Step 2: Define User Routes

```
// routes/users.js
const express = require('express');
const router = express.Router();
const usersController = require('../controllers/usersController');

router.get('/', usersController.getAllUsers);
router.get('/:id', usersController.getUserById);
router.post('/', usersController.createUser);
router.put('/:id', usersController.updateUser);
router.delete('/:id', usersController.deleteUser);

module.exports = router;

```

---

### Step 3: Add Controller Logic

```
// controllers/usersController.js

let users = []; // Sample in-memory array

exports.getAllUsers = (req, res) => {
  res.status(200).json(users);
};

exports.getUserById = (req, res) => {
  const user = users.find(u => u.id == req.params.id);
  user ? res.status(200).json(user) : res.status(404).json({ message: "User not found" });
};

exports.createUser = (req, res) => {
  const newUser = { id: Date.now(), ...req.body };
  users.push(newUser);
  res.status(201).json(newUser);
};

exports.updateUser = (req, res) => {
  const index = users.findIndex(u => u.id == req.params.id);
  if (index !== -1) {
    users[index] = { ...users[index], ...req.body };
    res.status(200).json(users[index]);
  } else {
    res.status(404).json({ message: "User not found" });
  }
};

exports.deleteUser = (req, res) => {
  const index = users.findIndex(u => u.id == req.params.id);
  if (index !== -1) {
    users.splice(index, 1);
    res.status(204).send(); // No content
  } else {
    res.status(404).json({ message: "User not found" });
  }
};

```

---

## 🎯 Best Practices for Clean REST API Design

### ✅ Use Proper HTTP Status Codes

| Code | Meaning |
| --- | --- |
| 200 | OK (Successful GET/PUT) |
| 201 | Created (POST success) |
| 204 | No Content (DELETE) |
| 404 | Not Found |
| 400 | Bad Request |

### 📐 Use Nouns, Not Verbs, in Routes

❌ `/getAllUsers`

✅ `/users`

---

## 🛠️ API Request Flow in Express

📈 **Diagram Idea:**

```
Client Request → Express Route → Middleware (auth, JSON parser, etc.) → Controller → Response

```

Each request goes through a pipeline before sending the final response.

---

## 🔁 Real-Life Example: Using Postman or Frontend

Let’s simulate using this API:

- `GET /users` → Returns all users
- `POST /users` with `{ "name": "Alice" }` → Adds Alice
- `PUT /users/123` → Updates user with ID 123
- `DELETE /users/123` → Deletes user 123

Tools like **Postman**, **Insomnia**, or even your React frontend can make these requests.

---

## 🧠 Final Thoughts

Designing a RESTful API with Express.js doesn’t have to be complex. With the right structure, proper use of routes, and good status codes, you can build scalable, maintainable backends in no time.

Whether you're working solo or in a team, following REST principles helps everyone stay on the same page—and keeps your app easy to grow and debug.