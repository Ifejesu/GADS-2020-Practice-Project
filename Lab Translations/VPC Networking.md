# VPC NETWORKING

##Objectives

In this lab, you learn how to perform the following tasks:
*Explore the default VPC network
*Create an auto mode network with firewall rules
*Convert an auto mode network to a custom mode network
*Create custom mode VPC networks with firewall rules
*Create VM instances using Compute Engine
*Explore the connectivity for VM instances across VPC networks

-View firewall-rules 

gcloud compute firewall-rules list

-Delete the firewalls 

gcloud compute firewall-rules delete firewall=default
 
-List the default networks

gcloud compute networks list 

-Delete the default network 

gcloud compute networks delete network=default

##Try to create a VM instance

gcloud compute instances create instance-1 --zone=us-central1-a --machine-type=f1-micro

-Cannot create a VM if there is no network and no firewall rules

##Task 2. Create an auto mode network
###Create an auto mode VPC network with firewall rules

Step1. 

//create a VPC network

gcloud compute networks create mynetwork --subnet-mode=auto

//create firewall rules

gcloud compute firewall-rules create --direction=INGRESS --priority=1000 --network=mynetwork --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

//Create a VM instance in us-central1

gcloud compute instances create mynet-us-vm --zone=us-central1-c --machine-type=n1-standard-1

//Create a VM instance in europe-west1

gcloud compute instances create mynet-eu-vm --zone=europe-west1-c --machine-type=n1-standard-1

//Verify connectivity for the VM instances

gcloud compute ssh mynet-us-vm --zone=us-central1-c

ping -c 3 10.132.0.2

ping -c 3 mynet-eu-vm

ping -c 3 104.199.94.63

//Convert the network to a custom mode network

gcloud compute networks update mynetwork --switch-to-custom-subnet-mode

##Task 3. Create custom mode networks

###Create the managementnet network

gcloud compute networks create managementnet  --subnet-mode=custom

gcloud compute networks subnets create managementsubnet-us --network=managementnet --region=us-central1 --range=10.130.0.0/20

###Create the privatenet network

gcloud compute networks create privatenet --subnet-mode=custom

gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-central1 --range=172.16.0.0/24

gcloud compute networks subnets create privatesubnet-eu --network=privatenet --region=europe-west1 --range=172.20.0.0/20

gcloud compute networks list

gcloud compute networks subnets list --sort-by=NETWORK

###Create the firewall rules for managementnet

gcloud compute firewall-rules create managementnet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=managementnet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

###Create the firewall rules for privatenet

gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

gcloud compute firewall-rules list --sort-by=NETWORK

###Create the managementnet-us-vm instance

gcloud compute instances create managementnet-us-vm --zone=us-central1-c --machine-type=f1-micro --subnet=managementsubnet-us

###Create the privatenet-us-vm instance

gcloud compute instances create privatenet-us-vm --zone=us-central1-c --machine-type=f1-micro --subnet=privatesubnet-us

gcloud compute instances list --sort-by=ZONE

##Task 4. Explore the connectivity across networks

gcloud compute ssh mynet-us-vm --zone=us-central1-c

ping -c 3 104.199.94.63

ping -c 3 <Enter managementnet-us-vm's external IP here>

ping -c 3 <Enter privatenet-us-vm's external IP here>

ping -c 3 <Enter mynet-eu-vm's internal IP here>

ping -c 3 <Enter privatenet-us-vm's internal IP here>

