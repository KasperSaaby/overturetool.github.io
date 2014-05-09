---
layout: default
title: Pacemaker
---

~~~
This model is made by Hugo Macedo as a part of his MSc thesis of a
Hugo Macedo, Validating and Understanding Boston Scientific Pacemaker
Hugo Daniel Macedo, Peter Gorm Larsen and John Fitzgerald, Incremental 
#******************************************************
~~~
###Accelerometer.vdmrt

{% raw %}
~~~

class Accelerometer is subclass of GLOBAL
operations
 public 
end Accelerometer

~~~{% endraw %}

###Environment.vdmrt

{% raw %}
~~~

class Environment is subclass of GLOBAL
 types 
public Inpline = (Sense * Chamber * ActivityData * Time);
public Outline = (Pulse * Chamber * Time);  
 instance variables
-- Input/Output 
inplines : seq of Inpline := [];
-- Environment  
busy : bool := true;
-- Amount of time we want to simulate
 instance variables
-- Leads
leads : map Chamber to Lead := {|->};
-- Accelerometer

 operations
-- Constructor

public 
public 

private 


public 
public
functions
convert : seq of Outline -> seq of Outline
operations

thread


sync 
per isFinished => not busy and time >= simtime;

end Environment

~~~{% endraw %}

###GLOBAL.vdmrt

{% raw %}
~~~

class GLOBAL
types 

-- Sensed activity
-- Heart chamber identifier

-- Accelerometer output

-- Paced actvity
-- Operation mode

-- PPM

-- Time
end GLOBAL

~~~{% endraw %}

###HeartController.vdmrt

{% raw %}
~~~

class HeartController is subclass of GLOBAL
instance variables 
 leads     : map Chamber to Lead;

operations
 public 


 public 

 public 

 private
 private
 private
 public 
 public 
 public 
 public 
thread
sync
per isFinished => sensed = {|->} and #active(pace) = 0;


mutex(sensorNotify,pace,setInterval);

~~~{% endraw %}

###Lead.vdmrt

{% raw %}
~~~

class Lead is subclass of GLOBAL
instance variables
 private chamber : Chamber;       
operations
 public 

 public 

 public 

 public 

 public 
 private 
 private 
   );


thread


sync
mutex(addLeadPace);
end Lead 

~~~{% endraw %}

###Pacemaker.vdmrt

{% raw %}
~~~

system Pacemaker 
 instance variables
 public static 
 public static 

instance variables
 public static 
 public static 

 instance variables
 public static 
instance variables
 cpu1 : CPU := new CPU(<FCFS>,1E3); 
 -- Lead (artia) <-> HeartController
 -- Lead (ventricle) <-> HeartController
 -- Accelerometer <-> RateController


operations
 public Pacemaker: () ==> Pacemaker
end Pacemaker

~~~{% endraw %}

###RateController.vdmrt

{% raw %}
~~~

class RateController is subclass of GLOBAL
instance variables


instance variables
inv threshold < 8
operations
 public 
   );
public
 private

 public 
 public

 public
 public 
 public 

thread

sync
per isFinished => finished;
per controlRate => sensed <> nil;
values
--V-LOW 1
end RateController

~~~{% endraw %}

###World.vdmrt

{% raw %}
~~~

class World is subclass of GLOBAL 
types
instance variables
public static env : [Environment] := nil;
operations
public World: seq of char * GLOBAL`Mode ==> World
     -- bind leads to the environment
     -- bind accelerometer to the environment
     -- bind leads to the controler
     -- set up mode
     start(Pacemaker`heartController);

  );

public Run: () ==> ()

end World

~~~{% endraw %}
