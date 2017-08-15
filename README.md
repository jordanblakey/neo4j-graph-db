# neo4j-graph-db

## Queries

  #### Create Nodes
  CREATE (n:Person {name : "Brad"}) RETURN n
  CREATE (n:Movie {title:"Caddyshack"}) RETURN n
  OPERATION (scope:Label {property:value"}) ACTION scope

  #### Return the Whole Node Graph
  MATCH (n) return n

  #### Set and Remove Properties
  MATCH (n:Person {name:"Jack"})  set n.age=35
  MATCH (n:Person {name:"Jack"})  REMOVE n.age

  #### Query Properties
  MATCH(n:Person) WHERE n.name='Jill' RETURN n
  MATCH(n:Person) WHERE n.name='Jill' RETURN n.name
  MATCH(n:Person) WHERE n.name='Jill' OR n.name='Mike' RETURN n

  #### Create Relationships
  MATCH (a:Person {name:"Jack"}), (b:Person {name:"Brad"}) MERGE (a)-[r:FRIENDS {since:"1998"}]->(b)
  MATCH(a:Person{name:"Jill"}), (b:Movie {name:"Scarface"}) MERGE (a)-[r:WATCHED {circa:"2002"}]->(b)
  MATCH (a:Movie), (b:Movie) MERGE (a)-[r:SIMILAR {since:"1998"}]-(b)

  #### Query Relationships
  MATCH(a:Person{name:'Jack'})-[:FRIENDS]->(b:Person) RETURN a,b
  MATCH(a:Person{name:'Jack'})-[:FRIENDS]->(b:Person) RETURN b
  MATCH(a:Person)-[:FRIENDS]->(b:Person{name:'Brad'}) RETURN b,a // Direction match
  MATCH(a:Person)-[:FRIENDS]-(b:Person{name:'Brad'}) RETURN b,a // Directionless match
  OPERATION(start-nodes:Label{property:'value'})-relationship[:LABEL]->(target-node:Label) RETURN nodes, nodes

  #### Deleting Nodes
  MATCH(a:Person{name:"Mike"})-[r]-(b) DELETE r // Can only delete nodes that have no Relationships
  MATCH(a:Person{name:"Mike"}) DELETE // Delete the matching node
  MATCH(n) OPTIONAL MATCH (n)-[r]-() DELETE n,r // Delete everything

## :help commands

- Information:	:help play
- Server:	:help server
- Cypher:	:help cypher
- REST:	:help REST GET :help REST POST
- Params:	:help param:help params
- Query status:	:help queries

===
## :play concepts
### Graph Fundamentals
Basic concepts to get you going.

A graph database can store any kind of data using a few simple concepts:

- Nodes - graph data records
- Relationships - connect nodes
- Properties - named data values

### A Graph Database
Neo4j stores data in a Graph, with records called Nodes.

The simplest graph has just a single node with some named values called Properties. Let's draw a social graph of our friends on the Neo4j team:

- Start by drawing a circle for the node
- Add the name Emil
- Note that he is from Sweden
- Nodes are the name for data records in a graph
- Data is stored as Properties
- Properties are simple name/value pairs

### Labels
Associate a set of nodes.

Nodes can be grouped together by applying a Label to each member. In our social graph, we'll label each node that represents a Person.

- Apply the label "Person" to the node we created for Emil
- Color "Person" nodes red
- A node can have zero or more labels
- Labels do not have any properties

### More Nodes
Schema-free, nodes can have a mix of common and unique properties.

Like any database, storing data in Neo4j can be as simple as adding more records. We'll add a few more nodes:

- Emil has a klout score of 99
- Johan, from Sweden, who is learning to surf
- Ian, from England, who is an author
- Rik, from Belgium, has a cat named Orval
- Allison, from California, who surfs
- Similar nodes can have different properties
- Properties can be strings, numbers, or booleans
- Neo4j can store billions of nodes

### Consider Relationships
Connect nodes in the graph

The real power of Neo4j is in connected data. To associate any two nodes, add a Relationship which describes how the records are related.

In our social graph, we simply say who KNOWS whom:

- Emil KNOWS Johan and Ian
- Johan KNOWS Ian and Rik
- Rik and Ian KNOWS Allison
- Relationships always have direction
- Relationships always have a type
- Relationships form patterns of data

### Relationship properties
Store information shared by two nodes.

In a property graph, relationships are data records that can also contain properties. Looking more closely at Emil's relationships, note that:

- Emil has known Johan since 2001
- Emil rates Ian 5 (out of 5)
- Everyone else can have similar relationship properties

=======================================
# Neo4j 3.2.3

Welcome to Neo4j release 3.2.3, a high-performance graph database.
This is the community distribution of Neo4j, including everything you need to
start building applications that can model, persist and explore graph-like data.

In the box
----------

Neo4j runs as a server application, exposing a Web-based management
interface and RESTful endpoints for data access.

Here in the installation directory, you'll find:

* bin - scripts and other executables
* conf - server configuration
* data - databases
* lib - libraries
* plugins - user extensions
* logs - log files
* import - location of files for LOAD CSV

Make it go
----------

For full instructions, see https://neo4j.com/docs/operations-manual/current/installation/

To get started with Neo4j, let's start the server and take a
look at the web interface ...

1. Open a console and navigate to the install directory.
2. Start the server:
   * Windows, use: bin\Neo4j.bat
   * Linux/Mac, use: ./bin/neo4j console
3. In a browser, open http://localhost:7474/
4. From any REST client or browser, open http://localhost:7474/db/data
   in order to get a REST starting point, e.g.
   curl -v http://localhost:7474/db/data
5. Shutdown the server by typing Ctrl-C in the console.

Learn more
----------

* Neo4j Home: https://neo4j.com/
* Getting Started: https://neo4j.com/docs/developer-manual/current/introduction/
* Neo4j Documentation: https://neo4j.com/docs/

License(s)
----------
Various licenses apply. Please refer to the LICENSE and NOTICE files for more
detailed information.
