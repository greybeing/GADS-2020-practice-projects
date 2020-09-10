## Objectives

In this lab, you learn how to perform the following tasks:

* Initialize **App Engine**.

* Preview an **App Engine** application running in cloud shell.

* Deploy an **App Engine** application, so that others can reach it.

* Disable an **App Engine** application, when you no longer want it to be visible.

## Task 1: Initialize App Engine

## Steps:

1. Initialize your App Engine app with your project and choose its region:

    `gcloud app create --project=$DEVSHELL_PROJECT_ID`

    > When prompted, select the region where you want your App Engine application located.


2. Clone the source code repository for a sample application in the hello_world directory:

   `git clone https://github.com/GoogleCloudPlatform/python-docs-samples`

3. Navigate to the source directory:

   `cd python-docs-samples/appengine/standard_python3/hello_world`

## Task 2: Run Hello World application locally

## Steps:

1. Execute the following command to download and update the packages list:

  `sudo apt-get update`

2. Set up a virtual environment in which you will run your application. Python virtual environments are used to isolate package installations from the system:

   `sudo apt-get install virtualenv`

   > If prompted [Y/n], press Y and then Enter.

   `virtualenv -p python3 venv`

3. Activate the virtual environment:

   `source venv/bin/activate`

4. Navigate to your project directory and install dependencies:

   `pip install  -r requirements.txt`

5. Run the application:

   `python main.py`

  > Please ignore the warning if any.

6. In **Cloud Shell**, click **Web preview** > **Preview on port 8080** to preview the application.

7. To end the test, return to Cloud Shell and press Ctrl+C to abort the deployed service.

## Task 3: Deploy and run Hello World on App Engine

## Steps:

1. Navigate to the source directory:

   
   `Navigate to the source directory`

2. Deploy your Hello World application:


   `gcloud app deploy`

   > If prompted "Do you want to continue (Y/n)?", press Y and then Enter.

   _This app deploy command uses the app.yaml file to identify project configuration_


3. Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com:


    `gcloud app browse`

    _Copy and paste the URL into a new browser window._

## Task 4: Disable the application

**App** Engine offers no option to Undeploy an application. After an application is deployed, it remains deployed, although you could instead replace the application with a simple page that says something like "not in service."

However you can disable the app through the console which makes it no longer accessible to users or enter the following command in the command line to stop the running version replacing "version" with your current version:

   `gcloud app versions stop [version]`

### Congratulations! You created your first application using App Engine.








