# Chat-room-for-Multiple-participants
Chat room for multiple participants using python
import socket 
Python’s socket module provides an interface to the Berkeley's Socket API. Sockets establishes communication acting as endpoints in a bidirectional communication channel between a server and one or more clients.
s=socket.socket() 
One socket(node) listens on a particular port at an IP, while other socket reaches out to the other to form a connection. Server forms the listener socket while client reaches out to the server. 
import sys 
sys module lets us access system-specific parameters and functions.
import time
This module provides various time related functions. It can provide the current time and seconds elapsed since epoch ( January 1, 1970)

Code for one to one chat room using API
Server.py
import socket//for connecting APIs
import sys
import time
## end of inports##
### init###

s=socket.socket()//Connecting 
host=socket.gethostname()//gets local host of your device
print("Server will start on host :", host)
port 8080
s.bind((host.port))//Server binds with host IP
print(" ")
print("Server alone binding to host and port successfully")
print(" ")
s.listen(1)// listens if there is any host available (ready for new connections)
conn.addr=s.accept()//connection is assigned is assigned with the physical socket and address is assigned with the IP address that it will be connecting
print(addr," Has connected to the server and is now online")//prints IP address of your host
print(" ")
while 1://so that the conversation continues
      message=input (are(">>"))
      message=message.encode()//converts texts to bytes
      conn.send(message)//sends message in byte format
      print("message has been sent..")
      print(" ")
      incoming_message =conn.recv(1024)
      incoming_message=incoming_message.decode()//converts bytes to text
      print("Client :", incoming_message)
      print(" ")


Client.py

import socket
import sys
import time

s=socket.socket()
host=input(str (" Please enter the hostname of the server: ")//we can enter the hostname of the server
port=8080
s.connect((host.port))//connected to host whose name we just entered
print("Connected to chat server ")
while 1:
       incoming_message =s.recv(1024)
       incoming_message=incoming_message.decode()
      print("Server :", incoming_message)
      print(" ")
      message=input (are(">>"))
      message=message.encode()
      s.send(message)
      print("message has been sent..")
      print(" ")


Chat room for multiple participants using local host

Server.py

import socket
s=socket.socket()
host=socket.gethostname()
port=8080
s.bind((host.port))
s.listen(1)
print("Waiting for 2 connections ")
conn.addr=s.accept()//connecting to 1st client
print("Client has connected")
conn.send("Welcome to the server ".encode())
print("Waiting for 1 connection ")
conn1.addr1=s.accept()//connecting to 2nd client
print("Client1 has connected ")
conn1.send("Welcome to the server ".encode())
while 1:
      message=input(str(">>"))
      message=message.encode()
      conn.send(message)
      conn1.send (message)//Sending message to both the clients
      print("Message set...")
      recv_message=conn.recv(1024)//Receiving the message from 1st client and sending to 2nd client
      print("Client: " ,recv_message.decode())//Decoding message received from 1st client
      conn1.send(recv_message)//Sending the message to the 2nd client 
      recv_message=conn1.recv(1024)//Recieved message from second client 
      print("Client :",recv_message.decode())//decoding received message from 2nd client
      conn.send(recv_message)//Sending message from the 2nd client to the 1st client
      

Client.py

import socket
s=socket.socket()
host=socket.gethostname()
port=8080
s.connect((host.port))
print("Connected to the server ")
message=s.recv(1024)
message=message.decode()
print("Server message :", message)
while 1:
      message=s.recv(1024)
      message=message.decode()
      print("Server :",message)
      new_message=input(str (">>"))
      new_message=new_message.encode()
      s.send(new_message)
      message=s.recv(1024)
      message=message.decode()
      print("Server: ", message)

Client 1.py

import socket
s=socket.socket()
host=socket.gethostname()
port=8080
s.connect((host.port))
print("Connected to the server ")
message=s.recv(1024)
message=message.decode()
print("Server message :", message)
while 1:
      message=s.recv(1024)//message received from server
      message=message.decode()//message is decodes from bytes to texts
      print("Server :",message)
      new_message=input(str (">>"))
      new_message=new_message.encode()
      s.send(new_message)// message sent to server
      print("Message sent")



In the one to one chat room, the server side socket binds with host API and then listens i.e. is open for any client waiting to connect. 
In the next step, conn gets assigned with the physical socket of the client and addr gets assigned with the IP address of the host which the client will connect to.
Now, with the while-loop, a state is reached when we can continue the conversation without any limit. A message from the server side is encoded ( converted from text to bytes) and then sent to the client with conn (client side socket ). The message sent from the client side is also received and decoded( converted from bytes to text) and printed on the screen. 
In the client side, the client connects to the host IP. The infinite while-loop starts and a message from the server is received, decoded and printed on the screen. Now, the client inputs a message, encodes it and sends it to the server, where it is been decoded and printed. 

In multiple participants chat room, one or more clients can connect to the server. The server binds to the host, and is open for connections from client side. After each connection, a message is displayed, that a particular client has connected. After all (two connecttions here) the connections, the while-loop starts and a message is encoded and sent to both the clients.The first client already connected to the host, not inputs, encodes and send a message to the server, which the server receives and sends it to the second client. It's the second client's turn, and it also inputs, encodes and sends a message to server. The server receives this message and sends it back to the first client. The first client now receives, decodes and prints the output. The conversation can further continue this way and we have successfully set up a chat room for 3 or more clients.
Wrapping up, this article provides you with an insight of how can on work on different libraries of python, server side APIs and establish a multi participant chat room with python.

