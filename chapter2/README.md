Notice that the response from the model is an AIMessage. This contains a string response along with other metadata about the response. Oftentimes we may just want to work with the string response. We can parse out just this response by using a simple output parser.

We first import the simple output parser.

from langchain_core.output_parsers import StrOutputParser

parser = StrOutputParser()

API Reference:StrOutputParser
One way to use it is to use it by itself. For example, we could save the result of the language model call and then pass it to the parser.

result = model.invoke(messages)

parser.invoke(result)

'Ciao!'