in this module we will setup Airflow on the VM, then create the DAG in python. 

We will setup both initial (file import) and incremental (api call to source upstream) from target api to source local database as the read-replica.  

download from Apache site

curl -LfO https://airflow.apache.org/docs/apache-airflow/2.10.0/docker-compose.yaml

open .yaml file and see volumes.  these are mapped to the docker container host drives (i.e. Codespaces storage).  These are persistent and survive a container lifecycle.

airflow/dags in the Codespace will be /opt/airflow/dags on the container Linux file system.

So, we create these in the host (Codespaces) where we will launch from:  
```mkdir -p ./dags ./logs ./plugins ./config```
```echo -e "AIRFLOW_UID=$(id -u)" > .env```

Then we will create a docker-compose.override.yaml file to override some of the std config settings from the docker-compose.yaml file.
This allows for all customizations to be kept together.
