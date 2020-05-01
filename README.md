# neoj4
Exercício 1- Retrieving Nodes  

1.1 Retrieve all nodes from the database.  
`match (n) return (n)`  

1.2 Examine the data model for the graph.  
`call db.schema.visualization`  

1.3 Exercise 1.3: Retrieve all Person nodes.  (131 pessoas)  
`match (p:Person) return p`  

1.4 Exercise 1.4: Retrieve all Movie nodes. (38 filmes)   
`match (m:Movie) return m`  

Exercício 2 – Filtering queries using property values  

2.1 Retrieve all movies that were released in a specific year.  
`match (m:Movie{released:1995}) where exists (m.released) return m`  

2.2 View the retrieved results as a table. 
Visualizado no Browser do Neo4j em formato de tabela.  

2.3 Query the database for all property keys.     
`call db.propertyKeys`

2.4 Retrieve all Movies released in a specific year, returning their titles.    
`match(m:Movie{released:1995}) return m.title`  

2.5 Display title, released, and tagline values for every Movie node in the graph.   
`match(m:Movie) return m.title, m.released, m.tagline`  

2.6 Display more user-friendly headers in the table.  
`match(m:Movie) return m.title as título, m.released as lançamento, m.tagline as slogan`  

Exercício 3 - Filtering queries using relationships

3.1 Display the schema of the database.  
`call db.schema.visualization`  

3.2 Retrieve all people who wrote the movie Speed Racer.  
`match(p:Person)-[rel:WROTE]->(m:Movie{title:'Speed Racer'}) return p`

3.3 Retrieve all movies that are connected to the person,Tom Hanks.  
`match (m:Movie) <-- (p:Person {name: 'Tom Hanks'}) return m.title`

3.4 Retrieve information about the relationships Tom Hanks had with the set of movies retrieved earlier.  
`match (m:Movie) -[rel]- (p:Person {name: 'Tom Hanks'}) return m.title, type(rel)`

3.5 Retrieve information about the roles that Tom Hanks acted in.  
`match (m:Movie) -[rel:ACTED_IN]- (p:Person {name: 'Tom Hanks'}) return m.title, type(rel)`

Exercício 4 – Filtering queries using WHERE clause

4.1: Retrieve all movies that Tom Cruise acted in.  
`match (m:Movie) -[rel:ACTED_IN]- (p:Person {name: 'Tom Cruise'}) return m.title, type(rel)`  

4.2: Retrieve all people that were born in the 70’s.
`match (p:Person) where p.born >= 1970 and p.born <= 1979 return p.name, p.born`  
  
4.3: Retrieve the actors who acted in the movie The Matrix who were born after 1960.  
`match (p:Person)-[rel:ACTED_IN]->(m:Movie{title:'The Matrix'}) where p.born > 1960 return p.name, p.born`  

4.4: Retrieve all movies by testing the node label and a property.   
`match (m:Movie) where m.title = 'The Matrix' return m`  

4.5: Retrieve all people that wrote movies by testing the relationship between two nodes.  
`match (p:Person)-[rel:WROTE]->(m:Movie) return p.name, m.title`  


4.6: Retrieve all people in the graph that do not have a property.  
`match (m:Movie) where not exists (m.tagline) return m`    


4.7: Retrieve all people related to movies where the relationship has a property. 
`match(p:Person)-[rel]->(m:Movie) where exists(rel.roles) return p.name,m.title, rel.roles`    


4.8: Retrieve all actors whose name begins with James.  
`match(p:Person) -[rel:ACTED_IN]->(m:Movie) where p.name =~ 'James.*'  return p.name, m.title, rel`  

4.9: Retrieve all REVIEW relationships from the graph with filtered results.  
`match (p:Person)-[rel:REVIEWED]->(m:Movie) where m.released > 2010  return m.title, m.released`  

4.10: Retrieve all people who have produced a movie, but have not directed a movie.  
`match (p:Person)-[:PRODUCED]->(m:Movie) where not ((p)-[:DIRECTED]->(:Movie)) return p.name,m.title`  

4.11: Retrieve the movies and their actors where one of the actors also directed the movie.   
`match (p:Person)-[:ACTED_IN]->(m:Movie)<-[:ACTED_IN]-(p2:Person) where exists{match (p)-[:DIRECTED]->(m)} return p.name as `Ator e Diretor`,p2.name as Atores, m.title`  


4.12: Retrieve all movies that were released in a set of years.  
`match (m:Movie) where m.released in [2000, 2004,2015] return  m.title, m.released`      


4.13: Retrieve the movies that have an actor’s role that is the name of the movie.  
`match (p:Person)-[r:ACTED_IN]-> (m:Movie) where m.title in r.roles return p.name, r.roles, m.title`   

Exercicio 5 - Controlling query processing    

5.1: Retrieve data using multiple MATCH patterns. 
`MATCH (a:Person)-[:ACTED_IN]->(m:Movie)<-[:DIRECTED]-(d:Person),
      (a2:Person)-[:ACTED_IN]->(m)
WHERE a.name = 'Tom Hanks'
RETURN m.title as Filme, d.name as Diretor , a2.name AS `Co-Atores``  

5.2: Retrieve particular nodes that have a relationship.  
`match(p:Person)-[:FOLLOWS]-(p2:Person) where p.name = 'Paul Blythe' return p, p2`  

5.3: Modify the query to retrieve nodes that are exactly three hops away.  
´match(p:Person)-[:FOLLOWS*3]-(p2:Person) where p.name = 'Paul Blythe' return p, p2´    

5.4: Modify the query to retrieve nodes that are one and two hops away.   
`match(p:Person)-[:FOLLOWS*1..2]-(p2:Person) where p.name = 'Paul Blythe' return p, p2´    

5.5: Modify the query to retrieve particular nodes that are connected no matter how many hops are required.  
`match(p:Person)-[:FOLLOWS*]-(p2:Person) where p.name = 'Paul Blythe' return p, p2`  

5.6: Specify optional data to be retrieved during the query.    
´match (p:Person) where p.name starts with 'Tom' optional match (p)-[:DIRECTED]->(m:Movie) return p.name, m.title´ 

5.7: Retrieve nodes by collecting a list.  
`match(p:Person)-[:ACTED_IN]->(m:Movie) return p.name, collect(m.title) as Filmes`  

5.8: (Este não estava no PDF mas inseri porque estava no Neo4j!
Retrieve all movies that Tom Cruise has acted in and the co-actors that acted in the same movie by collecting a list (Instructions)
`match(p:Person)-[:ACTED_IN]->(m:Movie)<-[:ACTED_IN]-(p2:Person) where p.name = 'Tom Cruise' return p.name, m.title, collect(p2.name) as `Co-Atores``   

5.9: Retrieve nodes as lists and return data associated with the corresponding lists.   
`match(p:Person)-[:REVIEWED]->(m:Movie) return collect(p.name) as reviwers, m.title, count(p) as qtdeReviwers`  

5.10: Retrieve nodes and their relationships as lists.  
`match(p:Person)-[:DIRECTED]->(m:Movie)<-[:ACTED_IN]-(p2:Person) return p.name as Director,count(p2) as qtdeAtores, collect(p2.name) as Atores`  

5.11: Retrieve the actors who have acted in exactly five movies.  
`match(p:Person)-[:ACTED_IN]->(m:Movie) with p, count(p) as qtdeFilmes, collect(m.title) as Filmes where qtdeFilmes = 5 return p.name, Filmes`  

5.12: Retrieve the movies that have at least 2 directors with other optional data.  
`match (m:Movie) with m, size((:Person)-[:DIRECTED]->(m)) as Diretores where Diretores >=2 optional match (p:Person)-[:REVIEWED]->(m) return m.title, p.name`  

Exercício 6 – Controlling results returned    

6.1: Execute a query that returns duplicate records.  
`match (a:Person)-[:ACTED_IN]->(m:Movie) where m.released >= 1990 and m.released < 2000 return  m.title as Filme,collect(a.name) as Atores, m.released as lançamento`  

6.2: Modify the query to eliminate duplication.  
`match (a:Person)-[:ACTED_IN]->(m:Movie) where m.released >= 1990 and m.released < 2000 return collect(m.title) as Filme,collect(a.name) as Atores, m.released as lançamento`  

6.3: Modify the query to eliminate more duplication.  
`match (a:Person)-[:ACTED_IN]->(m:Movie) where m.released >= 1990 and m.released < 2000 return collect(distinct m.title) as Filme,collect(a.name) as Atores, m.released as lançamento`  

6.4: Sort results returned.  
`match (a:Person)-[:ACTED_IN]->(m:Movie) where m.released >= 1990 and m.released < 2000 return collect(distinct m.title) as Filme,collect(a.name) as Atores, m.released as lançamento order by m.released desc`    

6.5: Retrieve the top 5 ratings and their associated movies 
`match (p:Person)-[r:REVIEWED]->(m:Movie) return m.title as Filme,r.rating as avaliação order by r.rating desc limit 5`  

6.6: Retrieve all actors that have not appeared in more than 3 movies. 
`match (a:Person)-[:ACTED_IN]->(m:Movie) with a, count(a) as qtdFilmes, collect(m.title) as Filmes where qtdFilmes <= 3 return a.name, Filmes, qtdFilmes`  

Exercício 7 – Working with cypher data    

7.1: Collect and use lists. 

7.2: Collect a list.  
7.3: Unwind a list.  
7.4: Perform a calculation with the date type  

Exercício 8 – Creating nodes    

8.1: Create a Movie node.  
8.2: Retrieve the newly-created node.  
8.3: Create a Person node.  
8.4: Retrieve the newly-created node.  
8.5: Add a label to a node.  
8.6: Retrieve the node using the new label.  
8.7: Add the Female label to selected nodes.  
8.8: Retrieve all Female nodes.  
8.9: Remove the Female label from the nodes that have this label.  
8.10: View the current schema of the graph.  
8.11: Add properties to a movie.  
8.12: Retrieve an OlderMovie node to confirm the label and properties.  
8.13: Add properties to the person, Robin Wright.  
8.14: Retrieve an updated Person node.  
8.15: Remove a property from a Movie node.  
8.16: Retrieve the node to confirm that the property has been removed.  
8.17: Remove a property from a Person node.  
8.18: Retrieve the node to confirm that the property has been removed.    

Exercício 9 – Creating relationships    

9.1: Create ACTED_IN relationships.  
9.2: Create DIRECTED relationships.  
9.3: Create a HELPED relationship.  
9.4: Query nodes and new relationships.  
9.5: Add properties to relationships.  
9.6: Add a property to the HELPED relationship.  
9.7: View the current list of property keys in the graph.  
9.8: View the current schema of the graph.  
9.9: Retrieve the names and roles for actors.  
9.10: Retrieve information about any specific relationships.  
9.11: Modify a property of a relationship.  
9.12: Remove a property from a relationship.  
9.13: Confirm that your modifications were made to the graph.  

Exercício 10 – Deleting nodes and relationships  

10.1: Delete a relationship.  
10.2: Confirm that the relationship has been deleted.  
10.3: Retrieve a movie and all of its relationships.  
10.4: Try deleting a node without detaching its relationships.  
10.5: Delete a Movie node, along with its relationships.  
10.6: Confirm that the Movie node has been deleted.  


