DJANGO APACHE DOCKER 
========================

This repo includes setup for hosting Django with Apache webserver over docker. When running 
django in production, `staticfiles` either need to be serve via external webserver or third party libraries like `whitenoise`.

- [httpd.conf](httpd/httpd.conf) file contains all the settings required to pass proxy to hosted django server via gunicorn.
- [Dockerfile.django](Dockerfile.django) file contains image instructions for running django
- [Dockerfile.httpd](httpd/Dockerfile.httpd) file contains image instructions for httpd.

> We are using **Reverse Proxy** to gunicorn server with Apache.

## Running Project 

```bash
docker-compose up --build
```

Above command will bootstrap `Django` server and `Apache` server together and 
can be accessed by `localhost`.

We are serving _static_ files using `Apache` where we are denying forward
proxy for `/static` and rather serving files through a common mapped volume.

```xml
    Alias /static "/usr/local/apache2/static"
    <Directory /usr/local/apache2/static>
        Require all granted
    </Directory>
```

> You can refer [httpd.conf](httpd/httpd.conf) file for further forward proxy reference.

**Author** : @satyamsoni2211