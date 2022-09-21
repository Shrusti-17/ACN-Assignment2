# ACN Assignment 2 - Socket Programming :keyboard:

## Question : 
*Part A*

a. Create a server (file server) program. It listens on a TCP socket. The
server is meant to send specific file(s) (.txt/.png/.pdf) to its client
depending on the file requested (file path).

b. Create a client program which interacts with the file server on TCP. Client
TCP connects to the file server to fetch a file given the file path in the
server. Assume that a valid client knows the ip address, port number of
the file server.

## Steps to Follow

Clone the repository and do following:

```bash
# Run the below command in separate terminal, and compile the server program (pass -lwsock32 as a parameter for windows compilation)
$ cd server
$ g++ -o server file_server.cpp -lwsock32

# Run the compiled object file (i.e. .exe file)
$ ./server

# Run the below command in separate terminal, and compile the client program (pass -lwsock32 as a parameter for windows compilation)
$ cd client
$ g++ -o client file_client.cpp -lwsock32

# Run the compiled object file (i.e. .exe file)
$ ./client
```
-------------------------------------------------

## Server Code Explaination
- ***WSADATA***
  - The ***WSADATA*** structure contains information about the Windows Sockets implementation. 
  - ***WSAStartup()*** is a function that set-up all the "behind the scenes stuff" that your application needs to use sockets. 
  - The ***MAKEWORD(2,2)*** parameter of WSAStartup makes a request for version 2.2 of Winsock on the system.
 
 - Socket programming is started by ***socket()*** where *SOCK_STREAM* specifies TCP Protocol.
 - ***sockaddr_in*** is a structure which allows you to bind a socket with the desired address so that a server can listen to the clients’ connection requests.
    - *sin_family* : This component refers to an address family which in most of the cases is set to “AF_INET”.
    - *sin_addr* : It represents a 32-bit IP address.
    - *sin_port* : It refers to a 16-bit port number on which the server will listen to the connection requests by the clients. 
 
 - ***bind()*** : When a socket is created with socket(), it exists in a name space (address family) but has no address assigned to it. bind() assigns the address specified by addr to the socket referred to by the file descriptor.

- ***listen()*** : announce willingness to accept the connection.
  - backlog parameter is the maximum length that the queue of pending connections may grow.

- ***processRequest()*** : a user defined function which specifies how client's request is handled by server. This function includes
  - ***accept()*** : accepts the connection request from client.
  - if the request is accepted by server, it sends an acknowledgement message to client via send() call.
  - Client's request for file is received by server using recv() call and is stored in a buffer.
  - If the requested file exists, open the file in read mode and read until the end of buffer.
     - Note: To indicate end of buffer, store '\0' as the last element in the buffer.  
  - the contents of requested file is sent to client.
 
 - ***sendFile()*** : user defined function which sends the requested file content to client.
   - find the size of the file to be sent and send it to client via send() call.
   - read the data of the file until it reached EOF and store it in a buffer.
   - send this file data to client via send() call.
  
 -------------------------------------------------
 ## Client Code Explaination
 
 - ***connect()*** : As we are using TCP protocol, it attempts to establish connection between 2 sockets.
 - if the connection is established successfully then the acknowlegment message sent by server is received via recv() call.
 - using fgets(), client requests for the object and stores it in a buffer.
 - the requested filename is sent to server via send() call.
 - if the file exists in the server, filesize of the requested object is received from server.
 - filesize shows how much data has to be sent to a client.

 - ***writeFile()*** : a user defined function which specifies how client receives the data from server.
    -   keep receiving the data from server until your receive all the bytes of the file.
    - using fwrite(), write the requested data to a new file .
 
