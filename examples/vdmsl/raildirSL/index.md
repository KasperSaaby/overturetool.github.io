---
layout: default
title: raildir
---

~~~

In this specification a model of interlocking systems is presented,
K.M. Hansen, Formalising Railway Interlocking Systems, 
Kirsten Mark Hansen. Linking Safety Analysis to Safety Requirements
#******************************************************
~~~
###rail.vdmsl

{% raw %}
~~~

module station
exports
  functions
definitions

types

functions
    NoReflexive : Tracks +> bool
  Symmetric : Tracks +> bool
functions
    Is_wf_Tracks : Tracks +> bool
types

functions
   PointsInTracks : Tracks * Points +> bool
   PointsInTracks (tracks,points) ==

   Inverses : Points +> bool
   Inverses (points) ==
   OkDomRng: Points +> bool
   OkDomRng (points) ==

   RelateToTracks: Tracks * Points +> bool
   RelateToTracks (tracks,points) ==
   Control2Dir: Points +> bool
   Control2Dir (points) ==
   Is_wf_Points: Tracks * Points +> bool
   Is_wf_Points (tracks,points) ==

   SeperateBranches: Tracks * Crossings +> bool
   SeperateBranches (tracks,crossings) ==

   CrossInTracks: Tracks * Crossings +> bool
   CrossInTracks (tracks,crossings) ==

   UniqueCross: Crossings +> bool
   UniqueCross (crossings) ==

   DiffPointsCrossings: Points * Crossings +> bool
   DiffPointsCrossings (points,crossings) ==
   Is_wf_Crossings: Tracks * Points * Crossings +> bool
   Is_wf_Crossings (tracks,points,crossings) ==
types
functions
   UniqueSignals: Signals +> bool
   UniqueSignals (signals) ==

   SigInTracks: Tracks * Signals +> bool
   SigInTracks (tracks,signals) ==
   Is_wf_Signals: Tracks * Signals +> bool
   Is_wf_Signals (tracks,signals) ==

types
functions
   Is_wf_Station_topo (stationtopo) ==

types
     Track_states  = map Track_id  to Track_state;
   Track_state   =  map Train_id to Train_type;
   Point_state    =  Point_control * Operation ;
      Signal_state = <stop> | <driveaspect>
functions
   ConformTracks: Tracks * Track_states  +> bool
   ConformTracks (tracks,trackstates)  ==

   TracksStateInTopo: Tracks * Track_states  +> bool
   TracksStateInTopo (tracks,trackstates)  ==

   TracksTopoInState: Tracks * Track_states  +> bool
   TracksTopoInState (tracks,trackstates)  ==

   ConformPoints: Points * Point_states  +> bool
   ConformPoints (points,pointstates)  ==

   PointsStateInTopo: Points * Point_states  +> bool
   PointsStateInTopo (points,pointstates)  ==
   PointsTopoInState: Points * Point_states  +> bool
   PointsTopoInState (points,pointstates)  ==
   ConformSignals: Signals * Signal_states  +> bool
   ConformSignals (signals,signalstates)  ==

   Is_wf_Trains: Tracks * Points * Crossings * Track_states +> 
   Is_wf_Trains (tracks,points,crossings,trackstates)  ==

   UniqueTrain : Track_states +> bool
   UniqueTrain (trackstates) ==
   Trains: Track_states * (map Train_id to set of Track_id) +> 
   Trains (trackstates,sorted)  ==
   Update: (Track_id * Track_state) * 
   Update (mk_(t,trackstate),sorted)  ==
   Connected: (map Train_id to set of Track_id) * Tracks +> bool
   Connected (trains,tracks)  ==

   ExistsPath: set of Track_id * Tracks +> bool
   ExistsPath (trackset,tracks)  ==

   Path: set of Track_id * seq of Track_id * Tracks * 
   Path (trackset,connected,tracks,tried)  ==
   OkPointTrains: (map Train_id to set of Track_id) * Points +> 
   OkPointTrains (trains,points)  ==
   OkCrossTrains: (map Track_id to set of Track_id) * Crossings +> 
   OkCrossTrains (trains,crossings)  ==
Is_wf_Station_state :  Station_topo * Station_state +> bool
Is_wf_Station_state (stationtopo,stationstate) ==

end station
module safe_req
imports
        Station_state :: trackstates  : station`Track_states
  functions
exports

definitions

functions
   SafeReq (stationtopo,stationstate)  ==
  pre Is_wf_Station_topo (stationtopo) and 
   NoCollision: Station_topo * Station_state +> bool
   NoCollision (stationtopo,stationstate)  ==
   OneTrainAtCross: Crossings * Track_states +> bool
   OneTrainAtCross (crossings,trackstates)  ==
   NoDerail: Station_topo * Station_state +> bool
   NoDerail (stationtopo,stationstate)  ==
   Trains: Track_states * (map Train_id to set of Track_id) +> 
   Update: (Track_id * Track_state) * 
   Update (mk_(t,trainids),sorted)  ==
   Ok_Point_states: (Track_id * Track_id) * Points * Point_states +> 
   Ok_Point_states (mk_(t1,t2),points,pointstates) ==
   pre mk_(t1,t2) in set dom points;
   Point_state_ok: (Track_id * Track_id) * Track_id * Points * 
   Point_state_ok (tpair,t,points,pointstates) ==
   pre t in set dom pointstates and tpair in set dom points and 
end safe_req
module impl
imports
   Station_state :: trackstates : station`Track_states
   Track_states  =  map station`Track_id to station`Track_state
   Point_states   =  map station`Track_id to station`Point_state
      Signal_states = map station`Signal_id to station`Signal_state
  functions
exports
definitions



types
functions
   Impl (stationtopo,stationstate) ==
   pre Is_wf_Station_topo (stationtopo) and 


   NoCollision: Areas * Crossings +> bool
   NoCollision (areas,crossings) ==
   NoDerail: Areas * Station_topo * Station_state +> bool
   NoDerail (areas,stationtopo,stationstate) ==
   NoDerailUnderTrains: Station_topo * Station_state +> bool 
   NoDerailUnderTrains (stationtopo,stationstate) == 
  NoDerailPossible : Areas * Station_topo * Station_state +> bool 
  NoDerailPossible (areas,stationtopo,stationstate) ==
   Trains: Track_states * (map Train_id to set of Track_id) +> 
   Trains (trackstates,sorted)  ==
   Update: (Track_id * Track_state) * 
   Update (mk_(t,trainids),sorted)  ==
   TrainType : Area * Station_state +> Train_type
   TrainType (area,stationstate) ==
   pre forall t in set area & t in set dom stationstate.trackstates ;
   NoDerailFixed : Area * Station_topo * Station_state +> bool
   NoDerailFixed (area,stationtopo,stationstate) ==
   Ok_Point_states: (Track_id * Track_id) * Points * Point_states +> 
   Ok_Point_states (mk_(t1,t2),points,pointstates) ==

   pre mk_(t1,t2) in set dom points;

   Point_state_ok: (Track_id * Track_id) * Track_id * Points * 
   Point_state_ok (tpair,t,points,pointstates) ==
   pre t in set dom pointstates and tpair in set dom points and 
   InterlockPoints: (Track_id * Track_id) * Points * Point_states +> 
   InterlockPoints (mk_(t1,t2),points,pointstates) ==
pre IsPoint (t1,points) or IsPoint (t2,points);
   IsPoint: Track_id * Points +> bool
   IsPoint (t,points) ==
   IsInterlockPoint: Track_id * Points * Point_states +> bool
   IsInterlockPoint (t,points,pointstates) ==
   NoDerailAutonomous: Area * Station_topo * Station_state +> bool
   NoDerailAutonomous (area,stationtopo,stationstate) ==

   OkAutonomPoint_states: (Track_id * Track_id) * Points * 
   OkAutonomPoint_states (mk_(t1,t2),points,pointstates) ==
   FindAreas : Station_topo * Station_state +> Areas
   FindAreas (stationtopo,stationstate) ==
   Occupied: Track_states * (map Train_id to set of Track_id) +> 
   pre forall trackstate in set rng trackstates & 

   RemoveTrain : Train_id * Track_states +> Track_states
   RemoveTrain (train,trackstates) ==

   DeduceAreas: (map Train_id to set of Track_id) * 
   FindArea : set of Track_id * Area * Station_topo * Station_state +> 
  FindArea (tracks,area,stationtopo,stationstate) ==

   Neighbours : Track_id * set of Track_id * Station_topo * 
   Neighbours (t,area,stationtopo,stationstate) ==
   NeighbourCandidates: Track_id * set of Track_id * Tracks +> 
   NeighbourCandidates (t,area,tracks) ==
   OkEdge: (Track_id * Track_id) * Station_topo * Station_state +> bool
   OkEdge (tpair,stationtopo,stationstate) ==
   OkPoints: (Track_id * Track_id) * Points * Point_states +> bool
   OkPoints (mk_(t,t'),points,pointstates) ==
   StopSignal: (Track_id * Track_id) * Signals * Signal_states +> bool
   StopSignal (tpair,signals,signalstates) ==
   Branch : (Track_id * Track_id) * Points +> bool
   Branch (mk_(t1,t2),points) ==
end impl 
module Test
exports all
definitions

tracksv = { mk_("K12","26"), mk_("26","K12"),
pointsv = { mk_("25","26")  |-> { "25" |-> <right> },
crossingsv = { mk_("17s", "17b")};
signalsv = { mk_("ol","K12") |-> "N",

trackstatev = { "K12" |-> {|->},
pointstatev = { "25" |-> mk_(<left>,<interlock>),
signalstatev = { "N"  |-> <stop>,

~~~{% endraw %}
