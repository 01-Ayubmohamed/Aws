#!/bin/bash 
yum isntall -y httpd
systemctl start httpd
systemctl enable httpd  
echo "<h1>Hello Ayub this in instance EC2 A</h1>" > /var/www/html/index.html

#!/bin/bash Application-Load-Balancer/userdata
yum install -y httpd    
systemctl start httpd
systemctl enable httpd  
echo "<h1>Hello Ayub, this is instance EC2 B</h1>" > /var/www/html/index.html   

#!/bin/bash 
yum install -y httpd    
systemctl start httpd
systemctl enable httpd  
echo "<h1>Hello Ayub, this is Auto Scaling instance </h1>" > /var/www/html/index.html
