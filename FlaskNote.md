Nginx is our gateway, which acts as the gateway between our application and external user, which is going to accept incoming request and then decides what to do with those request. we will have to configure Nginx so that those request goes straight into our application.
Nginx also communicate with uswgi to enable multithreaded operation for our flask app, it can also allows u run multiple flask apps simultaneously in your server while redirceting incoming request to differents apps depending on some parameters.