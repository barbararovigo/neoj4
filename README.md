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
Ok. Visualizado no Browser do Neo4j em formato de tabela.  

2.3 Query the database for all property keys.     
`call db.propertyKeys`

2.4 Retrieve all Movies released in a specific year, returning their titles.    
`match(m:Movie{released:1995}) return m.title`  

2.5 Display title, released, and tagline values for every Movie node in the graph.   
`match(m:Movie) return m.title, m.released, m.tagline`  

2.6 Display more user-friendly headers in the table.  
`match(m:Movie) return m.title as título, m.released as lançamento, m.tagline as slogan`  





