---
layout: default
title: Digraph
---

~~~

The specification describes how directed graphs and relations over
This model is only an illustration of the problems germane to automatic 
~~~
###digraph.vdmsl

{% raw %}
~~~
------------------------------------------------------------------
-- This model is only an illustration of the problems germane to automatic 


module digraph 
imports
  from flowgraph_types all,
exports all
definitions
types 
Node =  flowgraph_types`Node;
Flowgraph = flowgraph_types`FlowGraph;
functions
succ: Flowgraph * Node  -> set of Node
pred: Flowgraph * Node  -> set of Node
existspath: Flowgraph * Node * Node -> bool

end digraph
~~~{% endraw %}

###flowgraphtypes.vdmsl

{% raw %}
~~~
------------------------------------------------------------------
imports from relations
exports
definitions
types
Node = nat1;
Nodes = set of Node; -- any subset of Node
Arc = Node * Node; 
Variable = token;
Path = seq of Node;
FlowGraph::
ExtendedFlowGraph :: 

values
     N1: Nodes={1,...,4};
-- special  relations
     G1: FlowGraph= mk_FlowGraph(N1, A1,1,4); -- isolated nodes
 -- STATE DEFINITION
state ST of -- two isolated nodes, no arcs
end flowgraph_types
~~~{% endraw %}

###Relations.vdmsl

{% raw %}
~~~
------------------------------------------------------------------


module relations
exports all
definitions
types
     Node=nat1;
values
 A0: BinRel = {}; -- empty relation

functions
-- TESTING PROPERTIES OF RELATIONS
 IsReflexive:BinRel-> bool
IsSymmetrical:BinRel-> bool
 IsTransitive:BinRel-> bool
 IsEquivalence:BinRel-> bool

-- OPERATIONS ON RELATIONS
 domain:BinRel -> set of nat1 
 domain1:BinRel -> set of nat1
 range:BinRel -> set of nat1
 field:BinRel -> set of nat1
 inverse_rel:BinRel -> BinRel

 id_rel: BinRel -> BinRel
 Composition:BinRel * BinRel -> BinRel
 power_of:BinRel * nat1 -> BinRel --returns the xth power of R
 Power_rel: BinRel * nat -> BinRel

-- RELATIONAL CLOSURES
 Reflexive_cl: BinRel -> BinRel
 Symmetric_cl: BinRel -> BinRel  
 Transitive_cl: BinRel -> BinRel 
 TransitiveRefl_cl: BinRel -> BinRel
 PowerList: BinRel -> seq of BinRel

 BuildList: BinRel * nat1 -> seq of BinRel
 BuildList(R,n) == 

 max_set: set of int -> int

 max2: int * int -> int

operations
Warshall: BinRel ==> BinRel
 R := Q;

-- Testing functions&operations
functions
test_PowerList: BinRel -> bool

end relations
~~~{% endraw %}
