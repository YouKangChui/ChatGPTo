# ChatGPT
Reverse Engineered ChatGPT by OpenAI. Extensible for chatbots etc.

# Disclaimer
This is not an official OpenAI product. This is a personal project and is not affiliated with OpenAI in any way. Don't sue me

## Urgent help needed
- Writing tests
- More verbose error handling
- Decrecate bs4 in favor of pure requests
- Update documentation for email/password authentication (Working but needs documentation)
### Wiki is now open to all contributors

# Features
![image](https://user-images.githubusercontent.com/36258159/205534498-acc59484-c4b4-487d-89a7-d7b884af709b.png)
- No moderation
- Programmable

# Setup
## Install
`pip3 install revChatGPT --upgrade`

## Email and password authentication
```json
{
    "email": "<YOUR_EMAIL>",
    "password": "<YOUR_PASSWORD>"
}
```
Save this in `config.json` in current working directory

<details>
 <summary>Legacy authentication or if using Google Auth</summary>
Go to https://chat.openai.com/chat and log in or sign up
1. Open console with `F12`
2. Open `Application` tab > Cookies
![image](https://user-images.githubusercontent.com/36258159/205494773-32ef651a-994d-435a-9f76-a26699935dac.png)
3. Copy the value for `__Secure-next-auth.session-token` and paste it into `config.json.example` under `session_token`. You do not need to fill out `Authorization`
![image](https://user-images.githubusercontent.com/36258159/205495076-664a8113-eda5-4d1e-84d3-6fad3614cfd8.png)
4. Save the modified file to `config.json` (In the current working directory)
</details>

# Running
```
 $ python3 -m revChatGPT            

    ChatGPT - A command-line interface to OpenAI's ChatGPT (https://chat.openai.com/chat)
    Repo: github.com/acheong08/ChatGPT
    
Type '!help' to show commands
Press enter twice to submit your question.

You: !help


                !help - Show this message
                !reset - Forget the current conversation
                !refresh - Refresh the session authentication
                !exit - Exit the program
```

Refresh every so often in case the token expires.

## Installation
- Doesn't work on mac
- Tested on Linux alpine
- If you don't have Linux installed, you can try installing it with docker

# Development:
`pip3 install revChatGPT --upgrade`
```python
from revChatGPT.revChatGPT import Chatbot
import json
import requests

# Get your config in JSON
config = {
    "email": "<your_email>",
    "password": "<your_pass>"
}

prompt="Hi"

chatbot = Chatbot(config, conversation_id=None)
chatbot.reset_chat() # Forgets conversation
chatbot.refresh_session() # Uses the session_token to get a new bearer token
resp = chatbot.get_chat_response(prompt, output="text") # Sends a request to the API and returns the response by OpenAI
resp['message'] # The message sent by the response
resp['conversation_id'] # The current conversation id
resp['parent_id'] # The ID of the response

while(True):

  prompt = input("Human :")
  resp=chatbot.get_chat_response(prompt, output="text")

  print("AI : ",resp['message'])


```
This can be imported to projects for bots and much more. You can have multiple independent conversations by keeping track of the conversation_id.

# Awesome ChatGPT
[My list](https://github.com/stars/acheong08/lists/awesome-chatgpt)

If you have a cool project you want added to the list, open an issue.

# Star History

[![Star History Chart](https://api.star-history.com/svg?repos=acheong08/ChatGPT&type=Date)](https://star-history.com/#acheong08/ChatGPT&Date)
