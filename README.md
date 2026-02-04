# 2c.SIMULATING ARP /RARP PROTOCOLS
## REF NO:25015705
### DATE:04-02-2026
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
server.py
~~~
import socket

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 5000

server.bind((host, port))
server.listen(1)

print("ARP Server is waiting for connection...")

conn, addr = server.accept()
print("Connected to client:", addr)

ip_address = conn.recv(1024).decode()
print("Received IP:", ip_address)

mac_address = arp_table.get(ip_address, "IP Address not found in ARP Table")

conn.send(mac_address.encode())

conn.close()
server.close()
~~~
client.py
~~~
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 5000

client.connect((host, port))

ip = input("Enter IP Address: ")

client.send(ip.encode())

mac = client.recv(1024).decode()

print("MAC Address:", mac)

client.close()
~~~

## OUTPUT - ARP
server.py
<img width="1306" height="1064" alt="Screenshot 2026-02-04 095722" src="https://github.com/user-attachments/assets/c9c85b9a-7bcb-4174-8092-70d85a3b060c" />


client.py
<img width="1809" height="1061" alt="Screenshot 2026-02-04 095831" src="https://github.com/user-attachments/assets/f25a80e0-7422-49cb-88c0-2b2f0cfb226b" />


## PROGRAM - RARP
server.py 
~~~
import socket

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 6000

server.bind((host, port))
server.listen(1)

print("RARP Server is waiting for connection...")

conn, addr = server.accept()
print("Connected to client:", addr)

mac_address = conn.recv(1024).decode()
print("Received MAC:", mac_address)

ip_address = rarp_table.get(mac_address, "MAC Address not found in RARP Table")

conn.send(ip_address.encode())

conn.close()
server.close()
~~~
client.py
~~~
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 6000

client.connect((host, port))

mac = input("Enter MAC Address: ")

client.send(mac.encode())

ip = client.recv(1024).decode()

print("IP Address:", ip)

client.close()
~~~

## OUTPUT -RARP
server.py
<img width="1289" height="1062" alt="Screenshot 2026-02-04 100200" src="https://github.com/user-attachments/assets/ebc070f4-5339-4331-befc-df3bdab6b123" />
client.py
<img width="1539" height="1051" alt="Screenshot 2026-02-04 100231" src="https://github.com/user-attachments/assets/89a8908e-7f8e-4fc5-9260-33ea60201779" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
