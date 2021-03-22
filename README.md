PySpark Databricks Project
=======

---
## Features
This project provides a sample of databricks-connect PySpark applications with best practices and usability in mind.

This is project is designed to provide:
- Local IDE Development & Debugging
- Testing code with Pytest
- Structuring for PySpark Applications
- Packaging and Submitting to Cluster with Wheel
- Cl Building for deploying to Databricks Clusters

---

## Setup
Clone the repo to your desktop and open Windows Command Line Interface.

Create a Conda Environment:

``conda create --name dbconnectguide python=3.7``

For information on conda please use the provided link:
[Conda Docs](https://docs.conda.io/projects/conda/en/latest/)

Activate the newly created environment:

```conda activate dbconnectguide```

**IMPORTANT**: Open the requirements.txt file located in the projects root folder and ensure that the databricks-connect version matches your cluster's runtime!

Install requirements.txt to your Envrionment:

```pip install -r requirements.txt```

Setup databricks-connect:
```databricks-connect configure```

For information on setting up databricks-connect refer to the official documentation:
[Databricks Connect Docs](https://docs.databricks.com/dev-tools/databricks-connect.html)

Now from within the IDE of your choice open the cloned repo and configure your interpreter settings.
Choose the newly created conda environment as your interpreter.


.
![Interpreter Settings](https://i.imgur.com/taGsjSV.png)

---

## License
This is an open source repo and should be considered as so.
