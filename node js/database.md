# 7. Working with Databases in Node.js

Understanding how to interface Node.js with various databases is crucial for building modern backend and fullstack applications. Here's a practical overview and examples for connecting to popular databases and using ORMs/ODMs for streamlined data operations.

## Connecting Node.js to Databases

### MongoDB

- **MongoDB** is a popular NoSQL (document) database. You can connect to it directly with the official MongoDB driver or with an ODM like Mongoose for data modeling.

**Example: Using Native MongoDB Driver**
```js
const { MongoClient } = require('mongodb');
const uri = 'mongodb://localhost:27017';
const client = new MongoClient(uri);

async function run() {
  try {
    await client.connect();
    console.log('Connected to MongoDB');
    const db = client.db('test_database');
    // Perform operations here...
  } finally {
    await client.close();
  }
}

run().catch(console.dir);
```
- The connection string format might change for cloud databases (like MongoDB Atlas)[1][2].

### MySQL

- **MySQL** is a widely-used relational database. Node.js typically connects via the `mysql` package.

**Example: Connecting to MySQL**
```js
const mysql = require('mysql');
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'yourpassword',
  database: 'test_database'
});
connection.connect(err => {
  if (err) throw err;
  console.log('Connected to MySQL!');
});
```
- Use `connection.query()` to execute SQL queries[3][4][5].

### PostgreSQL

- **PostgreSQL** is a robust, open-source relational database. For Node.js, the `pg` package is the standard client.

**Example: Connecting to PostgreSQL**
```js
const { Client } = require('pg');
const client = new Client({
  host: 'localhost',
  user: 'postgres',
  password: 'yourpassword',
  database: 'test_database',
  port: 5432
});
client.connect()
  .then(() => console.log('Connected to PostgreSQL!'))
  .catch(err => console.error('Connection error', err.stack));
```
- Use `client.query()` to run SQL commands[6][7].

## Using ORMs and ODMs

### Sequelize (ORM for SQL databases)

- **Sequelize** abstracts data operations and works with PostgreSQL, MySQL, MariaDB, SQLite, and more. It uses models and provides a promise-based API.

**Example: Setting Up Sequelize**
```js
const { Sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize('test_database', 'root', 'yourpassword', {
  host: 'localhost',
  dialect: 'mysql' // or 'postgres', 'sqlite', etc.
});

const User = sequelize.define('User', {
  username: DataTypes.STRING,
  email: DataTypes.STRING
});

(async () => {
  await sequelize.authenticate();
  await sequelize.sync(); // creates tables if not exist
  const user = await User.create({ username: 'alice', email: 'alice@example.com' });
  console.log('User created:', user.toJSON());
})();
```
- Sequelize helps avoid writing raw SQL, supports migrations, and schema management[8][9][10].

### Mongoose (ODM for MongoDB)

- **Mongoose** provides schema-based modeling for MongoDB, making it easier to enforce data structure, run validations, and manage relationships.

**Example: Mongoose Setup**
```js
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/test_database', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log('Connected with Mongoose'))
  .catch(err => console.error('Connection error', err));

const userSchema = new mongoose.Schema({
  name: String,
  email: String
});
const User = mongoose.model('User', userSchema);

(async () => {
  const newUser = await User.create({ name: 'Bob', email: 'bob@example.com' });
  console.log('User:', newUser);
})();
```
- Mongoose is ideal for applications requiring strict data structures in MongoDB[11][2][12][13][14].

## Summary Table

| Database     | Driver/ORM      | Example Libraries      | Typical Usage                 |
|--------------|-----------------|-----------------------|-------------------------------|
| MongoDB      | Native Driver   | mongodb               | General MongoDB access        |
| MongoDB      | ODM             | mongoose              | Schema, data validation       |
| MySQL        | Native Driver   | mysql                 | SQL queries, admin scripts    |
| MySQL        | ORM             | sequelize             | Models, migrations, relations |
| PostgreSQL   | Native Driver   | pg                    | SQL, analytics, transactions  |
| PostgreSQL   | ORM             | sequelize             | As above                     |

## Interview Key Points

- Know how to install drivers (`npm install`), connect using credentials, and perform CRUD operations in code.
- Understand benefits of ORMs/ODMs: abstraction, model validation, migrations, and easier query construction.
- For production, always handle connection errors and use environment variables to store sensitive information.

# Advanced Node.js Database Usage and Specific CRUD Operations

Here are practical, advanced database patterns and specific queries for popular Node.js ORMs/ODMs and native drivers, covering both SQL (Sequelize) and NoSQL (Mongoose for MongoDB).

## Sequelize (SQL Databases: MySQL, PostgreSQL, etc.)

### Advanced CRUD Examples

#### 1. **Create with Associations**
Add a user with related posts in one operation.

```js
const user = await User.create({
  username: 'alice',
  posts: [
    { title: 'First Post', content: 'Hello!' }
  ]
}, {
  include: [Post] // post is an associated model
});
```

#### 2. **Complex Read/Query**
Find all users with posts containing a certain keyword, ordered by created date.

```js
const users = await User.findAll({
  include: [{
    model: Post,
    where: { content: { [Sequelize.Op.like]: '%keyword%' } }
  }],
  order: [['createdAt', 'DESC']]
});
```

#### 3. **Update with Conditions**
Update multiple users at once.

```js
await User.update(
  { active: false },
  { where: { lastLogin: { [Sequelize.Op.lt]: new Date('2024-01-01') } } }
);
```

#### 4. **Delete with Cascading**
Delete a user and automatically remove related posts if set in the model schema.

```js
await User.destroy({ where: { id: userId } });
// Assuming cascade: true in association
```

#### 5. **Transaction Example**
Wrap multiple operations to ensure atomicity.

```js
const t = await sequelize.transaction();
try {
  const user = await User.create({ username: 'bob' }, { transaction: t });
  await Post.create({ userId: user.id, title: 'New Post' }, { transaction: t });
  await t.commit();
} catch (error) {
  await t.rollback();
}
```

## Mongoose (MongoDB)

### Schema for Reference

```js
const postSchema = new mongoose.Schema({
  title: String,
  content: String,
  author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
});
const Post = mongoose.model('Post', postSchema);
```

### Advanced CRUD Examples

#### 1. **Create with References**

```js
const user = await User.create({ name: 'Alice' });
const post = await Post.create({
  title: 'Hello MongoDB',
  content: 'Using references.',
  author: user._id
});
```

#### 2. **Populate (Join) Data**

```js
const posts = await Post.find().populate('author', 'name email');
```
This fetches posts along with the author’s name and email, similar to a SQL JOIN.

#### 3. **Update with Operators**

```js
await User.updateOne(
  { email: 'alice@example.com' },
  { $set: { name: 'Alicia' }, $inc: { loginCount: 1 } }
);
```

#### 4. **Delete Many with Criteria**

```js
await Post.deleteMany({ title: /test/i }); // deletes posts with 'test' (case-insensitive) in title
```

#### 5. **Aggregation (Analytics) Example**

```js
const stats = await Post.aggregate([
  { $group: { _id: '$author', totalPosts: { $sum: 1 } } },
  { $sort: { totalPosts: -1 } }
]);
```

#### 6. **Transactions (MongoDB Replica Set/Cluster Only)**

```js
const session = await mongoose.startSession();
session.startTransaction();
try {
  await User.create([{ name: 'Charlie' }], { session });
  await Post.create([{ title: 'Tx Post', author: userId }], { session });
  await session.commitTransaction();
} catch (err) {
  await session.abortTransaction();
} finally {
  session.endSession();
}
```

## Tips for Production Use

- Always validate user input and handle errors.
- Use transactions for multi-step, critical updates.
- Index relevant fields for faster queries.
- Use lean queries (e.g., `.lean()`) for larger/faster data retrieval when no document instance methods are needed.
- Prefer pagination over skip/limit for large datasets.

If you want code for a specific scenario (e.g., soft deletes, upsert, or optimistic locking), just ask!

