# neo4j

1.1 Write a query to retrieve all nodes from the database.
> $match(n) return n

1.2 Write a query to display the schema of your database.
> $CALL db.schema()

1.3 Write a query to retrieve all Person nodes.
> $match(p:Person) return p

1.4 Write a query to retrieve all Movie nodes.
> $match(m:Movie) return m

2.1 Retrieve all Movie nodes that have a released property value of 2003.
> $match(m:Movie{released:2003}) return m

2.2 View the results you just viewed in Neo4j Browser as a table.
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

2.4 Retrieve all Movies released in 2006, returning their titles.
> $match(m:Movie {released:2006}) return m.title

2.5 Retrieve all Movie nodes from the database and return the title, released, and tagline values.
> $match(m:Movie) return m.title, m.released, m.tagline

2.6 Modify the query you just ran so that the headings for the columns of the table returned are more descriptive.
> $match(m:Movie) return m.title as `Título`, m.released as `Lançamento`, m.tagline as `Tag Line`
