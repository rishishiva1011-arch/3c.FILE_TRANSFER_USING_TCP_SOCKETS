# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM

server.py

```
import socket
port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)

print("Server listening on port", port)

while True:
    conn, addr = s.accept()
    print("Connected to", addr)
    
    data = conn.recv(1024)
    print('Server received', repr(data))

    filename = 'C:\\Users\\rishi\\Desktop\\CN\\Ex3c\\mytext.txt'
    with open(filename, 'rb') as f:
        l = f.read(1024)
        while l:
            conn.send(l)
            print('Sent', repr(l))
            l = f.read(1024)
    
    print('Done sending')
    conn.send('Thank you for connecting'.encode())
    conn.close()
```

client.py

```
import socket
s = socket.socket()
host = socket.gethostname()
port = 60000
s.connect((host, port))
s.send("Hello server!".encode())

with open('received_file', 'wb') as f:
    print('receiving data...')
    while True:
        data = s.recv(1024)
        print('data=%s', (data))
        if not data:
            break
        f.write(data)

print('Successfully received the file')
s.close()
print('connection closed')
```

mytext.txt

```
Hello Client,
This file was sent using Python socket programming.
TCP ensures reliable file transfer.
```
## OUPUT

Serverside


<img width="436" height="82" alt="Screenshot 2026-05-20 140720" src="https://github.com/user-attachments/assets/1099f6ea-5d15-48ba-a833-db25215bbfbd" />


Clientside


<img width="437" height="90" alt="Screenshot 2026-05-20 140732" src="https://github.com/user-attachments/assets/16f23794-d3ab-4d71-841d-a81480cd48cb" />


Received File(received_file)


<img width="527" height="136" alt="image" src="https://github.com/user-attachments/assets/2727b4f7-a16a-4aaf-9c4a-02bcc37af1c5" />


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
