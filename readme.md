# Wordpress dev stack

## Run for the first time

1. check if port 80 is available
    1. check if anything listens on your port 80 with `netstat -l | grep http`
    2. if yes, then stop it with something like `sudo service nginx stop`, `sudo service apache2 stop` or so on...
2. `cd ~`
3. `git clone git@github.com:jiripavlicek/wordpress-dev-stack.git`
4. `cd wordpress-dev-stack`
5. `docker-compose up`
6. navigate to http://localhost/
7. pass Wordpress install process
8. when finished - press Ctrl-C to exit the dev stack (on the console which you did used to start the dev stack)

## How to access MySQL

1. navigate to http://localhost:8080/?server=mysql&username=exampleuser&db=exampledb (see credentials in mysql part of docker-compose.yml)

## How to access site files

### ssh console

1. open new console
2. `docker exec -it wordpress-dev-stack_wordpress_1 /bin/bash`

### copy files

1. `mkdir ~/wordpress-folder-mirror`
2. `docker cp wordpress-dev-stack_wordpress_1:/var/www/html/ ~/wordpress-folder-mirror`

### ssh (allows map folder to access it instantly)

1. open new console
2. `docker exec -it wordpress-dev-stack_wordpress_1 /bin/bash`
3. `apt update`
4. `apt install openssh-server net-tools`
5. edit /etc/ssh/sshd_config
    1. change 'PermitRootLogin prohibit-password' to 'PermitRootLogin yes'
    2. change 'PasswordAuthentication no' to 'PasswordAuthentication yes'
6. run ssh daemon with `/etc/init.d/ssh start`
7. set user password with `passwd` command
8. use `ifconfig` to get IP address of this docker container
9. try to connect from your machine with `ssh root@X.X.X.X` (replace X.X.X.X with IP found in the previous step)

## Remove the dev stack

1. `docker rm wordpress-dev-stack_wordpress_1 wordpress-dev-stack_mysql_1 wordpress-dev-stack_adminer_1`
2. use `docker images` to get container IDS
3. `docker rmi XXX` (where XXX are container's IDS)

## TODO

1. an improvement idea - install smb into docker container to access site files from the network drive over smb share

## Resources

1. https://hub.docker.com/_/wordpress
2. https://wordpress.com/

