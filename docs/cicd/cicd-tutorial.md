---
title: Lifecycle management tutorial
description: Understand the workflow of using Git integration with deployment pipelines to manage the lifecycle of your apps.
author: mberdugo
ms.author: monaberdugo
ms.reviewer: NimrodShalit
ms.topic: tutorial 
ms.date: 07/12/2023
---

# Tutorial: Lifecycle management in Fabric

This tutorial takes you through the whole process of loading data into your workspace, and using deployment pipelines together with Git integration to collaborate with others in the development, testing, and publication of your data and reports.

## Prerequisites

Before you start, make sure of the following prerequisites:

* Fabric is enabled. If you don't have Fabric enabled yet, ask your admin to [enable Fabric for your organization](../admin/fabric-switch.md).
* You're signed up. If you're not signed up yet, [sign up for a free trial](../get-started/fabric-trial.md).
* You have access to an Azure Git repo. If you don't have one, see [Set up a Git repository](/devops/develop/git/set-up-a-git-repository) for information on creating one.
* Download the [FoodSales.pbix](https://github.com/microsoft/fabric-samples/blob/main/docs-samples/cicd/FoodSales.pbix) file into a Git repo that you can edit. This is the sample file we use in this tutorial. Alternatively, you can use your own dataset and report, if you prefer.

If you already have admin rights to a workspace with data, you can skip to [step 3](#step-3-connect-the-teams-development-workspace-to-git).

## Step 1: Create a Premium workspace

To create a new workspace and assign it a license:

1. From the left navigation bar of the **Power BI** experience, select **Workspaces > + New workspace**.

   :::image type="content" source="media/cicd-tutorial/create-workspace.png" alt-text="Screenshot of Create workspace.":::

1. Name the workspace **FoodSalesWS**.
1. (Optional) Add a description.

   :::image type="content" source="media/cicd-tutorial/name-workspace.png" alt-text="Screenshot of new workspace with name.":::

1. Expand the **Advanced** section to reveal **License mode**.
1. Select either **Trial** or **Premium capacity**.

   :::image type="content" source="media/cicd-tutorial/license-mode.png" alt-text="Screenshot of new workspace with license mode.":::

1. Select **Apply**.

For more on creating a workspace, see [Create a workspace](/power-bi/collaborate-share/service-create-the-new-workspaces).

## Step 2: Load content into the workspace

You can upload content from OneDrive, SharePoint, or a local file. In this tutorial, we load a *.pbix* file.

1. From the top menu bar, select **Upload > Browse**.

   :::image type="content" source="media/cicd-tutorial/upload-data.png" alt-text="Screenshot of Upload menu.":::

1. Browse to the location of the **FoodSales.pbix** file you [downloaded earlier](#prerequisites), or load your own sample dataset and report.

You now have a workspace with content in it for you and your team to work on.

:::image type="content" source="media/cicd-tutorial/workspace-with-content.png" alt-text="Screenshot of FoodSalesWS workspace with a report, dataset, and dashboard in it.":::

### Edit credentials - first time only

Before you create a deployment pipeline, you need to set the credentials. This step only needs to be done once for each dataset. After your credentials are set for this dataset, you won't have to set them again.

1. Go to **Settings > Power BI settings**.

   :::image type="content" source="media/cicd-tutorial/settings.png" alt-text="Screenshot of Settings menu.":::

1. Select **Datasets > Data source credentials > Edit credentials**.

    :::image type="content" source="media/cicd-tutorial/edit-credentials.png" alt-text="Screenshot of Data source credentials menu.":::

1. Set the **Authentication** method to *Anonymous*, the **Privacy level** to *Public*, and uncheck the **Skip test connection** box.

    :::image type="content" source="media/cicd-tutorial/set-credentials.png" alt-text="Screenshot of dataset credentials.":::

1. Select **Sign in**. The connection is tested and credentials set.

You can now create a deployment pipeline.

## Step 3: Connect the team's development workspace to git

This workspace is shared by the entire team and each member of the team can edit it. By connecting this workspace to git, you can keep track of all the changes and revert back to previous versions if necessary. When all the changes are merged into this shared branch, the workspace is deployed to production using the deployment pipeline.  
Read more about version control with Git in [Introduction to Git integration](./git-integration/intro-to-git-integration.md).

Let's connect this workspace to the main branch of your Azure repo so all team members can edit it and create pull requests.

1. Select the ellipsis (three dots) then **Workspace settings**.

   :::image type="content" source="./media/cicd-tutorial/workspace-settings-link.png" alt-text="Screenshot of workspace with workspace settings link displayed.":::

1. Select **Git integration**. You’re automatically signed into the Azure Repos account registered to the Azure AD user signed into the workspace.

1. From the dropdown menu, specify the following details about the branch you want to connect to:

   * [Organization](/azure/devops/user-guide/plan-your-azure-devops-org-structure)
   * [Project](/azure/devops/user-guide/plan-your-azure-devops-org-structure#how-many-projects-do-you-need)
   * [Git repository](/azure/devops/user-guide/plan-your-azure-devops-org-structure#structure-repos-and-version-control-within-a-project)
   * Select *main* (or *master*) branch
   * Type the name of folder in the repo where the *.pbix* file located. This is the folder that will be synced with the workspace.

     :::image type="content" source="./media/cicd-tutorial/git-connect-main.png" alt-text="Screenshot of workspace settings Git integration window with workspace connected to main branch of repo.":::

1. Select **Connect and sync**.

After you connect, the Workspace displays information about source control that allows you to view the connected branch, the status of each item in the branch and the time of the last sync. The Source control icon shows `0` because the items in the workspace Git repo are identical.

:::image type="content" source="./media/cicd-tutorial/git-sync-information.png" alt-text="Screenshot of source control icon and other Git information.":::

Now the workspace is synced with the main branch of your Git repo making it easy to keep track of changes.

For more information about connecting to git, see [Connect a workspace to an Azure repo](git-integration/git-get-started.md#connect-a-workspace-to-an-azure-repo).

## Step 4: Create a deployment pipeline

In order to share this workspace with others and use it for various stages of testing and development, we need to create a deployment pipeline. You can read about how deployment pipelines work in [Introduction to deployment pipelines](./deployment-pipelines/intro-to-deployment-pipelines.md).
To create a deployment pipeline and assign the workspace to the development stage, do the following:

1. From the workspace home page, select **Create deployment pipeline**.

   :::image type="content" source="media/cicd-tutorial/create-pipeline.png" alt-text="Screenshot of Create deployment pipeline.":::

1. Name your pipeline *FoodSalesDP*, give it a description (optional) and select **Create**.

   :::image type="content" source="media/cicd-tutorial/name-pipeline.png" alt-text="Screenshot of new pipeline with name.":::

1. Assign the FoodSalesWS workspace to the Development stage.

   :::image type="content" source="media/cicd-tutorial/assign-workspace.png" alt-text="Screenshot of Assign workspace.":::

The development stage of the deployment pipeline shows one dataset, one report, and one dashboard. The other stages are empty.

   :::image type="content" source="media/cicd-tutorial/development-stage.png" alt-text="Screenshot of Development stage.":::

You can read more about creating deployment pipelines in [Deployment pipelines overview](./deployment-pipelines/assign-pipeline.md).

## Step 5: Deploy content to other stages

Now, deploy the content to the other stages of the pipeline.

1. From the development stage of the deployment content view, select **Deploy**.

   :::image type="content" source="media/cicd-tutorial/deploy-to-test.png" alt-text="Screenshot of Deploy to test stage.":::

1. Confirm that you want to deploy the content to the test stage.

   :::image type="content" source="media/cicd-tutorial/confirm-deploy.png" alt-text="Screenshot of Confirm deploy.":::

   Notice the content of two stages are identical, since you deployed the entire content of the pipeline. This is indicated by the green check icon.

   :::image type="content" source="./media/cicd-tutorial/pipeline-compare-same.png" alt-text="Screenshot of Development stage and test stage of pipelines with a green check icon indicating they're the same.":::

1. Deploy the content from the test stage to the production stage.

   :::image type="content" source="media/cicd-tutorial/deploy-to-prod.png" alt-text="Screenshot of Deploy to production stage.":::

1. To refresh the dataset in any stage, select the refresh button next to the datasets icon in the summary card of each stage.

   :::image type="content" source="media/cicd-tutorial/refresh.png" alt-text="Screenshot of Refresh button.":::

This deployment pipeline is shared by the entire team. Each team member can edit the dataset and report in the development stage. When the team is ready to test the changes, they deploy the content to the test stage. When the team is ready to release the changes to production, they deploy the content to the production stage.

For more information on deploying content, see [Deploy content](./deployment-pipelines/deploy-content.md).

## Step 6: Create an isolated workspace

In order to edit the workspace without interfering with other team members' changes, each team member creates their own isolated workspace to work in until they're ready to share their changes with the team.

1. Create a new workspace like you did in [Step 1](#step-1-create-a-premium-workspace).

   :::image type="content" source="./media/cicd-tutorial/isolated-workspace.png" alt-text="Screenshot of workspace with new workspace link displayed.":::

1. Connect this new workspace to a new branch of the Git repo:

   From the dropdown menu, specify the following details about the branch you want to connect to:

   * [Organization](/azure/devops/user-guide/plan-your-azure-devops-org-structure)
   * [Project](/azure/devops/user-guide/plan-your-azure-devops-org-structure#how-many-projects-do-you-need)
   * [Git repository](/azure/devops/user-guide/plan-your-azure-devops-org-structure#structure-repos-and-version-control-within-a-project)
   * Select **+ New Branch** to create a new branch.
   * Name the new branch *MyFoodEdits*, branch it from *main* (or *master*), and Select **Create**.
   * The folder in the repo where the *.pbix* file located.

    :::image type="content" source="./media/cicd-tutorial/git-create-branch.png" alt-text="Screenshot of workspace settings window with create new branch.":::

1. Select **Connect and sync**.

The new workspace now contains the content of the Git repo folder. Notice it doesn't contain the *.pbix* file. Since *.pbix* files are unsupported, this file wasn't copied to the Git repo when we synced.  
This is the workspace you use to make changes to the dataset and report until you're ready to share them with your team.

## Step 7: Edit the workspace

Make changes to the workspace by creating, deleting, or editing an item. In this tutorial, we change the format of a dataset column. You can edit the workspace in [Power BI Desktop](/power-bi/fundamentals/desktop-what-is-desktop) or [data model](/power-bi/transform-model/service-edit-data-models). In this tutorial, we edit the workspace from the data model.

1. From the dataset workspace, select the dataset ellipsis (three dots)  > **Open data model**.

    :::image type="content" source="media/cicd-tutorial/open-data-model.png" alt-text="Screenshot of open data model in the expanded dataset menu.":::

   > [!NOTE]
   > If **Open data model** is disabled, go to **Workspace settings > Power BI > General** and enable **Data model settings**.
   >
   > :::image type="content" source="media/cicd-tutorial/data-model-settings.png" alt-text="Screenshot of data model settings check box.":::

1. From the **Order_details** table, select **Discount**.

    :::image type="content" source="media/cicd-tutorial/select-table.png" alt-text="Screenshot of connected tables in the data view with the discount column of the Order Details table selected.":::

1. From the **Properties** pane, change the **Format** from *General* to *Percentage*.

    :::image type="content" source="media/cicd-tutorial/change-format.png" alt-text="Screenshot of publishing changes in Git.":::

## Step 8: Commit changes

To commit this change from the workspace into the Git branch, go back to the workspace home page.

The source control icon now shows `1` because one item in the workspace was changed but not committed to the Git repo. The *FoodSales* dataset shows a status of *Uncommitted*.

:::image type="content" source="media/cicd-tutorial/source-control-icon.png" alt-text="Screenshot of source control icon showing one uncommitted change.":::

1. Select the source control icon to view the changed items in the Git repo. The dataset shows a status of *Modified*.
1. Select the item to commit and add an optional message.
1. Select **Commit**.

   :::image type="content" source="media/cicd-tutorial/commit-changes.png" alt-text="Screenshot of committing changes.":::

The Git status of the dataset changes to *Synced* and the workspace and Git repo are in sync.

## Step 9: Create PR and merge

In the Git repo, [create a pull request](/azure/devops/repos/git/pull-requests#create-a-pull-request) to merge the *MyFoodEdits* branch with the *main* branch.

1. Select **Create a pull request**.

   :::image type="content" source="media/cicd-tutorial/create-pull-request.png" alt-text="Screenshot of create pull request.":::

1. Provide a title, description, and any other information you want for the pull request. Then select **Create**.

   :::image type="content" source="media/cicd-tutorial/name-pull-request.png" alt-text="Screenshot of naming pull request and adding description.":::

1. [Merge the pull request](/azure/devops/repos/git/complete-pull-requests#complete-a-pull-request).

   :::image type="content" source="media/cicd-tutorial/complete-merge.png" alt-text="Screenshot of merge pull request.":::

## Step 10: Update shared workspace

Go back to the shared workspace connected to the dev stage of the deployment pipeline (the one we created in [Step 1](#step-1-create-a-premium-workspace)) and refresh the page.  
The source control icon now shows 1 because one item in the Git repo was changed and is different from the items in the FoodSales workspace. The FoodSales dataset shows a status of *Update required*.

:::image type="content" source="media/cicd-tutorial/update-required-icon.png" alt-text="Screenshot of source control icon showing one difference.":::

1. Select the source control icon to view the changed items in the Git repo. The dataset shows a status of Modified.

1. Select **Update all**.

   :::image type="content" source="media/cicd-tutorial/update-workspace.png" alt-text="Screenshot of update workspace.":::

The Git status of the dataset changes to *Synced* and the workspace is synced with the *main* Git branch.

## Step 11: Compare stages in deployment pipeline

1. Select **View deployment pipeline** to compare the content in the development stage with the content in the test stage.

   :::image type="content" source="media/cicd-tutorial/view-pipeline.png" alt-text="Screenshot of View deployment pipelines icon.":::

   Notice the orange `X` icon between the stages indicating that changes were made to the content in one of the stages since the last deployment.

   :::image type="content" source="media/cicd-tutorial/compare-stages-different.png" alt-text="Screenshot showing pipeline stages are different.":::

1. Select the down arrow > **Review Changes** to view the changes. The **Change Review** screen shows the difference between the datasets in the two stages.

   :::image type="content" source="media/cicd-tutorial/change-review.png" alt-text="Screenshot of change review.":::

1. Review the changes and close the window.

For more information about comparing stages in a deployment pipeline, see [Compare stages in a deployment pipeline](deployment-pipelines/compare-pipeline-content.md).

## Step 12: Deploy to test stage

When you’re satisfied with the changes, deploy the changes to the test and/or production stages using the same process you used in [Step 5](#step-5-deploy-content-to-other-stages).

## Summary

In this tutorial, you learned how to use deployment pipelines along with Git integration to manage the lifecycle of an app, report, or other content in a workspace.  
In particular, you learned how to:

* Setup workspaces and add content for managing their lifecycle in Fabric.
* Apply Git best practices to work alone and collaborate with teammates on changes.
* Combine Git and deployment pipelines for an efficient end to end release process.

## Next steps

[Manage Git branches](./git-integration/manage-branches.md)
