# alpaca-discord
A Simple Discord Bot for the Alpaca LLM

# Alpaca Discord Bot README

## Overview
Alpaca-Discord is a software project for running the Alpaca (or LLaMa) Large Language Model as a discord bot. The bot is designed to run locally on a PC with as little as 10GB of VRAM. The bot listens for messages mentioning its username, processes the message content, and generates a response based on the input.
Added support for simply DM'ing the bot for private conversations. Simply message and it will respond.

I am definitely open to Pull Requests and other contributions if anyone who likes the bot wants to collaborate on adding new features, making it more robust, etc.

Example:
![image](https://user-images.githubusercontent.com/127238744/226094603-5f4a1291-6af6-435a-b6b0-f9bfce21dabe.png)


## Dependencies
You must have either the LLaMa or Alpaca model (or theoretically any other fine tuned LLaMa based model) in HuggingFace format.
Please see this github gist page on pre-requisites and other information to get and use Alpaca: https://gist.github.com/teknium1/c022705857ba943fb2b7e4470d8677fb

To run the bot, you need the following Python packages:
- `discord`
- `transformers`
- `torch`

You can install discord using pip:

`pip install discord`

Currently, Transformers module only has support for Llama through the latest github repository, and not through pip package. Install it like so:

`pip install git+https://github.com/huggingface/transformers.git`

For Pytorch you need to install it with cuda enabled. See here for commands specific to your environment: https://pytorch.org/get-started/locally/

## How the bot works
The bot uses the `discord.py` library for interacting with Discord's API and the `transformers` library for loading and using the Large Language Model.

1. It creates a Discord client with the default intents and sets the `members` intent to `True`.
2. It loads the Llama tokenizer and Llama model from the local `./alpaca/` directory.
3. It initializes a queue to manage incoming messages mentioning the bot.
4. It listens for messages and adds them to the queue if the bot is mentioned.
5. It processes the queue to generate responses based on the text.
6. It sends the generated response to the channel where the original message was sent. 

[todo] Implement memory capabilities, particularly if it is replied to, so that it will know what message of it's your replying to in-context

[todo] Implement pre-made characters/personalities/modalities?

## How to run the bot
1. Ensure you have the required dependencies installed.
2. Create a Discord bot account and obtain its API key. Save the key to a file named `alpacakey.txt` in the same directory as the bot's script.
3. Make sure the Llama tokenizer and Llama model are stored in a local `./alpaca/` directory.
Your alpaca directory should have all of these files:  
![image](https://user-images.githubusercontent.com/127238744/226094774-a5371a98-947b-47a4-a4b2-f56e6331ee1e.png)  
4. Run the script using Python:
`python alpaca_bot.py`
5. Invite the bot to your Discord server.
6. Mention the bot in a message to receive a response generated by the Large Language Model.

## Customization options
You can customize the following parameters in the script to change the behavior of the bot:

- `load_in_8bit`: Set to `True` if you want to load the model using 8-bit precision.
- `device_map`: Set to `"auto"` to automatically use the best available device (GPU or CPU).
- `max_new_tokens`: Set the maximum number of new tokens the model should generate in its response.
- `do_sample`: Set to `True` to use sampling instead of greedy decoding for generating the response.
- `repetition_penalty`: Set a penalty value for repeating tokens. Default is `1.0`.
- `temperature`: Set the sampling temperature. Default is `0.8`.
- `top_p`: Set the cumulative probability threshold for nucleus sampling. Default is `0.75`.
- `top_k`: Set the number of tokens to consider for top-k sampling. Default is `40`.

## Credits, License, Etc.
While my repo may be licensed as MIT, the underlying code, libraries, and other portions of this repo may not be. Please DYOR to check what can
and can't be used and in what ways it may or may not be. If anyone can help me with proper attributions or licensing placement, please submit a PR

This would not be possible without the people of Facebook's Research Team: FAIR, and with Stanford's Research:
<pre>
@misc{alpaca,
  author = {Rohan Taori and Ishaan Gulrajani and Tianyi Zhang and Yann Dubois and Xuechen Li and Carlos Guestrin and Percy Liang and Tatsunori B. Hashimoto },
  title = {Stanford Alpaca: An Instruction-following LLaMA model},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/tatsu-lab/stanford_alpaca}},
}
</pre>

@Ristellise - https://github.com/Ristellise - For converting the code to be fully async and non-blocking

@Main - https://twitter.com/main_horse - for helping with getting the initial inferencing code working

You can find me on Twitter - @Teknium1 - https://twitter.com/Teknium1

Final thanks go to GPT-4, for doing much of the heavy lifting for creating both the original discord bot code, and writing a large portion of this readme! 
