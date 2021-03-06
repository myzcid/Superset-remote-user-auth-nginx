# Apache Superset remote user authentication

This code is easiest way to configure AUTH_REMOTE_USER on Superset and Flask_AppBuilder framework, enables automatic login on superset.

__ToDo__: Integrate SAML python library to manage token.

We suposse that you have Apache superset running as well. Let's do it

## AUTH_REMOTE_USER Login
There are bit steps to do

* Define middleware class, this will capture environment var 
* Update global ADDITIONAL_MIDDLEWARE
* Define Security Manager (extends SupersetSecurityManager)
* New Custom View class extends AuthRemoteUserView
* Change AUTH_USER_REGISTRATION to False

## Postman tests

Put on headers section your `key` and `value`. Of course user should be on Superset's database

## Ngnix config

Edit your serversite configuration file and add
```bash
server {
        ...
        location / {
            proxy_pass http://localhost:8000/;
            proxy_set_header HTTP_PROXY_REMOTE_USER $1;
        }
```
Where 8000 port is Gunicorn or Superset Debug mode listen. Choose your own bind port.


Links:

[Flask_AppBuilder](https://flask-appbuilder.readthedocs.io/en/latest/security.html#your-custom-security)

[Werkzeug project](http://werkzeug.pocoo.org/docs/0.14/wrappers/)

[Sairamkrish on Medium](https://medium.com/@sairamkrish/apache-superset-custom-authentication-and-integrate-with-other-micro-services-8217956273c1)

[Yamyamyuo on GitHub](https://github.com/yamyamyuo/superset-development)

[Mistercrunch on GitHub](https://gist.github.com/mistercrunch/6d31af4a11c47edcedc1ba6ceb5f5fab#file-supersetlogin-py)

