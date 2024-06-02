# Create and Host a Wordpress Website on AWS EC2
You can set up WordPress effortlessly using AWS Lightsail with just one click, but we'll take the traditional route. We'll create a virtual machine on EC2, install and configure a web server and a database management system, and then install WordPress.

## 1) Create virtual computer using EC2
    -> Click Launch instance, and then name your instance.
    -> Choose OS - Ubuntu.
    -> Instance type will be t2.micro (default).
    -> Create new key pair:
        -> Create key pair name.
        -> Key pair type - RSA.
        -> Private key file format - .pem.
        -> Click on Create key pair button.
        -> PRIVATE KEY is downloaded as a notepad file.
    -> Configure network settings:
        -> Enable both Allow HTTPS traffic from the internet.
        -> Enable Allow HTTP traffic from the internet.
    -> Storage setting will be default.
    -> Finally, click on Launch instance, this will create a virtual machine.

## 2) Assigning Elastic IP
    -> Before connecting, assign an elastic IP address to the instance (since rebooting the instance will change the public IPv4 address, we want the IP address to be static).
    -> Click on EC2 dashboard, then click on Elastic IP addresses.
    -> Click on Allocate IP address to create an elastic IP.
    -> Assign the elastic IP to the virtual computer that was created:
        -> Select the IP address that you created.
        -> Click on Actions, then click on Associate Elastic IP address.
        -> In the dialog box, choose your instance, and click on the Associate button to assign it to the virtual computer.

## 3) Access instance on MobaXterm SSH Client
    To connect to the instance you created, you will need an SSH client.

    -> Install Mobaxterm SSH client and open it.
    -> Click on Session, then click on SSH.
    -> In the session window dialog box under SSH settings, enter the Remote host IPv4 public address of the virtual computer that you created using AWS EC2.
    -> Enter the username. If you don't know the username, go to the EC2 dashboard, right-click on the EC2 instance you created, and then click on Connect. Further click on the SSH client option to find the username.
    -> In Mobaxterm, click on the Advanced SSH settings, select the radio button for USE PRIVATE KEY, and then browse for the private key (the notepad file that was downloaded).
    -> Finally, click on the OK button.
    Now you are connected to the virtual computer that you created.

## 4)Configuring & installing Apache, Mysql Database and Wordpress
    4.1) Now we need to install Apache web server on the instance, 
    so type the command in the mobaxterma terminal of your instance 
    command - sudo apt install apache
    To cross check whether the apache server is working go on tab in chrome or any web browser
    and type http://public ipv4 address, and check if you are able to see Apache2 Default page.

    4.2) Now we will have to install PHP runtime on the instance, since wordpess is built on PHP
    and also mysql connecter for PHp is installed
    command - sudo apt install php libapache2-mod-php php-mysql
    
    4.3) Install MySQL server for the database
    command - sudo apt install mysql-server
    A small configuration -> we need to change the MySQL authentication plugin to MySQL native password, so that we can login in the MySQL server by a normal password that is what is required to install wordpress

    First login to the sql prompt
    command - sudo MySQL -u root

    To change authentication plugin 
    command - ALTER USER 'root'@localhost IDENTIFIED with mysql_native_password BY 'enterpass';

    So other than root we need to create a separate user to use the wordpress
    command - CREATE USER 'wp_user'@localhost IDENTIFIED BY 'enterpass';
    
    4.4) NOW we need to create a separate database to use with wordpress
    command - CREATE DATABASE wp;

    Assign all the priviligies to the database and to the user that you created.
    command - GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;
    Hence SQL SERVER IS ALL CONFIGURED 
    Hold ctrl d to come out of the sql server

    4.5) Now we can install WordPress
       -> Navigate to the temp directory:
        Command: cd /tmp
    -> Open a web browser, go to wordpress.org, and click on Get WordPress.
    -> Copy the download link of the tar.gz file.
    -> Return to the terminal of Mobaxterm and run:
        Command: wget [paste the link] to download WordPress.
    -> Type ls and unzip the file by writing:
        Command: tar -xvf latest.tar.gz (Name of the archive)
    -> Type ls again.
    -> A WordPress folder will be displayed. Move this folder to the document root of Apache:
        Command: sudo mv wordpress/ /var/www/html/
    -> Navigate to the document root:
        Command: cd /var/www/html/
        You will find the WordPress folder there.

    Now in the browser, type your ip address of the instance/wordpress
        Now the WordPress installation screen will appear.
    -> Enter the following information:
        Database name: wp
        Username: wp_user
        Password: Testpassword@123
        Database host: localhost
        Table prefix: wp_
        Click on Submit.
    -> If you get an error: "Unable to write to wp-config.php file," follow these steps:
        Copy the code displayed.
        Go to the terminal and navigate to the WordPress directory:
            Command: cd /var/www/html/wordpress/
        Create a new file called wp-config.php:
            Command: nano wp-config.php
        Paste the copied code and save it. Then return to the browser and click on Run the installation.
    -> Enter the required details and click on Install WordPress.
       You will be directed to the login page for WordPress (Admin side).
       To see your website, enter your IP address followed by /wordpress in the browser.

    Now we just want to enter the ip and get the website instead of writing ip add/wordpress.
        -> Come back to the terminal:
        Command: cd /etc/apache2/sites-available/
    -> Edit the configuration file 000-default.conf:
        Open it with a sudo editor by typing:
            Command: sudo nano 000-default.conf
        Change the DocumentRoot to /var/www/html/wordpress
    -> Restart Apache:
        Command: sudo systemctl restart apache2
    Now if you refresh the earlier browser page, you will get the WordPress page.
    
    
