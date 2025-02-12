### Ansible configuration (password less)
* Lets create two vms
* create a user in ansible control node called as devops and same on node
 ```bash
 sudo adduser devops
```

* give admin permissions password less for devops
* generate a key pair on ansible control node
* copy the public key to the node
* now try connecting using ssh without password
* INstall ansible on control node 

```bash 
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```

* On both node add user devops
```bash
sudo adduser devops
```

* AWS will not allow password authentication by default, so we need to change the configuration rules
* Change the value of PasswordAuthentication to yes in sudo  /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
* restart sshd service
```bash
sudo systemctl restart ssh.service
```
* We need to grant admin permissions to devops user
```bash 

sudo visudo
```
* Now add the following line under the line %sudo (ALL=ALL)
```bash
devops  ALL=(ALL:ALL) NOPASSWD:ALL
```

* Now lets configure key based authentication between ansible control node and node 1

*Switch to devops user
```bash
 su devops
 ```

* Create a key pair ssh-keygen on ansible control node
```bash 
ssh-keygen
```

* Now copy the public key into node1 on ansible control node
```bash
ssh-copy-id devops@<node-1-ip>
```
* After this step we are up for passwordless authentication

* Lets install ansible on ansible control node
```bash

sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```
* Now create a hosts file and perform ansible ping test
```bash
vi <anyname> anyname=creates a vi file {example ---bash vi hosts ---}
```
* now give node-1 public ip or private ip in the vi file 
* to insert into vi file enter <i>
* enter the ip address of node-1
* after entering the ip address enter Esc 
* after enter :wq   to save your file and exit from vi file
* now you are set to go and connect with node-1
* run a ping test on ansible control node to check the connection
```bash 
ansible -i <vi file name> -m ping all 
```
* if you have no errors , your setup is wonderful. 
