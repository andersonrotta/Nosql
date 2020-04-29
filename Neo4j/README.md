# Nosql
#Disciplina Pós Data Science NoSql

1.1. call db.propertyKeys

1.2.

1.3. match(p:Person) return p

1.4. match(m:Movie) return m

2.1. match(m:Movie{released: 2000}) return m

2.2. match(m:Movie{released: 2000}) return m.movie, m.released

2.3.

2.4. match(m:Movie{released: 2000}) return m.title, m.released

2.5. match(m:Movie{released: 2000, tagline:"The rest of his life begins now"}) return m

2.6. match(m:Movie{released: 2000}) return m.title, m.released

3.1.

3.2. match (p:Person)-[:WROTE]->(m:Movie{title: 'Speed Racer'}) return p, m

3.3. match (p:Person)-->(m:Movie) where p.name='Tom Hanks'return m.title

3.4. match (p:Person)-[rel]->(m:Movie) where p.name='Tom Hanks'return m.title, type(rel)

3.5. match (p:Person)-[:ACTED_IN]->(m:Movie) where p.name='Tom Hanks'return m.title

4.1. match (p:Person)-[:ACTED_IN]->(m:Movie) where p.name='Tom Cruise'return m.title

4.2. match(p:Person) where p.born = 1970 return p.name

4.3. match(p:Person)-[:ACTED_IN]->(m:Movie)
where m.title='The Matrix' and p.born > 1960
return p.name, p.born as yearBorn

4.4. match(m:Movie {released:2009}) return m.movie, m.title

4.5. match(a:Person)-[:ACTED_IN]->[m:movie]<-[:DIRECTED]-[d:person]
return a.name, m.title, d.name

4.6. match (p:Person) where p.born > 1950 OPTIONAL MATCH(p) -[r:WROTE]->(m:Movie)
return p.name, p.born, m.title, type(r)

4.7.

4.8. match (p:Person) where p.name STARTS WITH 'James' 
Return p.name

4.9.

4.10. 

4.11. MATCH (p:Person)-[:ACTED_IN]->(m:Movie)<-[:DIRECTED]-(d:Person)
return m.title, p.name

4.12. match (m:Movie)
where m.released IN [1999, 2000]
return m.title, m.released

4.13. match (p)-[:ACTED_IN]->(m)
where p:Person and m.movie
return p.name, m.title

5.1.

5.2.

5.3. match (follower:person)-[:FOLLOWS*3]->(p:person)
where follower.name = 'Tom Hanks'
return p

5.4. match (follower:person)-[:FOLLOWS*1..2]->(p:person)
where follower.name = 'Tom Hanks'
return p

5.5. 

5.6. MATCH (p:Person) WHERE p.name STARTS WITH 'Neo'
OPTIONAL MATCH (p)-[r:REVIEWED]->(m:Movie)
RETURN p.name, type(r), m.title

5.7.

5.9.

5.10.

5.11. match (a:person)-[:ACTED_IN]->(m:Movie)
with a, count(a) AS numMovies, collect(m.title) as
movies
where numMovies = 5
return a.name, numMovies, movies

5.12.

6.1.

6.2. MATCH (p:Person)-[:DIRECTED | :ACTED_IN]->(m:Movie)
WHERE p.name = 'Tom Cruise’
RETURN m.released, collect(DISTINCT m.title) AS movies

6.3.

6.4. MATCH (p:Person)-[:DIRECTED | :ACTED_IN]->(m:Movie)
WHERE p.name = 'Tom Cruise’
RETURN m.released, collect(DISTINCT m.title) AS movies
Order by m.releaed desc

6.5. MATCH (p:Person)-[:DIRECTED | :ACTED_IN]->(m:Movie)
WHERE p.name = 'Tom Cruise’
RETURN m.released, collect(DISTINCT m.title) AS movies
Order by m.releaed ASC

6.6. match (a:person)-[:ACTED_IN]->(m:Movie)
with a, count(a) AS numMovies, collect(m.title) as
movies
where numMovies <= 3
return a.name, numMovies, movies

7.1.

7.2. MATCH (a:Person)-[:ACTED_IN]->(m:Movie)
WITH m, count(m) AS numCast, collect(a.name) as cast
RETURN m.title, cast, numCast ORDER BY size(cast)

7.3. 

7.4. MATCH (p:Person)-[:ACTED_IN]->(:Movie)
WHERE exists(p.born)// calculate the age
WITH DISTINCT p, date().year - p.born as age
RETURN p.name, age as `age today`
ORDER BY p.born DESC

#Exercício 8 – Creating nodes

8.1. create (:Movie {title: 'Maquina Mortifera'})
Added 1 label, created 1 node, set 1 property, completed after 284 ms.

 

8.2. match (m:Movie{title:"Maquina Mortifera"}) return m

 

8.3. create(:Person{name:"Mel Gibson"})

Added 1 label, created 1 node, set 1 property, completed after 64 ms.

8.4. match(m{name:"Mel Gibson"}) return m

8.5. match (m:Movie)
where m.title = "Maquina Mortifera"
set m: filmedeacao
return distinct labels(m)

8.6. match(m:filmedeacao) return m.title, m.released

8.7. match (p:Person)
where p.name starts with 'Emile'
set p: Female

8.8. match(p:Female) return p

8.9. match (p:Female) remove p:Female

8.10. call db.schema.visualization()

8.11. match (m:Movie{title:"Maquina Mortifera"})
set m:filmedeacao,
m.released = 1987,
m.tagline = "Voce ja Conheceu alguem que nao matou?",
m.lengthInMinutes = 117

8.12. match(m:filmedeacao{title:"Maquina Mortifera"}) return m

8.13. match(p:Person{name:"Mel Gibson"})
set p.birthPlace = " Peekskill, Nova York, EUA",
p.born = 1956

8.14. match (p:Person{name:"Mel Gibson"}) return p

8.15. match(m:Movie{title:"Maquina Mortifera"})
remove m.tagline

8.16. match(m:Movie{title:"Maquina Mortifera"}) return m

8.17. match(p:Person{name:"Mel Gibson"}) remove p.born

8.18. match (p:Person{name:"Mel Gibson"}) return p

#Exercício 9 – Creating relationships

9.1. match(m:Movie{title:"Maquina Mortifera"})
match(p:Person) where p.name in ["Mel Gibson"]
create (p)-[:ACTED_IN]->(m)
9.2. match(m:Movie{title:"Maquina Mortifera"})
match(p:Person{name:"Richard Donner"})
create (p)-[:DIRECTED]->(m)

9.3. match(p:Person{name:"Mel Gibson"})
match(p2:Person{name:"Danny Glover"})
create (p)-[:HELPED]->(p2)

9.4. match (p:Person)--(m:Movie{title:"Maquina Mortifera"}) return m, p

9.5. match(p:Person)-[r]-(:Movie{title:"Maquiana Mortifera"})
set r.roles =
case p.name
    when "Mel Gibson" then ["Martin Riggs"]
    when "Danny Glover " then ["Roger Murtaugh"]  
end

9.6.

9.7. call db.propertyKeys

9.8. call db.schema.visualization

9.9. match(p:Person)-[r:ACTED_IN]-(:Movie{title:"Maquina Mortifera"})
return p.name, r.roles

9.10. match (p:Person)-[:HELPED]-(p2:Person) return p,p2

9.11.

9.12.

9.13. match(p:Person)-[:ACTED_IN]-(m:Movie{title:"Maquina Mortifera"}) return p,m

$Exercício 10 – Deleting nodes and relationships

10.1. match (:Person)-[h:HELPED]->(:Person) delete h

10.2. match (:Person)-[h:HELPED]->(:Person) return h

10.3. match (mm:Movie)-[r]-(outro) where mm.title = 'Maquina Mortifera' return mm, r, outro

10.4. 


10.5. match (mm:Movie) where mm.title = 'Maquina Mortifera' detach delete mm

10.6. match (mm:Movie)-[r]-(outro) where mm.title = 'Maquina Mortifera' return mm, r, outro

