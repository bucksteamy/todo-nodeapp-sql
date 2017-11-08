# This repo sets out to demonstrate how to build a node app on VM scales sets which are connected to an Azure SQL DB over a secure/private connection. 

Steps:

* Create Resource group for Managed Services and Todo-App
* Create Vnet for MS and Todo-app
* Peer Vnets
* Spin up Azure SQL Server and DB
    * Add Local IP to firewall
    * Take note of server name, admin, and password
* Build base Ubuntu 17.0 VM in MS RG
    * Clone git repo, more node app to /opt, and clean up
        * git clone https://github.com/bucksteamy/todo-nodeapp-sql.git
        * Configure the node config file for your instance of Azure SQL DB 
            * sudo vim todo-nodeapp-sql/nodejs-express4-rest-api/config/default.json 
        * sudo cp -R todo-nodeapp-sql/nodejs-express4-rest-api/ /opt/todoapp
        * sudo mv todo-nodeapp-sql/todoapp.service /etc/systemd/system/
        * rm -Rf todo-nodeapp-sql
        * cd /opt/todoapp/
    * Install node and modules
        * curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
        * sudo apt-get install -y nodejs
        * sudo apt-get install -y build-essential
        * sudo npm install npm@latest -g
        * sudo npm install
    * Configure Linux Firewall to allow for node port
        * sudo iptables -A INPUT -p tcp -m tcp --sport 3000 -j ACCEPT
        * sudo iptables -A OUTPUT -p tcp -m tcp --dport 3000 -j ACCEPT    
    * Configure systemd service 
        * sudo systemctl enable todoapp.service
        * sudo systemctl start todoapp.service
        * sudo systemctl status todoapp.service
        * curl http://localhost:3000/todo
    