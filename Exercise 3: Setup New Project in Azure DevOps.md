## Exercise 3: Setup New Project in Azure DevOps

Duration: 20 minutes

### Task 1: Create New Project

1. Sign in to [Azure DevOps](http://dev.azure.com).

2. Select **+ New project**.

    ![In the Azure DevOps screen, the + New project button is selected.](media/devops-project-01.png 'Create new project')

3. Provide Project Name: `mlops-quickstart` and select **Create**.

    ![The Create new project dialog is shown populated with the value above. Visibility is set to Private, and the Create button is highlighted.](media/devops-project-02.png 'Create New Project Dialog')

### Task 2: Import Quickstart code from a GitHub Repo

1. Within the new project:

   a. Select **Repos** from left navigation bar.

   b. Select **Import** from the content section.

    ![In Azure DevOps, Repos is selected from the left menu. In the mlops-quickstart screen the Import button is selected in the Import a repository section.](media/devops-project-03.png 'Azure DevOps Repos')

2. Provide the following GitHub URL: `https://github.com/solliancenet/mcw-mlops-starter-v2` and select **Import**. This should import the code required for the quickstart.

    ![In the Import a Git repository dialog, the Clone URL is populated with the value indicated above and the Import button is selected.](media/devops-project-04.png 'Import a Git repository dialog')

    > **Note**: If you receive an error while importing the repository, please disable the preview feature **New Repos landing pages** and import the GitHub repository from the old UI, as shown in steps #3, #4, and #5 below.

3. [Optional] Select **Account settings, Preview features**.

    ![On the mlops-quickstart repo page, Settings is expanded in the taskbar and the Preview features item is highlighted.](media/preview_features-01.png 'Preview features')

4. [Optional] From the list of preview features, disable the preview feature **New Repos landing pages**.

   ![A list of preview features is displayed highlighting the New Repos landing pages features.](media/preview_features-02.png 'Disable New Repos landing pages')

5. [Optional] Repeat Step #1 above to import the GitHub repository from the old UI.

### Task 3: Update the build YAML file

1. Select and open the **azure-pipelines.yml** file.

2. Select **Edit** and update the following variables: **resourcegroup**, and **workspace**. If you are using your own Azure subscription, please provide names to use. If an environment is provided to you, be sure to replace XXXXX in the values below with your unique identifier.

    ![In the left menu, beneath Repos, the Files item is selected. In the files list, azure-pipelines.yml is selected. In the editor pane, the contents of the file are displayed with the resource group and workspace variables highlighted. The Edit button is selected in the top toolbar.](media/devops-build-pipeline-01.png 'Edit Build YAML file')

3. Select **Commit** to save your changes and select **Commit** again in the commit properties dialog.

    ![The content of azure-pipelines.yml is updated and the Commit button is selected in the top taskbar.](media/devops-build-pipeline-02.png 'Commit Build YAML file')

### Task 4: Create new Service Connection

1. From the left navigation, select **Project settings** and then select **Service connections**.

    ![In the left menu, Project settings is selected. In the Project Settings list, Service connections is selected. In the Create your first service connection screen, the Create service connection button is selected.](media/devops-build-pipeline-03.png 'Service Connections')

2. Select **Create service connection**, select **Azure Resource Manager**, and then select **Next**.

    ![In the New service connection dialog, Azure Resource Manager is selected from the list. The Next button is selected.](media/devops-build-pipeline-04.png 'Azure Resource Manager')

3. Select **Service principal (automatic)** and then select **Next**.

    ![In the New service connection dialog, under Authentication method, Service principal (automatic) is selected. The Next button is selected.](media/devops-build-pipeline-05.png 'Service principal authentication')

4. Provide the following information in the **New Azure service connection** dialog box and then select **Save**:

    a. **Scope level**: **Machine Learning Workspace**

    b. **Subscription**: Select the Azure subscription to use.

    > **Note**: It might take up to 30 seconds for the **Subscription** dropdown to be populated with available subscriptions, depending on the number of different subscriptions your account has access to.

    c. **Resource group**: This value should match the value you provided in the **azure-pipelines.yml** file.

    d. **Machine Learning Workspace**: This value should match the value you provided in the **azure-pipelines.yml** file.

    e. **Service connection name**: `quick-starts-sc`

    f. **Security**: Grant access permission to all pipelines is checked.

    ![The New Azure service connection form is populated with the values outlined above. The Save button is selected.](media/devops-build-pipeline-06.png 'Add an Azure Resource Manager service connection dialog')
