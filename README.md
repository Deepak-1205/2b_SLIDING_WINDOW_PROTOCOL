# 2c.SIMULATING ARP /RARP PROTOCOLS
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

ARP_client:
```
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

ARP_server:
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

    print(f"Received IP: {ip}")

    mac = address.get(ip, "MAC address not found")
    c.send(mac.encode())

c.close()
```
## OUPUT - ARP
<img width="1408" height="172" alt="image" src="https://github.com/user-attachments/assets/f6deecbc-5dcc-444f-8dfd-863982b67cbf" />
<img width="1400" height="203" alt="image" src="https://github.com/user-attachments/assets/d6eb2e82-af75-46a0-a9ec-9dd6a84da969" />


## PROGRAM - RARP
RARP_client:
```
import socket
c = socket.socket()
c.connect(('localhost', 8000))

while True:
    mac = input("Enter MAC address to find IP (or type 'exit' to quit): ")
    if mac.lower() == "exit":  
        break
    c.send(mac.encode())
    ip = c.recv(1024).decode()
    print(f"IP Address for {mac}: {ip}")
c.close()
```

RARP_server:
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening for RARP requests...")

c, addr = s.accept()
print(f"Connection established with {addr}")

rarp_table = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()
    if not mac:
        break

    print(f"Received MAC: {mac}")
    ip = rarp_table.get(mac, "IP address not found")
    c.send(ip.encode())

c.close()
s.close()

```

## OUPUT -RARP

<img width="1400" height="141" alt="image" src="https://github.com/user-attachments/assets/f95dbf8b-3c67-408d-a80e-ffb0da89a8b3" />
<img width="1402" height="163" alt="image" src="https://github.com/user-attachments/assets/68836bac-66be-4c6c-a826-5e8077622001" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
