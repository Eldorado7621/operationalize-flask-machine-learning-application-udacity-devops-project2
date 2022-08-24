## Project Plan
For a well structured project plan, a Trello board was used. This makes it easy for stakeholders and engineering team to see the project progress. The links to the Trello board and the Google sheet are as given below:

* Link to Trello: [Trello Board](https://trello.com/b/PpYFuT5Y/udacity-devops-project-2-flask-ml-app)

* Link to Google sheet project plan: [Google Sheet Project Plan](https://docs.google.com/spreadsheets/d/1-pyu9owJATX9E537SLlWJW2QgTuwefiHrezXzbF_lYg/edit?usp=sharing)


## Instructions

**ARCHITECTURE**

![architecture_ing](https://user-images.githubusercontent.com/34632633/186278856-8c6896c8-c7cb-40e9-884c-c5c701c3c521.png)


## Azure CLoud Shell Setup 

Below are the steps to get the project running using the Azure Cloud Shell

1. Fork this repo and then clone it to your Azure account using the Azure cloud shell
![repo-cloned-to-azure](https://user-images.githubusercontent.com/34632633/186281600-474e4241-34e0-43a1-acd1-ca93bc98a43f.png)

2.  Setup Gitup Action by selecting the Github Action on the repo.
![github_action2](https://user-images.githubusercontent.com/34632633/186384990-130ef4eb-be9d-48bf-b198-61e59f843305.png)

2. Create a Virtual environment using this command
  `python3 -m venv ~/.{project-name}` 
  This enables the python packages and modules to be confined to the virtual environment and not global-(system wide) thereby ensuring that there would be version conflicts of libraries and modules.
3. Source the newly created virtual environment and change to the directory of the cloned repo
   `source ~/.{project-name}/bin/activate
     cd udacity-flask-ml-project2`
     
![venv](https://user-images.githubusercontent.com/34632633/186282031-a3b5c0a9-7827-46fc-a3a4-11fe328e71ba.png)

4. Run `make all` to install the required packages, the lint test and the unit test as specified in the MakeFile

![pytest-passed-local](https://user-images.githubusercontent.com/34632633/186282320-378e5219-5de4-4321-9dbf-d6e59192857a.png)

5. Since all the test have been passed, the next step is to run the app locally. use `python app.py` from the AZure cloud shell,

![running-the-app](https://user-images.githubusercontent.com/34632633/186282515-3d666930-7ddf-4806-a7ee-7049114184c7.png)

6. You can preview the app on the browser by configuring the port. 
      1. Click on web preview in the azure cloud shell
      2. Type 5000 in the configure port
      3. Select open and browse
      
![port_config](https://user-images.githubusercontent.com/34632633/186346664-b69c49e1-5be1-4d4e-8388-b0fc328d7915.png)

  The output on the browser is as shown below
![webpage](https://user-images.githubusercontent.com/34632633/186347247-8f26664e-15a7-4bf9-9abd-ef7299a55d67.png)


## AZURE WEB APP SETUP
Since we were able to run the app locally, it is time we deploy the web application to the Azure Subscription.

1. Create a new resource group to hold the application. This can be via Azure portal(GUI) or using the AZure CLI. 
  `az group create -l westeurope -n "udcaity-project2-rg"`
![deploy_resource_group´](https://user-images.githubusercontent.com/34632633/186349181-4eb3fda0-4c70-4a41-a4f0-f698825b6af9.png)

2. Create an app service and deploy the app in the Azure cloud shell
  `az webapp up --name <Your_unique_app_name> --resource-group <resource-group-name> --runtime "PYTHON:3.7"`
  
![webapp-deployed](https://user-images.githubusercontent.com/34632633/186376357-b48d114a-72e5-4482-b1e4-70f99f00c857.png)

3.  You can confirm the deployment by checking the app in the azure portal
4.  
![app_deployed](https://user-images.githubusercontent.com/34632633/186377431-bbd4cb2b-297b-4457-83d0-f77550dd0e4d.png)

4.  You can also verify the deployed application works by browsing to the deployed URL. Go to 
       `https://<Your_unique_app_name>.azurewebsites.net/`
   and you should see the same output as in the screenshot below:
5.  To perform prediction, update the make_predict_azure_app.sh file in your github repo to match the deployed URL:
   `-X POST https://<yourappname>.azurewebsites.net:$PORT/predict`

6. You can then perform git pull to update the Azure cloud shell
   `git pull`
7. To make prediction use this command `./make_predict_azure_app.sh`  

## Setup Azure Pipeline

1. Goto https://dev.azure.com/ .If you don't already have an organization you will be prompted to make one. Once you've created your Azure DevOps account you can go ahead and create a new project.

2. On the top right and create a New Project

![pipleine create project](https://user-images.githubusercontent.com/34632633/186412056-470f8a3b-a826-4c92-a27e-ad77a157e092.png)

3. After creating your project, click on it and choose the Pipelines icon on the left side. You will be asked to configure the source of your code. Clicking Github should urge you to link your Github account to your Azure DevOps account, so go ahead and do that.

4. Following the creation of the project, the wizard will guide you through the procedures of choosing your repository, customizing the pipelines YAML file, and checking the YAML file into your repository before deploying your project to the chosen Azure resource. 

![azure_pipeline](https://user-images.githubusercontent.com/34632633/186413788-3c7946e8-c059-452d-8814-ec4bf2677b29.png)

