Serving with LangServe
Now that we've built an application, we need to serve it. That's where LangServe comes in. LangServe helps developers deploy LangChain chains as a REST API. You do not need to use LangServe to use LangChain, but in this guide we'll show how you can deploy your app with LangServe.

While the first part of this guide was intended to be run in a Jupyter Notebook or script, we will now move out of that. We will be creating a Python file and then interacting with it from the command line.

Install with:

pip install "langserve[all]"

Server
To create a server for our application we'll make a serve.py file. This will contain our logic for serving our application. It consists of three things:

The definition of our chain that we just built above
Our FastAPI app
A definition of a route from which to serve the chain, which is done with langserve.add_routes

And that's it! If we execute this file:

python serve.py

we should see our chain being served at http://localhost:8000.

Playground
Every LangServe service comes with a simple built-in UI for configuring and invoking the application with streaming output and visibility into intermediate steps. Head to http://localhost:8000/chain/playground/ to try it out! Pass in the same inputs as before - {"language": "italian", "text": "hi"} - and it should respond same as before.

Client
Now let's set up a client for programmatically interacting with our service. We can easily do this with the langserve.RemoteRunnable. Using this, we can interact with the served chain as if it were running client-side.

from langserve import RemoteRunnable

remote_chain = RemoteRunnable("http://localhost:8000/chain/")
remote_chain.invoke({"language": "italian", "text": "hi"})

'Ciao'

