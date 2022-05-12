## LOAD BALANCER SOLUTION WITH APACHE

`sudo apt update`

`sudo apt install apache2 -y`

`sudo apt-get install libxml2-dev`

`sudo a2enmod rewrite`

`sudo a2enmod proxy`
`sudo a2enmod proxy_balancer`
`sudo a2enmod proxy_http`
`sudo a2enmod headers`
`sudo a2enmod lbmethod_bytraffic`

`sudo systemctl restart apache2`

![Apache](./images/Apache%20status%20running..jpg)

`sudo vi /etc/apache2/sites-available/000-default.conf`

`<Proxy "balancer://mycluster">
               BalancerMember http://<WebServer1-Private-IP-Address>:80 loadfactor=5 timeout=1
               BalancerMember http://<WebServer2-Private-IP-Address>:80 loadfactor=5 timeout=1
               ProxySet lbmethod=bytraffic
               # ProxySet lbmethod=byrequests
        </Proxy>

        ProxyPreserveHost On
        ProxyPass / balancer://mycluster/
        ProxyPassReverse / balancer://mycluster/`

`sudo systemctl restart apache2`

`http://<Load-Balancer-Public-IP-Address-or-Public-DNS-Name>/index.php`

![PAGE.PNG](./images/Load%20IP%20address%20Loading%20page.jpg)

![Pro.PNG](./images/Propitix%20tooling%20through%20load%20balancer%20IP%20address.jpg)


** WEB SERVER 1**

`sudo tail -f /var/log/httpd/access_log`

** WEB SERVER 2**

`sudo tail -f /var/log/httpd/access_log`

Optional steps were followed for knowledge purposes 

