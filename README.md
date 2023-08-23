# NodeJS
Appilcation tester for deploy to EC2 Instances

# Command to deploy EC2 Instances
user data:
#cloud-config
package_update: true
package_upgrade: true
runcmd:
- yum install - y gcc-c++ make
- curl -sL https://rpm.nodesource.com/setup_14.x | sudo -E bash -
- yum install -y nodejs
- yum install -y git
- git clone https://github.com/sam-meech-ward-bcit/lotr
- cd lotr
- npm i
- node server.js
_____________________________________________
config your database using this code :
MYSQL_HOST="YOUR_HOST_OR_IP" MYSQL_USER="YOUR_USER" MYSQL_PASSWORD="YOUR_PASSWORD" MYSQL_DATABASE="YOUR_NAME_DATABASE" PORT="6060" node server.js
_____________________________________________
- sudo vim /etc/systemd/system/lotr.service = Isikan kode ini sesuai dgn LKS
_____________________________________________
[Unit]
Description=YourAppName
After=multi-user.target

[Service]
ExecStart=/usr/bin/node /home/ec2-user/your_app_dir/server.js
Restart=always
RestartSec=10
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=YourAppName
User=ec2-user
EnvironmentFile=/home/ec2-user/your_app_dir/app.env

[Install]
WantedBy=multi-user.target
_____________________________________________
- vim app.env = isikan data dari MYSQL_HOST MYSQL_USER MYSQL_PASSWORD MYSQL_DATABASE PORT="6060"
_____________________________________________
MYSQL_HOST="nodejsdb.cde3yjwwxzuh.ap-southeast-1.rds.amazonaws.com" 
MYSQL_USER="maulamuhammad" 
MYSQL_PASSWORD="maulamuhammad" 
MYSQL_DATABASE="lotr" 
_____________________________________________
- sudo systemctl start lotr.service
- sudo systemctl status lotr.service
_____________________________________________

