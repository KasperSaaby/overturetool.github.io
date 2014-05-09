---
layout: default
title: NDB
---

~~~
The Non-programmer database system (NDB) is a nicely engineered binary 
A. Walshe, "NDB: The Formal Specification and Rigorous Design of a 
J.S. Fitzgerald and C.B. Jones, "Modularizing the Formal Description 
~~~
###ndb.vdmsl

{% raw %}
~~~
types
	Eid = token;
	Maptp = <ONETOONE>|<ONETOMANY>|<MANYTOONE>|<MANYTOMANY>;
	Tuple :: fv : Eid
	Rinf :: tp : Maptp
	Rkey :: nm : [Rnm]
functions
checkinv : map Esetnm to set of Eid * map Eid to [Value] * map Rkey to


state Ndb of
	 esm : map Esetnm to set of Eid
	 inv mk_Ndb(esm,em,rm) == checkinv (esm,em,rm)
init  ndb == ndb = mk_Ndb({|->},{|->},{|->})
	operations

	ADDES(es:Esetnm)
	DELES(es:Esetnm)

	ADDENT(memb : set of Esetnm, val : [Value]) eid :Eid
	DELENT(eid:Eid)
	ADDREL( rk:Rkey, tp:Maptp)
	DELREL (rk:Rkey)
	ADDTUP (fval,tval : Eid, rk:Rkey)
	DELTUP(fval,tval:Eid, rk:Rkey)
~~~{% endraw %}
