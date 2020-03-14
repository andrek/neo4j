# Práticas da disciplina de Banco de Dados Não Relacionais (neo4j)

1.1 Retrieve all nodes from the database.
> $match(n) return n

1.2 Examine the data model for the graph.
> $call db.schema()

1.3 Retrieve all Person nodes.
> $match(p:Person) return p

1.4 Retrieve all Movie nodes.
> $match(m:Movie) return m

2.1 Retrieve all movies that were released in a specific year.
> $match(m:Movie{released:2003}) return m

2.2 View the retrieved results as a table.
```
{
  "title": "The Matrix Reloaded",
  "tagline": "Free your mind",
  "released": 2003
}
{
  "title": "The Matrix Revolutions",
  "tagline": "Everything that has a beginning has an end",
  "released": 2003
}
{
  "title": "Something's Gotta Give",
  "released": 2003
}
```

2.3 Query the database for all property keys.
> $call db.propertyKeys()

2.4 Retrieve all Movies released in a specific year, returning their titles.
> $match(m:Movie {released:2006}) return m.title

2.5 Display title, released, and tagline values for every Movie node in the graph.
> $match(m:Movie) return m.title, m.released, m.tagline

2.6 Display more user friendly headers in the table
> $match(m:Movie) return m.title as `Título`, m.released as `Lançamento`, m.tagline as `Tag Line`

3.1 Display the schema of the database.
> $call db.schema()

3.2 Retrieve all people who wrote the movie Speed Racer.
> $match (p:Person)-[rel:WROTE]->(m:Movie { title: 'Speed Racer'}) return p.name

3.3 Retrieve all movies that are connected to the person Tom Hanks.
> $match(m:Movie)--(p:Person {name:'Tom Hanks'}) return m.title

3.4 Retrieve information about the relationships Tom Hanks had with the set of movies retrieved earlier.
> $match(m:Movie)-[rel]-(:Person {name: 'Tom Hanks'}) return m.title, type(rel)

3.5 Retrieve information about the roles that Tom Hanks acted in.
> $match(m:Movie)<-[rel:ACTED_IN]-(p:Person {name:'Tom Hanks'}) return m.title, rel.roles

4.1: Retrieve all movies that Tom Cruise acted in.
> $match(m:Movie)<-[:ACTED_IN]-(p:Person) where p.name = 'Tom Cruise' return m.title

4.2: Retrieve all people that were born in the 70’s.
> $match(p:Person) where p.born >= 1970 AND p.born < 1980 return p.name, p.born

4.3: Retrieve the actors who acted in the movie The Matrix who were born after 1960.
> $match(p:Person)-[:ACTED_IN]->(m:Movie) where m.title = 'The Matrix' AND p.born > 1960 return p.name, p.born

4.4: Retrieve all movies by testing the node label and a property.
> $match(m) where m:Movie and m.released = 1995 return m.title

4.5: Retrieve all people that wrote movies by testing the relationship between two nodes.
> $match(p)-[rel]->(m) where p:Person AND type(rel) = 'WROTE' AND m:Movie return p.name, m.title

4.6: Retrieve all people in the graph that do not have a property.
> $match(p:Person) where exists(p.born) = false return p.name

4.7 Retrieve all people related to movies where the relationship has a property.
> $match(p:Person)-[rel]-(m:Movie) where exists(rel.rating) return p.name, m.title, m.rating

4.8: Retrieve all actors whose name begins with James.
> $match(p:Person) where p.name STARTS WITH 'James' return p.name

4.9: Retrieve all all REVIEW relationships from the graph with filtered results.
> $match(p:Person)-[rel:REVIEWED]->(m:Movie) where tolower(rel.summary) contains 'but' return m.title, rel.summary, rel.rating

4.10: Retrieve all people who have produced a movie, but have not directed a movie.
> $match(p:Person)-[:PRODUCED]->(m:Movie) where not ((p)-[:DIRECTED]->(:Movie)) return p.name

4.11: Retrieve the movies and their actors where one of the actors also directed the movie.
> $match (a:Person)-[:ACTED_IN]->(m:Movie)<-[:ACTED_IN]-(d:Person) where exists((d)-[:DIRECTED]->(m)) return a.name as Ator, d.name as `Ator/Diretor`, m.title

4.12: Retrieve all movies that were released in a set of years.
> $match(m:Movie) where m.released in [1995, 1998, 2000] return m.title, m.released

4.13: Retrieve the movies that have an actor’s role that is the name of the movie. 
> $match(p:Person)-[rel:ACTED_IN]->(m:Movie) where m.title in rel.roles return m.title, rel.roles, p.name



