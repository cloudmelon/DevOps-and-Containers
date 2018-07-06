# Get Ready for DevOps and Containers

An introduction to the principles of DevOps and containerisation using Azure DevOps Project and Kubernetes.

## What is Azure DevOps Project?

Azure DevOps Project presents a simplified experience where you bring your existing code and Git repository, or choose from one of the sample applications to create a continuous integration (CI) and continuous delivery (CD) pipeline to Azure.  

The DevOps project automatically creates Azure resources such as the Azure Kubernetes Service (AKS) to run containerised applications, creates and configures a release pipeline in Visual Studio Team Services (VSTS) that includes a build definition for CI, sets up a release definition for CD, and then creates an Azure Application Insights resource for monitoring your application to make sure it's healthy.

## In this lab, you will:

1. Create an Azure DevOps project for an ASP.NET Core App and AKS
2. Configure VSTS and an Azure subscription 
3. Examine the AKS cluster
4. Examine the VSTS CI Build definition
5. Examine the VSTS CD Release Management definition
6. Commit changes to VSTS and automatically deploy to Azure

## Prerequisites

* An Azure subscription. You can get one free through [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/).

## Create an Azure DevOps project for an ASP.NET Core App and AKS

The Azure DevOps Project creates a CI/CD pipeline in VSTS.  You can create a **new VSTS** account or use an **existing account**.  The Azure DevOps Project also creates **Azure resources** such as an AKS cluster in the **Azure subscription** of your choice.

1. Sign into the [Microsoft Azure portal](https://portal.azure.com).

1. Choose the **Create a resource** icon in the left navigation bar, then search for **DevOps project**.  Choose **Create**.

   	![Starting Continuous Delivery](_img/azure-devops-project-aks/fullbrowser.png)

1. Select **.NET**, and then choose **Next**.

1. For **Choose an application Framework**, select **ASP.NET Core**, and then select **Next**.

1. Select **Kubernetes Service**, then choose **Next**.  

## Configure VSTS and an Azure subscription

1. Create a **new** VSTS account or choose an **existing** account.  Choose a **name** for your VSTS project.  

1. Select your **Azure subscription**.

1. Select the **Change** link to see additional Azure configuration settings, and identify the **number of nodes** for the **Kubernetes cluster**.  There are various options here for configuring the type and location of Azure services.
 
1. Exit the Azure configuration area, and choose **Done**.

1. It will take several minutes for the process to complete.  A sample ASP.NET Core application is set up in a repository in your VSTS account, an AKS cluster is created, a build and release executes, and your application deploys to Azure.  

	Once complete, the Azure DevOps **project dashboard** loads in the Azure portal.  You can also navigate to the **Azure DevOps Project Dashboard** directly from **All resources** in the **Azure Portal**.  

	This dashboard provides visibility into your VSTS **code repository**, **VSTS CI/CD pipeline**, and **AKS cluster**.  You can further configure additional options in VSTS.  On the right-side of the dashboard, select **Browse** to view your running application.

## Examine the AKS cluster

The Azure DevOps Project automatically configures an AKS cluster.  You can explore and customize the cluster.  Follow the steps below to familiarize yourself with the AKS.

1. Navigate to the **Azure DevOps Project dashboard**.

1. On the right-side of the DevOps project dashboard, select the **Kubernetes service**.

1. A blade opens for the AKS cluster.  From this view you can perform various actions such as **monitor container health**, **search logs**, and open the **Kubernetes dashboard**.

1. On the right-side of the screen, select **View Kubernetes dashboard**.  Optionally follow the steps to open the Kubernetes dashboard.

## Examine the VSTS CI Build definition

The Azure DevOps Project automatically configures a full VSTS CI/CD pipeline in your VSTS account.  You can explore and customize the pipeline.  Follow the steps below to familiarize yourself with the VSTS build definition.

1. Navigate to the **Azure DevOps Project dashboard**.

1. Select **Build Pipelines** from the **top** of the **Azure DevOps project dashboard**.  This link opens a browser tab and opens the VSTS build definition for your new project.

1. Move the mouse cursor to the right of the build definition next to the **Status** field. Select the **ellipsis** that appears.  This action opens a menu where you can perform several activities such as **queue a new build**, **pause a build**, and **edit the build definition**.

1. Select **Edit**.

1. From this view, **examine the various tasks** for your build definition.  The build performs various tasks such as fetching sources from the VSTS Git repository, restoring dependencies, and publishing outputs used for deployments.

1. At the top of the build definition, select the **build definition name**.

1. Change the **name** of your build definition to something more descriptive.  Select **Save & queue**, then select **Save**.

1. Under your build definition name, select **History**.  You see an audit trail of your recent changes for the build.  VSTS keeps track of any changes made to the build definition and allows you to compare versions.

1. Select **Triggers**.  The Azure DevOps project automatically created a CI trigger, and every commit to the repository initiates a new build.  You can optionally choose to include or exclude branches from the CI process.

1. Select **Retention**.  Based on your scenario, you can specify policies to keep or remove a certain number of builds.

## Examine the VSTS CD Release Management definition

The Azure DevOps Project automatically creates and configures the necessary steps to deploy from your VSTS account to your Azure subscription.  These steps include configuring an Azure service connection to authenticate VSTS to your Azure subscription.  The automation also creates a VSTS Release Definition, and this provides the CD to the Azure.  Follow the steps below to examine more about the VSTS Release Definition.

1. Select **Build and Release**, then choose **Releases**.  The Azure DevOps project created a VSTS release definition to manage deployments to Azure.

1. On the left-hand side of the browser, select the **ellipsis** next to your release definition, then choose **Edit**.

1. The release definition contains a **pipeline**, which defines the release process.  Under **Artifacts**, select **Drop**.  The build definition you examined in the previous steps produces the output used for the artifact. 

1. To the right-hand side of the **Drop** icon, select the **Continuous deployment trigger** **icon** (which appears as a lightning bolt.)  This release definition has an enabled CD trigger.  The trigger initiates a deployment every time there is a new build artifact available.  Optionally, you can disable the trigger, so your deployments will then require manual execution. 

1. On the right-hand side of the browser, select **View releases**.  This view shows a history of releases.

1. Select the **ellipsis** next to one of your releases, and choose **Open**.  There are several menus to explore from this view such as a **release summary**, **associated work items**, and **Tests**.

1. Select **Commits**.  This view shows code commits associated with the specific deployment. You can compare releases to view the commit differences between deployments.

1. Select **Logs**.  The logs contain useful information about the deployment process.  They can be viewed both during and after deployments.

## Commit changes to VSTS and automatically deploy to Azure 

 > [!NOTE]
 > The steps below test the CI/CD pipeline with a simple text change to your web app.

You're now ready to collaborate with a team on your app with a CI/CD process that automatically deploys your latest work to your web site.  Each change to the VSTS git repo initiates a build in VSTS, and a VSTS Release Management definition deploys your changes to Azure.  Follow the steps below, or use other techniques to commit changes to your repository.  For example, you can **clone** the Git repository in your favorite tool or IDE, and then push changes to this repo.

1. Select **Code** and then **Files** from the VSTS menu, and navigate to your repository.
1. Navigate to the **Views\Home** directory, then select the **ellipsis** next to the **Index.cshtml** file, and then choose **Edit**.

1. Make a change to the file such as some text inside one of the **div tags**.  At the top right, select **Commit**.  Select **Commit** again to push your change. 

1. In a few moments, a **build initiates in VSTS**, and then a release executes to deploy the changes.  You can monitor the **build status** with the DevOps project dashboard or in the browser with your VSTS account.

1. Once the release completes, **refresh your application** in the browser to verify you see your changes.
