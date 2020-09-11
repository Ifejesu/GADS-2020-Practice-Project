# COURSE: Google Cloud Platform Fundamentals - Core Infrastructure

## MODULE: Development, Deploying and Monitoring in the Cloud
## LAB: Google Cloud Fundamentals: Getting Started with App Engine



### OBJECTIVES:

In this lab, you will learn how to perform the following tasks:

    - Initialize App Engine.

    - Preview an App Engine application running locally in Cloud Shell.

    - Deploy an App Engine application, so that others can reach it.

    - Disable an App Engine application, when you no longer want it to be visible.

### STEPS:

1.  Initialize App Engine.

    - Initialize your App Engine app with your project:

            gcloud app create --project=$DEVSHELL_PROJECT_ID --region=us-central1

    - Clone the source code repository for a sample application in the hello_world directory:

            git clone https://github.com/GoogleCloudPlatform/python-docs-samples

    - Navigate to source directory:
            
            cd python-docs-samples/appengine/standard_python3/hello_world

2.  Preview your Hello World application running locally in Cloud Shell.

    - Execute the following command to download and update the packages list:

            sudo apt-get update

    - Set up a virtual environment in which you will run your application using this command:

            sudo apt-get install virtualenv

    - When prompted [Y/n], press Y and then Enter. Enter the command below:

            virtualenv -p python3 venv

    - Activate the virtual environment:

            source venv/bin/activate

    - Navigate to your project directory and install dependencies with this command:

            pip install  -r requirements.txt

    - Run the application:

            python main.py

    - In Cloud Shell, click Web preview (Web Preview) > Preview on port 8080 to preview the application.

    - Return to Cloud Shell and press Ctrl+C to end the test.

3. Deploy and run Hello World on App Engine so that others can reach it.

    - Navigate to the source directory:

            cd ~/python-docs-samples/appengine/standard_python3/hello_world

    - Deploy your Hello World application:

            gcloud app deploy

4. Disable the application

    - To disable the app, run the following command:

        gcloud app versions stop v1