# nginx
- lets say we go to a website(for example airbnb.ca), we will see our website is served a bunch of content, we have many images, and text everywhere.
- how did our browser get all of this content?
- we disect this by inspecting, and looking at network tab, as soon as we refresh we get a bunch of network requests
- these were requests made by browser to a particular server to get content
- if we go in headers, and scroll down a little bit we see the server is nginx, so nginx was serving webcontent to the browser, thats why nginx is very typically known as a webserver, but thats not accurate.

## What we think happens
- lets say we are on our computer and we go to airbnc.ca, typically what we would think is we are making a request over the internet to a server that airbnb is hosting on aws or something.
- once we make a request it will process our request, and send us a response for that webcontent, whether its an image or webcontent whatever, uptil now there is no nginx, this is not how webcontent is served

## What really happens
- when we go to airbnb.ca, instead of making request directly to airbnb server, we make request to nginx server, and then nginx server makes request to airbnb server, the airbnb server responds to nginx server and nginx sends back the content to the browser. This is actually known as a reverse proxy.

### Why do we need this middleman here?
**UseCase 1**
- why cant we make a request directly to the airbnb server? this wouldnt be a bad idea, if we werent getting a lot of traffic to our application.
- when we get a lot of traffic, what we need to do is we need to increase the number of servers we have inside our aws account
- if airbnb has millions of request, then the server will get so many requests it will reach a bottleneck and latency will be extremely low. so we need to increase the number of servers.
- now we have a problem, how to distribute our network traffic? this is where nginx comes, the client only sends requests to nginx and nginx is responsible for forwarding our requests to available server. this is role of loadbalancer. this is very good for scaling your application.


**Usecase 2(Encryption)**
When you have multiple servers behind a load balancer or reverse proxy, each server would need to handle SSL/TLS encryption and decryption if the HTTPS protocol is used. This would mean:
Each server must have its own SSL certificate.
Each server must perform encryption and decryption for incoming and outgoing traffic.

- when we visit website we see it is either http, or https
- if it is https, that means server is encrypting and decrypting data that is being sent and returned
- this is a problem when we have multiple servers, if we have multiple servers we would have to encrypt every single one
- solution: instead of having this encryption and decryption in every single server, we can just have it in nginx

Client → Nginx (HTTPS): The client connects to Nginx using HTTPS. Nginx decrypts the encrypted data (SSL/TLS termination).

Nginx → Backend Server (HTTP): After decrypting the request, Nginx forwards the unencrypted request to the backend server over HTTP.

Backend Server → Nginx (HTTP): The backend server responds to Nginx in an unencrypted format.

Nginx → Client (HTTPS): Nginx encrypts the response data again using HTTPS and sends it to the client.


# NGINX Terminology:
- in nginx.conf we will see there are two distinct things that exist in it.
1) Some thing like key value pair
```
worker_processes 1
include mime.types
```
- we have a bunch of those things

2) event block(within it we have key value pair)

### Directives
- these key value pairs are known as directives


### Context
- blocks of code with curly braces
- within context we can have directives for specific context


# Working with nginx
### Starting nginx:
```nginx```
- and now if we go to browser, we see welcome page of nginx
- if we go to network, we can see request and server is nginx
