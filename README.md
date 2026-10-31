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

## Client:
```
import socket

c = socket.socket()
c.connect(('localhost', 8000))
c.settimeout(5)

while True:
    msg = input("Message: ")
    c.send(msg.encode())

    if msg == "exit":
        break

    try:
        if c.recv(1024).decode() == "ACK":
            print("ACK received")
    except socket.timeout:
        print("No ACK, retransmitting...")

c.close()
```

## Server:
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server ready...")

c, _ = s.accept()
while True:
    msg = c.recv(1024).decode()
    if not msg:
        break
    print("Received:", msg)
    c.send(b"ACK")
    if msg == "exit":
        break

c.close()
s.close()
```
## OUTPUT

## Client:
<img width="372" height="235" alt="Screenshot 2026-10-31 081909" src="https://github.com/user-attachments/assets/62837ef9-4347-4384-8d37-87342784c248" />

## Server:
<img width="305" height="156" alt="Screenshot 2026-10-31 081924" src="https://github.com/user-attachments/assets/749919ac-41b6-435c-82eb-dc248c55e84c" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
