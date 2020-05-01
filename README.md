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


4.11: Retrieve the movies and their actors where one of the actors also directed the movie.  


4.12: Retrieve all movies that were released in a set of years.  


4.13: Retrieve the movies that have an actor’s role that is the name of the movie.  






