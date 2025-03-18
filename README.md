# LAMP_stacks
Setup LAMP  Stacks on an EC2 instance and deploy Wordpress
Launch a EC2 instance  and deploy WordPress using Ubuntu OS
Connect to Your EC2 Instance via SSH
ssh -i your-key.pem ubuntu@your-elastic-ip
Install Apache Web Server
sudo apt update -y
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
Check if Apache is running:
sudo systemctl status apache2
Install MySQL (MariaDB)
sudo apt install mariadb-server -y
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo mysql_secure_installation
Follow the prompts:
Set root password → Yes
Remove anonymous users → Yes
Disallow root login remotely → Yes
Remove test database → Yes
Reload privilege tables → Yes
Install PHP
sudo apt install php libapache2-mod-php php-mysql -y
sudo systemctl restart apache2
php -v (check php version)
Download and Configure WordPress
cd /var/www/html
sudo rm -rf *
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
Set proper permissions:
sudo chown -R ubuntu:ubuntu /var/www/html
sudo chmod -R 755 /var/www/html
Create a WordPress Database
sudo mysql -u root -p
CREATE DATABASE wordpress;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'yourpassword';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wp_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
Configure WordPress
sudo mv wp-config-sample.php wp-config.php
sudo nano wp-config.php
Update Database Details
define('DB_NAME', 'wordpress');
define('DB_USER', 'wp_user');
define('DB_PASSWORD', 'yourpassword');
define('DB_HOST', 'localhost');
sudo systemctl restart apache2 
Now, open your browser an
http://localhost or ip (example)
