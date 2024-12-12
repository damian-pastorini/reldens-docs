## Demo server setup - Amazon Linux (2024)


### - Update software packages
```
$ sudo yum update -y
```


### - Install and enable nginx (using a reverse proxy)
```
$ sudo yum install ngnix -y

$ systemctl enable nginx

$ systemctl start nginx
```


### - Configure Proxy settings inside Nginx config:
```
$ vi /etc/nginx/nginx.conf
```

In the Nginx config set the following:
```
server {
    listen 80;
    listen [::]:80;
    server_name _;
    root /usr/share/nginx/html;
    # load configuration files for the default server block
    include /etc/nginx/default.d/*.conf;

    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        
    }

    error_page 404 /404.html;
    location = /404.html {
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
    }
}
```


### - Install NVM and validate NodeJS installation

Assume super user role:
```
$ sudo -i
```

Then install NVM:
```
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
. ~/.nvm/nvm.sh

$ nvm install --lts

$ node -e "console.log('Running Node.js ' + process.version)"
```

That should return something like: Running Node.js v20.11.0 (version may vary).


### - Install MySQL client

Run the following commands:
```
$ dnf -y localinstall https://dev.mysql.com/get/mysql80-community-release-el9-4.noarch.rpm

$ dnf -y install mysql mysql-community-client
```

Test database connectivity:
```
$ mysql -u <dbuser> -p -h <database_enpoint>
```

### - Inside MySQL, create database if it was not created previously:
```sql
CREATE DATABASE reldens;
```

### - Install git and clone your game repository

```
$ yum install git -y

$ git clone https://github.com/damian-pastorini/reldens-skeleton.git 

$ cd reldens-skeleton/
```

### Install PM2, project and run

```
$ npm install pm2 -g

$ npm install

$ pm2 start index.js --name "reldens"
```

Give it a shoot on the domain you may have set for your server, the project should be up and running.
