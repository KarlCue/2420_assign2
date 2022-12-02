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
4. 
