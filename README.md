# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM:
Implementation of sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### client
```
import socket

s = socket.socket()
s.bind(('localhost', 5000)) 
s.listen(5)
c, addr = s.accept()
size = int(input("Enter number of frames to send: "))
l = list(range(size))
window_size = int(input("Enter window size: ")) 

st = 0
i = 0

while i < len(l):
    st = min(i + window_size, len(l)) 
    c.send(str(l[i:st]).encode())
    ack = c.recv(1024).decode()
    if ack:
        print("Acknowledgment received for frames:", l[i:st])
        i += window_size  
    else:
        break

c.close()  

```
### Server
```
import socket

s = socket.socket()
s.connect(('localhost', 5000))  

while True:
    data = s.recv(1024).decode()
    if data:
        print("Received frames:", data)
        s.send("Acknowledgment received from the client".encode())  
    else:
        break

s.close() 

```
## OUPUT

### Client
![image](https://github.com/user-attachments/assets/ef158e5a-a2c3-4997-9b7a-ab803864e958)
### server
![image](https://github.com/user-attachments/assets/0cb8aac7-bffd-4d7f-a7ec-6cfb5abc5042)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
