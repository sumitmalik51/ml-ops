## Exercise 5: Setup the Release Pipeline

Duration: 20 minutes

### Task 1: Create an Empty Job

1. Return to Azure DevOps and navigate to **Pipelines, Releases** and select **New pipeline**.

    ![In Azure DevOps, the Pipelines item is expanded in the left menu with the Releases item selected. In the content pane, a message indicates No release pipelines found and the New pipeline button is selected.](media/devops-release-pipeline-01.png 'New Release Pipeline')

2. Select **Empty job**.

    ![In the Select a template dialog, the Empty job item is selected above the list featured templates.](media/devops-release-pipeline-02.png 'Select a template: Empty job')

3. Provide Stage name: `Deploy and Test` and close the dialog.

    ![On the Stage dialog, the Stage name textbox is populated with Deploy and Test. The close button at the top of the dialog is selected.](media/devops-release-pipeline-03.png 'Deploy and Test Stage')

### Task 2: Add Build Artifact

1. Select **+ Add an artifact**.

    ![In the New release pipeline screen, on the Pipeline tab, the + Add a new artifact item is selected within the Artifacts tile.](media/devops-release-pipeline-04.png 'Add an artifact')

2. Select **Source type**: **Build**, **Source (build pipeline)**: **mlops-quickstart**.

    > **Note**: Observe the note that shows that the mlops-quickstart publishes the build artifact named devops-for-ai.

    Finally, select **Add**.

    ![The Add an artifact dialog form is populated with the aforementioned values. The Add button is selected.](media/devops-release-pipeline-05.png 'Add a build artifact')

### Task 3: Add Variables to Deploy and Test stage

1. Open **View stage tasks** link.

    ![On the New release pipeline screen, within the Deploy and Test tile, the View stage tasks link is selected.](media/devops-release-pipeline-06.png 'View Stage Tasks')

2. Open the **Variables** tab.

    ![On the New release pipeline screen, the Variables tab is selected.](media/devops-release-pipeline-07.png 'Release Pipeline Variables')

3. Add four Pipeline variables as name - value pairs and then select **Save** (use the default values in the **Save** dialog):

    a. **Name**: `aks_name` **Value**: `aks-cluster01`

    b. **Name**: `aks_region` **Value**: `eastus`

    c. **Name**: `service_name` **Value**: `compliance-classifier-service`

    d. **Name**: `description` **Value**: `"Compliance Classifier Web Service"`

    > **Note**: Include the double quotes around the **description** value!
    

    > **Note**:
    >   - Keep the scope for the variables to the **Deploy and Test** stage.
    >   - The name of the Azure region should be the same one that was used to create Azure Machine Learning workspace earlier on.

      ![On the New release pipeline screen, the Variables tab is selected, and the Pipeline variables item is selected from a list of variable types. The list of Pipeline variables is displayed showing the variables that were just created.](media/devops-release-pipeline-08.png 'Add Pipeline Variables')

### Task 4: Setup Agent Pool for Deploy and Test stage

1. Open the **Tasks** tab.

    ![On the New release pipeline screen, the Tasks tab is selected.](media/devops-release-pipeline-09.png 'Pipeline Tasks')

2. Select **Agent job** and set **Agent pool** to `Azure Pipelines` and change **Agent Specification** to `ubuntu-16.04`.

    ![On the New release pipeline screen, Tasks tab, the Agent job is selected. The Agent job details form is populated with the aforementioned values.](media/devops-release-pipeline-10.png 'Agent Job Setup')

### Task 5: Add Use Python Version task

1. Select **Add a task to Agent job** (the **+** button), search for `Use Python Version`, and select **Add**.

    ![On the New release pipeline screen, the Tasks tab is selected. Agent job is displayed in the list of tasks. The + button is selected in the Agent job tile. The Add tasks pane is displayed with Use Python version entered in the search box, and the Use Python version search result is highlighted with its Add button selected.](media/devops-release-pipeline-11.png 'Add Use Python Version Task')

2. Provide **Display name:** `Use Python 3.6` and **Version spec:** `3.6`

    ![The Use Python version form is displayed populated with the preceding values.](media/devops-release-pipeline-12.png 'Use Python Version Task Dialog')

### Task 6: Add Install Requirements task

1. Select **Add a task to Agent job** (the **+** button), search for `Bash`, and select **Add**.

    ![On the New release pipeline screen, the Tasks tab is selected. A list of tasks includes the Agent job that has a Use Python 3.6 task. The + button is selected in the Agent job tile, and in the Add tasks form, Bash is entered into the search text box and the Bash item is highlighted in a list of search results with its Add button selected.](media/devops-release-pipeline-13.png 'Add Bash Task')

2. Provide **Display name:** `Install Requirements` and select **Browse script path ...** to provide **Script Path**.

    ![On the New release pipeline screen, the Tasks tab is selected. A list of tasks is displayed below the Agent job. The Install requirements job is selected from this list. In the Bash form, fields are populated with the preceding values.](media/devops-release-pipeline-14.png 'Bash Task Dialog')

3. Navigate to **Linked artifacts/_mlops-quickstart (Build)/devops-for-ai/environment_setup** and select **install_requirements.sh**.

    ![A Select a file or folder dialog is displayed showing the location hierarchy to the install_requirements.sh file. The OK button is selected.](media/devops-release-pipeline-15.png 'Select Path Dialog')

4. Expand **Advanced** and select **Browse working directory ...** to provide **Working Directory**.

    ![On the Bash form, the Advanced section is expanded. The ellipsis button is selected next to the Working Directory textbox.](media/devops-release-pipeline-16.png 'Bash Task - Advanced Section')

5. Navigate to **Linked artifacts/_mlops-quickstart (Build)/devops-for-ai** and select **environment_setup**.

    ![In the Select a file or folder dialog, the location hierarchy is displayed to the environment_setup folder.](media/devops-release-pipeline-17.png 'Select Path Dialog')

### Task 7: Add Deploy and Test Webservice task

1. Select **Add a task to Agent job** (the **+** button), search for `Azure CLI`, and select **Add**.

    ![In the New release pipeline screen, the Tasks tab is selected. In the list of Tasks, in the Agent job tile, the + button is selected. In the Add tasks form, Azure CLI is entered into the search box, and the Azure CLI search result is highlighted with its Add button selected.](media/devops-release-pipeline-18.png 'Azure CLI Task')

2. Provide the following information for the Azure CLI task:

    a. **Display name**: `Deploy and Test Webservice`

    b. **Azure subscription**: **quick-starts-sc**

    > **Note**: This is the service connection we created in Exercise 1 / Task 4.

    c. **Script Location**: **Inline script**

    d. **Inline Script**: `python aml_service/deploy.py --service_name $(service_name) --aks_name $(aks_name) --aks_region $(aks_region) --description $(description)`

    ![On the Tasks tab of the New release pipeline screen, the Deploy and Test Webservice task is selected beneath the Agent job item. The Azure CLI form is populated with the preceding values.](media/devops-release-pipeline-19.png 'Azure CLI Task Dialog')

3. Expand **Advanced** and provide **Working Directory:** `$(System.DefaultWorkingDirectory)/_mlops-quickstart/devops-for-ai`.

    ![In the Azure CLI form, the Advanced section is expanded and the Working Directory field is populated with the specified value.](media/devops-release-pipeline-20.png 'Azure CLI Task - Working Directory')

> **Note**: Please review the code in `aml_service/deploy.py`. By using the `eval_info.json` file that is associated with each trained model, this script can determine if the new trained model's performance is better than the currently deployed model. If it determines the new model has better performance, it will deploy the new model to production in an **Azure Kubernetes Service (AKS)** cluster.

### Task 8: Define Deployment Trigger

1. Navigate to **Pipeline** tab, and select **Pre-deployment conditions** for the **Deploy and Test** stage.

2. Select **After release**.

    ![In the New release pipeline screen, the Pipelines tab is selected. Within the Stages tile, the Pre-deployment Condition item is selected in the Deploy and Test stage tile. The Pre-deployment conditions form is displayed with the Triggers section expanded. After release is selected as the trigger.](media/devops-release-pipeline-21.png 'Pre-deployment Conditions Dialog')

3. Close the dialog.

### Task 9: Enable Continuous Deployment Trigger

1. Select **Continuous deployment trigger** for `_mlops-quickstart` artifact.

2. Enable: **Creates a release every time a new build is available**.

    ![In the New release pipeline screen, the Pipelines tab is selected. Within the Artifacts tile, the Continuous deployment trigger option is selected on the _mlops-quickstart tile. The Continuous deployment trigger form is displayed indicating that it is Enabled.](media/devops-release-pipeline-22.png 'Continuous Deployment Trigger Dialog')

3. Close the dialog.

### Task 10: Save the Release Pipeline

1. Provide name: `mlops-quickstart-release`.

2. Select **Save** (use the default values in the **Save** dialog).

    ![In the header of the New pipeline screen, the pipeline name is set to mlops-quickstart-release, and the Save button is selected from the top taskbar.](media/devops-release-pipeline-23.png 'Save')
