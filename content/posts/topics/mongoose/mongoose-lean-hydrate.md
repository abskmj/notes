---
title: "Lean option and Hydrate method in Mongoose"
date: 2019-03-08T03:09:10Z
tags: ["Topic","Mongoose","Model","Query", "Lean", "Hydrate"]
---

# Lean option on Query
While returning data from the database as an API response,  the virtuals/methods available on a mongoose document are unnecessary. [Lean option](https://mongoosejs.com/docs/api.html#query_Query-lean) can be set on such queries to return just the data directly from the database. It also improves the overall performance of the API.

> Documents returned from queries with the lean option enabled are plain javascript objects, not MongooseDocuments. They have no save method, getters/setters, or other Mongoose magic applied.

```javascript
app.use(async (req, res) => {
   let users = await User.find({ status: 'active' }).limit(10).lean();
   res.json(users);
});
```

# Hydrate method on Model
Hydrating is the opposite of the lean option. [Hydrate method](https://mongoosejs.com/docs/api.html#model_Model.hydrate) is used to initialize a mongoose document from a plain javascript object to get access to its virtuals/methods.

```javascript
let user = await User.findOne().lean();
let document = User.hydrate(user);

assert(document instanceof mongoose.Document); // true
```

# Code Repository
A working code repository is available at [github](https://github.com/abskmj/example-mongoose-lean-hydrate). Get started in your local machine.

```bash
git clone https://github.com/abskmj/example-mongoose-lean-hydrate.git
cd example-mongoose-lean-hydrate
npm install
npm test
```