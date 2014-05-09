---
layout: default
title: ReaderWriter
---

~~~

#******************************************************
~~~
###Buffer.vdmpp

{% raw %}
~~~
class Buffer
~~~{% endraw %}

###io.vdmpp

{% raw %}
~~~
class IO
-- 	Overture STANDARD LIBRARY: INPUT/OUTPUT
types
public
functions
-- Write VDM value in ASCII format to std out:
-- Write VDM value in ASCII format to file.
-- Read VDM value in ASCII format from file
operations
-- Write text to std out. Surrounding double quotes will be stripped,
-- Write text to file like 'echo'
-- The in/out functions  will return false if an error occur. In this
-- New simplified format printing operations
public static print: ? ==> ()
public static printf: seq of char * seq of ? ==> ()
end IO
~~~{% endraw %}

###Reader.vdmpp

{% raw %}
~~~

~~~{% endraw %}

###TestClass.vdmpp

{% raw %}
~~~

~~~{% endraw %}

###Writer.vdmpp

{% raw %}
~~~
class Writer
~~~{% endraw %}
