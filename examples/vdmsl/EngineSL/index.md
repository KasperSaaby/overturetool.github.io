---
layout: default
title: Engine
---

~~~
As with many modern engineered products, the control software developed at Rolls-
#******************************************************
~~~
###engine.vdmsl

{% raw %}
~~~
types
ValvePos = <open> | <closed>;
SwitchPos = <on> | <off>;
StartAttempt = nat1
StartState = <FuelSwitchAtCut> | 
values
DVMINN2GNDFOC : real = 26;
DVMINTGTGNDFOC : real = 100;
DVATORABOVEIDLE : real = 55;
DVMAXNUMBERATTEMPTS : int = 2;
DVHOTSTART : real = 305;
DVMAXLIGHTWAITTIME : int = 180;
STATEMAP = {1 |-> <FuelSwitchAtCut>, 
state StartingSystem of
functions
LightUpDetect : real -> bool
FOCDetect : SwitchPos * SwitchPos * real * bool -> bool
ReturnState : int -> StartState
LightupTimeOutDetect : int -> bool
GroundFailureDetected : bool * bool * bool * bool * bool * real -> bool
operations
StarterOn () 
StarterOff () 
OpenSOV () 
IgnOn (tempTGT : real) 
IgnOff (tempTGT : real) 
StartComplete (tempTGT : real) 
SequenceAbort () 
CoolFlush (tempTGT : real)
~~~{% endraw %}
