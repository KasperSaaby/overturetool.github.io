---
layout: default
title: HASL
---

~~~
This is a VDM-SL version of a home automation example constructed
More information can be found in:
#******************************************************
~~~
###HA.vdmsl

{% raw %}
~~~
types
HAInputs = seq of HAInput;
Change = bool;
TargetTemp = nat
CurrentTemp = nat
TargetHumid = nat
CurrentHumid = nat
HAOut = seq of OutStep;
EnvManipulation = <OpenWindow> | <CloseWindow> | <IncTemp> | <DecTemp> | <LeaveTemp>;

values
TempChangeDuration  : nat = 2;

functions
HomeAutomation: HAInputs -> HAOut
HA: HAInputs * HAOut * nat -> HAOut
ChangeHA: HAInputs * HAOut * AbsTime -> HAOut
AddOutput: nat * nat * nat * nat * nat * seq of OutStep -> seq of OutStep

TempChanged: nat * nat * nat * seq of OutStep -> seq of OutStep

HumidChanged: nat * nat * nat * nat * nat * seq of OutStep -> seq of OutStep

InterruptOutput : seq of OutStep * nat -> seq of OutStep
CounterOutput : seq of OutStep * nat -> seq of OutStep
~~~{% endraw %}
