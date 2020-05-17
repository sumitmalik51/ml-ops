## Exercise 2: Registering the model

Duration: 15 minutes

In this exercise, you explore the approaches you can take to managing the model versions, their association with Experiment Runs, and how you can retrieve the models both programmatically and via the [Azure Machine Learning studio](https://ml.azure.com).

### Task 1: Register Model using Azure Machine Learning Python SDK

1. Download the [**Register Model.ipynb**](./notebooks/Register&#32;Model.ipynb) notebook to your computer, by selecting the **Raw** view in GitHub, and then **right-click + Save as**. This is the notebook you will step through executing in this exercise.If you are not able to  redirected to the path provided in link you can go to Labguide icon provided in the Desktop of Your Virtual Machine, go to **Hands on Lab** , select **Hol step-by-step** go to the step where you are accesing the path of file and performing the steps.  


2. In the Studio, navigate to **Notebooks**, and select **Upload files** option in the top menu.

3. Browse your local computer for the downloaded notebook, **Register Model.ipynb** and then select **MCW-MLOps** as the target folder. Select **Upload**.

4. On the top bar, select the **notebooks-compute** compute instance to use to run the notebook. Select **Edit in, Jupyter** or **Edit in, JupyterLab**.

5. Follow the instructions within the notebook to complete the lab.

6. Navigate back to the [Azure Machine Learning studio](https://ml.azure.com) either directly or via the [Azure Portal](https://portal.azure.com). Make sure you select the Azure Machine Learning workspace that you created from the notebook. Open your **Models** section, and observe the **version 1** of the registered model: `compliance-classifier`.

    ![In Azure Machine Learning Studio, from the left menu, Models is selected. In the Model List, the compliance-classifier with the version of 1 is highlighted.](media/model-registry-01.png 'Registered Model: compliance-classifier')

### Task 2: Register Model from Azure Machine Learning studio

1. In  [Azure Machine Learning studio](https://ml.azure.com), open your **Models** section and select **+ Register model**.

    ![In Auzre Machine Learning Studio, Models is selected in the left menu. In the taskbar of the Model list, the + Register Model button is selected.](media/model-registry-02.png 'Register Model in Azure Machine Learning studio')
  
2. Provide the following input to the **Register a model** dialog, and then select **Register**.

    a. Name: `compliance-classifier`

    b. Description: `Deep learning model to classify the descriptions of car components as compliant or non-compliant.`

    c. Model Framework: **TensorFlow**

    d. Model Framework Version: `2.0`

    e. Model file: Select the `model.onnx` file from your local disk.

    ![The Register a Model form is displayed populated with the preceding values.](media/model-registry-03.png 'Register a model Dialog')

3. Navigate to your **Models** section, and observe the **version 2** of the registered model: **compliance-classifier**.

    ![The Model list is displayed showing two rows containing both versions of the compliance-classifier model. Version 2 of the compliance-classifier model is highlighted in the list.](media/model-registry-04.png 'Registered Model: compliance-classifier version 2')
