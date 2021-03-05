# Chapter 1
## Clone the Accelleran xApp Framework Package repository

The official xApp Framework Package is located in a public repository located here: 
[https://github.com/accelleran/xapp-framework-package](https://github.com/accelleran/xapp-framework-package)

You can clone it using th following command:

```shell
git clone https://github.com/accelleran/xapp-framework-package
```

---

# Chapter 2
## Building the xApp Core Docker image
We need to first create the Docker image for the xApp core. This can be done using the following commands (assuming you are in the xapp-framework-package folder):

```shell
cd xapp_core
docker build -t <my-xapp-docker-image-name>:<tag> .
```

NOTE: You might need to use `sudo docker...` depending on the way your Docker is configured.

## Deploying the development environment

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
```

Once this is done, you can deploy the development environment (replace <dev-env-name> to whichever name you want ot give this development environment; replace <tag> with the tag used during Docker image build ):
```shell
helm install <dev-env-name> . --set developerMode.enabled=true --set developerMode.hostPath=/path/to/xapp-framework-package/xapp_core/ --set image.tag=<tag>
```

You can now access the development environment by going into the container in Kubernetes using:

```shell
kubectl exec -it <xapp-core-pod-name> -- /bin/bash
```

Finally you can start your xApp by issuing the following command inside the container:

```shell
python3 xapp_main.py
```