---
layout: default
title: MSAW
---

~~~
This example is created by Augusto Ribeiro illustrating different concepts in VDM 
~~~
###AirSpace.vdmrt

{% raw %}
~~~
class AirSpace is subclass of GLOBAL
instance variables
airspace : map FOId to FO := {|->};
inv forall foid1, foid2 in set dom airspace & 
operations
public addFO : FO ==> ()
public removeFO : FOId ==> ()
public getFO : FOId ==> FO
public getAirspace : () ==> set of FO
public updateFO : FOId * Coordinates * Altitude ==> ()
end AirSpace
~~~{% endraw %}

###atc.vdmrt

{% raw %}
~~~
class AirTrafficController is subclass of GLOBAL
instance variables  
busy      : bool            := false;
operations

OverviewAllRadars: () ==> map FOId to FO
private getDirectionVectors : FOId ==> seq of Vector
public getAltitudeHistory : FOId ==> seq of nat

public updateHistory : () ==> ()
private registerHistory : FO ==> ()
private cleanUpHistory : () ==> ()
functions
private last : History -> Position
operations
public addRadar : Radar ==> ()

public addObstacle : Obstacle ==> ()
public findThreats : () ==> ()
public UpdatesPresent:() ==> ()
functions
public detectedByTwoRadars : set of Radar -> set of FO
public detectedByAllRadars : set of Radar -> set of FO

functions
isFOSafe : Obstacle * Position -> bool

isFOatSafeAltitude : MinimumSafetyAltitude * Position -> bool
operations
willFObeSafe : Obstacle * FO ==> ()

private writeObjectWarning : Obstacle * FO ==> ()  
private writeRadarWarning : Radar ==> ()
private isPredictPossible : FO ==> [set of Position]

private predictPosition : FO ==> set of Position
  in
functions
private predictAltitude : seq of nat -> nat

operations  
public Step : () ==> ()
thread
periodic (1600E6,0,0,0) (Step)
sync 

end AirTrafficController
~~~{% endraw %}

###environment.vdmrt

{% raw %}
~~~
class Environment is subclass of GLOBAL
types 
InputTP   = (Time * seq of inline);
inline  = FOId * int * int * Altitude * Time;
FOOut = FOId * Coordinates * Altitude * FOWarning * 

outline = FOOut | RadarOut; 

instance variables 
  io : IO := new IO();
  airspace : [AirSpace] := nil;
public Environment : String ==> Environment
public setAirSpace : AirSpace ==> ()
public handleFOWarningEvent : FOId * Coordinates * Altitude * FOWarning * 
public handleRadarWarningEvent : Coordinates * nat1 * RadarWarning * 

public showResult : () ==> ()

private updateFOs : () ==> ()

public isFinished : () ==> () 
sync
mutex(updateFOs);
mutex(handleFOWarningEvent);
per isFinished => not busy;

mutex(handleRadarWarningEvent);
thread

end Environment
~~~{% endraw %}

###FO.vdmrt

{% raw %}
~~~
class FO is subclass of GLOBAL
instance variables 

operations
public FO : FOId * Coordinates * Altitude ==> FO
public getId : () ==> FOId
public getCoordinates : () ==> Coordinates
public setCoordinates : Coordinates ==> ()
public getAltitude : () ==> Altitude
public setAltitude : Altitude ==> ()
public getPosition : () ==> Position

end FO
~~~{% endraw %}

###GLOBAL.vdmrt

{% raw %}
~~~
class GLOBAL
types
public Altitude = real;
public FOId = token;
public
public Time = nat;
public String = seq of char;
public ObstacleType = <Natural> | <Artificial> | <Airport>  | <Military_Area>;
public FOWarning = ObstacleType | <EstimationWarning>;   
public RadarWarning = <Saturated>;
public MinimumSafetyAltitude = nat | <NotAllowed>;
public Position ::
public History = seq of Position;
public Vector ::
functions
protected isPointInRange : Coordinates * nat1 * Coordinates -> bool
protected vectorSum : Vector * Vector -> Vector
protected vectorDiv : Vector * int -> Vector 
protected addVectorToPoint : Vector * Position -> Coordinates
protected vectorLength : Vector -> real 
protected unitVector : Vector -> Vector
protected dotProduct : Vector * Vector -> real
protected angleBetweenVectors : Vector * Vector -> real
protected radians2degree : real -> real
protected atan2 : real * real -> real
protected signedVectorAngle : Vector * Vector -> real
protected vectorAngle : Vector -> real * real
protected vectorRotate : Vector * real -> Vector
protected round : real -> real
operations
public test : real * real * real * real ==> 
end GLOBAL

~~~{% endraw %}

###MSAW.vdmrt

{% raw %}
~~~
system MSAW
instance variables 
cpu1 : CPU := new CPU(<FCFS>,1E6);
bus1 : BUS := new BUS(<FCFS>,1E6,{cpu1,cpu2,cpu3});
public static atc : AirTrafficController := new AirTrafficController();
public static radar1 : Radar := new Radar(6,11,20);
public static radar2 : Radar := new Radar (30,30,5);  
public static airspace : AirSpace := new AirSpace();
public static militaryZone : Obstacle := 
operations 
public MSAW : () ==> MSAW
end MSAW
~~~{% endraw %}

###obstacle.vdmrt

{% raw %}
~~~
class Obstacle is subclass of GLOBAL
instance variables
  MSA            : MinimumSafetyAltitude ;
operations 
public Obstacle : MinimumSafetyAltitude * Coordinates * nat * nat * 
public getType : () ==> ObstacleType 
public getCoordinates : () ==> Coordinates
public getSecureRange : () ==> nat1
public getMSA : () ==> MinimumSafetyAltitude


end Obstacle 
~~~{% endraw %}

###Radar.vdmrt

{% raw %}
~~~
class Radar is subclass of GLOBAL
types 
instance variables
operations
public Radar : int * int * nat1 ==> Radar
public Scan : AirSpace ==> ()
private InRange : FO ==> bool
public getDetected : () ==> set of FO
public getDetectedMap : () ==> map FOId to FO
public saturatedRadar : () ==> bool
public getSaturatingFOs : () ==> set of FOId
public getLocation : () ==> Coordinates
public getRange : () ==> nat1
private UpdatePriorityList : () ==> ()
    );
private removeNotDetected : set of FO ==> ()
private addNewlyDetected : map FOId to FO ==> ()
public isFinished: () ==> ()
functions
set2seqFOm : set of FO -> nat

operations
detectFOs : () ==> ()

Step : () ==> ()
thread
periodic(2000E6,0,0,0) (Step)
sync 

end Radar
~~~{% endraw %}

###world.vdmrt

{% raw %}
~~~
class World
instance variables  
public static
operations
public 
public Run : () ==> ()
end World
~~~{% endraw %}
