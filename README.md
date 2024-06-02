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

## 3) Access instance on MobaXterma SSH Client
    To connect to the instance you created, you will need an SSH client.

    -> Install Mobaxterm SSH client and open it.
    -> Click on Session, then click on SSH.
    -> In the session window dialog box under SSH settings, enter the Remote host IPv4 public address of the virtual computer that you created using AWS EC2.
    -> Enter the username. If you don't know the username, go to the EC2 dashboard, right-click on the EC2 instance you created, and then click on Connect. Further click on the SSH client option to find the username.
    -> In Mobaxterm, click on the Advanced SSH settings, select the radio button for USE PRIVATE KEY, and then browse for the private key (the notepad file that was downloaded).
    -> Finally, click on the OK button.
    Now you are connected to the virtual computer that you created.

## 4)Configuring & installing Apache, Mysql Database and Wordpress
    **Now we need to install Apache web server on the instance**, so type the command
    
