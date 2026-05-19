# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
client:
```
import socket

client = socket.socket()
client.connect(('localhost', 8000))

while True:
    data = client.recv(1024).decode()

    if not data:
        break

    print("Received frames:", data)

    client.send("Acknowledgement received from client".encode())

client.close()
```
Server:
```
import socket

server = socket.socket()
server.bind(('localhost', 8000))
server.listen(5)

print("Server is waiting for connection...")

conn, addr = server.accept()
print("Connected with", addr)

size = int(input("Enter number of frames to send : "))
frames = list(range(size))

window_size = int(input("Enter Window Size : "))

i = 0

while i < len(frames):
    packet = frames[i:i + window_size]
    conn.send(str(packet).encode())

    ack = conn.recv(1024).decode()
    print(ack)

    i += window_size

conn.close()
server.close()
```

## OUTPUT
<img width="1331" height="697" alt="Screenshot 2026-05-19 114418" src="https://github.com/user-attachments/assets/1a6f1af2-0007-4019-95d2-aeaa6bd94076" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
