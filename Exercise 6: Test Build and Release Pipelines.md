
## Exercise 6: Test Build and Release Pipelines

Duration: 30 minutes

### Task 1: Make Edits to Source Code

1. Navigate to: **Repos -> Files -> scripts -> `train.py`**.

2. **Edit** `train.py`.

3. Change the **learning rate (lr)** for the optimizer from **0.1** to **0.001**.

4. Change the number of training **epochs** from **3** to **5**.

5. Select **Commit**.

    ![In Azure DevOps, the Repos item is expanded in the left menu with Files selected. In the file list, beneath the expanded scripts folder, train.py is selected. The train.py contents is displayed with the source code changes indicated in the previous steps in place. The Commit button is selected in the top toolbar.](media/devops-test-pipelines-01.png 'Edit Train.py')

6. Provide comment: `Improving model performance: changed learning rate.` and select **Commit**.

    ![On the Commit dialog, the comment above is entered and the Commit button is selected.](media/devops-test-pipelines-02.png 'Commit - Comment')

### Task 2: Monitor Build Pipeline

1. Navigate to **Pipelines, Pipelines**. Observe that the CI build is triggered because of the source code change.

   ![In Azure DevOps, Pipelines is selected below the Pipeline item in the left menu. In the Pipelines list, the Recent tab is selected. A currently running pipeline is shown and selected in this list.](media/devops-test-pipelines-03.png 'Pipelines - pipelines')

2. Select the pipeline run and monitor the pipeline steps. The pipeline will run for 18-25 minutes. Proceed to the next task when the build pipeline successfully completes.

   ![In the Job details screen, the progress of the pipeline run is shown. Every step shows success.](media/devops-test-pipelines-04.png 'Build Pipeline Steps')

### Task 3: Monitor Release Pipeline

1. Navigate to **Pipelines, Releases**. Observe that the Release pipeline is automatically triggered upon successful completion of the build pipeline. Select as shown in the figure to view pipeline logs.

   ![In Azure DevOps, on the left menu, Pipelines is expanded and the Releases item is selected. The ml-ops-quickstart-release screen is displayed with the Releases tab selected. A release named Release-1 is highlighted with a button in the Stage column that is used to view the pipeline logs.](media/devops-test-pipelines-05.png 'Pipelines - Releases')

2. The release pipeline will run for about 15 minutes. Proceed to the next task when the release pipeline successfully completes.

### Task 4: Review Release Pipeline Outputs

1. From the pipeline logs view, select **Deploy and Test Webservice** task to view details.

    ![In the Release-1, Deploy and Test Stage results, A list of tasks related to Agent job is displayed. The Deploy and Test Webservice task is selected from the list.](media/devops-test-pipelines-06.png 'Pipeline Logs')

2. Observe the **Scoring URI** and **API Key** for the deployed webservice. Please note down both the **Scoring URI** and **API Key** for **Exercise 8**.

    ![The Deploy and Test Webservice task logs are displayed. Within the logs the Webservice URI and Webservice API Key are highlighted.](media/devops-test-pipelines-07.png 'Deploy and Test Webservice Task Logs')

3. Log in to Azure Machine Learning studio. Open your **Endpoints** section, and observe the deployed webservice: **compliance-classifier-service**.

    ![In Azure Machine Learning Studio, the Endpoints item is selected from the left menu. In the list of Endpoints, the compliance-classifier-service is selected.](media/devops-test-pipelines-08.png 'Azure Machine Learning studio - Workspace, Deployments')
