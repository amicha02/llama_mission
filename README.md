# Llama2 on a mission (In progress)



## Overview
Welcome! This repository contains a modified version of the [Llama 2](https://ai.meta.com/llama/) originally developed by Meta. This project includes the customization and systematic training of a 7B parameter Llama for field-specific prompts, just by giving the topic as an input. The [llama.cpp](https://github.com/ggerganov/llama.cpp) repository has also been used for this project to run the LLaMA model using 4-bit integer quantization on a MacBook.



<p align="center">
  <img src="llama.png" width="300"/>
</p>

# Setting it up on an Apple silicon machine:
1. /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
2. brew install cmake python@3.10 git wget
1. Create a repo named "llama2"
2. git clone https://github.com/facebookresearch/llama
3. git clone https://github.com/ggerganov/llama.cpp
   You need to convert your model from its original structure to a new one
4. Go to https://github.com/facebookresearch/llama, and request download link from the README.rd file. You'll get a link, which will allow you to download any models of your preference (f.e Llama-2-7b/13b/70b)
5. Download model and transfer it to a new folder under llama2 named meta_models. Copy the tokenizer_checklist.chk and tokenizer_model to the meta_models file
6. Run "make" under llama.ccp file
8. Using the Command Palatte in VS code to install a virtual enviroment (.venv file) and install the dependencies under llama.ccp
10. Now that our python enviroment is installed and activated, and our requirements are installed, we run the covert file. The output file that is given to this command line, under the models folder 7B/name of the model, type f 16 and then where can I find the original model. It converted the .pth file to a .bin format
- python3 -m pip install -r requirements.txt (if not already installed automatically through VS Code)
- Create a 7B directory which is meant for the 7 billion parameter models under models
- python3 convert.py --outfile models/7B/ggml-model-f16.bin --outtype f16 ../../llama2/meta_models/llama-2-7b-chat
- Go to the meta_models/*model_name* directory Change the vocabulary_size value in the params.json file from -1 to whatever the desired vocabulary size is
11. Quantize models into a smaller file size. The model which has just been converted into a .bin file and put the new one in the same folder. The output is at the order of tens of gigabites smaller than the original version.

- ./quantize  ./models/7B/ggml-model-f16.bin ./models/7B/ggml-model-q4_0.bin q4_0



## How to inference
1. Running the following command line for inference. That is the model that we are going to use for chatting(=inference). 
./main <quantized model> -n(will allow the # of tokens) <number of tokens we can respond with>
This command line above will spew alot of nonsense and some Python code too. You don't have to run this command, but it could be used to see if the model is running properly. 

- ./main -m ./models/7B/ggml-model-q4_0.bin -n 1024 --repeat_penalty 1.0 --color -i -r "User:" -f ./prompts/chat-with-bob.txt
2. This is running on the CPU. Have a Task Manager open while giving prompts, and you'll see CPU message spikes of main folder. 


# Training
..

# Customize Dataset
..