# 🔐 Authentication and Authorization – Securing Your Node.js App the Smart Way

Building a cool app? Awesome! But what happens when you want to protect user data or restrict access? That’s where **authentication** (knowing *who* a user is) and **authorization** (knowing *what* they can access) come in.

Let’s dive into how Node.js handles auth, using **JWTs**, **sessions**, and **bcrypt** for password protection—plus diagrams and practical examples to tie it all together.

---

## 🙋‍♂️ First, What’s Authentication vs Authorization?

Imagine you’re at a concert:

- **Authentication** is showing your **ticket** at the entrance. It proves *you’re allowed in*.
- **Authorization** is showing your **VIP pass**. It tells *where you’re allowed to go* (like backstage).

---

## 🔑 Passwords 101 – Always Hash Before You Store

Before you save any password in a database, it should be **hashed**—turned into an unreadable string—using something like `bcrypt`.

### ✅ Why?

Because storing raw passwords is like writing down ATM PINs on a napkin.

### Example:

```
const bcrypt = require('bcrypt');
const password = 'supersecret123';
const hashed = await bcrypt.hash(password, 10);

```

Then during login:

```
const isMatch = await bcrypt.compare('userinput', hashed);

```

---

## 🪙 JWT (JSON Web Token) – Modern, Token-Based Auth

JWT is like giving the user a **digital badge** that they carry around. It's stateless—no need for the server to remember who you are between requests.

### 🔄 JWT Auth Flow:

1. **Login →** server validates credentials
2. **Server returns a signed token (JWT)**
3. **Client stores token (usually in localStorage or cookies)**
4. **Client sends token with each request**
5. **Server verifies token and grants access**

```
const jwt = require('jsonwebtoken');
const token = jwt.sign({ userId: user._id }, 'secretKey', { expiresIn: '1h' });

```

To protect routes:

```
function verifyToken(req, res, next) {
  const token = req.headers.authorization?.split(" ")[1];
  if (!token) return res.status(401).send("Unauthorized");

  try {
    const decoded = jwt.verify(token, 'secretKey');
    req.user = decoded;
    next();
  } catch {
    res.status(403).send("Invalid token");
  }
}

```

🧠 **Diagram Idea: JWT Login Flow**

```
Client → [POST /login] → Server
             ↓
       JWT Created & Sent Back
             ↓
Client stores JWT → Sends JWT in headers → Server verifies on each request

```

---

## 🛑 What About Refresh Tokens?

Access tokens expire quickly. **Refresh tokens** are longer-lived tokens used to get a new access token without asking the user to log in again.

🧠 **Diagram Idea:**

```
Client → /login → Server
         ↳ Access Token (short-lived)
         ↳ Refresh Token (long-lived)

Client → /refresh-token → Server → New Access Token

```

---

## 🗂️ Session-Based Authentication – Old but Gold

In traditional apps, the server creates a **session** and stores it. A **session ID** is sent to the client as a cookie.

### 🔄 Session Flow:

1. **Login →** server stores user ID in memory
2. **Client gets a cookie with session ID**
3. **On each request, cookie is sent**
4. **Server matches session ID to user**

With **Express-session**:

```
const session = require('express-session');

app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true,
}));

```

Store login info:

```
req.session.userId = user._id;

```

Protect a route:

```
if (!req.session.userId) {
  return res.status(401).send("Please log in");
}

```

---

## 🔐 Which One Should I Use?

| Feature | JWT | Session |
| --- | --- | --- |
| Storage | Client (token) | Server (in memory/DB) |
| Stateless | ✅ | ❌ (server stores session) |
| Scalability | ✅ Easier with microservices | ❌ Needs session store |
| Use Case | APIs, mobile apps | Traditional web apps |

📌 **Note:** Don’t **compare JWT vs sessions vs cookies** as if they’re enemies. JWT and sessions are **auth strategies**; cookies are just **storage mechanisms**.

---

## 🛠️ Mini Auth System Example (Register → Login → Protected Route)

### 👤 Register

```
app.post('/register', async (req, res) => {
  const hashed = await bcrypt.hash(req.body.password, 10);
  const user = await User.create({ email: req.body.email, password: hashed });
  res.send("User registered");
});

```

### 🔓 Login

```
app.post('/login', async (req, res) => {
  const user = await User.findOne({ email: req.body.email });
  const match = await bcrypt.compare(req.body.password, user.password);
  if (!match) return res.status(403).send("Invalid credentials");

  const token = jwt.sign({ userId: user._id }, 'secret', { expiresIn: '1h' });
  res.json({ token });
});

```

### 🔐 Protected Route

```
app.get('/dashboard', verifyToken, (req, res) => {
  res.send("Welcome to your dashboard!");
});

```

---

## 🧠 Final Thoughts

Authentication is your app's **front gate**, and authorization controls **what users can access inside**.

Start with:

✅ Hashing passwords with `bcrypt`

✅ Choosing between **JWT or Sessions**

✅ Protecting routes with middleware

It’s one of the most essential skills for every backend developer—and once you build one secure system, you'll never forget how powerful it feels.