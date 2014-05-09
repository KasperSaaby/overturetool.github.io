---
layout: default
title: AlarmErr
---

~~~

This is an erronerous version of the alarm example from the VDM-SL

#******************************************************
~~~
###alarmerr.vdmsl

{% raw %}
~~~
types
  Plant :: schedule : Schedule
  Schedule = map Period to set of Expert
  Period = token;
  Expert :: expertid : ExpertId
  ExpertId = token;
  Qualification = <Elec>  <Mech> | <Bio> | <Chem>;
  Alarm :: alarmtext : seq of char
functions
  NumberOfExperts: Period * Plant -> nat
  ExpertIsOnDuty: Expert * Plant -> set of Period
  ExpertToPage(a:Alarm,per:Period,plant:Plant) r Expert
  QualificationOK: set of Expert * Qualification -> bool
~~~{% endraw %}
