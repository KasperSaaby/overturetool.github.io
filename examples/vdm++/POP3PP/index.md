---
layout: default
title: POP3
---

~~~
This example is written by Paul Mukherjee and it is used in the VDM++ book
~~~
###connectionchannel.vdmpp

{% raw %}
~~~

class MessageChannelBuffer
instance variables
instance variables
data : [MessageChannel] := nil;
operations
public Put: MessageChannel ==> ()
operations
public Get: () ==> MessageChannel
sync
per Get => data <> nil;
sync
end MessageChannelBuffer

~~~{% endraw %}

###messagechannel.vdmpp

{% raw %}
~~~

class MessageChannel
instance variables
instance variables
instance variables
io : IO := new IO();
operations
Send: POP3Types`ClientCommand | 
Listen: () ==> POP3Types`ClientCommand | 
operations
public ServerSend: POP3Types`ServerResponse ==> ()
public ClientListen: () ==> POP3Types`ServerResponse
public ClientSend: POP3Types`ClientCommand ==> ()
public ServerListen: () ==> POP3Types`ClientCommand
sync 
  per ClientListen => #fin(ServerSend) - 1 = #fin(ClientListen);
  per ServerSend => #fin(ClientSend) = #fin(ServerListen) and
  per ClientSend => #fin(ServerSend) = #fin(ClientListen) 
end MessageChannel

~~~{% endraw %}

###pop3clienthandler.vdmpp

{% raw %}
~~~

class POP3ClientHandler
types
types
ServerState = <Authorization> | <Transaction> | <Update>;

values
unknownMessageMsg: seq of char = "No such message";
alreadyDeletedMsg: seq of char = "Message already deleted";
instance variables
instance variables

operations
public POP3ClientHandler: POP3Server * MessageChannel ==> POP3ClientHandler

                              --[ReceiveCommand]

ReceiveQUIT: POP3Types`QUIT ==> POP3Types`ServerResponse

ReceiveSTAT: POP3Types`STAT ==> POP3Types`ServerResponse

ReceiveLIST: POP3Types`LIST ==> POP3Types`ServerResponse

functions
MakeScanListHeader: set of POP3Server`MessageInfo -> seq of char

set2seq[@tp]: set of @tp -> seq of @tp
MakeScanListing: set of POP3Server`MessageInfo -> seq of char

MakeMultilineResponse: seq of seq of char -> seq of char
MakeLineSeq: seq of char -> seq of seq of char
GetLine: seq of char -> (seq of char) * (seq of char)
Len: seq of char | seq of seq of char -> nat
sum: set of nat -> nat
Card: set of nat -> nat

operations
ReceiveRETR: POP3Types`RETR ==> POP3Types`ServerResponse
ReceiveDELE: POP3Types`DELE ==> POP3Types`ServerResponse


ReceiveNOOP: POP3Types`NOOP ==> POP3Types`ServerResponse

ReceiveRSET: POP3Types`RSET ==> POP3Types`ServerResponse


ReceiveTOP:  POP3Types`TOP ==> POP3Types`ServerResponse
ReceiveUIDL: POP3Types`UIDL ==> POP3Types`ServerResponse

ReceiveUSER: POP3Types`USER ==> POP3Types`ServerResponse

ReceivePASS: POP3Types`PASS ==> POP3Types`ServerResponse
functions
static public int2string: int -> seq of char
static Abs: int -> nat
static int2stringR: nat -> seq of char
static Id: nat -> nat



thread
end POP3ClientHandler

~~~{% endraw %}

###pop3message.vdmpp

{% raw %}
~~~

class POP3Message
instance variables

operations
public POP3Message: seq of char * seq of char * seq of char ==> POP3Message
public GetBody: () ==> seq of char
public GetHeader: () ==> seq of char
public GetText: () ==> seq of char
public Delete: () ==> POP3Message
public IsDeleted: () ==> bool
public Undelete: () ==> POP3Message
public GetSize: () ==> nat
public GetUniqueId: () ==> seq of char
end POP3Message

~~~{% endraw %}

###pop3server.vdmpp

{% raw %}
~~~

class POP3Server
types
public MessageInfo :: index : nat
instance variables
instance variables
types
public MailDrop = map POP3Types`UserName to MailBox;
operations
public POP3Server: POP3Server`MailDrop * MessageChannelBuffer * 
public AuthenticateUser: POP3Types`UserName * POP3Types`Password ==> bool
public IsLocked: POP3Types`UserName ==> bool

operations
SetUserMessages: POP3Types`UserName * seq of POP3Message 
GetUserMail: POP3Types`UserName ==> MailBox
sync
operations
GetUserMessages: POP3Types`UserName ==> seq of POP3Message

public RemoveDeletedMessages: POP3Types`UserName ==> bool
public AcquireLock: ClientHandlerId * POP3Types`UserName ==> ()

public ReleaseLock: ClientHandlerId ==> ()
sync
operations
CreateClientHandler: MessageChannel ==> ()

public IsMessageNumber: POP3Types`UserName * nat ==> bool
public IsValidMessageNumber: POP3Types`UserName * nat ==> bool
public MessageIsDeleted: POP3Types`UserName * nat ==> bool
public DeleteMessage: POP3Types`UserName * nat ==> ()
public GetMsgHeader: POP3Types`UserName * nat ==> seq of char
public GetMsgBody: POP3Types`UserName * nat ==> seq of char


public ResetDeletedMessages: POP3Types`UserName ==> ()
public GetMessageText: POP3Types`UserName * nat ==> seq of char
public GetMessageSize: POP3Types`UserName * nat ==> nat
public GetMessageInfo: POP3Types`UserName * [nat] ==> set of MessageInfo


public GetUidl: POP3Types`UserName * nat ==> seq of char
public GetAllUidls:  POP3Types`UserName ==> seq of seq of char

public GetNumberOfMessages: POP3Types`UserName ==> nat

public GetMailBoxSize: POP3Types`UserName ==> nat
public GetChannel: () ==> MessageChannelBuffer
functions
public sumseq: seq of nat -> nat
Len: seq of nat -> nat

thread
while true do
operations
public WaitForServerStart: () ==> ()
sync
per WaitForServerStart => serverStarted;
end POP3Server

~~~{% endraw %}

###pop3test.vdmpp

{% raw %}
~~~
class POP3Test
values
users : seq of POP3Types`UserName = 
passwords : seq of POP3Types`Password = 
headers : seq of seq of char = 
bodies : seq of seq of char = 
functions
public MakePasswordMap: () -> map POP3Types`UserName to POP3Types`Password

public MakeMailDrop: () -> POP3Server`MailDrop
public MakeMessages: POP3Types`UserName -> seq of POP3Message
TestRun1: () -> seq of POP3Types`ClientCommand
instance variables
   server : POP3Server;
operations
public StartServer: POP3Server ==> ()


public Test1: () ==> ()
public Test2: () ==> ()
Start: POP3TestSender | POP3TestListener ==> ()
public POP3Test:() ==> POP3Test
traces
  Two: StartServer(server);
end POP3Test
class POP3TestSender
instance variables
id   : seq of char;
operations
public POP3TestSender: seq of char * seq of POP3Types`ClientCommand * 
LogClient: POP3Types`ClientCommand ==> ()
SendCmd: MessageChannel * POP3Types`ClientCommand ==> ()
thread

end POP3TestSender
class POP3TestListener
instance variables
id : seq of char;
operations
public POP3TestListener: seq of char * MessageChannel ==> POP3TestListener
LogServer: POP3Types`ServerResponse ==> ()
public IsFinished: () ==> ()
sync 
thread
end POP3TestListener
~~~{% endraw %}

###pop3types.vdmpp

{% raw %}
~~~

class POP3Types
types
public ClientCommand = StandardClientCommand | 

public QUIT :: ;

public STAT :: ;

public LIST :: messageNumber : [nat];

public RETR :: messageNumber : nat;
public DELE :: messageNumber : nat;

public NOOP :: ;

public RSET :: ;

public TOP :: messageNumber : nat

public UIDL :: messageNumber : [nat];

public USER :: name : UserName;

public PASS :: string : seq of char;

public APOP :: name   : seq of char

public UserName = seq of char;

public ServerResponse = OkResponse | ErrResponse;
functions
end POP3Types

~~~{% endraw %}
