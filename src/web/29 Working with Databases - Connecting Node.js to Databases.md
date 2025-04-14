# 🗄️ Working with Databases – Connecting Node.js to MongoDB and SQL

So, your app is running, routes are set, and Express is cruising smoothly… but where does all the data go?

Just like a notebook holds your class notes, **databases** store your app's data. In Node.js, you can easily hook up both **SQL (structured)** and **NoSQL (flexible)** databases using tools like **Prisma** and **Mongoose**.

Let’s walk through how Node.js connects to both MongoDB and SQL databases—and how you can start saving and retrieving data like a pro.

---

## 🍃 Option 1: MongoDB with Mongoose (NoSQL)

MongoDB stores data as **documents (JSON-like objects)** inside collections, which makes it great for flexible, fast-moving projects.

### 🧠 Example Use Case:

Let’s say we want to store users.

### Step 1: Install Mongoose

```bash
npm install mongoose

```

### Step 2: Connect to MongoDB

```
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/myapp')
  .then(() => console.log("MongoDB connected"))
  .catch(err => console.error(err));

```

### Step 3: Create a Schema and Model

```
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number
});

const User = mongoose.model('User', userSchema);

```

### Step 4: Save a User

```
const newUser = new User({ name: 'Alice', email: 'alice@example.com', age: 25 });
await newUser.save();

```

### Step 5: Retrieve Users

```
const users = await User.find();
console.log(users);

```

📊 **Diagram Idea:**

Entity-relationship diagram showing a `User` collection with fields like `name`, `email`, `age`.

---

## 🧱 Option 2: SQL with Prisma (Relational Databases)

SQL databases like PostgreSQL and MySQL store data in tables and rows with strict structure. **Prisma** makes it easy to work with SQL using a type-safe, modern interface.

### 🧠 Real-World Fit:

Perfect when your data has relationships, like "each post belongs to a user".

### Step 1: Install Prisma & Set Up

```bash
npm install prisma --save-dev
npx prisma init

```

In `prisma/schema.prisma`:

```
datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id    Int    @id @default(autoincrement())
  name  String
  email String @unique
}

```

### Step 2: Generate Prisma Client

```bash
npx prisma generate

```

And create the database:

```bash
npx prisma migrate dev --name init

```

### Step 3: Use Prisma Client in Code

```
const { PrismaClient } = require('@prisma/client');
const prisma = new PrismaClient();

// Save
await prisma.user.create({
  data: { name: 'Bob', email: 'bob@example.com' }
});

// Retrieve
const users = await prisma.user.findMany();
console.log(users);

```

📊 **Diagram Idea:**

A table-based schema showing `User(id, name, email)` with Prisma model.

---

## 🥊 SQL vs NoSQL – What's the Difference?

| Feature | SQL (Prisma) | NoSQL (Mongoose) |
| --- | --- | --- |
| Structure | Fixed schema, strict types | Flexible, document-based |
| Relationships | Strong (joins, foreign keys) | Weak or manual references |
| Use Case | Banking, Inventory systems | Blogs, Chat apps, fast MVPs |
| Examples | PostgreSQL, MySQL | MongoDB |

---

## 🔄 API → Controller → DB Flow

📈 **Diagram Idea:**

```
Client Request
   ↓
Express Route
   ↓
Controller Function
   ↓
Database Query (Prisma or Mongoose)
   ↓
Response Sent to Client

```

---

## 💡 Bonus Tips

- Use **try/catch** for all async DB calls to catch errors
- Keep DB logic in **separate service files** for maintainability
- Always **validate and sanitize** user input before storing it

---

## 🧠 Final Thoughts

Whether you choose **MongoDB for flexibility** or **SQL for structure**, Node.js has powerful tools like **Mongoose** and **Prisma** to make your database life easier.

Start simple: create one model, store a few records, and read them back. You’ll quickly see how fun and empowering it is to build full-stack apps with real data.