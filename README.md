# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
### Client
```

import socket
s = socket.socket()
s.connect(("localhost",8081))
ch = input("1.Download 2.Upload : ")
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())
    data = s.recv(4096)
    print(data.decode())
else:
    msg = input("Enter data to upload: ")
    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())
    data = s.recv(1024)
    print(data.decode())
s.close()
```

### Server
```

import socket
s = socket.socket()
s.bind(("localhost",8081))
s.listen(1)
print("Server running...")
while True:
    c,addr = s.accept()
    request = c.recv(1024).decode()
    print("Request received")
    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()
        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())
    elif "POST" in request:
        data = request.split("\n\n")[1]
        
        f = open("upload.txt","w")
        f.write(data)
        f.close()
        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())
    c.close()
```

## OUTPUT
##DOWNLOAD:

<img width="759" height="175" alt="ex 10a(i)" src="https://github.com/user-attachments/assets/05e3dc59-f3cb-48cd-87b1-efca0029b183" />

<img width="765" height="672" alt="ex 10a(ii)" src="https://github.com/user-attachments/assets/e481c523-9bc0-4cf8-8b78-6cf8127be8e4" />

##UPLOAD:

<img width="887" height="249" alt="Screenshot 2026-09-05 142033" src="https://github.com/user-attachments/assets/4df818ef-9a37-4a5e-99a9-e8c7b8329a34" />

<img width="883" height="330" alt="Screenshot 2026-09-05 142023" src="https://github.com/user-attachments/assets/eea2e781-add4-47cb-9fea-a14f11117428" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
