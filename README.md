# srvmongo
Lookup MongoDB SRV dns records.
This can be helpful with debugging mongodb connection issues, especially when firewalls are involved.
The script takes a Mongo SRV dns record as input. It resolves the name to one or more server addresses. For example:

```
 $ srvmongo mydb-dev-pl-0.gvuq2z.mongodb.net
 pl-0-westus-azure.gvuq2z.mongodb.net:1024
 pl-0-westus-azure.gvuq2z.mongodb.net:1025
 pl-0-westus-azure.gvuq2z.mongodb.net:1026
 mydb-dev-pl-0.mvuq2z.mongodb.net: "authSource=admin&replicaSet=atlas-nikeu2-shard-0"
```
In the exmaple, the name ```mydb-dev-pl-0.gvuq2z.mongodb.net``` resolves to a network interface in an Azure virtual network.

```
 $ nslookup pl-0-westus-azure.gvuq2z.mongodb.net
 Name:  pl-0-westus-azure.gvuq2z.mongodb.net
 Address: 10.102.2.8
```
The network interface is a private link connection (Load Balancer) to the MongoDB cloud.
Each port on the Load Balancer represents a separate MongoDB server (in this case these are a primary, secondary and an analytics node).

The srvmongo.py script was taken from this MongoDB article https://www.mongodb.com/developer/products/mongodb/srv-connection-strings/
