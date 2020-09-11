# COURSE: Google Cloud Platform Fundamentals - Core Infrastructure

## MODULE: Development, Deploying and Monitoring in the Cloud
## LAB: Google Cloud Fundamentals: Getting Started with Deployment Manager and Cloud Monitoring



### OBJECTIVES:

In this lab, you will learn how to perform the following tasks:

    - Create a Deployment Manager deployment.

    - Update a Deployment Manager deployment.

    - View the load on a VM instance using Cloud Monitoring.


### STEPS:

1. Create a Deployment Manager deployment

    -  Place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. Type this command at the Cloud Shell prompt:

            export MY_ZONE=us-central1-a

    - Download an editable Deployment Manager template using this command:

            gsutil cp gs://cloud-training/gcpfcoreinfra/mydeploy.yaml mydeploy.yaml

    - Use the sed command to replace the PROJECT_ID placeholder with your Google Cloud Platform project ID using this command:

            sed -i -e "s/qwiklabs-gcp-02-c95800701495/$DEVSHELL_PROJECT_ID/" mydeploy.yaml

    - Use the sed command to replace the MY_ZONE placeholder with your Google Cloud Platform project ID using this command:

            sed -i -e "s/ZONE/$MY_ZONE/" mydeploy.yaml

    - View the mydeploy.yaml file, with your modifications, with this command:

            cat mydeploy.yaml

    - Build a deployment from the template with this command:

            gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml

2. Update a Deployment Manager deployment.

    - Launch the nano text editor to edit the mydeploy.yaml file:

            nano mydeploy.yaml

    - Look for the line that sets the value of the startup script, value: "apt-get update", and edit it that it looks like this:

            value: "apt-get update; apt-get install nginx-light -y"

    - Press Ctrl+O and then press Enter to save your edited file and then press Ctrl+X to exit the nano text editor.

    - Cause Deployment Manager to update your deployment to install the new startup script by using this command:

            gcloud deployment-manager deployments update my-first-depl --config mydeploy.yaml

3. View the Load on a VM using Cloud Monitoring.

    - SSH into the my-vm instance using this command:

            gcloud compute ssh my-vm --zone=us-central1-a

    - Execute this command to create a CPU load:

            dd if=/dev/urandom | gzip -9 >> /dev/null &

        This Linux pipeline forces the CPU to work on compressing a continuous stream of random data

    - To terminate your workload, on the ssh session on my-vm, enter this command:

            kill %1
