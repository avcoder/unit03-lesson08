---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /assets/intro.jpg
# some information about your slides (markdown enabled)
title: Software Development | Foundations
info: |
  ## Software Development | Foundations
# apply unocss classes to the current slide
class: text-left
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Mongoose
Back-End Development - part 8/12
- [ ] Schemas and models
- [ ] Create/Read MongoDB documents with Mongoose models
- [ ] Update/Delete MongoDB documents with Mongoose models

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
-->

---
transition: slide-left
---

# Recap
(10 min)

1. what command is used to view all databases in MongoDB?
1. how do you switch to a databased named `school` in the MongoDB shell?
1. what does the following command do? `db.createCollection("students")`
1. how would you insert a document into a collection called `books`?
1. what is the result of running this command? `db.students.find()`
1. what does `db.students.updateOne({ name: "Al"}, {$set: {age: 22}})` do?
1. Does MongoDB allow you to just randomly add any new property/value when updating an existing document without validation?
1. In Data Modeling, list the 3 types of relationships we discussed
- fyi: Compass has equivalent CRUD actions (see buttons: "Add Data", "Update", "Delete")

<!--
1. show dbs
2. use school
3. creates a new collection named students
4. db.books.insert({title: 'ABC'})
5. returns all documents in the students collection
6. updates one student named Al and sets their age to 22
-->

---
transition: slide-left
---

# Mongoose
(10 min) Install mongoose and use it in our node app to interact with mongoDB

- mongoose is an ODM (similar to ORM but used with document databases instead of relational)
   - a library that helps us talk to the database with our preferred programming language
   - since we we can't use mongo shell commands in our API
   - allows us to model data via schemas
   - establish relationships with models
   - mongoose DOES care if you try to randomly add a new property (it won't allow it)
   - adds support for Promises
- mongoose is open source and is made by Automatic, the same people who own Wordpress
- we use mongoose to interact with mongoDB

---
transition: slide-left
---

# Exercise #1: Mongoose
(30 mins)

- create new basic node project (in compass, copy Connection String)
```js
const mongoose = require('mongoose');
// paste connection string below and
// Ensure DBname is present otherwise data will go to test db
const connect = () => {
  return mongoose.connect('mongodb://some-path-name/DBname') 
}
```
- then we need to create a Schema (this is our mongoose's way of wrapping structure and validation around mongoDB to ensure you can't just randomly insert new properties)
```js
const OrderSchema = new mongoose.Schema({
  name: String,
  isReady: Boolean,
  orders: [String],
});

const Order = mongoose.model("order", OrderSchema);
```

Goto next slide

<!--
-->

---
transition: slide-left
---

# Exercise #1 continued: Mongoose

```js
connect()
  .then(async connection => {
    const order = await Order.create({
      name: "albert", 
      isReady: false,
      orders: ["2 fries", "2 tacos"],
    });
    console.log(order)
    await mongoose.connection.close();
  })
  .catch((e) => {
    console.error(e);
    mongoose.connection.close();
  });
```

- run it to see if it inserted documents in the database (in Compass click refresh underneath Reset button)
- Notice we used mongoose's `createOrder({})` rather than mongoDB's `db.orders.insertOne({})`
- So how did mongoose know to target `orders` collection within the foodtruck database?

Goto next slide

---
transition: slide-left
---

# Exercise #1 continued: 💡 Personal Project Ideas 💡

Take what you've just learned and apply it to your personal interest (see below for project ideas). Whatever idea you choose, we'll use it thoughout the next several weeks.  After each group exercise, you will be asked to incrementally apply what you've learned to your personal project.

- 📈 Task Management App: Create a Task schema with title, description, completed, and dueDate
- 🍉 Grocery List App | Schema: name, quantity, purchased (Boolean), category
- 👩‍🏫 Student Attendance Tracker | Schema: studentName, class, date, isPresent
- 🎥 Movie Watchlist | Schema: movieTitle, watched, genre, rating
- 🏃‍♂️ Habit Tracker | Schema: habitName, startDate, streakCount, completedToday
- ☎️ Contact Manager | Schema: name, email, phone, isFavorite
- 📚 Book Library | Schema: title, author, isCheckedOut, checkedOutBy, dueDate
- 🛒 Simple E-commerce Product Catalog | Schema: productName, price, inStock, categories, description
- 💡 whatever hobby/interest you like 

---
transition: slide-left
---

# Exercise #2: Schemas
(30 min) 

- What are schemas and models?
- Read ["Defining your schema"](https://mongoosejs.com/docs/guide.html)
   - Everything starts with a schema which defines the shape of the documents
- Read ["What is a SchemaType"](https://mongoosejs.com/docs/schematypes.html) to be aware of all 15 schema types
- Read ["Compiling your first model" and "Constructing Documents"](https://mongoosejs.com/docs/models.html) to know how Models are used
- Challenge #1: Create a new node app similar to Exercise #1 but this time...
   1. Define a schema for a `Student` with the following fields: `name`, `age`, `isEnrolled`
   1. Create a Model from the Schema
   1. Create a new student and save it to DB
   1. check Compass: Did data save to your Students collection?

Goto next slide...

---
transition: slide-left
---

# Exercise #2 continued: Schemas

- Challenge #2: Adjust the `Student` schema to include [validation](https://chanwingkeihaha.medium.com/validation-in-mongoose-where-how-and-handle-errors-b44f68cccae3) as follows:
   - name: should be a String and must be a required field
   - age: should be a Number, required, must be at least 16
   - isEnrolled: should be Boolean whose default value is set to true
   - grades: should be an Array of numbers

- Stretch goal: Reorganize folder structure (hint use `module.exports = Student`) to emulate the following:
```
mongoose-practice/
│
├── models/
│   └── Student.js      // where schema/model definition is exported
├── index.js            // where you can import schema/model here
└── package.json
```

💡 Apply Schemas with validation to your personal project 💡

---
layout: image-right
transition: slide-left
image: /assets/moss.png
backgroundSize: 500px 110px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 🏃 [Mongoose Getting Started](https://mongoosejs.com/docs/)
- 🗺️ [Mongoose Guides](https://mongoosejs.com/docs/guides.html)
- ✅ [Mongoose Validation](https://mongoosejs.com/docs/validation.html)

<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)

<!-- 
- take attendance
-->

---
transition: slide-left
---

# Exercise #3: CRUD with Models
(30 min) 

Time to put our previous foodtruck Express app, with mongoose/mongo and put it all together.  Your mission: Implement the following CRUD operations for our Express [food truck/orders app](https://github.com/avcoder/food-truck-express).  May ask ChatGPT: "in learning mongoose/mongodb and express, how do i incorporate a basic find command inside a route?"

- Read ["Querying" section](https://mongoosejs.com/docs/models.html#querying)
   - Test it out; convince yourself it works in your basic mongoose index.js file
   - Create an express foodtruck endpoint that returns all data 
- Read ["Deleting" section](https://mongoosejs.com/docs/models.html#deleting)
   - Test it out... then Create an express foodtruck endpoint that deletes based on id (or name)
- Read ["Updating" section](https://mongoosejs.com/docs/models.html#updating)
   - Test it out... then Create an express foodtruck update endpoint based on search/replace criteria

💡 Apply CRUD operations to your personal project 


<!--
-->


---
transition: slide-left
---

# Exercise #4: 
(remainder of time) Incorporate a basic front end page to test your work so far

Download or `git clone` my [basic HTML table page](https://github.com/avcoder/basic-table) that should work for 💡 your project idea 💡 (and/or food truck app)

- Put it in a new folder which you can launch with "Go Live"
- Modify the table columns to fit your project app's needs
- Add client-side JavaScript (can use ChatGPT to help scaffold some quick ideas) to fetch from your express endpoints
- Challenge #1: display all data upon requesting from your GET all endpoint

Stretch goals below:
- Challenge #2: delete a row upon requesting from your DELETE endpoint **
- Challenge #3: update a row upon requesting from your UPDATE endpoint
- Challenge #4: create a new row upon requesting from your POST endpoint
- Challenge #5: filter data when a user types a keyword in the search box

** Discuss: How should you handle the response?  Fetch GET / again to get all rows? or frontend solution? 



<!--
-->

---
transition: slide-left
---

# Homework

- Make a To-Do List App with MongoDB [see instructions in LMS](https://courses.circuitstream.com/d2l/le/lessons/9514/topics/49825)