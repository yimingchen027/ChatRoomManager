by YIMING CHEN


Use 'make' to compile my program, and 'make clean' to delete all the executable files. 

Using 'make' will create 3 executable file: coordinator, session_server and client.


Run ./coordinator to start the server, run ./client to start the client.

coordinator program will print connection information for compiling.



In client, it has two modes. 
In one mode, the screen print "Enter command" which means it haven't connected to a session yet. So user could use 'START s_name' or 'JOIN s_name' to join a session. The session name s_name can't exceed 8 characters and all characters must be alphabets. If you try SUBMIT, LEAVE or GET command in this mode, it will simply tell you you haven't connected yet.


In the other mode, the screen print "please enter message". This indicate that user is already connected to a session. User don't need to type SUBMIT before its message, it can simply type message. But all messages must end in '.' to indicate the end of message. 

User can use GET ONE to get one message, GET ALL to get all the messages. User can only get messages that are posted after it join this session, and can only get messages from other users in this session. User could also use LEAVE to leave this session. In this mode, user can't use FIND or START to join another session, it has to leave the current session first using "LEAVE" command.

User could use 'EXIT' command anytime to exit the program.



I use fork() to create process for each session, and use pipes to communicate between coordinator and session processes. Use UDP socket to communicate between clients and coordinator, use TCP socket to communicate between session server and client. 

The session server will close the connection and notify the coordinator to close this session when there's no user in this session(means all the users have left this session). 
