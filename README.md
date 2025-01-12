# Location Context
- Allows us to specify certain endpoints, certain pages we can hit
- then we can serve different types of html elements

- when we hit /fruits directory, we want to serve fruits/index.html file
- we can do that with location context, this will be inside server

- it will append /fruits automatically to ```root C:\Users\user\Desktop\Self\mysite;```
```
http{
    include mime.types;
    server {
        listen 8080;
        root C:\Users\user\Desktop\Self\mysite;

        location /fruits{
            root C:\Users\user\Desktop\Self\mysite;
        }
    }
}

events {

}
```

- lets say we want to go to /carbs, and we want same fruits
```
location /carbs {
    root C:\Users\user\Desktop\Self\mysite;
}
```
- this will present an issue, because it will append \carbs and not \fruits
- instead we have to specify we dont want to append it to end of root, and we want it to be \fruits
- we would use alias here, it will not append

```
location /carbs {
    alias C:\Users\user\Desktop\Self\mysite\fruits
}
```


### try_files
- what if we want to show some other files, by default it will show index.html
- i want to show veges.html
- by default it will look for index.html, however when we specify try_files we can specify bunch of different directories we want tot ry.
```
location /vegetables {
    root C:\Users\user\Desktop\Self\mysite;
    try_files /vegetables/veges.html /index.html =404;
}
```

### Regex
```
location ~* /count/[0-9] {
    root C:\Users\user\Desktop\Self\mysite;
    try_files /index.html =404;
}
```