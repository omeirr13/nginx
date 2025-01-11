# Mimetypes
- lets say we are sick of our plain old website, and we crave some styles.
- if we make a styles.css file, and go back and see styles wont be applied, why is that? are they not being served?

- if we go to network tab, styles.css is actually served to the webpage, why do we not see it?

### Reason:
- if we click on styles.css request, its Content-Type is text/plain, whereas it should text/css

### Solution:
- inside http context, we can define all of the types
- anything that is text/css will have css extension
- anything that is text/html will have html extension
```
http{
    types {
        text/css        css;
        text/html       html;
    }
    server {
        listen 8080;
        root C:\Users\user\Desktop\Self\mysite;
    }
}

events {
    
}
```

- there are so many different files outthere, we would have to catch all files manually and add them in types here, luckily we dont have to do here, because nginx comes with default mimetypes in mime.types
- we can copy paste, but better is including it.

```
http{
    types {
       include mime.types
    }
    server {
        listen 8080;
        root C:\Users\user\Desktop\Self\mysite;
    }
}

events {
    
}
```