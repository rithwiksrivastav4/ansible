### Deployment of a Simple Website
* We need a linux server
* This can be an azure vm or aws ec2 instance
 * We need to install webserver software
         * apache
         * nginx
* We need to copy the website Refer Here to particular
```bash
    /var/www/html
```    
* Manual Steps
```bash
 Install nginx
sudo apt update
sudo apt install nginx -y
```
* Now webserver should be installed
```bash
sudo systemctl status nginx
```

* Now we can access the webserver over http => http://publicip
* Now lets download the website into /tmp
```bash
cd /tmp
wget https://www.free-css.com/assets/files/free-css-templates/download/page295/antique-cafe.zip
```

* Install unzip
```bash
sudo apt install unzip -y
```
* Now unzip the antique-cafe
```bash
unzip antique-cafe.zip
```

* Now lets copy the folder 2126_antique_cafe to /var/www/html/cafe/
```bash
sudo mv 2126_antique_cafe/ /var/www/html/cafe
```

* Now access http://<public-ip>/cafe

* Possible Options to automate the website deployment

* Shell Scripts:
* Procedural in nature (i.e. define how it has to be done)
* Are not idempotent by default
* Solution:
```bash
#!/bin/bash
WEB_DESIGN_ZIP='https://www.free-css.com/assets/files/free-css-templates/download/page295/antique-cafe.zip'
SITE_NAME='cafe'
sudo apt update
sudo apt install nginx -y
cd /tmp
wget $WEB_DESIGN_ZIP
sudo apt install unzip -y
unzip antique-cafe.zip
sudo mv 2126_antique_cafe/ /var/www/html/$SITE_NAME
```
### Configuration Management
* Declarative in nature (what we want )
* Most of the ansible is idempotent
* Setup Ansible (on Azure VM)

# Installation overview

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```

* To verify the installation
````bash
ansible --version
```

# Ansible ping test
* This is used to check if the ansible control node can communicate with the node or not
* Create an inventory file with node ip in it

* Now execute the following command
```bash
ansible -i hosts -m ping all
```
* In the above case we have not passed credentials
