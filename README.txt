Firts step you must Run server file

1- gcc server.c -o server
2- ./server 8080

./server <port>

second you must run single or multiple client file

1- gcc client.c -o client
2- ./client 127.0.0.1 8080

./server  <IP> <port>


in the client section you can use this commands :

ls    ------> list all file inside folder
get   ------> get file
put   ------> send file
quite ------> end program
