## Exercise 1: Creating and evaluating compliance classification models

Duration: 40 minutes

In this exercise, you create a model for classifying component text as compliant or non-compliant. This tutorial uses the cloud notebook server in your Azure Machine Learning workspace for an install-free and pre-configured experience, available in Azure Machine Learning studio.

> **Note:** The new [Azure Machine Learning studio](https://ml.azure.com) provides a new immersive experience for managing the end-to-end machine learning lifecycle. You can use it either by logging in directly to it or by selecting the **Try the new Azure Machine Learning studio, Launch now** option in the **Overview** section of your Azure Machine Learning workspace.

### Task 1: Setup the notebooks environment

1. Download the [**Deep Learning with Text.ipynb**](./notebooks/Deep&#32;Learning&#32;with&#32;Text.ipynb) notebook to your computer, by selecting the **Raw** view in GitHub, and then **right-click + Save as**. This is the notebook you will step through executing in this lab.If you are not able to  redirected to the path provided in link you can go to Labguide icon provided in the Desktop of Your Virtual Machine, go to **Hands on Lab** , select **Hol step-by-step** go to the step where you are accesing the path of file and performing the steps.  

2. Sign in to [Azure Machine Learning studio](https://ml.azure.com).

3. Select your subscription and the workspace you have available.

4. Select **Notebooks** on the left navigation pane.

    ![In Azure Machine Learning Studio, Notebooks is selected from the left navigation pane.](media/notebook-00.png 'Open notebooks in Azure Machine Learning Studio')

5. Open the root folder under the **User files** section. It should be named as the currently logged user name. Select the option to **Create folder** in the top menu.

    ![On the Notebooks screen, the current user is selected beneath the User Files section, and the Create Folder icon is highlighted in the top toolbar.](media/notebook-01.png 'Create new notebooks folder')

6. Fill in the folder name: `MCW-MLOps`.

7. Select the **Upload files** option in the top menu.

    ![On the Notebooks screen, beneath user files, the folder of the current user is expanded displaying the folder that was created in the previous step. The Upload files icon is highlighted in the top toolbar.](media/notebook-02.png 'Upload notebook to the workspace file share')

8. Browse for the downloaded notebook, **Deep Learning with Text.ipynb** and then select **MCW-MLOps** folder as the target folder. Select **Upload**.

9. Select the notebook. Select **+ New Compute** to create the compute instance VM.

    ![On the Notebooks screen, beneath user files, the folder of the current user is expanded along with the folder that was created in step 6. Inside this folder the Notebook that we uploaded in the previous step is displayed and is selected. On the Compute screen to the right, the + New Compute button is highlighted in the top taskbar.](media/notebook-03.png 'Create new compute instance')

10. Provide the necessary data for creating a new compute instance to run on your notebooks.

    a. Compute name: `notebooks-compute`. When you create a VM, provide a name. The name must be between 2 to 16 characters. Valid characters are letters, digits, and the - character, and must be unique across your Azure subscription, you can add your deployment id associated with your Machine Learning Workspace and a six digit unique number while creating Compute instance.

    b. Virtual Machine size: **Standard_D3_v2**.

    c. Then select **Create**. It can take approximately 5 minutes to set up your VM.

    ![The New Compute Instance form is displayed populated with the preceding values.](media/computeinstance.png 'Configure the new compute instance')

    > **Note**: Once the VM is available it will be displayed in the top toolbar. You can now run the notebook either by using **Run all** in the toolbar, or by using **Shift+Enter** in the code cells of the notebook.

11. Having selected the uploaded **Deep Learning with Text.ipynb** notebook, select the **Edit in** drop down on the far right, then select **Jupyter** or **JupyterLab**. The new browser window will be opened.

    ![On the Notebooks screen, the Deep Learning with Text Notebook is selected. On the Compute screen to the right, a drop down list shows the compute currently running for the notebook, and in the taskbar the Edit In option is expanded with the options Edit in Jupyter and Edit in JupyterLab.](media/notebook-05.png 'Edit the notebook in Jupyter')

12. Select **Python 3.6 - Azure ML** if you are asked to select a Kernel.

    ![A Kernel not found dialog is displayed with Python 3.6 - Azure ML selected from a drop down list. A Set Kernel button is available to confirm the kernel selection.](media/notebook-06.png 'Select Kernel version')

### Task 2: Create the classification model using a notebook

1. Follow the instructions within the notebook to complete the lab.

2. Back to the [Azure Machine Learning Studio](https://ml.azure.com), in **Notebooks**, under the **MCW-MLOps** folder, navigate to the **model** folder and download the **model.onnx** file to your local disk. We will use the downloaded model file in the next exercise.

   > **Note**: If the downloaded file name is changed to **utf-8 model.onnx** or **notebooks_model_model.onnx**, then rename the file back to `model.onnx`.

   > **Note**: The **model.onnx** file is generated during the execution of the notebook at the previous step (step 1). When running the notebook, make sure the execution is successful, and the file is correctly created.
