# Module 7: Productizing an xApp

# Chapter 7.1: Packaging the xApp

## Build the Production xApp Core Docker image

First we need to build the xApp core Docker image, now using the "prod" target. We can use the following docker command:

```shell
docker build --target prod --tag <image-name>:<image-version> /path/to/xapp-framework-package/xapp_core/
```

### Saving the xApp Core Docker image

```shell
docker save -o example-xapp-0.1.0.tar example-xapp:0.1.0
```

### Load the xApp Core Docker image

```shell
docker load -i example-xapp-0.1.0.tar
```

### Pushing the xApp Core Docker image

First we need to tag the local image with the remote repository location:

```shell
docker image tag example-xapp:0.1.0 registry-host:5000/myname/example-xapp:0.1.0
```

And then we can push the image:

```shell
docker image push registry-host:5000/myname/example-xapp:0.1.0
```

## Package the Helm chart

We can package th eHelm chart into a .tgz file using:

```shell
helm package /path/to/xapp-framework-package/helm_chart/xapp/
```

# Chapter 7.2: Deploying a production xApp

We can either use the dRAX Dashboard and the user-friendly GUI interface.

Or we can use the dRAX API Gateway to deploy an xApp in a programatic way:

```shell
curl -X POST "http://10.55.1.2:31315/api/deploy/xapp" -H "accept: application/json" -H "Content-Type: multipart/form-data" -F 'xAppForm={"xAppName":"example-xapp","organization":"Accelleran","team":"dRAX","version":"0.1.0","owner":"dRAX","method":"Upload Helm Chart","namespace":"default"}' -F "file=@/home/ad/xapp-training-course/xapp-0.1.0.tgz;type=application/x-compressed-tar" -F "values=@/home/ad/xapp-training-course/values.yaml;type=application/x-yaml"
```

The parameters are:
- 10.55.1.2 - Is the Kubernetes IP
- example-xapp - is the xApp name
- Accelleran - is the organisation 
- dRAX - is the team
- 0.1.0 - is the version of the xApp
- Owner - the owner of the xApp
- Upload Helm Chart/Remote Helm Repository - specifies whether we are uploading a helm .tgz package or using a remote Helm repository
- If a .tgz helm package file is used, then @/home/dimitris/Desktop/5g_logs/xapp-hello-world-0.1.0.tgz specifies the location of the .tgz helm package
- If a remote helm repository is used, then https://accelleran.github.io/xapp-hello-world/ is the URL to the remote repository
- If a remote helm repository is used, then xapp-hello-world is the name of the helm chart in the remote repository
- If a remote helm repository is used, then example-repo-name is the generic name used to save the repository URL in helm
- Finally, @/home/dimitris/Desktop/5g_logs/values.yaml specifies where the optional values.yaml file is located

## Deleting an xApp

This can also be done through the dRAX Dashboard by clicking the *Uninstall* button in the xApps tab.

Or using the dRAX API Gateway:

```shell
curl -X PUT -H "accept: application/json" -H "Content-Type: application/json" -d '{"name":"accelleran-drax-example-xapp-010", "namespace":"default"}' http://10.55.1.2:31315/api/deploy/delete
```

Here we use the curl command to reach the API endpoint, and use the following parameters:
- accelleran-drax-example-xapp-010 - This is the name of the xApp
- default - This is the namespace where the xApp is deployed
- 10.55.1.2 - This is an example Kubernetes advertise IP

Details can also be found in the xApp Dev Guide: [https://cutt.ly/drax-xapp-dev-guide](https://cutt.ly/drax-xapp-dev-guide)
