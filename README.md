# CCS - Behavior Tree - Mappings: Demo Resources

This repository contains all necessary resources to test and run the example application that demonstrates behavior trees as semantics preserving implementation of Milner CCS process expressions. 

This repository contains supplementary material to the paper "Behavior Trees as executable representation of Milner Calculus notations", submitted to the 20th International Conference on Practical Applications of Agents and Multi-Agent Systems (PAAMS'22).

## Setup

1. Install and configure the AJAN Multi Agent Platform Service and Editor as described in the respective projects:
  - https://github.com/aantakli/AJAN-service
  - https://github.com/aantakli/AJAN-editor  
2. Build the demo scenario endpoint that will provide the simulation of the shopfloor, and run the application to listen on server port 8190:
    1. cd ./paams22-scenario
    2. mvn install
    3. cd target/
    4. java -jar paams22-demo-scenario-1.0-SNAPSHOT.jar --server.port=8190
3. Build the SPARQL API Proxy that will receive SPARQL queries by the agents, and evaluate them against the demo scenario endpoints. The service is supposed to run on port 8091:
    1. cd ./sparql-api-wrapper/sparql-api-wrapper/
    2. mvn install
    3. cd target/
    4. java -jar paams22-demo-scenario-1.0-SNAPSHOT.jar --server.port=8091

## Try the Demo

1. Start AJAN and the AJAN Editor as documented in the respective projects
2. In the AJAN Editor "Behaviors" tab ...
    1. ... select _File->Import Repo ..._
    2. ... select the file ./behaviors/behaviors.ttl .
    3. You should now see a list of Behavior Trees available in the drop down list, named for example PAAMS_SENSE, PAAMS_OHA_PERC, etc.
3. In the AJAN Editor "Agents" tab ...
  	1. Make sure you are currently to in the "Agents/Templates" tab
    2. ... select _File->Import Repo ..._
    3. ... select the file ./behaviors/agents.ttl .
3. Switch to the  "Agents/Instances" Tab:
    1. Click "+" to create a new instance
    2. Assign any name, and select as class "OHA"
    3. Copy from ./behaviors/agent_knowledge.ttl the RDF snippet (including including namespaces) under "############## OHA", and paste it as "Initial Knowledge"
    4. Click "Create"

What you should observe:

1. When refreshing the list of agent instances, you should see a list of further agents created. These are the JSA and JEA created according to the algorithm as originally described in the paper.
2. When visiting http:localhost:8190/products/ , you should see a list of products created by the JEA along the way. Ultimately, the product specified in http:localhost:8190/orders/order_1, an IOT board, should become available.

## Acknowledgements
_This work has been supported by the German Federal Ministry for Education and Research (BMBF) as part of the MOSAIK project (grant no. 01IS18070-C)._

