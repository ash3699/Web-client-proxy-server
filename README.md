### PORT numbers:

* Simple Web Server: 12001
* Proxy Server: 12002

### How to Run the Client.py
---------------------------

#### Connecting through normal web server:

1. Enter this in command line: `python3 Client.py {hostname/IP of website} {Port number of the website} {Path}`
2. Now Client will send a GET request for base html file.
3. After getting the html file the client will send a GET request one by one for all the objects(except links) in the html file.
4. Now for each object the client will first check the status code in the response from the server, now if the status code = 200, then we save the object but if status is something else then the client will handle the status code and print the respective comment for status code.
5. The client saves the downloaded objects in download folder.

#### Connecting through proxy:

1. First run proxy program in some terminal by executing this command: `python3 Proxy.py`
2. Now run the Client on other terminal by executing this in command line: `python3 Client.py {hostname/IP of website} {Port number of the website} {IP of Proxy server} {Port of Proxy server} {Path}`
3. Now Client will send a GET request for base html file through proxy server.
4. After getting the html file the client will send a GET request one by one for all the objects(except links) in the html file by establishing a connection through proxy each time.
5. Now for each object the client will first check the status code in the response from the server, now if the status code = 200, then we save the object but if status is something else then the client will handle the status code and print the respective comment for status code.
6. The client saves the downloaded objects in download folder.

### How to Run the Proxy.py
---------------------------

1. First run proxy program in some terminal by executing this command: `python3 Proxy.py`
2. Now the proxy will create a socket and start listening on PORT 12002
3. Now whenever a client connects to proxy, the proxy creates a new thread for each client connection.
4. When proxy recieves a request from client, it parses the request and gets hostname and port number of the webserver hosting the requeired file and also the path to that file.
5. Now proxy creates a new socket to establish a connection between the proxy and webserver using the hostname and port number it parsed earlier. Proxy sends request to webserver through this connection.
6. Whenever the proxy gets back a response from webserver, it parses the response and modifies the header by adding a new header line containing the IP address of proxy.
7. Proxy now sends this new modified response to the client.
8. When proxy recieves no further response from webserver, it closes the connection with both webserver and client.

### How to Run the Server.py
---------------------------

1. Enter this in command line: `python3 Server.py`
2. Now the server will start listening on PORT 12001
3. Now whenever a client connects to the webserver the webserver makes a new thread for each client and serve each client in a new Thread.
4. Now if the file requested by the client is present the server will send the file to the client with headers(including the 200 OK response)
5. But if the file is not present then client will send a "404 NOT FOUND" response to the client.
6. After this the connection to the server from the client is closed.

### How to Run the ExtendedClient.py
-------------------------------

1. Enter this in command line: `python3 ExtendedClient.py {hostname/IP of website} {Port number of the website} {Path}`
2. Now Client will send a GET request for base html file.
3. After getting the html file the client will send a GET request one by one for all the objects(except links) in the html file. The thing to note here is that parallel TCP connection will be used for getting the objects.
4. Now for each object the client will first check the status code in the response from the server, now if the status code = 200, then we save the object but if status is something else then the client will handle the status code and print the respective comment for status code.
5. The client saves the downloaded objects in Parallel_download folder.
