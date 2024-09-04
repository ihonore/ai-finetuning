# **Step-by-Step Guide to Train LLaMA 3.1 Base Model using PyTorch**

This guide will help you run and modify the Jupyter notebook for fine-tuning the LLaMA 3.1 base model, using your own local dataset. The environment (`base`) is already set up, so no need to install additional dependencies.

## **Step 1: Open the Downloads Folder in VS Code**

1. Launch **Visual Studio Code**.
2. Navigate to the Downloads folder where the notebook file `Llama_3_1_8b_+_Unsloth_2x_faster_finetuning.ipynb` is located.
   
   You can do this by clicking **File > Open Folder** and selecting the `Downloads` folder or by running the following command in the terminal to open VS Code in that folder:

   ```bash
   code /home/{{username}}/Downloads/
   ```
## **Step 2: Activate the Virtual Environment (base)**

activate the myenv environment in the terminal. You can do this within the VS Code terminal or an external terminal, You can also switch environments in VS Code editor:

From the termal run:

  ```bash
  conda activate base
  ```

## **Step 3: Open the Jupyter Notebook in VS Code**

1. Open the notebook Llama_3_1_8b_+_Unsloth_2x_faster_finetuning.ipynb
2. You should be able to see the notebook interface and the code cells. If you don't see it as a notebook, VS Code might prompt you to install the Jupyter extension.

## **Step 4: Modify the Dataset to Use Your Local Dataset**

In the notebook, Data Prep Section, you will find a line where the dataset is loaded as follows:
`dataset = load_dataset("yahma/alpaca-cleaned", split="train")`

You can replace that with any dataset from huggingface or other sources.

To load a local dataset, Replace the above line with the following code to load your own local dataset forexample `rtilaDataset.json` from the Downloads folder:

`dataset = load_dataset("json", data_files="/home/username/Downloads/rtilaDataset.json", split="train")
`

Ensure that you replace /home/username with your actual Linux username.

## **Step 5: Run the Notebook Cell by Cell**

1. Start running the notebook cell by cell. You can do this by selecting each cell and clicking the `Run` button or using `Shift + Enter` to execute the cells sequentially.

2. As you execute the cells, the notebook will load the model, preprocess the dataset, and start the fine-tuning process using the provided configurations.