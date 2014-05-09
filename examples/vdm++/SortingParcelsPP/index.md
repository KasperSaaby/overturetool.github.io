---
layout: default
title: SortingParcels
---

~~~
The purpose of this VDM++ model is to analyse the rules governing for
#******************************************************
~~~
###Colli.vdmpp

{% raw %}
~~~

class Colli
functions
instance variables
ID : int := 0;
operations
public Colli: int * int ==> Colli
public getDestination : () ==> int
public getID : () ==> int
public setID : int ==> ()
public setDestination : int ==> ()
end Colli
~~~{% endraw %}

###Conveyor.vdmpp

{% raw %}
~~~
class Conveyor
functions
instance variables
operations
 public addColli : Colli ==> ()
 public addSlide : Slide ==> ()
 public getSlides : () ==> seq of Slide
 public
 public removeGoods : Colli ==> ()
 public checkForUndeliverableGoods : () ==> set of Colli
--print methods for testing
 public printSlides : () ==> ()
end Conveyor

~~~{% endraw %}

###Slide.vdmpp

{% raw %}
~~~
class Slide
functions
instance variables
operations
public Slide : int ==> Slide
public getID : () ==> int
public addGoods : Colli ==> ()
public setID : int ==> ()
public printColli : () ==> ()
end Slide
~~~{% endraw %}

###test.vdmpp

{% raw %}
~~~
class Test
instance variables
goods : set of Colli := {new Colli(0,0),
operations
 for all y in set slides do
 IO`print("\nTest started..");
 IO`print("\ngoods in conveyor:\n");
 for all s in set elems conveyor.getSlides() do
 IO`print("\n\n..Distributing goods!\n");
 IO`print("\ngoods in conveyor:\n");
 for all s in set elems conveyor.getSlides() do
 temp := conveyor.checkForUndeliverableGoods();
 IO`print("\nundeliverable goods:\t");
);
end Test
~~~{% endraw %}
