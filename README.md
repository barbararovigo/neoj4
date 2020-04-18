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

3.2 Retrieve all people who wrote the movie Speed Racer.  

3.3 Retrieve all movies that are connected to the person,Tom Hanks.  

3.4 Retrieve information about the relationships Tom Hanks had with the set of movies retrieved earlier.  

3.5 Retrieve information about the roles that Tom Hanks acted in.  


Exercício 4 – Filtering queries using WHERE clause

4.1: Retrieve all movies that Tom Cruise acted in.  


4.2: Retrieve all people that were born in the 70’s.  


4.3: Retrieve the actors who acted in the movie The Matrix who were born after 1960.  


4.4: Retrieve all movies by testing the node label and a property.  


4.5: Retrieve all people that wrote movies by testing the relationship between two nodes.  


4.6: Retrieve all people in the graph that do not have a property.  


4.7: Retrieve all people related to movies where the relationship has a property.  


4.8: Retrieve all actors whose name begins with James.  


4.9: Retrieve all all REVIEW relationships from the graph with filtered results.  


4.10: Retrieve all people who have produced a movie, but have not directed a movie.  


4.11: Retrieve the movies and their actors where one of the actors also directed the movie.  


4.12: Retrieve all movies that were released in a set of years.  


4.13: Retrieve the movies that have an actor’s role that is the name of the movie.  






