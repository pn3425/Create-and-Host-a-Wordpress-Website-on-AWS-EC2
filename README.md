# Create and Host a Wordpress Website on AWS EC2
You can set up WordPress effortlessly using AWS Lightsail with just one click, but we'll take the traditional route. We'll create a virtual machine on EC2, install and configure a web server and a database management system, and then install WordPress.

## 1) Create virtual computer using EC2
->Click Launch instance , and then name your instance 
->Choose OS - Ubuntu
->Instance type will be t2.micro(default)
->Create new key pair
   ->Create key pair name
   ->key pair type - RSA
   ->private key file format - .pem
   ->Click on create key pair button
   ->PRIVATE KEY is downloaded as notepad file
->Configure network setting 
   ->Enable both Allow HTTPSs traffic from the internet
   ->Allow HTTP traffic from the internet
->Storage setting will be default
->Finally create on launch instance, this will create a virtual machine 
