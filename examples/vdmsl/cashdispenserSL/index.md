---
layout: default
title: cashdispenser
---

~~~
This model is described in VDM-SL as a short, flat specification. 
#******************************************************
~~~
###cashdispenser.vdmsl

{% raw %}
~~~
state System of
types
  Transaction :: date : Date
  Card :: code : Code
  Cardholder :: name : Name;
  AccountId = nat;
functions
  TransactionsInvariant : seq of Transaction +> bool
  DateTotal : Date * seq of Transaction +> nat
values
operations
  InsertCard : Card ==> ()
  Validate : PinCode ==> <PinOk> | <PinNotOk> | <Retained>        
  ReturnCard : () ==> ()
  GetBalance : () ==> nat
  MakeWithdrawal : nat * Date ==> bool
  RequestStatement : () ==> Name * seq of Transaction * nat
functions
  IsLegalCard : Card * set of CardId * map AccountId to Account -> bool
operations
  ReportIllegalCard : CardId ==> ()
  AddAccount : AccountId * Account ==> ()
functions
  Sum: seq of real +> real
  Len: seq of real +> nat
traces
TestCash: let c in set {mk_Card(1,1,1), mk_Card(2,2,2)}
~~~{% endraw %}
