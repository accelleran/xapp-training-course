# Module 2: Developing your first xApp

# Chapter 2.1: Setting the environment
## Clone the Accelleran xApp Framework Package repository
The official xApp Framework Package is located in a public repository located here: 
[https://github.com/accelleran/xapp-framework-package](https://github.com/accelleran/xapp-framework-package)

You can clone it using th following command:

```shell
git clone https://github.com/accelleran/xapp-framework-package
```


# Chapter 2.2: Building and deploying an xApp
## Building the Development xApp Core Docker image
We need to first create the Docker image for the xApp core. This can be done using the following commands (assuming you are in the xapp-framework-package folder):

```shell
cd xapp_core
docker build --target dev --tag <my-xapp-docker-image-name>:<tag> .
```

NOTE 1: You might need to use `sudo docker...` depending on the way your Docker is configured.

NOTE 2: We are using the "dev" target in the Dockerfile, which enables Developer options in the xApp docker image, which we use in these exercises. 

## Preparing the values.yaml for the Helm chart

While in the phase of developing an xApp, we have created a development environment which a developer can use for quick development and testing.
The development environment is deployed using Helm. 

We first have to edit the *values.yaml* file of the Helm chart. Assuming you are in the xapp-framework-package root folder:

```shell
cd helm_chart/xapp
vi values.yaml
```

There are two fields that we should edit:

```yaml
global:
  # THIS SHOULD BE REPLACED WITH THE KUBERNETES IP
  kubeIp: "10.55.1.2" 
  
image:
  # THIS SHOULD BE REPLACE WITH <my-xapp-docker-image-name> WE USED DURING DOCKER IMAGE BUILD
  repository: <my-xapp-docker-image-name> 
  ...
  # REPLACE THIS WITH TH EVERSION TAG USED DURING DOCKER IMAGE BUILD
  tag: ""
```

## Deploying the development environment

Once this is done, you can deploy the development environment (replace <dev-env-name> to whichever name you want to give this development environment):
```shell
helm install <dev-env-name> . --set developerMode.enabled=true --set developerMode.hostPath=/path/to/xapp-framework-package/xapp_core/
```

NOTE: The path to the xapp_core folder is an absolute path!

## Accessing the development environment

You can now access the development environment by going into the container in Kubernetes using:

```shell
kubectl exec -it <xapp-core-pod-name> -- /bin/bash
```

## Start the xApp in the development environment

Finally you can start your xApp by issuing the following command inside the container:

```shell
python3 xapp_main.py
```

# Chapter 2.3: Development workflow

Edit the processor.py file in the xapp_core to enable Example 1:

```python
### Example 1: Just logging all the messages received from the dRAX Databus
logging.info("Received message from dRAX Databus!")
logging.info("dRAX Databus message: {data}".format(data=data))
```

Restart the xApp by running the xapp_main.py again:

```shell
python3 xapp_main.py
```
