# Create and Host a Wordpress Website on AWS EC2
You can set up WordPress effortlessly using AWS Lightsail with just one click, but we'll take the traditional route. We'll create a virtual machine on EC2, install and configure a web server and a database management system, and then install WordPress.

## 1) Create virtual computer using EC2
    -> Click Launch instance, and then name your instance.
    Choose OS - Ubuntu.
    Instance type will be t2.micro (default).
    Create new key pair:
        Create key pair name.
        Key pair type - RSA.
        Private key file format - .pem.
        Click on Create key pair button.
        PRIVATE KEY is downloaded as a notepad file.
    Configure network settings:
        Enable both Allow HTTPS traffic from the internet.
        Enable Allow HTTP traffic from the internet.
    Storage setting will be default.
    Finally, click on Launch instance, this will create a virtual machine.
