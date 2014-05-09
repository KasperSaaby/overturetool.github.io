---
layout: default
title: Enigma
---

~~~
This VDM++ model is developed by Marcel Verhoef as a part of the VDM++ book
#******************************************************
~~~
###Alphabet.vdmpp

{% raw %}
~~~
class Alphabet
instance variables
inv AlphabetInv(alph)
functions
operations
  public GetChar: nat ==> char
  public GetIndex: char ==> nat
  public GetIndices: () ==> set of nat
  public GetSize: () ==> nat
  public Shift: nat * nat ==> nat
  public Shift: nat ==> nat
~~~{% endraw %}

###AlphabetTest.vdmpp

{% raw %}
~~~

class AlphabetTest
values
operations
  protected SetUp: () ==> ()
  protected RunTest: () ==> ()
  protected TearDown: () ==> ()
end AlphabetTest

~~~{% endraw %}

###Component.vdmpp

{% raw %}
~~~
class Component
instance variables
operations
  public SetNext: Component ==> ()
  public Substitute: nat ==> nat
  public Rotate: () ==> ()
  public Rotate: nat ==> ()
end Component
~~~{% endraw %}

###Configuration.vdmpp

{% raw %}
~~~
class Configuration
instance variables
operations
  protected Decode: nat ==> nat
  public Substitute: nat ==> nat
end Configuration
~~~{% endraw %}

###ConfigurationTest.vdmpp

{% raw %}
~~~

class ConfigurationTest
values
operations
  protected SetUp: () ==> ()
  protected RunTest: () ==> ()
  protected TearDown: () ==> ()
end ConfigurationTest

~~~{% endraw %}

###EnigmaTest.vdmpp

{% raw %}
~~~
class EnigmaTest
end EnigmaTest
~~~{% endraw %}

###Plugboard.vdmpp

{% raw %}
~~~
class Plugboard
instance variables
functions
operations
  public Substitute: nat ==> nat
end Plugboard
~~~{% endraw %}

###PlugboardTest.vdmpp

{% raw %}
~~~
class PlugboardTest
values
  rotcfg : inmap nat to nat =
  pbcfg : inmap nat to nat =
instance variables
operations
  protected SetUp: () ==> ()
  protected SimpleTest: () ==> ()
  protected ComplexTest: () ==> ()
  protected RunTest: () ==> ()
  protected TearDown: () ==> ()
end PlugboardTest
~~~{% endraw %}

###Reflector.vdmpp

{% raw %}
~~~
class Reflector
instance variables
functions
operations
  public Substitute: nat ==> nat
end Reflector
~~~{% endraw %}

###ReflectorTest.vdmpp

{% raw %}
~~~

class ReflectorTest
values
instance variables
operations
  protected SetUp: () ==> ()
  SimpleTest: () ==> ()

  ComplexTest: () ==> ()
  protected RunTest: () ==> ()
  protected TearDown: () ==> ()
end ReflectorTest

~~~{% endraw %}

###Rotor.vdmpp

{% raw %}
~~~
class Rotor
instance variables
inv RotorInv(latch_pos, config, alph)
functions
operations
  public Rotate: () ==> ()
  public Rotate: nat ==> ()
end Rotor
~~~{% endraw %}

###RotorTest.vdmpp

{% raw %}
~~~

class RotorTest
values
  rotcfg : inmap nat to nat =
instance variables
operations
  protected SetUp: () ==> ()
  protected SimpleTest: () ==> ()
  protected ComplexTest: () ==> ()
  protected RunTest: () ==> ()
  protected TearDown: () ==> ()
end RotorTest

~~~{% endraw %}

###SimpleEnigma.vdmpp

{% raw %}
~~~
class SimpleEnigma
values
operations
  public Keystroke : char ==> char
  -- this is needed to make this a non-abstract class

end SimpleEnigma
~~~{% endraw %}

###SimpleEnigmaTest.vdmpp

{% raw %}
~~~
class SimpleEnigmaTest is subclass of TestCase
operations
  protected SetUp: () ==> ()
  protected RunTest: () ==> ()
  protected TearDown: () ==> ()
end SimpleEnigmaTest
~~~{% endraw %}

###Test.vdmpp

{% raw %}
~~~
class Test
operations
end Test

~~~{% endraw %}

###TestCase.vdmpp

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

###TestResult.vdmpp

{% raw %}
~~~
class TestResult
instance variables
operations
  public Print: seq of char ==> ()
  public Show: () ==> ()
end TestResult
~~~{% endraw %}

###TestSuite.vdmpp

{% raw %}
~~~
class TestSuite
instance variables
operations
  public Run: TestResult ==> ()
  public AddTest: Test ==> ()
end TestSuite
~~~{% endraw %}
