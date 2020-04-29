# Nosql
#Disciplina Pós Data Science NoSql
#Exercio 1: Aquecendo com os pets

1: > db.pets.insert({name: "frodo", species: "peixe"})
WriteResult({ "nInserted" : 1 })
> db.pets.insert({name: "frodo", species: "Hamster"})
WriteResult({ "nInserted" : 1 })

2:> db.pets.find().count ()
  8

3:

4: > db.pets.find({name:"kilha"})
{ "_id" : ObjectId("5ea87e2fdca6cb5eadb8cdf8"), "name" : "kilha", "species" : "gato" }
 
5:

6: > db.pets.find({species:"Hamster"})
{ "_id" : ObjectId("5ea87e07dca6cb5eadb8cdf6"), "name" : "mike", "species" : "Hamster" }
{ "_id" : ObjectId("5ea87ea5dca6cb5eadb8cdfd"), "name" : "frodo", "species" : "Hamster" }
 

7:  > db.pets.find({name:"mike"})
{ "_id" : ObjectId("5ea87e07dca6cb5eadb8cdf6"), "name" : "mike", "species" : "Hamster" }
{ "_id" : ObjectId("5ea87e54dca6cb5eadb8cdf9"), "name" : "mike", "species" : "cachorro" }

8:

#Exercício 2 mama mia

1: > db.italians.find({age: 99}).count()
0
> db.italians.find({age: 99})

2: > db.italians.find({age: 65}).count()
134
 

3: > db.italians.find({"age": { "$gte": 12, "$lte": 18 }}).count()
844

 

4: > db.italians.find({dog: { $exists: true }}).count()
4017

> db.italians.find({cat: { $exists: true }}).count()
5991
 
> db.italians.find({cat: {$exists : false}, dog:{$exists : false}}).count()
2400
 

5: > db.italians.find({age: {"$gt":60}}, {cat: {$exists:true}}).count()
2431
 

6: > db.italians.find({age: {$gte: 12, $lte:18}}, {dog: {$exists: true}}).count()
844
 
7:

8: db.italians.find({ $and: [ { cat: { $exists: true }}, {$where: "this.age < this.cat.age"}]})

9:

10: db.italians.find({ bloodType: /.*-$/ }, {firstname: 1, surname: 1})

11: db.italians.find({ $where: "this.cat || this.dog" }, {"cat.name": 1, "dog.name": 1, _id: 0})

12: db.italians.find({ surname: "Rossi" }).limit(5).sort({ age: -1 })

13: > db.italians.insert( { "firstname": "Joseph", "surname": "Rotta", "leao": {name: "Adolf", age: 3}})
WriteResult({ "nInserted" : 1 })
 
14:  > db.italians.find({firstname: "Joseph" })
{ "_id" : ObjectId("5ea99308c82cfd867d62244a"), "firstname" : "Joseph", "surname" : "Rotta", "leao" : { "name" : "Adolf", "age" : 3 } }
> db.italians.find({"_id": ObjectId("5ea99308c82cfd867d62244a")})
{ "_id" : ObjectId("5ea99308c82cfd867d62244a"), "firstname" : "Joseph", "surname" : "Rotta", "leao" : { "name" : "Adolf", "age" : 3 } }
> db.italians.deleteOne({"_id": ObjectId("5ea99308c82cfd867d62244a")})
{ "acknowledged" : true, "deletedCount" : 1 }
> db.italians.find({"_id": ObjectId("5ea99308c82cfd867d62244a")})
>

15: > db.italians.update({}, {$inc: { age: 1, "cat.age": 1, "doc.age": 1 }}, { multi: true })
WriteResult({ "nMatched" : 10001, "nUpserted" : 0, "nModified" : 10001 })
 
16: > db.italians.find({age: 66, cat: {$exists: true}}).count()
134
> db.italians.remove({age: 66, cat: {$exists: true}})
WriteResult({ "nRemoved" : 134 })
> db.italians.find({age: 66, cat: {$exists: true}}).count()
0
>

17:

18: db.italians.aggregate([{ $group: { _id: "$firstname" } }])

19:

20: db.italians.find( { $and: [ {"age": { "$gt": 20, "$lt": 60 }}, { $or: [ {favFruits: ["Banana"]}, {favFruits: ["Maçã"]}]}, { $or: [ { dog: {$exists: true}}]} , { $or: [ { cat: {$exists: true}}]}]})

#Exercício 3 – Stockbrokers




