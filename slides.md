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

# Exercise: Mongoose
(30 min) Install mongoose and use it in our node app to interact with mongoDB

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

# Exercise: Mongoose
- create new basic node project
- in compass, click cluster's 3-dot-menu > copy Connection String
- `npm i mongoose`
```js
const mongoose = require('mongoose');
// paste connection string below  
mongoose.connect('mongodb://some-path-name/DBname') // Ensure DBname is present otherwise data will go to test db
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

# Exercise: Mongoose

```js
async function createOrder(order) {
  try {
    const result = await Order.create(order);
    console.log("Order created: ", result);
  } catch (e) {
    console.log("Error: ", err);
  } finally {
    mongoose.connection.close(); // what happens if you comment this line out?
  }
}

createOrder({
  id: 1, // what happens now if you try adding a new property that wasn't specified in the schema 
  name: "albert", 
  isReady: false,
  orders: ["2 fries", "2 tacos"],
});
```

- run it to see if it inserted documents in the database (in Compass click refresh underneath Reset button)
- Notice we used mongoose's `createOrder({})` rather than mongoDB's `db.orders.insertOne({})`
- So how did mongoose know to target `orders` collection within the foodtruck database?

---
transition: slide-left
---

# Exercise: Schemas
(30 min) 

- What are schemas and models?
- See [schema docs](https://mongoosejs.com/docs/guide.html)
   - Everything starts with a schema which defines the shape of the documents
- See [schema types](https://mongoosejs.com/docs/schematypes.html)
- See [model docs](https://mongoosejs.com/docs/models.html)
   - Models create, read, update, delete documents from the database
- Challenge #1:
   1. Define a schema for a `Student` with the following fields: `name`, `age`, `isEnrolled`
   1. Create a Model from the Schema
   1. Create a new student and save it to DB

Goto next slide...

---
transition: slide-left
---

# Exercise: Schemas

- Challenge #2: Adjust the `Student` schema to include [validation](https://chanwingkeihaha.medium.com/validation-in-mongoose-where-how-and-handle-errors-b44f68cccae3) as follows:
   - String, required
   - age: Number, required, must be at least 16
   - isEnrolled: Boolean, default to true
   - grades: Array of numbers

- Stretch goal: Reorganize folder structure to emulate the following:
```
mongoose-practice/
│
├── models/
│   └── Student.js      // where schema/model definition is exported
├── index.js            // where you can import schema/model here
└── package.json
```
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

# Exercise 
(30 min) 


<!--
-->


---
transition: slide-left
---

# Exercise
(30 min) 

- 

<!--
-->

---
transition: slide-left
---

# Homework

- Make a To-Do List App with MongoDB [see instructions in LMS](https://courses.circuitstream.com/d2l/le/lessons/9514/topics/49825)