## NBA-Players-Online
**Project Description**
This project is the Linux Server Configuration Project. In this project, I have deployed my “NBA Players” application through AWS Lightsail.

### **Basic Information**

1. IP address: 
```
http://35.153.171.25
```
2. SSH port: 2200
3. A complete URL: 
```
http://ec2-35-153-171-25.compute-1.amazonaws.com
```
4. Grader passphrase: grader123

### **Software to Install During the Configuration**

1. apache2
2. mod_wsgi
3. postgreSQL
4. git
5. pip
6. Virtualenv
7. httplib2
8. oauth2client
9. SQLAlchemy
10. SQLAlchemy_utils
11. Flask
12. libpq-dev
13. Psycopg2

### **Check Points**
1. Check Login as “Ubuntu” and Check Port 2200: 
In your local machine in Git Bash, please do: 
```
ssh -i ~/.ssh/LightsailDefaultKey.rsa ubuntu@35.153.171.25 -p 2200
```
2. Check Port 22 Does NOT work:
In your local machine in Git Bash, please do: 
```
ssh -i ~/.ssh/LightsailDefaultKey.rsa ubuntu@35.153.171.25 -p 22
```
3. Check Login as “root” Does NOT work: 
In your local machine in Git Bash, please do: 
```
ssh -i ~/.ssh/LightsailDefaultKey.rsa root@35.153.171.25 -p 22
```
You can also check the sshd_config file: 
```
cd /etc/ssh
sudo nano sshd_config
PermitRootLogin is set to “no”
```
4. Check Login as “Grader”:
In your local machine in Git Bash, please do:
ssh -i ~/.ssh/grader_key -p 2200 grader@35.153.171.25
grader_key is the key you have moved in ~/.ssh folder in the preparation step.
Then type in grader passphrase: grader123

5. Check Grader has Sudo Access:
After you login as “grader”, please do: 
sudo -l

6. Check All the Packages Have Been Updated:
After you login as “grader”, please do: 
sudo apt-get update
sudo apt-get upgrade

7. Check Uncomplicated Firewall (UFW): 
After you login as “grader”, please do: 
sudo ufw status
Type in grader password: grader123

10. Check Local Timezone to UTC: 
After you login as “grader”, please do:
date

11. Check the Virtual Host settings (and Port 80 used for web server)
After you login in as “grader”, please do: 
cd /etc/apache2/sites-available
Then you can open the catalog.conf:
sudo nano catalog.conf 

12. Check WSGI settings
After login as “grader”, please do:
cd /var/www/catalog
Then you can open the catalog.wsgi setting:
sudo nano catalog.wsgi

13. Check Apache2 status: 
After you login as “grader”, please do: 
sudo service apache2 status

14. Check PostgresSQL data setup:
After you login, please switch user: 
sudo  su – postgres
Then open PostgreSQL by typing: psql
Listing the existing roles by typing: \du
Exit psql: \q
Switch back to the grader user: exit

15. Check Database can store data: 
Switch user to catalog:
Sudo su – catalog
Then type in: psql
Listing all the tables: \d
Check the data in each table: 
Select * from category; 
Select * from category_item;
Exit psql: \q
Exit catalog: exit

16. Check data can be saved to database:
After login, please temporarily stop apache2:
sudo service apache2 stop
Then please change directory:
cd /var/www/catalog/catalog
Then go to virtual machine:
. venv/bin/activate
Then book data: 
python database_setup.py
python players.py
Here you can see data is saved in database
Finally restart the apache2: 
sudo service apache2 restart


### **Special note:**
Google authorization works only with the top-level domains. http://35.153.171.25
and http://ec2-35-153-171-25.compute-1.amazonaws.com are not top-level domains. So I cannot let google login works in my user interface. 
I followed the instruction from this threads in the Udacity discussion forum: 
https://knowledge.udacity.com/questions/2893
