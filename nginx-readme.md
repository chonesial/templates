# Nginx | Installation | Reverse Proxy Configuration

### Contents

- [Installation](#installation)
- [Reverse Proxy set-up](#reverseproxy)


<a id="installation"> Installation method </a>

```
sudo apt update
sudo apt install nginx
```


#### Nginx firewall list 
When the firewall is installed and we need to allow list of modules to authenticate for firewall passing .

```
sudo ufw app list
```

Output
these are the list of module apps used by Nginx. 

```
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```

Now, allow all the modules or as per the preffered work.


```
  sudo ufw allow 'Nginx Full'
```

verify settings by firewall using :

```
sudo ufw status
```

Thus, the Installation is complete . 

### you can checkout the browser on localhost:80 


# Reverse Proxy <a id="reverseproxy"> </a>

Intermediary Components that receives requests and forwards it to relevant endpoint .

for example :- running npm app on port 3001 instead of 3000

for doing that , first go to the site-enable directory 

```
    cd etc/nginx/sites-enabled
```

root@ip-192-168-111-120:/etc/nginx/sites-enabled# ls
default

### we need to edit this "default" file 
```
      vi default
```
here we can change some values 

like changing listening server 

from 

default_server to any domain name or ip server such as your own domain or a 3rd party domain 


```
        server {
        listen 80 default_server;
```

in our case , we will change this to port to 3001 for testing  

```
        server {

        listen 3001 default_server;
```

now add proxy setting on the block to look like this 

```

location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.

        proxy_pass           "http://localhost:3001";


                try_files $uri $uri/ =404;
        }

```
### Save the file 

for checking the file's compatibility and errors type -
```

nginx -t

```
output should look like this 

```

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

```

Restart 

```

systemctl restart nginx

```

#### Now the user visit port 80 will be re-directed to app on 3001 .
