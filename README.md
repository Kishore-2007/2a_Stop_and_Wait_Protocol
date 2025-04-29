# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
CLIENT:
```python
import socket
import time
client = socket.socket()
client.connect(('localhost', 8000))
client.settimeout(5)  
while True:
    msg = input("Enter a message (or type 'exit' to quit): ")
    client.send(msg.encode())  
    if msg.lower() == 'exit':  
        print("Connection closed by client")
        client.close()
        break
    try:
        ack = client.recv(1024).decode()
        if ack == "ACK":
            print(f"Server acknowledged: {ack}")
    except socket.timeout:
        print("No ACK received, retransmitting...")
        continue  
```
SERVER:
```python
import socket
server = socket.socket()
server.bind(('localhost', 8000))
server.listen(1)
print("Server is listening...")
conn, addr = server.accept()
print(f"Connected with {addr}")
while True:
    data = conn.recv(1024).decode()
    if data:
        print(f"Received: {data}")
        conn.send("ACK".encode())
        if data.lower() == 'exit':  
            print("Connection closed by client")
            conn.close()
            break
```
## OUTPUT
CLIENT:
![Screenshot 2025-04-29 200122](https://github.com/user-attachments/assets/38048d66-dacc-4c44-9276-74f77b37dd12)

SERVER:
![Screenshot 2025-04-29 200140](https://github.com/user-attachments/assets/ca3213a8-0e69-4ec0-a9fc-a2e4f914fc10)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
