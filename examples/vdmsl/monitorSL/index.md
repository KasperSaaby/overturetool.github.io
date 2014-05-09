---
layout: default
title: monitor
---

~~~
This example comes from the VDM-SL book by John Fitzgerald and Peter Gorm
The monitor records the five most recent temperature readings in the
#******************************************************
~~~
###monitor.vdmsl

{% raw %}
~~~
-- A temperature monitor
types
  TempRead = seq of int
functions
-- the last reading in a sample is greater than the first
  Rising: TempRead -> bool
-- there is a reading in excess of 400 degrees
  OverLimit: TempRead -> bool
-- alternative formulation using a quantified expression
  OverLimit2: TempRead -> bool
-- all readings in a sample exceed 400 degrees
  ContOverLimit: TempRead -> bool
-- alternative formulation using a quantified expression
  ContOverLimit2: TempRead -> bool
-- detecting whether a reactor can be considered safe
  Safe: TempRead -> bool
-- detecting whether an alarm should be raised
  RaiseAlarm(temp: TempRead) alarm : bool
  MixQuant: TempRead -> bool
~~~{% endraw %}
