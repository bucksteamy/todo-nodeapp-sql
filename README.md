# This repo sets out to demonstrate how to build a node app on VM scales sets which are connected to an Azure SQL DB over a secure/private connection. 

Steps:

* Create Resource group for Managed Services and Todo-App
* Create Vnet for MS and Todo-app
* Peer Vnets
* Spin up Azure SQL Server and DB
    * Add vNet Rule
    * Take note of server name, admin, and password
    * hydrate DB via portal with script found in nodejs-express4-rest-api/setup/setup.sql
* Deploy VMSS
    * Fork this repo https://github.com/bucksteamy/todo-nodeapp-sql.git
        * Configure the node config file for your instance of Azure SQL DB 
    * Configure Cloud Shell in the Azure Portal
    * copy cloud-init.txt to Cloudshell fileshare
    ```bash
    ADMIN_USER="" 
    ADMIN_PASSWORD='' 
    RESOURCE_GROUP="" 
    VMSS_NAME="" 
    IMAGE_NAME="" 
    VNET_NAME="" 
    SUBNET_NAME=""

    az vmss create --vnet-name $VNET_NAME \
    --subnet $SUBNET_NAME \
    --admin-username $ADMIN_USER \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data ~/clouddrive/cloud-init.txt \
    -n $VMSS_NAME \
    -g $RESOURCE_GROUP \
    --generate-ssh-keys
   ```
* Configure healthprobe and load balance rule on the Azure Load Balancer created at VMSS deployment time
            
