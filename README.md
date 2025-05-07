![2c-rarp c](https://github.com/user-attachments/assets/f7c6efbf-dc71-4ece-a137-b98e006b1127)![2c-apr c](https://github.com/user-attachments/assets/5ab24ef1-029e-4764-989d-b08bf1e7aa03)# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
```
CLIENT:
import socket

c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

    if ip.lower() == "exit":
        break

    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")

c.close()
```

SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break
    try:
        mac = address[ip]
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())

c.close()
s.close()
```
## OUPUT - ARP
CLIENT:
![2c-apr c](https://github.com/user-attachments/assets/c959499b-0af5-4b9c-b0dc-83453a35e2ae)


SERVER:
![2c-apr s](https://github.com/user-attachments/assets/07372196-069e-4cb1-92bd-443b92056906)



## PROGRAM - RARP
```
CLIENT:
import socket

c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

    if ip.lower() == "exit":
        break

    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")

c.close()
```

SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
     "6A:08:AA:C2":"165.165.80.80",
    "8A:BC:E3:FA" :"165.165.79.1"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break
    try:
        mac = address[ip]
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())

c.close()
s.close()
```
## OUPUT -RARP

CLIENT:
![2c-rarp c](https://github.com/user-attachments/assets/1a007a76-d2d6-4c33-8a69-ae4e49c1e94b)

SERVER:
![2c-rarp s](https://github.com/user-attachments/assets/ba29eae0-55f9-43a5-ac49-8e84ac4acc48)

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
