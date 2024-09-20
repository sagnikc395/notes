---
title: Building a Knowledge Graph
tags:
  - knowledge-graph
  - graphs
  - system-design
---
## Building a Scalable Knowledge based graph and trained with OLLAMA 

- While planning for a thing, importnat to show all critical info for the user for making optimal decisions and able to train AI on it.
- Cannot use relational DB as :
	- Relational DB for each type of entity have an table, and for every single row of the entity has a table.
	- Foreign key references matching them.
	- Good for transactional thing ,on a individual entity level.

- want to 'surf' within the data.

### Infra:
- Knowledge graph infra has 3 components:
	- Graph storage
	- Graph query API
	- Storage Mutator -> can be updated or knowledge learned.

- Graph storage:
	- entire knowledge graph is stored in a relational DB , but stored as nodes and edges as tuples.
	Eg: < document-no, tags, main-topic, ... > , where other fields are exttracted from the AI.
	- Each node type has a different schema 
	- Each edge type stores node that connect together.
	- define the node type and the schema , and they would be able to get that type of schema.
	- each edge type -> what types of node it can connect to -> (traditional way) -> need to improve on the architecture.
	-  




### References:
1. https://www.youtube.com/watch?v=7xKgQmqkfD0
2. 