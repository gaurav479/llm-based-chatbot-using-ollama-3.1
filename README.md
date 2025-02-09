# llm-based-chatbot-using-ollama-3.1
This is a student project code  to demonstrate setting building up a llm based chat bot using ollama 3.1

Step 1: At first we need to create an environment variable. We will install all the packages which are needed to run this project in this envrionment.to create the environment we open a new terminal and write command 
"conda create -p venv python==3.17
As a we will see that venv folder is created. In this venv folder only we will install all the packages

 Step 2 : Download ollama3.1 from ollama.com and install it. It helps to work with ollama3.1 online
After installation it can be run offline 
by writing the command
ollama run llama3.1

Step 3 : create environment variables. and after that we need to activate the environment by the command
"conda activate venv"
write these two env variable in .env file
#LANGCHAIN_API_KEY="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"
#LANGCHAIN_PROJECT="PROJECTCHATBOT"
 Here it is to be noted that langchain is free and one needs to generate their own api key from 
"https://docs.smith.langchain.com/administration/how_to_guides/organization_management/create_account_api_key"
That key needs to be used

Step 4:Now we create a new python file.In my case I created ollama.py. In that I defined the following two environment variables
#LANGCHAIN_API_KEY="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"
#LANGCHAIN_PROJECT="PROJECTCHATBOT"

Step 5 : Now we will install requirement.txt.To do this we will first create a txt file with name"requirenment.tx".In it we will write the following
langchain_openai 
langchain_core
python-dotenv
streamlit
langchain_community
langserve
 Then we will run this command in the terminal window
	"pip install -r requirenment.txt"
 and we will do this installation
Step 6 we will copy the same environment variables in .env file and in another python file named app.py

Step 7 :Get you own api key from langsmith and use it your ptyhon files(#LANGCHAIN_API_KEY) in ollama.py

Step 8 :we will now important libraries in the ollama.py file
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_community.llms import Ollama
import streamlit as st
import os
from dotenv import load_dotenv

Step 9: we then load I ollama.py
load_dotenv() 
to load environment variables

Step 10 : Now we call environment variables in the ollama.py file
os.environ["LANGCHAIN_TRACING_V2"]="true" // to start the tracing
os.environ["LANGCHAIN_API_KEY"]=os.getenv("LANGCHAIN_API_KEY")

Step 11 Now we will create the chat by following the steps.
first we will create a prompt. This prompt tells us how our chat bot will behave
we wll make two tuple
one for the system- i.e how the system will behave
second is the user.- i.e If user asks a question than what format it should be in. The following code is written in ollama.py file

## Prompt Template

prompt=ChatPromptTemplate.from_messages(
    [
        ("system","You are a helpful assistant. Please response to the user queries"),//this is the prompt  given to user
        ("user","Question:{question}") //this is the format in which the user question would be taken as input 
    ]
)
//Now we will create streamlit framework as the end to end project will be made using this.GUI part

## streamlit framework

st.title('Langchain Demo With LLAMA3.1 API')
input_text=st.text_input("Search the topic u want")
Now we write code for ollama llm call
# ollama LLAma2 LLm 
llm=Ollama(model="llama3.1")
output_parser=StrOutputParser() // it will display out put in format of string to the user


Now we will form a chain which is responsible to give response
chain=prompt|llm|output_parser
 Now the last step 
the last lines to invoke the chain when the user enters . The users question is here assigned to input.text
if input_text:
    st.write(chain.invoke({"question":input_text}))

Step 12: Now to run the chat bot write
streamlit run ollama.py
