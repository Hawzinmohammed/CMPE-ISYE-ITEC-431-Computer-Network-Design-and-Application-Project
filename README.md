Project Overview:
You will first write a server program that allows users (clients) to upload and download files
to and from a specified directory. The server will be run as follows:
server directory port
where "directory" is the location of the files to be accessed and "port" is the TCP port number
that clients will use to locate the server. For example,
$ server /home/student/files 1888
File server listening on localhost port 1888
After the server has started, it simply spins in an infinite loop waiting for incoming
connections until you decide to kill it.
To connect to the server, you can use nc (netcat) as client for testing.
Once the client has connected to the server, it should allow the user to interactively get a
directory listing, download and upload files, and close the connection.
For example:
$ nc localhost 1888
Welcome to Bob's file server.
USER test test123
200 User test granted to access.
LIST
a.out 5876
client 9130
client.c 580
.
GET client.c
#include<stdlib.h>
#include<stdio.h>
main() { }
.
GET foobar
404 File foobar not found.
PUT test
This is text message that put as example
.
200 44 Byte test file retrieved by server and was saved.
LIST
a.out 5876
client 9130
client.c 580
test 44
.
DEL a.out
200 File a.out deleted.
DEL nofile
404 File nofile is not on the server.
QUIT
Goodbye!
$
First, the server must be able to handle multiple client connections (all of which might be
active at any given time).
Protocol
This version of FTP will be slight variation of the FTP protocol implemented over a TCP
connection which is guaranteed to be reliable.
Commands
The client and server will communicate with each other by sending ASCII Commands as it
given above. You should implement following commands:
USER <Username> <PASS>
Server should handle simple user and passwprd authentication. If user name and password
okay server should give “200” response and allow following commands otherwise should
give Error code like “400 User not found” . If user not found client only should use
command USER or QUIT.
USER test test100
200 User test granted to access.
USER nobody xxx
400 User not found. Please try with another user.
If user and password is Okay server should accept following commands:
LIST
If client gives this command in this case server should list filenames and file sizes to client.
And after files listed list should terminated with “.”.
Filename1 X
Filename2 Y
Filename3 Z
.
GET <filename>
If client gives this command in this case server should read file content of filename and send
content to client side. Also after file content dumped it should terminated with “.”. If file is
not found server should give 404 Error.
GET file
This is file content.
.
GET foobar
404 File foobar not found.
PUT <filename>
If client gives this command in this case server should read file content from client and save
to server side. Client should terminated file with “.”. After server take file should give
message 200 and report hom much Byte transfered and saved on server side. If server can not
save file should give 400 Error.
PUT test
This is text message that put as example
.
200 44 Byte test file retrieved by server and was saved.
PUT test
400 File cannot save on server side.
DEL <filename>
If client gives this command in this case server should delete file from server side. If its
succedded server should give 200 message otherwise should give 404.
DEL a.out
200 File a.out deleted.
DEL nofile
404 File nofile is not on the server.
QUIT
If client gives this command in this case server should give goodbye message and terminates
the client connection.
QUIT
Goodbye!
