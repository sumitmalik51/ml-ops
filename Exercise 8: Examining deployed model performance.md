## Exercise 8: Examining deployed model performance

Duration: 15 minutes

In this exercise, you learn how to monitor the performance of a deployed model.

### Task 1: Activate App Insights and data collection on the deployed model

1. Download the [**Model Telemetry.ipynb**](./notebooks/Model&#32;Telemetry.ipynb) notebook to your computer, by selecting the **Raw** view in GitHub, and then **right-click + Save as**. This is the notebook you will step through executing in this exercise.

2. In the Azure Machine Learning Studio, navigate to **Notebooks**, and select **Upload files** option in the top menu.

3. Browse your local computer for the downloaded notebook, **Model Telemetry.ipynb** and then select **MCW-MLOps** folder as the target folder. Select **Upload**.If you are not able to  redirected to the path provided in link you can go to Labguide icon provided in the Desktop of Your Virtual Machine, go to **Hands on Lab** , select **Hol step-by-step** go to the step where you are accesing the path of file and performing the steps.

4. On the top bar, select the **notebooks-compute** compute instance to use to run the notebook. Select **Edit in, Jupyter** or **Edit in, JupyterLab**.

5. Follow the instructions within the notebook to complete the task. When finished, your deployed model has now both [Application Insights](https://docs.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview) integration and data collection activated.

6. Note that if there are errors (for example, **Too many requests for service compliance-classifier-service (overloaded)** or **No ready replicas for service compliance-classifier-service.**) when you make calls against the deployed web service after your enable app insights (last cell in the **Model Telemetry** notebook), you should wait for 5 minutes and rerun the cell to make the calls.

### Task 2: Check Application Insights telemetry

1. Navigate to the [Azure portal](https://portal.azure.com) and locate the resource group you created for this lab (the one where the Azure Machine Learning service workspace was created in).

2. Locate the Application Insights instance in the resource group and select it.

    ![The Application Insights resource is selected in the resource group.](media/model-telemetry-01.png 'Resource Group Overview')

3. Go to **Overview**.

4. From the top row of the right section, select **Logs**. This will open the Application Insights query editor with an empty new query.

    ![On the Application Insights resource screen, the Overview item is selected in the left menu, and the Logs item is selected from the top toolbar.](media/model-telemetry-02.png 'Application Insights - Dashboard')

5. In the left pane, make sure the **Schema** tab is selected.

6. Hover over **requests** and select the icon on the right side - "Show sample records from this table".

    ![On the Application Insights Logs screen, a New Query tab is shown with the Tables tab selected. The icon next to the requests table is selected.](media/model-telemetry-03.png 'Create Requests Query')

7. Look at the results displayed. Application Insights is tracing all requests made to your model. Sometimes, a couple of minutes are needed for the telemetry information to propagate. If there are no results displayed, wait a minute. Call your model wait a minute and select **Run** to re-execute the Application Insights query.

   ![On the Application Insights Logs screen, a query is run against the requests table and a list of results is displayed.](media/model-telemetry-04.png 'Requests Query Results')

> **Note**: If you do not see telemetry information after selecting **Run** to re-execute the Application insights query. Please rerun the last cell in the **Model Telemetry** notebook a few more times to generate more data. Then select **Run** on this page to re-execute the Application insights query.

### Task 3: Check the data collected

1. Navigate to the [Azure portal](https://portal.azure.com) and locate the resource group you created for this lab (the one where the Azure Machine Learning service workspace was created in).

2. Locate the Storage Account instance in the resource group and select it.

    ![The Storage account resource is selected in the resource group.](media/model-telemetry-05.png 'Resource Group Overview')

3. Go to **Storage Explorer (preview)**.

4. Expand the **BLOB CONTAINERS** section and identify the **modeldata** container. Select **More->Refresh** if you do not see **modeldata** container.

    ![In the Storage Explorer screen, the BLOB CONTAINERS item is expanded with the modeldata item selected.](media/model-telemetry-06.png 'Storage Explorer')

5. Identify the CSV files containing the collected data. The path to the output blobs is based on the following structure:

    **modeldata -> subscriptionid -> resourcegroup -> workspace -> webservice -> model -> version -> identifier -> year -> month -> day -> inputs.csv**

    ![In the Storage Explorer, the modeldata container is selected beneath BLOB containers. The inputs.csv file is selected in the list of files at the path specified above.](media/model-telemetry-07.png 'Storage Explorer - inputs.csv')
