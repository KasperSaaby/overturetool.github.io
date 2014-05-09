---
layout: default
title: LUPSL
---

~~~
This VDM model is made by Lothar Schmitz and it has taken different
David Gries: The Science of Programming, Springer-Verlag 1981, 
Janusz Laski und William Stanley, Software Verification and Analysis, 
#******************************************************
~~~
###LUPSL.vdmsl

{% raw %}
~~~
types
array = seq1 of int;
values
a1: array = [1,2,9,4,7,3]; --,11,8,14,6]; 
functions
MaxOfSet: set of int -> int
CardInt: set of int -> nat
lupsltok : array * nat1 -> nat
lupsl : array -> nat
ascending : array * set of int -> bool
lupslSpec : array -> int
operations
lupslOp1Laski : array ==> nat
state lups of
operations
lupsmOp1Gries : array ==> nat
lupsm4kop1Gries : array * nat1 ==> ()
lupslOp2Laski : array ==> nat
lupsmOp2Gries : array ==> nat
lupsm4kop2Gries : array * nat1 ==> ()
lupslOp3Laski : array ==> nat
lupsltokop1Laski : array * nat1 ==> nat
lupsmOp3Gries : array ==> nat
lupsm4kop3Gries : array * nat1 ==> ()
lupslOp4Laski : array ==> nat
lupsltokop2Laski : array * nat1 ==> nat


~~~{% endraw %}
