---
layout: default
title: hotel
---

~~~
This example is used to illustrate the difference between different
Daniel Jackson, Software Abstractions, MIT Press, April 2006
#******************************************************
~~~
###hotel.vdmsl

{% raw %}
~~~
types 
Key = token;
Card :: fst : Key
Desk :: issued : set of Key
state Hotel of 
inv h == dom h.desk.prev subset dom h.locks and
init h == h.desk.issued = {} and 
end
operations
CheckIn(g:Guest,r:Room)
ext wr desk   : Desk
pre r in set dom desk.prev
post exists new_k:Key &

Enter(r:Room,g:Guest)
ext wr locks  : map Room to Key
pre r in set dom locks  and 
post exists c in set guests(g) & 
CheckInExpl: Guest * Room ==> ()
--
EnterExpl: Room * Guest ==> ()
IssueCard: () ==> Key
AddRoom: Room * Key ==> ()
AddGuest: Guest * set of Card ==> ()
~~~{% endraw %}
