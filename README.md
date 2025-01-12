# Redirects
- whenever we go to /crops, we want to show stuff in 
```
location /fruits{
    root C:\Users\user\Desktop\Self\mysite
}
```
- one way of doing that is just to add a location block, but we've already done that
- whenever we go to /fruits crops we want to redirect to /fruits

```
location /crops {
    return 307 /fruits;
}
```
- but now when we go here, it will also change the url to ```http://localhost:8080/fruits/```, what if we dont want this to happen?
- in that case we will rewrite instead of redirect, for rewrite we do not have to specify in location context, just write in server context

```
rewrite /crops /fruits
```
