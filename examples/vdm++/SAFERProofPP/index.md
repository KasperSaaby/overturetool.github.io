---
layout: default
title: SAFERProof
---

~~~

#******************************************************
~~~
###saferproof.vdmpp

{% raw %}
~~~
class SAFERSys
types
 public SAFER:: clock: nat  -- init s == s = mk_SAFER(0)
functions  -- operations
  ControlCycle: SwitchPositions * HandGripPosition * RotCommand *
functions
  ThrusterConsistency: set of ThrusterName +> bool

----------------
values
--  arbitrary_value = mk_token(1001);
  axis_command_set : set of AxisCommand = {<Neg>,<Zero>,<Pos>};
  tran_axis_set : set of TranAxis = {<X>,<Y>,<Z>};
 public rot_axis_set : set of RotAxis = {<Roll>,<Pitch>,<Yaw>};
  null_tran_command : TranCommand = {a |-> <Zero> | a in set tran_axis_set};
  null_rot_command : RotCommand = {a |-> <Zero> | a in set rot_axis_set};
  null_six_dof : SixDofCommand 
types
 public AxisCommand = <Neg> | <Zero> | <Pos>;
  TranAxis = <X> | <Y> | <Z>;
 public RotAxis = <Roll> | <Pitch> | <Yaw>;
  TranCommand = map TranAxis to AxisCommand
 public RotCommand = map RotAxis to AxisCommand
  SixDofCommand ::
----------------

types
types
public  EngageState = <AAH_off> | <AAH_started> | <AAH_on> | <pressed_once> |
values
  click_timeout: nat = 10 -- was 100, changed for test purposes
functions -- operations
  Transition: ControlButton * SixDofCommand * nat * AAH -> AAH
functions
  AllAxesOff: set of RotAxis +> bool
  ButtonTransition: EngageState * ControlButton * set of RotAxis * 
----------------
types
 public SwitchPositions ::
 public ControlModeSwitch = <Rot> | <Tran>;
 public ControlButton = <Up> | <Down>;
 public HandGripPosition:: vert  : AxisCommand
-- add inv to exclude impossible combinations???
functions
  GripCommand: HandGripPosition * ControlModeSwitch +> SixDofCommand
---------------
types 
 public ThrusterName = <B1> | <B2> | <B3> | <B4> | <F1> | <F2> | <F3> | <F4> |
 public ThrusterSet = set of ThrusterName
functions
  RotCmdsPresent: RotCommand +> bool 
  PrioritizedTranCmd: TranCommand +> TranCommand
  CombinedRotCmds: RotCommand * RotCommand * set of RotAxis +> RotCommand
  IntegratedCommands: SixDofCommand * RotCommand * set of RotAxis * set of RotAxis +> SixDofCommand
  BFThrusters: AxisCommand * AxisCommand * AxisCommand +> 
  LRUDThrusters: AxisCommand * AxisCommand * AxisCommand +> 
  SelectedThrusters: SixDofCommand * RotCommand * set of RotAxis * set of RotAxis +> ThrusterSet
operations
public BigTest: () ==> map (SwitchPositions * HandGripPosition * RotCommand) to (ThrusterSet * SAFER * AAH)
public HugeTest: () ==> map (SwitchPositions * HandGripPosition * RotCommand) to (ThrusterSet * SAFER * AAH)
end SAFERSys
~~~{% endraw %}
