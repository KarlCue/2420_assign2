http://24.199.71.23/

# Creating Digital Ocean Infrastrucure
## Creating VPC

1. Go to Networking (could be seen on the manage tab left corner of the screen)
2. Click VPC (options under networking)
3. Click Create VPC Network
4. Set up your desired configurations
5. Once you're all set up click Create VPC Network at the bottom of the screen

## Creating Droplet
1. Start a new Project
2. Click Get Started With a New Project
3. Make sure to add tags
4. Create Droplet

## Creating a Load Balancer
1. Go to Networking 
2. Click Load Balancer
3. Create Load Balancer
4. Click the region where your droplets are 
5. Click the VPC you just created
6. Add your tags
7. Create Load Balancer

## Creating Firewall
1. Go to Networking
2. Click Firewall
3. Keep SSH settings in Inbound Rules 
4. Add http and replaces sources to you load balancer in Inbound Rule
5. Specify your tag

## Creating a regular user for your droplet
1. Open up your terminal and enter ``` ssh -i ~/.ssh/server-key root@(server ip address) ```
2. ```adduser <username>```
![Add_user](https://github.com/KarlCue/2420_assign2/blob/main/images/addinguser.jpg)
3. Give sudo privilages with ```sudo usermod -aG sudo newuser ```

## Install Caddy
>sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
>curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
>curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
>sudo apt update
>sudo apt install caddy

##Create an HTML file
1. Create a folder with ```mkdir html```
2. cd into your folder
3. Create a File with ```vim index.html```
```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
        <h1> Server 1 </h1>
</body>
</html>
```
4. Copy your file to /var/www ```sudo cp -r /html/index.html /var/www```

##Create an SRC file
1. Create a folder with ```mkdir src```
2. cd into your folder
3. Create a JS file with ```vim index.js```

![jsfile](https://github.com/KarlCue/2420_assign2/blob/main/images/indexjs.jpg)

4. Copy your file to /var/www ```sudo cp -r /src/index.js /var/www```

## Install nodejs and fastify
### Node
1. ```curl -sL https://deb.nodesource.com/setup_lts.x | sudo -E bash - ```
2. ```sudo apt-get install -y nodejs```
### Fastify
1. cd to your src folder
2. ```npm init``` and ```npm i fastify``` inside the folder

## Caddy File
1. Edit your caddy file ```vim /etc/caddy/Caddyfile```
2. Remove and replace the content 
```
http://<load balancer's IP address> {

        root * /var/www/<load balancer's IP address'/html

        file_server

        reverse_proxy /api localhost:5050

}
```

### Caddy Service
1. Create your caddy service with ```vim /etc/systemd/system/caddy.service```

![jsfile](https://github.com/KarlCue/2420_assign2/blob/main/images/caddyservice.jpg)

3. ```sudo systemctl daemon-reload``` re runs all generators
4. ```sudo systemctl start caddy.service``` to start the caddy service
5. ```sudo chown caddy:caddy /var/www```

### Install node and npm with Volta
```curl https://get.volta.sh | bash
source ~/.bashrc
volta install node```

### Node Service
1. Create your hello_web.service with ```vim /etc/systemd/system/hello_web.service```

```
[Unit]
Description=Runs the node application for load balancer
After=network-online.target
Wants=network-online.target

[Service]
ExecStart=/home/karl/.volta/bin/node /home/karl/2420assign2/src/index.js
User=karl
Group=root
Restart=always
RestartSec=10
TimeoutStopSec=90
SyslogIdentifier=hello_web

[Install]
WantedBy=multi-user.target
```
3. ```sudo systemctl enable caddy.service``
4. ```sudo systemctl start caddy.service``


