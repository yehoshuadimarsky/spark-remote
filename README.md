# spark-remote

A painless Docker-based setup for using `databricks-connect` to develop locally against remote Spark clusters running in Databricks on [Azure](https://docs.microsoft.com/en-us/azure/databricks/dev-tools/databricks-connect) or [AWS](https://docs.databricks.com/user-guide/dev-tools/db-connect.html).

Databricks created the `databricks-connect` for this. But if you are a Windows user like me (and like 95% of the world), it can be a challenge to set up - you need to install a few things locally, which can be frustrating, not work, and time consuming:
* Java
* Python environment

I've done all the hard work for you, just use this DockerFile.

## Quickstart
* You will be using Visual Studio Code - install it and open it ([read this](https://code.visualstudio.com/docs/remote/containers))
* Install the [Remote Development Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) extension in VS Code
* Clone this repo (or your fork of it)
* Open the repo locally from within VS Code - it will prompt you to open it using the container
* Configure your credentials - see the Databricks docs
* Test by running `databricks-connect test`
* Voila! enjoy!

