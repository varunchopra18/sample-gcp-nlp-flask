# Python Google Natural Language Cloud sample for Google App Engine Flexible Environment

This sample demonstrates how to use the [Google Cloud Natural Language API](https://cloud.google.com/natural-language) and [Google Cloud Datastore](https://cloud.google.com/datastore/) on [Google App Engine Flexible Environment](https://cloud.google.com/appengine).


## Setup
Head over to the [Google Cloud Platform console](https://console.cloud.google.com/) and make sure you are in the desired project.

Open the Cloud Shell by clicking this button on the top right of the console:

![img.png](../docs/img.png)

Create your App Engine application by typing:

    gcloud app create

You will have to select a region. Choose one that is close to your location.

## Get Service Account Key

You can do all of this directly in the Cloud Shell or if you setup Cloud SDK on your local machine as well (see below on how to do that)

Get the project ID and save it into an environment variable

    export PROJECT_ID=$(gcloud config get-value core/project)


Get the key.json for the App Engine service account:

    gcloud iam service-accounts keys create ~/key.json --iam-account \
    ${PROJECT_ID}@appspot.gserviceaccount.com

<span style="color:red">
<h1>
<b>
IMPORTANT: Keep this key.json a secret. You should not commit this file ever.
</b>
</h1>
</span>

## Running the Backend on Cloud Shell

Run the following command to clone the Github repository to your cloud shell:

    git clone https://github.com/Jiaxen/sample-gcp-nlp-flask.git

Change directory to the backend directory:

    cd sample-gcp-nlp-flask/backend_api

## Running Flask on Cloud Shell
To run our app through the cloud shell (that is, not deploying it just yet), we should create a virtual environment. This is just an environment where we install the specific dependencies needed by the project and can run the code.

Install virtualenv:

    pip install virtualenv

Create a virtual environment and install dependencies:

    virtualenv -p python3 env

If you do `ls` now, you will see an `/env` folder created which contains the virtual environment. 

Start your virtual environment:

    source env/bin/activate

Install the dependencies:

    pip install -r requirements.txt

Start your application via cloud shell using your virtual environment:

    python main.py

Visit the link generated ('Running on http://127.0.0.1:8080/') to view your application running locally. Test it out! (click on the link from cloud shell)

You should be presented with a [Swagger UI](https://swagger.io/tools/swagger-ui/) page. This page will allow you to interact with the backend REST API easily. In the examples we have given you can make a post request where we apply sentiment analysis on some given text and then save it to [GCP Datastore](https://cloud.google.com/datastore/docs/quickstart)

Press `Control-C` on your command line when you are finished to stop the application.

 
## Deactivating your virtual environment
When you are ready to leave your virtual environment:

    deactivate

## Deploying to App Engine

Deploy your application to App Engine with the following command. Please note that this may
take several minutes.

    gcloud app deploy

Visit `https://[YOUR_PROJECT_ID].appspot.com` to view your deployed application.

You can continue to make new versions of the application and deploy them with the above command.

## Running Locally (Optionally)
Alternatively, if you do not wish to use the Cloud Shell you can setup the Cloud SDK on your local machine instead.

Download the Cloud SDK here https://cloud.google.com/sdk/docs/downloads-interactive

Once downloaded and installed login using:

    gcloud auth login

Link to the correct project (using the wrong project might accidently bill you instead). Extra documentation https://cloud.google.com/sdk/docs/initializing

    gcloud init

Then follow the instructions from the top as normal (some small adjustments may be required if using windows)

Additionally, to set environment variables such as the project id on windows use 'set' and with mac you can continue to use 'export'. If there are issues with this you can just manually copy and paste the project id. 

For windows activating your python environment is slightly different

    \venv\Scripts\activate

And if you get an error about not being abel to execute scripts you may need to do the following as well:

    Set-ExecutionPolicy Unrestricted -Scope Process