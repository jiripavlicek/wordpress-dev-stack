# Wordpress dev stack

## Check if port 80 is available

1. check if anything listens on your port 80 with `netstat -l | grep http`
2. if yes, then stop it with something like `sudo service nginx stop`, `sudo service apache2 stop` or so on...

## Run for the first time

1. `cd ~/wordpress`
2. `docker-compose up`
3. navigate to http://localhost/
4. pass Wordpress install process
5. install Woocommerce
    1. http://localhost/wp-admin/plugins.php
    2. click ‘Add New’
    3. write down ‘WooCommerce’ top right in the search field
    4. click ‘Install Now’
    5. left menu click ‘Installed Plugins’
    6. Activate WooCommerce plugin
    7. Set up my store

## MySQL access

1. navigate to http://localhost:8080/?server=mysql&username=exampleuser&db=exampledb (see credentials in mysql part of docker-compose.yml)

## access site files

### ssh console

1. open new console
2. `docker exec -it wordpress_wordpress_1 /bin/bash`

### copy files

1. `mkdir ~/test`
2. `docker cp wordpress_wordpress_1:/var/www/html/ ~/test`

### ssh (allows map folder to access it instantly)

1. open new console
2. `docker exec -it wordpress_wordpress_1 /bin/bash`
3. `apt update`
4. `apt install openssh-server net-tools`
5. edit /etc/ssh/sshd_config
    1. change 'PermitRootLogin prohibit-password' to 'PermitRootLogin yes'
    2. change 'PasswordAuthentication no' to 'PasswordAuthentication yes'
6. `/etc/init.d/ssh start`
7. set user password with `passwd`
8. use `ifconfig` to get IP address
9. try to connect from your machine with `ssh root@172.20.0.4` (replace 172.20.0.4 with IP from previous step)
10. press Ctrl-C to exit

## Remove

1. `docker rm wordpress_wordpress_1 wordpress_mysql_1 wordpress_adminer_1`
2. use `docker images` to get container IDS
3. `docker rmi XXX` (where XXX are container's IDS)

## TODO

1. install smb into docker container to access site files from the network drive over smb share

## Resources

1. https://hub.docker.com/_/wordpress
2. https://woocommerce.com/document/installing-uninstalling-woocommerce/
