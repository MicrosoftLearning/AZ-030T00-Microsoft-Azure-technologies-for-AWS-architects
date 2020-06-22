# Mini-lab: Run Azure Container Instances

In this demonstration you create a container in Azure and expose it to the Internet with a fully qualified domain name (FQDN).

Azure Container Instances is useful for scenarios that can operate in isolated containers, including simple applications, task automation, and build jobs. Here are some of the benefits:

* **Fast startup**: Launch containers in seconds.

* **Per second billing**: Incur costs only while the container is running.

* **Hypervisor-level security**: Isolate your application as completely as it would be in a VM.

* **Custom sizes**: Specify exact values for CPU cores and memory.

* **Persistent storage**: Mount Azure Files shares directly to a container to retrieve and persist state.

* **Linux and Windows**: Schedule both Windows and Linux containers using the same API.

For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend Azure Kubernetes Service (AKS).

## Create a container

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/) with your Azure subscription.

2. Open the Azure Cloud Shell from the Azure portal using the Cloud Shell icon.

![Picture 7](../../Linked_Image_Files/demo_Azure_containers_image1.png)

3. Create a new resource group with the name **learn-deploy-aci-rg** so that it will be easier to clean up these resources when you are finished with the module. If you choose a different resource group name, remember it for the rest of the exercises in this module. You also need to choose a region in which you want to create the resource group, for example **East US**.

```Azure CLI
az group create --name learn-deploy-aci-rg --location eastus
```

You create a container by providing a name, a Docker image, and an Azure resource group to the ```az container create``` command. You can optionally expose the container to the Internet by specifying a DNS name label. In this example, you deploy a container that hosts a small web app. You can also select the location to place the image - you'll use the **East US** region, but you can change it to a location close to you.

4. You provide a DNS name to expose your container to the Internet. Your DNS name must be unique. For learning purposes, run this command from Cloud Shell to create a Bash variable that holds a unique name.

```Azure CLI
DNS_NAME_LABEL=aci-demo-$RANDOM
```

5. Run the following ```az container create``` command to start a container instance.

```Azure
az container create \
  --resource-group learn-deploy-aci-rg \
  --name mycontainer \
  --image microsoft/aci-helloworld \
  --ports 80 \
  --dns-name-label $DNS_NAME_LABEL \
  --location eastus
```

```$DNS_NAME_LABEL``` specifies your DNS name. The image name, **microsoft/aci-helloworld**, refers to a Docker image hosted on Docker Hub that runs a basic Node.js web application.

6. When the ```az container create``` command completes, run ```az container show``` to check its status.

```Azure CLI
az container show \
  --resource-group learn-deploy-aci-rg \
  --name mycontainer \
  --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
  --out table
```

You see your container's fully qualified domain name (FQDN) and its provisioning state. Here's an example.

```Output
FQDN ProvisioningState

-------------------------------------- -------------------

aci-demo.eastus.azurecontainer.io Succeeded
```

If your container is in the **Creating** state, wait a few moments and run the command again until you see the **Succeeded** state.

7. From a browser, navigate to your container's FQDN to see it running. You will see this.

![Screenshot of the sample Node.js container app running in a browser.](../../Linked_Image_Files/demo_Azure_containers_image2.png)
