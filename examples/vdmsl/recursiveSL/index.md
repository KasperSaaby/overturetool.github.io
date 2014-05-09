---
layout: default
title: recursive
---

~~~
This example is made by John Fitgerald and Peter Gorm Larsen and it
#******************************************************
~~~
###graphs.vdmsl

{% raw %}
~~~
types
Graph = map Id to set of Id
ASyncGraph = Graph
Path = seq of Id;
Id = nat
functions
Paths: ASyncGraph * Id -> set of Path
measureTransClos : ASyncGraph * Id -> nat
LinearPath: Graph * Id -> Path
TransClos: Graph * Id -> set of Id
TransClosAux: Graph * Id * set of Id -> set of Id
measureGraphReached : Graph * Id * set of Id -> nat
AsycDescendents: AcyclicGraph * Id -> set of Id
Descendents: Graph * Id * set of Id -> set of Id
AllDesc: Graph * Id -> set of Id
types
AcyclicGraph = Graph
values
  graph : Graph = {1 |-> {2,3},
~~~{% endraw %}

###labgraphs.vdmsl

{% raw %}
~~~
types
LabGraph = map NodeId to (map ArcId to NodeId)
AcyclicLabGraph = LabGraph
NodeId = nat;
ArcId = nat
functions
AllLabDesc: LabGraph * NodeId -> set of NodeId
measureLabGraphReached : LabGraph * Id * set of Id -> nat
LabDescendents: LabGraph * NodeId * set of NodeId -> set of NodeId
UniqueArcIds: map NodeId to (map ArcId to NodeId) -> bool
values
  lgraph : LabGraph = {1 |-> {1 |-> 2,2 |-> 3},
~~~{% endraw %}
