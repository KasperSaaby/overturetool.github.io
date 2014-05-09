---
layout: default
title: CM
---

~~~
The counter measures example was developed by Peter Gorm Larsen and Marcel 
#******************************************************
~~~
###CMflat.vdmsl

{% raw %}
~~~

types
  MissileInputs = seq of MissileInput;
  MissileInput = MissileType * Angle;
  MissileType = <MissileA> | <MissileB> | <MissileC> | <None>;
  Angle = nat
  Output = map MagId to seq of OutputStep;
  MagId = token;
  OutputStep = FlareType * AbsTime;
  Response = FlareType * nat;
  AbsTime = nat;
  FlareType = <FlareOneA>  | <FlareTwoA>  | <FlareOneB> |
  Plan = seq of (FlareType * Delay);
  Delay = nat;
values
  responseDB : map MissileType to Plan =
  missilePriority : map MissileType to nat
  stepLength : nat = 100;
  testval1 : MissileInputs = [mk_(<MissileA>,88),
  testval2 : MissileInputs = [mk_(<MissileC>,188),
  testval3 : MissileInputs = [mk_(<MissileA>,288),
functions
CounterMeasures: MissileInputs -> Output
CM: MissileInputs * Output * map MagId to [MissileType] * 
CMLen: MissileInputs * Output * map MagId to [MissileType] * nat -> nat
InterruptPlan: nat * Output * Plan * MagId -> Output
LeavePrefixUnchanged: seq of OutputStep * nat -> 
MakeOutputFromPlan : nat * seq of Response -> seq of OutputStep
OutputAtTimeZero : seq of Response -> seq of OutputStep
RelativeToAbsoluteTimes : seq of Response -> 
RespLen: seq of Response -> nat
Angle2MagId: Angle -> MagId

~~~{% endraw %}
