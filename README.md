# This repo sets out to demonstrate how to build a node app on VM scales sets which are connected to an Azure SQL DB over a secure/private connection. 

Steps:

* Create Resource group for Managed Services and Todo-App
* Create Vnet for MS and Todo-app
* Peer Vnets
* Spin up Azure SQL Server and DB
    * Add Local IP to firewall
    * Take note of server name, admin, and password
* Build base Ubuntu 17.0 VM in MS RG
    * clone git repo
    * install dependencies
