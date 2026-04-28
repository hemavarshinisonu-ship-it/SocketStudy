# Ex.No:1a  			Study of Socket Programming

## Aim: 
To implement the study on Socket Programming using Jupiter Notebook
## Introduction:
     Socket programming enables communication between computers over a network using client–server architecture. It allows data exchange through sockets, which act as endpoints identified by IP address and port number.
## Understanding Socket Programming:
     Socket programming uses sockets, identified by an IP address and port number, to enable communication between a client and a server. It mainly includes stream sockets, which are reliable and connection-oriented, and datagram sockets, which are connectionless and faster but less reliable.
## Key Concepts in Socket Programming:
1. Sockets:
     A socket is a communication endpoint identified by an IP address and port number. It is of two types: stream sockets (reliable, connection-oriented) and datagram sockets (connectionless, best-effort).
2. Client–Server Model:
     Socket programming follows a client-server model where the server waits for connections and the client initiates communication.
3. TCP/IP Protocol:
     TCP ensures reliable and ordered data transmission, while IP handles routing of data between devices.
4. Basic Socket Functions:
     Common functions include socket(), bind(), listen(), accept(), connect(), send(), and recv() for communication.

## Server-Side Operations:
•	Servers create a socket using socket() and bind it to a specific IP address and port using bind().
•	They then listen for incoming connections with listen() and accept connections with accept().
•	Once a connection is establi
•	shed, servers can send and receive data using send() and recv().

## Client –Server Operations
    1. Clients create a socket using socket() and connect to a server using connect().
    2. After establishing a connection, clients can send and receive data using send() and recv().

## Use Cases of Socket Programming:
     Socket programming is widely used in web development, file transfer, online gaming, and real-time communication. It forms the basis of protocols like HTTP, FTP, and SMTP, enabling data exchange between client and server systems over a network.
## Example Use Cases:
     1.Web Servers: Use sockets to handle HTTP requests and send web pages.
     2.Chat Applications: Enable real-time messaging between users.
     3.File Transfer: Used in protocols like FTP for sending files.
     4.Online Games: Support communication between players and servers.
     5.RPC: Allows execution of code on remote systems using sockets.
~~~
import socket
import threading
import time

HOST = '127.0.0.1'
PORT = 9002   # new port

# ---------------- SERVER ----------------
def server():
    s = socket.socket()
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    s.bind((HOST, PORT))
    s.listen(1)

    print("Saveetha Engineering College Server is starting...")
    conn, addr = s.accept()
    print("Connected to client:", addr)

    messages = [
        "Good morning. Welcome to Saveetha Engineering College.",
        "May I know which program you are interested in?",
        "We offer undergraduate programs such as Computer Science, Information Technology, and Electronics.",
        "You can apply through our official admission portal.",
        "Thank you for contacting Saveetha Engineering College. Have a good day."
    ]

    for msg in messages:
        conn.send(msg.encode())
        time.sleep(1)

        reply = conn.recv(1024).decode()
        print("Client:", reply)

    conn.close()
    print("Server closed")


# ---------------- CLIENT ----------------
def client():
    time.sleep(1)

    s = socket.socket()
    s.connect((HOST, PORT))
    print("Client connected to server")

    replies = [
        "Good morning.",
        "I am interested in the Computer Science program.",
        "That sounds informative. Thank you.",
        "Could you please guide me on the application process?",
        "Thank you for your assistance."
    ]

    for reply in replies:
        data = s.recv(1024).decode()
        print("Server:", data)

        s.send(reply.encode())
        time.sleep(1)

    s.close()
    print("Client closed")


# ---------------- THREADS ----------------
t1 = threading.Thread(target=server)
t2 = threading.Thread(target=client)

t1.start()
t2.start()

t1.join()
t2.join()

print("Conversation completed successfully.")
~~~
## Output:
<img width="1113" height="361" alt="1a" src="https://github.com/user-attachments/assets/1c9a397d-0655-4e81-b72f-85745f1e5863" />

## Result:
Thus the study of Socket Programming Completed Successfully
