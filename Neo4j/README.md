# Nosql
#Disciplina Pós Data Science NoSql

1.1 call db.propertyKeys

1.2

1.3 match(p:Person) return p

1.4 match(m:Movie) return m

2.1 match(m:Movie{released: 2000}) return m

2.2 match(m:Movie{released: 2000}) return m.movie, m.released

2.3

2.4 match(m:Movie{released: 2000}) return m.title, m.released

2.5 match(m:Movie{released: 2000, tagline:"The rest of his life begins now"}) return m

2.6 match(m:Movie{released: 2000}) return m.title, m.released

3.1

3.2 match (p:Person)-[:WROTE]->(m:Movie{title: 'Speed Racer'}) return p, m

3.3 match (p:Person)-->(m:Movie) where p.name='Tom Hanks'return m.title

3.4 match (p:Person)-[rel]->(m:Movie) where p.name='Tom Hanks'return m.title, type(rel)

3.5 match (p:Person)-[:ACTED_IN]->(m:Movie) where p.name='Tom Hanks'return m.title

4.1 match (p:Person)-[:ACTED_IN]->(m:Movie) where p.name='Tom Cruise'return m.title

4.2 match(p:Person) where p.born = 1970 return p.name

4.3 match(p:Person)-[:ACTED_IN]->(m:Movie)
where m.title='The Matrix' and p.born > 1960
return p.name, p.born as yearBorn

4.4 match(m:Movie {released:2009}) return m.movie, m.title

4.5 match(a:Person)-[:ACTED_IN]->[m:movie]<-[:DIRECTED]-[d:person]
return a.name, m.title, d.name

4.6 match (p:Person) where p.born > 1950 OPTIONAL MATCH(p) -[r:WROTE]->(m:Movie)
return p.name, p.born, m.title, type(r)

4.7

4.8 match (p:Person) where p.name STARTS WITH 'James' 
Return p.name

4.9

4.10 

4.11 MATCH (p:Person)-[:ACTED_IN]->(m:Movie)<-[:DIRECTED]-(d:Person)
return m.title, p.name

4.12 match (m:Movie)
where m.released IN [1999, 2000]
return m.title, m.released

4.13 match (p)-[:ACTED_IN]->(m)
where p:Person and m.movie
return p.name, m.title
