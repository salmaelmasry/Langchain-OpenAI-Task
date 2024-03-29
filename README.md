# -*- coding: utf-8 -*-
"""main.ipynb

Automatically generated by Colaboratory.

Original file is located at
    https://colab.research.google.com/drive/1EYWj76r6uLfg9CSiL_IH2sCH6Yg3Sis2
"""

!pip install -qU \
    langchain==0.0.227 \
    openai==0.27.8

import os

os.environ['OPENAI_API_KEY'] = 'fdfccbb206f34e3baa7a1a32553dc672'
os.environ['OPENAI_API_TYPE'] = 'azure'
os.environ['OPENAI_API_VERSION'] = '2023-03-15'
os.environ['OPENAI_API_BASE'] = 'https://healthgpt-openai-eslsca-gradproject.openai.azure.com/'

from langchain.chat_models import AzureChatOpenAI

llm = AzureChatOpenAI(

    deployment_name="gpt-35-turbo",
    model_name="gpt-35-turbo",
    openai_api_key=os.environ['OPENAI_API_KEY'],  # Add this line to pass the API key
    openai_api_type=os.environ['OPENAI_API_TYPE'],
    openai_api_version=os.environ['OPENAI_API_VERSION'],
    openai_api_base=os.environ['OPENAI_API_BASE']

)

from langchain.schema import (
    SystemMessage,
    HumanMessage,
    AIMessage
)

messages = [
    SystemMessage(content="You are ExpertGPT, an AGI system capable of " +
                          "anything except answering questions about cheese. " +
                          "It turns out that AGI does not fathom cheese as a " +
                          "concept, the reason for this is a mystery.")
]

messages.append(
    HumanMessage(
        content="Hey how are you doing today? What is the meaning of life?"
    )
)

"""And get a response:"""

res = llm(messages)
res

"""We then add this response to our `messages` to continue the conversation:"""

messages.append(res)

"""And continue chatting:"""

messages.append(
    HumanMessage(
        content="Can you give me one concrete example of one of these interpretations?"
    )
)

res = llm(messages)
res

messages.append(res)

messages.append(
    HumanMessage(
        content="Thanks! What color is cheese?"
    )
)

res = llm(messages)
res

# Existing code ...

# Ask the user for input
user_prompt = input("You: ")

# Add user's input to the messages
messages.append(HumanMessage(content=user_prompt))

# Get the response
res = llm(messages)

# Display the response
print("AI: " + res.content)

# Add the AI's response to messages
messages.append(res)

# Continue the conversation with more user inputs if needed
# For example:
user_prompt = input("You: ")
messages.append(HumanMessage(content=user_prompt))

res = llm(messages)
print("AI: " + res.content)
messages.append(res)

# Continue the conversation as needed...

# End of the code

"""---"""
