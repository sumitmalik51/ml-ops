## Exercise 4: Setup and Run the Build Pipeline

Duration: 25 minutes

> **Note**: This exercise requires the new version of the **Pipelines** user interface. To activate it, select **Pipelines** from the left navigation. If the first option below **Pipelines** is **Builds**, you are still running on the previous version of the user interface. In this case, a popup should appear suggesting the activation of the new user interface.
>
> ![The Multi-stage pipelines dialog is displayed prompting to use the new UX with a Learn more and Try it! button.](media/devops-ui-activation.png 'Multi-stage pipelines activation')
>
> Select **Try it!** to activate the new Pipelines user interface. When successfully activated, the first option below **Pipelines** from the left navigation will change to **Pipelines**.

### Task 1: Setup Build Pipeline

1. From left navigation select **Pipelines, Pipelines** and then select **Create pipeline**.

    ![In the left menu, the Pipelines item is expanded with the Pipelines item selected. In the content pane, the Create pipeline button is highlighted.](media/devops-build-pipeline-07.png 'Create Build Pipeline')

2. Select **Azure Repos Git** as your code repository.

    ![On the Connect tab of your pipeline screen, Azure Repos Git is selected beneath the Where is your code? prompt.](media/devops-build-pipeline-08.png 'Repository Source')

3. Select **mlops-quickstart** as your repository.

    ![On the Select tab of your pipeline screen, beneath the Select a repository section, the mlops-quickstart repository is selected.](media/devops-build-pipeline-09.png 'Select Repository')

4. Review the YAML file.

    The build pipeline has four key steps:

    a. Attach folder to workspace and experiment. This command creates the **.azureml** subdirectory that contains a **config.json** file that is used to communicate with your Azure Machine Learning workspace. All subsequent steps rely on the **config.json** file to instantiate the workspace object.

    b. Create the AML Compute target to run your master pipeline for model training and model evaluation.

    c. Run the master pipeline. The master pipeline has two steps: (1) Train the machine learning model, and (2) Evaluate the trained machine learning model. The evaluation step evaluates if the new model performance is better than the currently deployed model. If the new model performance is improved, the evaluate step will create a new Image for deployment. The results of the evaluation step will be saved in a file called **eval_info.json** that will be made available for the release pipeline. You can review the code for the master pipeline and its steps in **aml_service/pipelines_master.py**, **scripts/train.py**, and **scripts/evaluate.py**.

    d. Publish the build artifacts. The **snapshot of the repository**, **config.json**, and **eval_info.json** files are published as build artifacts and thus can be made available for the release pipeline.

    ![On the Review tab of your pipeline screen, the contents of azure-pipelines.yml is displayed.](media/devops-build-pipeline-10.png 'Build pipeline YAML')

### Task 2: Run the Build Pipeline

1. Select **Run** to start running your build pipeline.

    ![On the Review tab of your pipeline screen, the contents of azure-pipelines.yml is displayed. The Run button is selected from the top taskbar.](media/devops-build-pipeline-11.png 'Run Build Pipeline')

2. Monitor the build run. The build pipeline, for the first run, will take around 15 minutes to run.

    ![A build pipeline run summary screen is displayed indicating it was manually triggered. A single job is selected in the Jobs section with a status of Success.](media/devops-build-pipeline-12.png 'Monitor Build Pipeline')

3. Select **Job** to monitor the detailed status of the build pipeline execution.

    ![In the Jobs screen, the Job that was selected in the previous step is expanded displaying multiple steps. To the right a summary of the run is displayed.](media/devops-build-pipeline-13.png 'Monitor Build Pipeline Details')

### Task 3: Review Build Artifacts

1. The build will publish an artifact named `devops-for-ai`. Select **1 published** to review the artifact contents.

    ![On the build pipeline run summary, in the table outlining the manual run, the 1 published beneath the artifacts column is selected.](media/devops-build-pipeline.png 'Build Artifacts')

2. Select **outputs, eval_info.json**, and then select the download arrow. The `eval_info.json` is the output from the *model evaluation* step. The information from the evaluation step will be used in the release pipeline to deploy the model. Select the back arrow to return to the previous screen.

    ![On the Artifacts screen, a list of files are displayed. The outputs folder is expanded and the eval-info.json file download button is selected. The back arrow is selected a the top of the screen to navigate back to the previous page.](media/devops-build-pipeline-15.png 'Download JSON file')

3. Open the **eval_info.json** in a json viewer or a text editor and observe the information. The json output contains information such as if the model passed the evaluation step (**deploy_model**: **true** or **false**), and the name and id of the created image (**image_name** and **image_id**) to deploy.

    ![The contents of the eval_info.json file is displayed in Visual Studio.](media/devops-build-pipeline-16.png 'Eval Info JSON File')

### Task 4: Review Build Outputs

1. Log in to [Azure Machine Learning studio](https://ml.azure.com) either directly or via the [Azure Portal](https://portal.azure.com). Make sure you select the Azure Machine Learning workspace that you created from the notebook earlier. Open your **Models** section, and observe the versions of the registered model: **compliance-classifier**. The latest version is the one registered by the build pipeline you ran in the previous task.

    ![In Azure Machine Learning Studio, models is selected in the left menu. A list of multiple versions of the compliance-classifier model is displayed in the Model list table with the largest version of the model highlighted in the table.](media/devops-build-outputs-01.png 'Registered Models in Azure Machine Learning studio')

2. Select the latest version of your model to review its properties. The **build_number** tag links the registered model to the Azure DevOps build that generated it.

    ![The model screen for the latest version of the compliance-classifier is displayed with the Build_Number tag highlighted.](!media/../media/devops-build-outputs-02.png 'Registered model details and Build_Number tag')

3. Open your **Datasets** section and observe the versions of the registered dataset: **connected_car_components**. The latest version is the one registered by the build pipeline you have run in the previous task.

    ![In Azure Machine Learning Studio, Datasets is selected from the left menu. The Datasets screen displays a list of datasets on the Registered datasets tab. The connected_car_components dataset is selected in the table with its tag indicating the build number matching the value from the previous step.](media/devops-build-outputs-03.png 'Registered Datasets in Azure Machine Learning studio')

4. Select the latest version of your dataset to review its properties. Notice the **build_number** tag that links the dataset version to the Azure DevOps build that generated it.

    ![The registered dataset version properties screen is displayed with a tag that indicates the build_number.](medial/../media/devops-build-outputs-04.png 'Registered dataset details in Azure Machine Learning studio')

5. Select **Models** to view a list of registered models that reference the dataset.

    ![A list of registered models that reference the selected dataset is displayed.](media/devops-build-outputs-05.png 'Registered dataset model references in Azure Machine Learning studio')

6. Log in to the [Azure Portal](https://portal.azure.com), open your **Resource Group, Workspace, Images** section, and observe the deployment image created during the build pipeline: `compliance-classifier-image`.

    ![In the Images resource page, Images is selected from the left menu, and a list of Images is displayed. Multiple compliance-classifier-image images are shown with their associated versions. The latest version image is highlighted in the table.](media/devops-build-outputs-06.png 'Images in Azure Portal')
