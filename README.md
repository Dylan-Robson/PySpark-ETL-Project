PySpark Databricks Project
=======

---
This Project is designed to show the ability of using databricks-connect and PySpark together to create an environment 
for developing  Spark Applications both locally or submitting it to a remote cluster.

This Project addresses the following topics:
- Best practices for Structuring ETL Code for easily testing and debugging
- How to install and setup `databricks-connect` on your local machine
- How to handle dependencies via modules and packages within your project
- Performing a "worthwhile" test on the ETL Job

---

## PySpark Project Structure
The project structure is simple as seen below:
``` bash
root/
|-- configs/
|   |-- job_configs.json
|-- dependencies/
|   |-- logging.py
|   |-- spark.py
|-- jobs/
|   |-- spark_etl_job.py
|-- tests/
|   |-- test_data/
|   |-- |-- products/
|   |-- |-- products_reports/
|   |-- test_spark_etl.py
|   build_dependents.sh
|   packages.zip
|   Pipfile
|   Pipfile.lock
```

The main entry point to this project is contained in the `spark_etl_job.py`. This is the module that will be sent to the
cluster. External configuration parameters that are required by the main module are stored in a JSON file within 
`configs/job_configs.json`. All other modules that support the main module are kept in the `dependencies` folder. 
Found in the projects root there is an included `build_dependents.sh` which is a bash script for building the dependencies
and package those built out dependencies into a zip-file. This allows for the dependencies to be sent to the cluster via
the `packages.zip` folder. Unit testing and corresponding modules are stored in the `tests`
folder. This allows for performing small chunks of input and output data that are used with the tests, which are kept in
`tests/test_data` folders.

___
## Getting Started

When building this project I wanted to provide a way for users that aren't working within a
UNIX based OS to (_Windows OS_) to have an easy and straightforward way to deploy a Spark App. I spent countless hours
searching and searching for an easier way to access Spark Clusters on my workstation, as well as utilize a remote Azure 
Databricks cluster. Why Databricks you say? Well to keep it short and sweet, dealing with setting up a local Spark Cluster
is a pain and if you or the company you work with want to save time and brain power Databricks is the way to go. More on
[Databricks](https://databricks.com/documentation) can be found via the link provided.

So where do we begin? How about dealing with something that is a bit of a nuisance as a Windows User. That is the
winutils.exe which is apart of hadoop and **needed** for Spark to work appropriately on Windows. 

### Winutils
Open Powershell as administrator and within the console type the following:
- ```New-Item -Path "C:\Hadoop\Bin" -ItemType Directory -Force```

This will create the directory the `winutils.exe` will be stored in.

Next grab the `winutils.exe` from the github repo using the following:
- `Invoke-WebRequest -Uri https://github.com/steveloughran/winutils/raw/master/hadoop-2.7.1/bin/winutils.exe -OutFile "C:\Hadoop\Bin\winutils.exe"`

What we do here is use powershell to pull the `winutils.exe` from github and install it within the directory we created
in the step above.
  
Finally we will create an Environment Variable and set `HADOOP_HOME` to the path of the Directory we created at the start:
- `[Environment]::SetEnvironmentVariable("HADOOP_HOME", "C:\Hadoop", "Machine")`

We now have installed the needed `winutils.exe` and created an Environment variable based on the path to where it is stored
on our local machine.

### Databricks-connect & PySpark
Setting up PySpark is essentially done via the `databricks-connect` setup process since with this library it installs
PySpark within the library itself (more on this later).

First we need to create a new environment that will be used to manage all project dependencies and the overall Python Environment.
We will be using [pipenv](https://docs.pipenv.org/) as our 'Project Manager' (similar to a venv or conda env). This helps ensure that any changes
or packages used while developing the Spark Application are described within the `Pipfile`. Their corresponding downstream
dependencies are described in the `Pipfile.lock`.

Install `pipenv` if you haven't done so using:
- `pip install pipenv`

If you are on macOS or Linux you can use Homebrew instead:
- `brew install pipenv`

Now that we have setup `pipenv` within your console/terminal migrate to where the directory resides for the cloned repo.
- `cd path/to/dir`

Run the following in console/termial to install the projects dependencies:
- `pipenv install --dev`

This will install **ALL** the required dependencies for both the overall project as well as the development dependencies.
Before running the above in CLI/Terminal make sure that you set the `databricks-connect` module equal to the version your
Databricks Cluster is running. To find out what runtime version is running on you Databricks cluster head to your cluster
and look for the **Databricks Runitme Version**. 

.

![Runtime Version](https://i.imgur.com/tYA6QLQ.png)

Once you have found your specific runtime ensure that your `Pipfile` reflects that runtime.








