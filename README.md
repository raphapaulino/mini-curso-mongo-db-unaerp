# No-SQL Crash-Course
## Installation

[Ubuntu (Ubuntu already has git installed)](https://ubuntu.com/download/desktop/)

[Git](https://git-scm.com/downloads/)

[MongoDB](https://www.mongodb.com/docs/manual/installation/) (Version: 6.0 LTS)

[Install MongoDB on Ubuntu](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/)

[NodeJS](https://nodejs.org/en/)

<hr>

## Some Concepts and Tips - Data Type

**"word"** - string (case sensitive)

**126** - number

**36.50** - floating points: double | float

**{  }** - object - brackets 

**[  ]** - array - list

**somethingCalled()** - function

**true** / **false** - boolean

<hr>

## Some Concepts and Tips - CRUD

**C** reate

**R** ead

**U** pdate

**D** elete

<hr>

## Basic Commands
```
$ mongosh
```
```
test> show dbs
```
```
test> use appdb
```
```
appdb> show collections
```
```
appdb> db.users.insertOne({ name: "John"  })
```
```
appdb> db.dropDatabase()
```
```
appdb> exit 
```
```
$ mongosh
```
```
test> show dbs
```
```
test> use appdb
```
```
appdb> db
```

## Insert Commands
```
appdb> db.users.insertOne({ name: "John"  })
```
```
appdb> db.users.find()
```
```
appdb> db.users.insertOne({ name: "Sally", age: 19, address: { street: "987 North St" }, hobbies: ["Running"]  })
```
```
appdb> db.users.find()
```
```
appdb> db.users.insertMany([{ name: "Kyle", age: 26, hobbies: ["Weight Lifting", "Bowling"], address: { street: "123 Main St", city: "New York City"}}, { name: "Billy", age: 41, hobbies: ["Swimming", "Bowling"], address: { street: "442 South St", city: "New York City"}}])
```
```
appdb> db.users.find()
```
```
appdb> db.users.insertMany([{ name: "Jill" }, { name: "Mike" }])
```

## Basic Query Commands - Part 1

```
appdb> db.users.find().limit(2)
```
```
appdb> db.users.find()
```
```
appdb> db.users.find().sort({ name: 1 }).limit(2)
```
```
appdb> db.users.find().sort({ name: -1 }).limit(2)
```
```
appdb> db.users.find().sort({ age: 1, name: -1 }).limit(2)
```
```
appdb> db.users.find().sort({ age: -1, name: -1 }).limit(2)
```
```
appdb> db.users.find().limit(2)
```
```
appdb> db.users.find().skip(1).limit(2)

```

## Basic Query Commands - Part 2

```
appdb> db.users.find({ name: "Kyle" })
```
```
appdb> db.users.find({ name: /k/ })
```
```
appdb> db.pessoas.find({ name: /k/i })
```
```
appdb> db.users.find({ name: /^Bi/ })
```
```
appdb> db.users.find({ name: /ly$/ })
```
```
appdb> db.users.find({ age: 26 })
```
```
appdb> db.users.find({ age: "26" })
```
```
appdb> db.users.find({ name: "Kyle" }, { name: 1, age: 1 })
```
```
appdb> db.users.find({ name: "Kyle" }, { name: 1, age: 1, _id: 0 })
```
```
appdb> db.users.find({ name: "Kyle" }, { age: 0 })
```

## Complex Query Commands - Part 1
```
appdb> db.users.find({ name: { $eq: "Sally" }})
```
```
appdb> db.users.find({ name: { $ne: "Sally" }})
```
```
appdb> db.users.find({ age: { $gt: 13 }})
```
```
appdb> db.users.find({ age: { $gte: 19 }})
```
```
appdb> db.users.find({ age: { $lte: 19 }})
```
```
appdb> db.users.find({ age: { $lt: 19 }})
```
```
appdb> db.users.find({ name: { $in: ["Kyle", "Sally"] }})
```
```
appdb> db.users.find({ name: { $nin: ["Kyle", "Sally"] }})
```

## Complex Query Commands - Part 2

```
appdb> db.users.find({ age: { $exists: true }})
```
```
appdb> db.users.find({ age: { $exists: false }})
```
```
appdb> db.users.insertOne({ age: null, name: "Bill" })
```
```
appdb> db.users.find({ age: { $exists: true }})
```
```
appdb> db.users.find({ age: { $gte: 20, $lte: 40 }})
```
```
appdb> db.users.find({ age: { $gte: 20, $lte: 40 }, name: "Sally" })
```
```
appdb> db.users.find({ age: { $gte: 20, $lte: 40 }, name: "Kyle" })
```
```
appdb> db.users.find({ $and: [{ age: 26 }, { name: "Kyle" }] })
```

## Complex Query Commands - Part 3

```
appdb> db.users.find({ $or: [{ age: { $lte: 20 } }, { name: "Kyle" }] })
```
```
appdb> db.users.find({ age: { $not: { $lte: 20 } }})
```
```
appdb> db.users.find({ age: { $gt: 20 } })
```
```
db.users.insertMany([{ name: "Tom", balance: 100, debt: 200 }, { name: "Kristin", balance: 20, debt: 0 }])
```
```
appdb> db.users.find({ $expr: { $gt: ["debt", "balance"]} })
```
```
appdb> db.users.find({ $expr: { $gt: ["$debt", "$balance"]} })
```
```
appdb> db.users.find({ "address.street": "123 Main St" })
```
```
appdb> db.users.findOne({ age: { $lte: 40 }})
```
```
appdb> db.users.countDocuments({ age: { $lte: 40 }})

```

## Update Commands - Part 1
```
appdb> db.users.updateOne({ age: 26 }, { age: 27 })
```
```
appdb> db.users.updateOne({ age: 26 }, { $set: { age: 27 } })
```
```
appdb> db.users.updateOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") }, { $set: { name: "New Name" } })
```
```
appdb> db.users.findOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") })
```
```
appdb> db.users.updateOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") }, { $inc: { age: 3 }})
```
```
appdb> db.users.findOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") })
```

## Update Commands - Part 2

```
appdb> db.users.updateOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") }, { $rename: { name: "firstName" }})
```
```
appdb> db.users.updateOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") }, { $unset: { age: "" } })
```
```
appdb> db.users.findOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") })
```
```
appdb> db.users.updateOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") }, { $push: { hobbies: "Swimming" } })
```
```
appdb> db.users.findOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") })
```
```
appdb> db.users.updateOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") }, { $pull: { hobbies: "Bowling" } })
```
```
appdb> db.users.findOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") })
```

## Update Commands - Part 3

```
appdb> db.users.updateMany({ address: { $exists: true }}, { $unset: { "address.city": ""  }} )
```
```
appdb> db.users.updateMany({ address: { $exists: true }}, { $unset: { address: ""  }} )
```
```
appdb> db.users.updateOne({ _id: ObjectId("6360f68b1f6e56ddc88efcf0") }, { $unset: { age: "" } })
```
```
appdb> db.users.find()
```
```
appdb> db.users.replaceOne({ age: 30 }, { name: "John" })
```
```
appdb> db.users.find({ name: "John" })
```

## Delete Commands

```
appdb> db.users.deleteOne({ name: "John" })
```
```
appdb> db.users.find({ name: "John" })
```
```
appdb> db.users.deleteMany({ age: { $exists: false }})
```
```
appdb> db.users.find()
```
```
appdb> db.users.drop()
```

## Do you have any doubts about the course?

[WhatsApp Group](https://chat.whatsapp.com/HlshTARZCLKDZpW2ZXRlWv)

## Contacts

[LinkedIn](https://www.linkedin.com/in/raphaelalvespaulino/)

[GitHub](https://github.com/raphapaulino/)

[My Portfolio](https://www.raphaelpaulino.com.br/)

[The Company](https://633k.com.br/)