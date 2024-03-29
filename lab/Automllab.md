# Automated Machine learning Lab

## Create Azure resources

Create the resources enumerated above (it is better to have the resources enabled ahead of time). Some of these resources depend on Azure account permissions, so this aspect needs to be verified ahead of time. For Enterprise Accounts, creating a service principle account needs the IT/Identity Team to create a service principle account that you can use.

### Resource Group

Create a resource Group: name it: AMLv2Lab

### Azure Machine learning service

- Go into the resource group

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image003.png "Resoruce Group")

- Click Add to create a new resource for Azure Machine Learning Service

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image005.png "AML Service")

- Select Machine Learning Service Workspace and then click Create

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image009.png "AML Service")

- Give a name and select the resource group and also select the region you wan to use and then click Review and Create.

- The below image is a sample of resources that the above workspace creates. please note you won't have access the below workspace.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image013.png "AML Service")

### Blob Storage

- Create a blob storage account.

### Azure Container Registry

- Container Registry and application insights and Key vault are all create as part of the machine learning service workspace

### Machine Learning Compute

- Go into the machine learning workspace and go to Compute section.

- Now it is time to create compute so that we can use for training.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image017.png "AML Service")

> above image shows the details for compute resource. For more details take a look at documentation. For now select the min nodes and max nodes, also select the VM type. Give the compute a name and select the region. Keep the region as same for all the resources used in the lab.

### Azure Kubernetes Service

- Kubernetes service needs Service principle account. To Create a New Azure Kubernetes Service please search for Kubernetes Service. 
- Fill the details for name of cluster and nodes and other details like below image.
![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image023.png "AML Service")

- Now navigate to scale and then Authentication.Click on Configure Service Principle. Creating a service principle needs admin access to Azure AD.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image025.png "AML Service")

> https://docs.microsoft.com/en-us/azure/aks/kubernetes-service-principal

> Use the above link to create service prinicple first.

- Next is keep going each tab and then click Create. Wait untill AKS cluster gets created.

> If you want to access the Kubenetes dashboard kubectl CLI should be installed. Here is the link https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-windows

### PostMan and Rest Client tools

- Postman or Rest Client is needed for testing the api that gets deployed by the azure machine learning service

- Download and install postman from https://www.getpostman.com/downloads/

- Download and install Rest Client from https://chrome.google.com/webstore/detail/advanced-rest-client/hgmloofddffdnphfgcellkdfbfbjeloo?hl=en-US

## Now it is time to start the Lab

> Now that the resources are created for the lab it is time to start creating experiment and run through automated Machine learning to find best model and then deploy and consume. This would cover the entire Data science life cycle process. The entire data science life cycle process will covered in azure machine learning service workspace.


### Upload the Dataset

- Click on New on bottom left and select data set and upload the dataset csv file. file name: mlsample1.csv

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image041.png "AML Service")

- Click New experiment. Before that you can also upload the data set

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image039.png "AML Service")


### Creae a new Experiment

- Go to Azure Machine learning service workspace. On the left menu select visual interface

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image029.png "AML Service")

- Visual interface would open in a new browser tab. On the left there should be the menu and will show Experiment, datasets for the experment creation

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image033.png "AML Service")

### Build Model

- Now it is time to build a model using visual interface. Drag and drop the mlsample1.csv data set. Bring in Split data, Model to train, Train module, Score module and evaluate Module.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image049.png "AML Service")

- Make sure all the module are there as wpe below image.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image073.png "AML Service")

- Now it is time to Run the model.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image049.png "AML Service")

- below is the image where the option to run the model.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image085.png "AML Service")

- Select the compute target as compute. Usually it takes 5 - 10 minutes depending on the nodes in compute target.

### Create Automated machine learning for Model

- now it is time to create a New Experiment for automated machine learning
- Now the left menu in AML workspace Click Automated Machine learning

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image095.png "AML Service")

> Select the Experiment created before. Then select the compute target. Next upload the data set in default blob location shown in the workspace. On the prediction Task select regression. on the Target column select consumption.
Click Start and allow the other values default for now.

- This steps takes  a longer time to complete the model.
- Once the model is complete here is what you should see the chart with individual alogrithmn performance and also the tablular list of alogrithm that you can download as pickle file.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image103.png "AML Service")

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image105.png "AML Service")

### Deploy the best model

- Now it is time to deploy best model
- Click Deploy Model and follow the step and Model gets deployment as docker container in ACI cluster.
- In the deployment section of workspace you should see the details.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image109.png "AML Service")

### Consume the best model

- Use post man or Rest client to test the API deployed in ACI.

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image139.png "AML Service")

- Get the details from deployment section and use that in post man to test the API

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image143.png "AML Service")

![alt text](https://github.com/balakreshnan/AzureMLV2/blob/master/lab/images/image145.png "AML Service")

### Delete all resources

- Delete the complete resoruce group which will delete all the resource we created for the lab.
