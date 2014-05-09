---
layout: default
title: CM
---

~~~
This example is used in the guidelines for developing distributed 
~~~
###BaseRTThread.vdmrt

{% raw %}
~~~
class BaseRTThread
types
public static ThreadDef ::
instance variables
protected period : nat1 := 1000E6;
protected registeredSelf : BaseRTThread;
operations
protected BaseRTThread : BaseRTThread ==> BaseRTThread
Step : () ==> ()
thread
periodic(period, jitter, delay, offset)(Step);
end BaseRTThread
~~~{% endraw %}

###CMTest.vdmrt

{% raw %}
~~~

class CMTest
end CMTest

~~~{% endraw %}

###CMTestCase2.vdmrt

{% raw %}
~~~

class CMTestCase2 is subclass of TestCase
operations
  protected SetUp: () ==> ()
  protected RunTest: () ==> ()
  protected TearDown: () ==> ()
end CMTestCase2

~~~{% endraw %}

###environment.vdmrt

{% raw %}
~~~

class Environment is subclass of GLOBAL, BaseRTThread
types
public inline  = EventId * MissileType * Angle * Time;
instance variables
-- access to the VDMTools stdio
-- the input file to process
-- the output file to print
-- maintain a link to all sensors
busy : bool := true;
operations
public Environment: seq of char * [ThreadDef] ==> Environment
  if tDef <> nil
public addSensor: Sensor ==> ()
private createSignal: () ==> ()
public handleEvent: EventId * FlareType * Angle * Time * Time ==> ()
public showResult: () ==> ()
public isFinished : () ==> ()
public GetAndPurgeOutlines: () ==> seq of outline
public Step : () ==> ()
sync
mutex (handleEvent);
end Environment

~~~{% endraw %}

###fighteraircraft.vdmrt

{% raw %}
~~~

system CM
instance variables
-- cpu to deploy sensor 1 and 2
-- cpu to deploy sensor 3 and 4
-- cpu to deploy the MissileDetector
-- cpus for the flare dispensers
-- bus to connect sensors 1 and 2 to the missile detector
-- bus to connect sensors 3 and 4 to the missile detector
-- bus to connect flare controllers to the dispensers
-- maintain a link to the detector
public static sensor0 : Sensor := new Sensor(detector,0);
public static controller0 : FlareController := new FlareController(0, nil);
public static dispenser0 : FlareDispenser := new FlareDispenser(0, mk_BaseRTThread`ThreadDef(1000E6,true,0,0,0));
public static dispenser4 : FlareDispenser := new FlareDispenser(0, mk_BaseRTThread`ThreadDef(1000E6,true,0,0,0));
public static dispenser8 : FlareDispenser := new FlareDispenser(0, mk_BaseRTThread`ThreadDef(1000E6,true,0,0,0));
operations
public CM: () ==> CM
   -- set-up sensor 0 and 1
   -- set-up sensor 2 and 3
   -- add the first controller with four dispensers
   -- add the second controller with four dispensers
   -- add the third controller with four dispensers
end CM

~~~{% endraw %}

###flarecontroller.vdmrt

{% raw %}
~~~

class FlareController is subclass of GLOBAL, BaseRTThread
instance variables
-- the left hand-side of the working angle
-- maintain a link to each dispenser
-- the relevant events to be treated by this controller
-- the status of the controller
operations
public FlareController: Angle * [ThreadDef] ==> FlareController  
  if tDef <> nil
public addDispenser: FlareDispenser ==> ()
-- get the left hand-side start point and opening angle
-- addThreat is a helper operation to modify the event
-- getThreat is a local helper operation to modify the event list
public isFinished: () ==> ()
Step: () ==> ()
sync
-- addThreat and getThreat modify the same instance variables
-- getThreat is used as a 'blocking read' from the main
end FlareController

~~~{% endraw %}

###flaredispenser.vdmrt

{% raw %}
~~~

class FlareDispenser is subclass of GLOBAL, BaseRTThread
values
responseDB : map MissileType to Plan =
missilePriority : map MissileType to nat =
types
public Plan = seq of PlanStep;
public PlanStep = FlareType * Time;
instance variables
public curplan : Plan := [];
operations
public FlareDispenser: Angle * [ThreadDef] ==> FlareDispenser
  if tDef <> nil
public GetAngle: () ==> nat
async public addThreat: EventId * MissileType * Time ==> ()
async Step: () ==> ()
private releaseFlare: EventId * FlareType * Time * Time ==> ()
public isFinished: () ==> ()
sync
mutex (addThreat,Step);
end FlareDispenser

~~~{% endraw %}

###global.vdmrt

{% raw %}
~~~

class GLOBAL
values
types
  -- there are nine different flare types, three per missile
  -- the angle at which the missile is incoming
public EventId = nat;
public Time = nat
operations
  public getAperture: () ==> Angle * Angle
end GLOBAL

~~~{% endraw %}

###missiledetector.vdmrt

{% raw %}
~~~

class MissileDetector is subclass of GLOBAL, BaseRTThread
-- the primary task of the MissileDetector is to
instance variables
-- maintain a link to each controller
-- collects the observations from all attached sensors
-- status of the missile detector
operations
public MissileDetector: [ThreadDef] ==> MissileDetector
-- addController is only used to instantiate the model
-- addThreat is a helper operation to modify the event
-- getThreat is a local helper operation to modify the event list
public isFinished: () ==> ()
Step: () ==> ()
sync
-- addThreat and getThreat modify the same instance variables
-- getThreat is used as a 'blocking read' from the main
end MissileDetector

~~~{% endraw %}

###RTTimeStamp.vdmrt

{% raw %}
~~~
class RTTimeStamp
instance variables
registeredThreads : set of BaseRTThread := {};
operations
-- private constructor (singleton pattern)
-- public operation to get the singleton instance
public RegisterThread : BaseRTThread ==> ()
public UnRegisterThread : BaseRTThread ==> ()
public IsInitialising: () ==> bool
public DoneInitialising: () ==> ()
sync 
mutex (RegisterThread);
end RTTimeStamp
~~~{% endraw %}

###sensor.vdmrt

{% raw %}
~~~

class Sensor is subclass of GLOBAL
instance variables
-- the missile detector this sensor is connected to
-- the left hand-side of the viewing angle of the sensor
operations
public Sensor: MissileDetector * Angle ==> Sensor
-- get the left hand-side start point and opening angle
-- trip is called asynchronously from the environment to
end Sensor

~~~{% endraw %}

###Test.vdmrt

{% raw %}
~~~

class Test
operations
end Test

~~~{% endraw %}

###TestCase.vdmrt

{% raw %}
~~~

class TestCase
instance variables
operations
  public GetName: () ==> seq of char
  protected AssertTrue: bool ==> ()
  protected AssertFalse: bool ==> ()
  public Run: TestResult ==> ()
  protected SetUp: () ==> ()
  protected RunTest: () ==> ()
  protected TearDown: () ==> ()
end TestCase

~~~{% endraw %}

###TestResult.vdmrt

{% raw %}
~~~

class TestResult
instance variables
operations
  public Print: seq of char ==> ()
  public Show: () ==> ()
end TestResult

~~~{% endraw %}

###TestSuite.vdmrt

{% raw %}
~~~

class TestSuite
instance variables
operations
  public Run: TestResult ==> ()
  public AddTest: Test ==> ()
end TestSuite

~~~{% endraw %}

###world.vdmrt

{% raw %}
~~~

class World
instance variables
-- maintain a link to the environment
operations
public World: () ==> World
   -- add the first controller with four dispensers
   -- add the second controller with four dispensers
   -- add the third controller with four dispensers
-- the run function blocks the user-interface thread
end World

~~~{% endraw %}
