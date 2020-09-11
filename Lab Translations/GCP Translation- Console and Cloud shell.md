# COURSE: Essential Google Cloud Infrastructure: Foundation

## MODULE: Introduction to Google Cloud
## LAB: Console and Cloud Shell



### OBJECTIVES:

In this lab, you will learn how to perform the following tasks:

    - Create a Cloud Storage bucket using the Cloud Console.

    - Create a Cloud Storage bucket using Cloud Shell.

    - Become familiar with Cloud Shell features.

## STEPS:

1. Create a bucket using the Cloud Console:

        gsutil mb gs://qwiklabs-gcp-02-c95804751492

2. Create a Cloud Storage bucket using Cloud Shell.

        gsutil mb gs://qwiklabs-gcp-02-c95804751492shell

3. Become familiar with Cloud Shell features.

    1. Upload a file

        - Click the three dots icon in the Cloud Shell toolbar to display more options.

        - Click "Upload file" option. Upload a file from your local machine to the Cloud Shell VM. This file in my case is named sakoloweto.txt.

        - Confirm that the file was uploaded.

                ls

        - Copy the file into one of the buckets you created earlier in the lab.

                gsutil cp sakoloweto.txt gs://qwiklabs-gcp-02-c95804751492shell

    2. Create a persistent state in Cloud Shell.

        1. Identify available regions.

            - To list all available regions, execute the following command:

                gcloud compute regions list

        2. Create and verify an environment variable

            - Create an environment variable and set your preferred region to it which is "us-central1" in my case:
                
                INFRACLASS_REGION=us-central1

            - Verify it with echo:

                echo $INFRACLASS_REGION

        3. Append the environment variable to a file.

            - Create a subdirectory for materials used in this class:

                    mkdir infraclass

            - Create a file called config in the infraclass directory:

                    touch infraclass/config

            - Append the value of your Region environment variable to the config file:

                    echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config
        
            - Create a second environment variable for your Project ID:

                    INFRACLASS_PROJECT_ID=qwiklabs-gcp-02-c95804751492

            - Append the value of your Project ID environment variable to the config file:

                    echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config

            - Use the source command to set the environment variables, and use the echo command to verify that the project variable was set:

                    source infraclass/config
                    echo $INFRACLASS_PROJECT_ID

        4. Modify the bash profile and create persistence.

            - Edit the shell profile with the following command:

                    nano .profile

            - Add the following line to the end of the file:

                    source infraclass/config

            - Press Ctrl+O, ENTER to save the file, and then press Ctrl+X to exit nano. Then close and then re-open Cloud Shell to cycle the VM.

            - Use the echo command to verify that the variable is still set:

                    echo $INFRACLASS_PROJECT_ID