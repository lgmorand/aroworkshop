---
sectionid: lab2-app-install
sectionclass: h2
title: Application Installation
parent-id: lab-clusterapp
---

### Deploy an application from OpenShift Web Console

{% collapsible %}

Red Hat OpenShift proposes several strategies to build and deploy applications on the platform. It is very helpful to leverage containers technology without knowledges about it. 

![Docker registry connection](/media/lab2/build_strategies_ocp.png)

* **From Git** uses the Source-to-Image (S2I) mecanism. With source code repository located in a Git repository it builds the image and creates useful resources to deploy it on OpenShift. No need to add build files to the source code.

* **Container Image** deploys the application from an Image located in the internal OpenShift container registry or in an external container registry.

* **From Catalog** is the "Developer Catalog". It provides templates a wide range of middleware, runtimes, database images certified and supported by Red Hat. It helps to deploy advanced use-cases such as a back-end (i.e : Nodejs) and its database (MongoDb). Developer Catalog content can be customize with other images.

* **From Dockerfile** helps to deploy an app from a DockerFile located anywhere.

* **YAML** creates resources from a YAML file gathering different kind of Kubernetes objects.

* **Database** displays all database images supported and certified by Red Hat. Custom images can be added of course.


#### Deploy a nodeJS application from the Developer Catalog

First, create a project as shown in the previous parts and name it **<MY_USERNAME>-s2i** or the following command :

```
oc new-project <MY_USERNAME>-s2i 
```

On the Web Console, follow those instructions :


![Docker registry connection](/media/lab2/catalog_developer.png)

Make sure the right project is selected

1. Choose the Developer panel
2. Click on "+Add"
3. Click on From Git

We set now the Git repository url :

![Docker registry connection](/media/lab2/s2i_nodejs.png)

1. The URL is : **https://github.com/gestrem/pacman** .
Explore Advanced git Options which are useful when there are custom files / directories locations.
2. The Builder image is set automaticaly due to the presence of package.json file. 
3. Couples of NodeJS version are available. We will use version 10 SCL.

Let others fields with default values.
Pay attention to "Advanced Options". A route is created. it means the application will exposed outside the cluster.

Click on "Create"

#### Check application Deployment

First, the build is executed on OpenShift to create the image. This image is pushed to the internal image registry with its tag. 
Then the deployement is triggered to deploy and run the container from the pushed image.

Look at resources created by clicking on "Topology" and on the "Pacman" pod. 


![Docker registry connection](/media/lab2/pod_running.png)

**Pods** running represents the container running. Click on it to access Metrics, logs, terminal and state of the container.

**Builds** represent builds related to all images version pushed into the registry. Which is helpful to get builds history and easily rollback on OpenShift.

**Services** stands for Kubernetes service which an abstraction to expose an application running a set of pods as a network service.  Here it defines also port (8080) opened to access the application

**Routes** is the url to access the application outside OpenShift cluster.

Click on the url and access the original Pacman game online :  

![Docker registry connection](/media/lab2/pacman.png)

Now we know to use the Web console to build and deploy an application easily, we will use the terminal to deploy an other application with extra Kubernetes resources and explore them !

{% endcollapsible %}