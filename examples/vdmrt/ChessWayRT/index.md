---
layout: default
title: ChessWay
---

~~~
This example shows the discrete event model used for
~~~
###Accelerometer.vdmrt

{% raw %}
~~~

class Accelerometer
instance variables
operations
  public getAccelerationData: () ==> real * real * real
end Accelerometer

~~~{% endraw %}

###Actuator.vdmrt

{% raw %}
~~~
class Actuator is subclass of IActuatorReal
instance variables
-- actuator value
operations
-- constructor for PWM
-- default constructor for PWM
-- set actuator value
end Actuator
~~~{% endraw %}

###ChessWay.vdmrt

{% raw %}
~~~

system ChessWay
instance variables
  -- communication infrastructure (one BUS at 100 kpbs)
instance variables
  -- actuators (co-simulation variables)
instance variables
  -- flag to enable debugging logging in system classes
operations
end ChessWay

~~~{% endraw %}

###Controller.vdmrt

{% raw %}
~~~

class Controller
values
instance variables
  -- the motor that is controlled
operations
instance variables
operations
  -- push a value to the environment
  -- get a value from the environment
values
operations
operations
operations
  -- auxiliary operation are used for diagnostics
  public CtrlLoopBody: () ==> ()
  -- auxiliary operation are used for diagnostics
thread
end Controller

~~~{% endraw %}

###DirectionSwitch.vdmrt

{% raw %}
~~~

class DirectionSwitch
instance variables
operations
types
operations
end DirectionSwitch

~~~{% endraw %}

###DTControl.vdmrt

{% raw %}
~~~
class DTControl is subclass of DTObject
operations
-- calculates output, based on the error
end DTControl
~~~{% endraw %}

###DTObject.vdmrt

{% raw %}
~~~
class DTObject
instance variables
protected sampletime: real := 1.0E-9;
operations
public SetSampleTime: real ==> ()
end DTObject
~~~{% endraw %}

###Environment.vdmrt

{% raw %}
~~~

class Environment
values
types
  -- map open-loop sensor name to non-empty sequence of 3-tuples
instance variables
operations
  -- auxiliary operation to load a simulation scenario
  -- auxiliary operation executed by the main loop
  public evalSingle: real * seq of char * tCtCurve ==> ()
instance variables
instance variables
  -- the maximum simulation time
  -- the wheel model
  -- the hall sensor model
  -- the user model
operations
      -- set the maximum simulation time
      -- create the wheel models
      -- create the hall sensor models
      -- force the initial values for the Hall sensors
      -- create the user model
instance variables
  -- actuators
instance variables
operations
  private setCosimValue: seq of char * real ==> ()
  -- auxiliary operation to retrieve sensor data
  private getCosimValue: seq of char ==> real
sync
operations
      -- update the open-loop sensor values and user behavior
      -- update the wheel models
      -- update the Hall sensor models
      -- update the user model
      -- optional diagnostics
      -- check if the maximum simulation time was reached
  -- operation to signal the main thread once we're done
thread
operations
  public printEnvironment: () ==> ()
end Environment

~~~{% endraw %}

###Gyroscope.vdmrt

{% raw %}
~~~

class Gyroscope
instance variables
operations
  public getYawRateData: () ==> real
end Gyroscope

~~~{% endraw %}

###HallSensor.vdmrt

{% raw %}
~~~

class HallSensor
instance variables
  -- link to the environment
  -- link to the motor
functions
operations
  private setSensor: seq of char * bool ==> ()
  public setSensors: bool * bool * bool ==> ()
  public evaluate: () ==> ()
end HallSensor

~~~{% endraw %}

###IActuatorReal.vdmrt

{% raw %}
~~~
class IActuatorReal
operations
-- set actuator value
end IActuatorReal
~~~{% endraw %}

###ISensorReal.vdmrt

{% raw %}
~~~
class ISensorReal
operations
-- set actuator value
end ISensorReal
~~~{% endraw %}

###LeftController.vdmrt

{% raw %}
~~~

class LeftController
values
instance variables
  -- sensors connected to the left controller
operations
instance variables
operations
instance variables
  -- time at control loop entry
  -- enable debug logging

operations
  public CtrlLoopBody: () ==> ()
  public CtrlLoopExit: () ==> ()
operations
operations
operations
end LeftController

~~~{% endraw %}

###MotorActuator.vdmrt

{% raw %}
~~~

class MotorActuator
types
instance variables
  -- link back to the controller managing this resource
operations
  public initActuator: () ==> ()
  public isActuated: () ==> bool
  public setFreeRunning: () ==> ()
  public setActuated: () ==> ()
  public SetValue: real ==> ()
  public setPWM: real ==> ()
  public printDiagnostics: () ==> ()
end MotorActuator

~~~{% endraw %}

###MotorSensor.vdmrt

{% raw %}
~~~

class MotorSensor
instance variables
  -- link back to the controller managing this resource
operations
  public GetValue: () ==> real
  public getHallSensorData: () ==> bool * bool * bool
end MotorSensor

~~~{% endraw %}

###OnOffSwitch.vdmrt

{% raw %}
~~~

class OnOffSwitch
instance variables
operations
  public getStatus: () ==> bool
end OnOffSwitch

~~~{% endraw %}

###P.vdmrt

{% raw %}
~~~
class P is subclass of DTControl
instance variables
-- design parameters
operations
-- constructor for PD
-- default constructor for PD
-- calculates output, based on the error
values
-- defaults
end P
~~~{% endraw %}

###PD.vdmrt

{% raw %}
~~~
class PD is subclass of DTControl
instance variables
-- design parameters
-- variables
operations
-- constructor for PD
-- constructor for PD
-- default constructor for PD
-- calculates output, based on the error
values
-- defaults
end PD
~~~{% endraw %}

###PI.vdmrt

{% raw %}
~~~
class PI is subclass of DTControl
instance variables
-- design parameters
-- variables
operations
-- constructor for PI
-- default constructor for PI
-- calculates output, based on the error
values
-- defaults
end PI
~~~{% endraw %}

###PID.vdmrt

{% raw %}
~~~
class PID is subclass of DTControl
instance variables
-- design parameters
-- variables
operations
-- constructor for PID
-- constructor for PID
-- default constructor for PID
-- calculates output, based on the error
values
-- defaults
end PID
~~~{% endraw %}

###RightController.vdmrt

{% raw %}
~~~

class RightController
values
instance variables
  -- sensors connected to the right controller
operations
instance variables
operations
instance variables
  -- time at control loop entry
  -- enable debug logging

operations
  public CtrlLoopBody: () ==> ()
  public CtrlLoopExit: () ==> ()
operations
operations
operations
end RightController

~~~{% endraw %}

###SafetySwitch.vdmrt

{% raw %}
~~~

class SafetySwitch
instance variables
operations
  public getStatus: () ==> bool
end SafetySwitch

~~~{% endraw %}

###Sensor.vdmrt

{% raw %}
~~~
class Sensor is subclass of ISensorReal
instance variables
-- sensor value
operations
-- constructor for Sensor
-- default constructor for Sensor
-- get sensor value
end Sensor
~~~{% endraw %}

###SetpointProfileCSV.vdmrt

{% raw %}
~~~
class SetpointProfileCSV
instance variables
-- file to read and the number of lines it contains
-- current and next setpoint
operations
-- constructor for SetpointProfileCSV
-- constructor for SetpointProfileCSV
-- read the next setpoint from the file
-- return the value of the current setpoint
	-- read from file if we need to
	-- update setpoint if necessary
    -- show the computed setpoint
	-- return current setpoint
-- quit with given error (printf version)
-- quit with given error (println version)
end SetpointProfileCSV
~~~{% endraw %}

###User.vdmrt

{% raw %}
~~~

class User
values
instance variables
  -- link to both wheels
  -- last evaluated at time step
  -- current deviation from upright
operations
  public evaluate: () ==> ()
end User

~~~{% endraw %}

###Wheel.vdmrt

{% raw %}
~~~

class Wheel
values
instance variables
  -- link to the environment
  -- last evaluated at time step
  -- current angular acceleration
  -- current angular speed
  -- current angular position
operations
  private isActuated: () ==> bool
  private getPWM: () ==> real
  public evaluate: () ==> ()
end Wheel

~~~{% endraw %}

###World.vdmrt

{% raw %}
~~~

class World
values
  -- maximum simulation time is 10 seconds
instance variables

operations
  -- top-level access function for ChessWay DE only simulation
  -- top-level access function to run a particular scenario
      -- load a simulation scenario
      -- link the environment to the system controllers
      -- cross link the two system controller models
      -- announce start of simulation run
	  -- initialize the system tasks
      -- start the environment and periodic loopcontroller tasks
      -- wait for simulation run end (lock main DESTECS GUI thread)
      -- announce end of simulation run
instance variables
operations
  public signal: () ==> () 
sync
end World

~~~{% endraw %}
