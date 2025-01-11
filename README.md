# Serving static html

- make a new directory mysite having file index.html

- we somehow have to configure nginx to serve this index.html file, whenever we go to localhost:8080
- because we are dealing with http responses we need
1) http context
2) event context(which we wont use, just need to define for nginx configuration to work)


- inside http define another context server, and inside server we will have a bunch of directives that will configure nginx server.
- listen 8080
- root (this directive will be a file path that will contain a bunch of different files that we want to serve, when we go to this port right over here)
thats pretty much all we have to do to serve static html
```
http{
    server {
        listen 8080;
        root C:\Users\user\Desktop\Self\mysite;
    }
}
```

- now after this we will see our changes are not reflecting, that is because we have to reload nginx, have to go to nginx directory and run this command:
```
nginx -s reload 
```