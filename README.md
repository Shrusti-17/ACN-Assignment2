# ACN Assignment 2 - Socket Programming :keyboard:


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
