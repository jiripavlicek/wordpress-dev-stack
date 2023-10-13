# Wordpress dev stack

## Run for the first time

1. check if ports 80, 3306, 8080, 1025 and 8025 are available
    1. check if anything listens required ports with `netstat -l | grep 'http\|mysql\|http-alt\|1025\|8025'`
    2. if yes, then stop it with something like `sudo service nginx stop`, `sudo service apache2 stop`, `docker stop XXX` or so on...
2. `cd ~`
3. `git clone git@github.com:jiripavlicek/wordpress-dev-stack.git`
4. `cd ~/wordpress-dev-stack`
5. `docker-compose up`
6. navigate to http://localhost/
7. pass Wordpress install process
8. recommended step - install & configure 'POST SMTP Mailer' plugin
   1. install & activate plugin
   2. Account tab
   2. configure plugin with 'Show All Settings'
   3. Type: SMTP
   4. MailerType: PostSMTP
   5. Outgoing Mail Server Hostname: mailhog
   6. Outgoing Mail Server Port: 1025
   7. Envelope-From Email Address: (use your e-mail here)
   8. Security: None
   9. Authentication: None
   10. Use Fallback?: No
   11. Message tab
   11. Email Address: (use your e-mail here)
   12. Save Changes
   13. Send a Test Email
   14. yould see it in Mailhog on http://localhost:8025/ 
8. when finished - press Ctrl-C to exit the dev stack (on the console which you did used to start the dev stack)

## How to access MySQL

1. navigate to http://localhost:8080/?server=mysql&username=exampleuser&db=exampledb (see credentials in mysql part of docker-compose.yml)

## How to see e-mails sent

1. install & configure 'POST SMTP Mailer' plugin 
2. navigate to http://localhost:8025

## How to access site files

### ssh console

1. there is ~/wordpress-dev-stack/wordpress folder which contains all Wordpress site's files

## Remove the dev stack

1. `docker rm wordpress-dev-stack_wordpress_1 wordpress-dev-stack_mysql_1 wordpress-dev-stack_adminer_1 wordpress-dev-stack_mailhog_1`
2. use `docker images` to get container IDS
3. `docker rmi XXX` (where XXX are container's IDS)

## Resources

1. https://hub.docker.com/_/wordpress
2. https://wordpress.com/
3. https://wordpress.org/plugins/post-smtp/