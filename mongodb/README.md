# Nosql
#Disciplina Pós Data Science NoSql
#Exercio 1

1 > db.pets.insert({name: "frodo", species: "peixe"})
WriteResult({ "nInserted" : 1 })
> db.pets.insert({name: "frodo", species: "Hamster"})
WriteResult({ "nInserted" : 1 })

2> db.pets.find().count ()
  8

3 

4 > db.pets.find({name:"kilha"})
{ "_id" : ObjectId("5ea87e2fdca6cb5eadb8cdf8"), "name" : "kilha", "species" : "gato" }
 
5

6 > db.pets.find({species:"Hamster"})
{ "_id" : ObjectId("5ea87e07dca6cb5eadb8cdf6"), "name" : "mike", "species" : "Hamster" }
{ "_id" : ObjectId("5ea87ea5dca6cb5eadb8cdfd"), "name" : "frodo", "species" : "Hamster" }
 

7  > db.pets.find({name:"mike"})
{ "_id" : ObjectId("5ea87e07dca6cb5eadb8cdf6"), "name" : "mike", "species" : "Hamster" }
{ "_id" : ObjectId("5ea87e54dca6cb5eadb8cdf9"), "name" : "mike", "species" : "cachorro" }

 



