Right now we are passing a list of messages directly into the language model. Where does this list of messages come from? Usually, it is constructed from a combination of user input and application logic. This application logic usually takes the raw user input and transforms it into a list of messages ready to pass to the language model. Common transformations include adding a system message or formatting a template with the user input.

PromptTemplates are a concept in LangChain designed to assist with this transformation. They take in raw user input and return data (a prompt) that is ready to pass into a language model.

Let's create a PromptTemplate here. It will take in two user variables:

language: The language to translate text into
text: The text to translate
from langchain_core.prompts import ChatPromptTemplate

API Reference:ChatPromptTemplate
First, let's create a string that we will format to be the system message:

system_template = "Translate the following into {language}:"

Next, we can create the PromptTemplate. This will be a combination of the system_template as well as a simpler template for where to put the text to be translated

prompt_template = ChatPromptTemplate.from_messages(
    [("system", system_template), ("user", "{text}")]
)

The input to this prompt template is a dictionary. We can play around with this prompt template by itself to see what it does by itself

result = prompt_template.invoke({"language": "italian", "text": "hi"})

result

ChatPromptValue(messages=[SystemMessage(content='Translate the following into italian:'), HumanMessage(content='hi')])


We can see that it returns a ChatPromptValue that consists of two messages. If we want to access the messages directly we do:

result.to_messages()

[SystemMessage(content='Translate the following into italian:'),
 HumanMessage(content='hi')]