# Azure Kubernetes and DevOps Workshop

This `README` assumes that you have a valid Azure subscription.

# Configuration

## Install azure CLI

First we need to install Azure CLI in order to operate Azure resources. This is different depending on your operating system and you can find the instructions in the following url:

- https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest

Once, you have installed Azure CLI, execute `az login` and provide your credentials.

We can use Azure CLI later on to explore the content of our AKS cluster.

## Fork GitHub project into your own account

Browse the following URL:
- https://github.com/nearform/azure-workshop

Click on `Fork` to create a copy of the repository in your own GitHub account so that you can change the code without affecting anyone else.

## Create Azure DevOps Project

Now it is time to create an Azure DevOps project. Browse to:

- https://portal.azure.com

Login with your credentials and click on `Create a resource`. Type `DevOps` and select `DevOps Project`.

Now click on `Bring your own code` and click on `Next`. Select GitHub and onnect your GitHub account and select the repository that you forked above.

On the next step, select `Yes` as the answer to the question `Is app Dockerized` and click next.

Now choose Kubernetes Service, leave the Dockerfile path with the default value and enter `helm` on the `Path to the Chart folder` textbox.

On the next screen select the appropriate values on:

- Project name: The value of your choice.
- Cluster name: The value of your choice.
- Location: Choose somewhere in Europe (preferably Europe West)

Click on Done.

This is going to create:
- An AKS Cluster
- An Azure Container Registry

The release pipeline will fail but we are going to fix it on the next step.

## Fix Helm Chart path error

By default, Azure DevOps is unable to find out the name of your Chart, on the releases pipeline, update
the value using the explorer to the zip file that the browser shows (helm-0.1.0.zip by default)

## Customize build pipelines to build the three Docker images

Now it is time to adjust the build pipelines to build not one but the three Docker images that the project is composed of.

# Exercises

Now it is time to explore Azure DevOps. Ask as many questions as you need and make sure that you understand what you are doing.

## Customize the release pipeline to use the most recently built images

We have adapted the build pipelines to build and deploy the three images that compose our system into an Azure container registry. Now it is time to customize the release pipeline to use these images instead of the default ones from Docker Hub.

## Make some changes to the app and redeploy

Now it is time to change the app, push the changes to GitHub and see what happens through the pipelines on Azure DevOps (https://dev.azure.com)

## Use release gates/criteria to seek for manual approval before releasing

We have seen how to build an artifact and release it. Now we want to configure our release pipeline to require manual releasing and seek for approval. This will require someone to manually create a release and someone else (can be the same person on this workshop) to approve the release.
