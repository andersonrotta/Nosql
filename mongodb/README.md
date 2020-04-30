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


1.	db.stocks.find( { "Profit Margin": { "$gt": 0.5 } } ).limit(10)

2.	db.stocks.find( { "Profit Margin": { "$lt": 0 } } ).limit(10)

3.	db.stocks.find().limit(10).sort({ "Profit Margin": -1 })

4.	> db.stocks.find({}, {"Sector": 1}).limit(1).sort({ "Profit Margin": -1 })
{ "_id" : ObjectId("52853801bb1177ca391c1af3"), "Sector" : "Basic Materials" }

5.	>
 
6.	> db.stocks.updateMany( {}, { $rename: { "Profit Margin": "profit" } } )
{ "acknowledged" : true, "matchedCount" : 6756, "modifiedCount" : 4302 }

7.> > db.stocks.find({}, {"Company": 1, "profit": 1})
{ "_id" : ObjectId("52853800bb1177ca391c1802"), "Company" : "iShares MSCI AC Asia Information Tech" }
{ "_id" : ObjectId("52853800bb1177ca391c1803"), "Company" : "Altisource Asset Management Corporation" }
{ "_id" : ObjectId("52853800bb1177ca391c17ff"), "Company" : "Agilent Technologies Inc.", "profit" : 0.137 }
{ "_id" : ObjectId("52853800bb1177ca391c1800"), "Company" : "Alcoa, Inc.", "profit" : 0.013 }
{ "_id" : ObjectId("52853800bb1177ca391c1801"), "Company" : "WCM/BNY Mellon Focused Growth ADR ETF" }
{ "_id" : ObjectId("52853800bb1177ca391c1805"), "Company" : "Aaron's, Inc.", "profit" : 0.06 }
{ "_id" : ObjectId("52853800bb1177ca391c1806"), "Company" : "Applied Optoelectronics, Inc.", "profit" : -0.023 }
{ "_id" : ObjectId("52853800bb1177ca391c1804"), "Company" : "Atlantic American Corp.", "profit" : 0.056 }
{ "_id" : ObjectId("52853800bb1177ca391c180a"), "Company" : "American Assets Trust, Inc.", "profit" : 0.155 }
{ "_id" : ObjectId("52853800bb1177ca391c1808"), "Company" : "Advance Auto Parts Inc.", "profit" : 0.063 }
{ "_id" : ObjectId("52853800bb1177ca391c1809"), "Company" : "Apple Inc.", "profit" : 0.217 }
{ "_id" : ObjectId("52853800bb1177ca391c180b"), "Company" : "Almaden Minerals Ltd." }
{ "_id" : ObjectId("52853800bb1177ca391c180c"), "Company" : "Advantage Oil & Gas Ltd.", "profit" : -0.232 }
{ "_id" : ObjectId("52853800bb1177ca391c180e"), "Company" : "iShares MSCI All Country Asia ex Jpn Idx" }
{ "_id" : ObjectId("52853800bb1177ca391c180d"), "Company" : "Atlas Air Worldwide Holdings Inc.", "profit" : 0.071 }
{ "_id" : ObjectId("52853800bb1177ca391c1807"), "Company" : "AAON Inc.", "profit" : 0.105 }
{ "_id" : ObjectId("52853800bb1177ca391c180f"), "Company" : "AllianceBernstein Holding L.P.", "profit" : 0.896 }
{ "_id" : ObjectId("52853800bb1177ca391c1811"), "Company" : "ABB Ltd.", "profit" : 0.069 }
{ "_id" : ObjectId("52853800bb1177ca391c1810"), "Company" : "Abaxis Inc.", "profit" : 0.1 }
{ "_id" : ObjectId("52853800bb1177ca391c1812"), "Company" : "AbbVie Inc.", "profit" : 0.24 }
Type "it" for more
>

8.

9. db.stocks.aggregate([{ $group: { _id: "$Sector" } }])
> db.stocks.aggregate([{ $group: { _id: "$Sector" } }])
{ "_id" : "Technology" }
{ "_id" : "Financial" }
{ "_id" : "Healthcare" }
{ "_id" : "Consumer Goods" }
{ "_id" : "Industrial Goods" }
{ "_id" : "Utilities" }
{ "_id" : "Basic Materials" }
{ "_id" : "Services" }
{ "_id" : "Conglomerates" }
>

#Exercício 3 – Fraude na Enron!




