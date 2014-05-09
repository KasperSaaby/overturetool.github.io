---
layout: default
title: Alarm++proof
---

~~~
This is a version of the alarm example from the VDM++ book, John 
#******************************************************
~~~
###alarmProof.vdmpp

{% raw %}
~~~
-- alarm-with-POs.vdm
types
  Plant :: schedule : Schedule
  Schedule = map Period to set of Expert
public Period = token;
  Expert :: expertid : ExpertId
  ExpertId = token;
  Qualification = <Elec> | <Mech> | <Bio> | <Chem>;
  Alarm :: alarmtext : seq of char
functions
  NumberOfExperts: Period * Plant -> nat
  ExpertIsOnDuty: Expert * Plant -> set of Period
  ExpertToPage(a:Alarm,peri:Period,plant:Plant) r: Expert
static  QualificationOK: set of Expert * Qualification -> bool
operations
public RunTest : () ==> set of Period
end alarm

~~~{% endraw %}
