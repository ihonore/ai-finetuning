## **Step-by-Step Guide to Train LLaMA 3.1 Base Model using PyTorch and unsloth on your data**

This guide will help you run and modify the Jupyter notebook for fine-tuning the LLaMA 3.1 base model, using your own local dataset. The environment (`base`) is already set up, so no need to install additional dependencies unless required.

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

1. Open the notebook Llama*3_1_8b*+\_Unsloth_2x_faster_finetuning.ipynb
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

## **Pushing the Model to Hugging Face or Ollama**

### **1. Pushing to Hugging Face Hub**

In the notebook under the section **"Saving, loading finetuned models"**, you can either push the model to the Hugging Face Hub or save it locally. To push the model to Hugging Face, you will need to uncomment the provided lines and add your Hugging Face token.

Here’s how to push the model and tokenizer to the Hugging Face Hub:

```python
# Uncomment these lines and replace "your_name/lora_model" with the name of your model
# Add your Hugging Face token in place of the "..."
model.push_to_hub("your_name/lora_model", token="your_huggingface_token")  # Push the model
tokenizer.push_to_hub("your_name/lora_model", token="your_huggingface_token")  # Push the tokenizer
```

### **2. Pushing to Ollama**

To push the model to Ollama, follow these steps:

1. Convert the model to GGUF format: First, convert the fine-tuned model to the GGUF format using the section **"GGUF / llama.cpp Conversion"** in the notebook.

In the notebook, you'll find these lines that allow you to save the GGUF model locally or push it to Hugging Face in GGUF format. Replace `False` with `True` in the code for the actions you want to perform.

**For example**:

```python
# Save the GGUF model locally
if True:
    model.save_pretrained_gguf("model", tokenizer, quantization_method="f16")

# Push the GGUF model to Hugging Face
if True:
    model.push_to_hub_gguf("hf/model", tokenizer, quantization_method="f16", token="your_huggingface_token")
```

2. Edit the Modelfile for Ollama:

- Locate the Modelfile in the Downloads folder.
- Open the Modelfile in VsCode and edit the `FROM` path to point to your new GGUF model directory. For example:

```bash
FROM /home/username/Downloads/model/gguf_model_name.gguf
```

3. **Push the model to Ollama**: After editing the Modelfile, open the terminal in the `Downloads` directory and run the following command to create the model in Ollama:

```bash
ollama create -f Modelfile rtila/name_of_the_model
```

By following these steps, you can successfully push your model either to Hugging Face or Ollama after fine-tuning.
