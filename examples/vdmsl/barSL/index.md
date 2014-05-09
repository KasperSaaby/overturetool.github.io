---
layout: default
title: bar
---

~~~

This specification was produced during a VDM-SL course presented by Peter 
#******************************************************
~~~
###bag.vdmsl

{% raw %}
~~~

module BAG
exports
types
functions
  Empty: () -> Bag;
values
definitions
types
functions
  -- Minimum value of a pair of two integers
  -- Maximum value of a pair of two integers
  -- Add a sequence of elements, s, to a bag, b, 
  LenPar1 : seq of Elem * Bag -> nat
  -- Functions Required by Customer
  Empty : () -> Bag
  Add : Elem * Bag -> Bag
  Remove : Elem * Bag -> Bag
  Count : Elem * Bag -> nat
  In : Elem * Bag -> bool
  Join : Bag * Bag -> Bag
  Union : Bag * Bag -> Bag
  SubBag : Bag * Bag -> bool
  Difference : Bag * Bag -> Bag
  Size : Bag -> nat 
   CardDom: Bag -> nat
  Intersection : Bag * Bag -> Bag
  SeqToBag : seq of Elem -> Bag
values 
end BAG

~~~{% endraw %}

###bagtest.vdmsl

{% raw %}
~~~

module BAGTEST
imports from BAG all
exports all
definitions
functions 
  TestBagAll: () -> bool
  TestAdd1: () -> bool
  TestAdd2: () -> bool
  TestCount1: () -> bool
  TestCount2: () -> bool
  TestDifference: () -> bool
  TestEmpty: () -> bool
  TestIn1: () -> bool
  TestIn2: () -> bool
  TestIntersection: () -> bool
  TestJoin: () -> bool
  TestRemove1: () -> bool
  TestRemove2: () -> bool
  TestRemove3: () -> bool
  TestSeqToBag: () -> bool
  TestSize: () -> bool
  TestSubBag1: () -> bool
  TestSubBag2: () -> bool
  TestUnion: () -> bool
end BAGTEST

~~~{% endraw %}

###bar.vdmsl

{% raw %}
~~~

module BAR
from BAG
types
functions
  Empty: () -> BAG`Bag;
values
exports all
definitions
types
functions
  -- Given a level of bar stocking, 
  -- A patron buys a round (list) of drinks from the bar
  -- Given a map of suppliers and what they have, 
   CardCellar: CellarLevel * Pub * 
  -- Sell one drink to a patron
  -- The pub is devoid of alcohol
  -- Return by a patron of an unopenned bottle
  -- Work out the highest single stock for 
  CardDom: map Supplier to Stock -> nat CardDom(m) ==
  -- How many drinks are there in the pub
values -- introduced for the purposes of testing
end BAR 

~~~{% endraw %}
