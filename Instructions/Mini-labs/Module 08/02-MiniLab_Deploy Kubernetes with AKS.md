# Mini-lab: Deploy Kubernetes with AKS

In this mini-lab, you will:

* Create a new resource group.

* Configure cluster networking.

* Create an Azure Kubernetes Service cluster.

* Connect to the Kubernetes cluster by using kubectl.

* Create a Kubernetes namespace.

## Create a new resource group

You'll first need to create a resource group for your resources to deploy into.

1. Sign in to Azure Cloud Shell with your Azure account. Select the Bash version of Cloud Shell.

[Azure Cloud Shell](https://shell.azure.com/)

2. You need to choose a region where you want to create a resource group, for example, **East US**. If you select a different value, remember it for the rest of the exercises in this module. You may need to redefine the value between Cloud Shell sessions. Run the following commands to record these values in Bash variables.

```Azure CLI
REGION_NAME=eastus
RESOURCE_GROUP=aksworkshop
SUBNET_NAME=aks-subnet
VNET_NAME=aks-vnet
 ```

You can check each value using the echo command, for example, echo ```$REGION_NAME```.

3. Create a new resource group with the name **aksworkshop. Deploy all resources created in these exercises in this resource group. A single resource group makes it easier to clean up the resources after you finish the module.

```Azure CLI
az group create \
    --name $RESOURCE_GROUP \
    --location $REGION_NAME
```

## Configure networking

There are two network models to choose from when deploying an AKS cluster. The first model is *Kubenet networking*, and the second is *Azure Container Networking Interface (CNI) networking*.

## Kubenet networking

Kubenet networking is the default networking model in Kubernetes. With Kubenet networking, nodes get assigned an IP address from the Azure virtual network subnet. Pods receive an IP address from a logically different address space to the Azure virtual network subnet of the nodes.

Network address translation (NAT) is then configured so that the pods can reach resources on the Azure virtual network. The source IP address of the traffic is translated to the node's primary IP address and then configured on the nodes. Note that pods receive an IP address that's "hidden" behind the node IP.

## Azure Container Networking Interface (CNI) networking

With Azure Container Networking Interface (CNI), the AKS cluster is connected to existing virtual network resources and configurations. In this networking model, every pod gets an IP address from the subnet and can be accessed directly. These IP addresses must be unique across your network space and calculated in advance.

Some of the features you'll use require you to deploy the AKS cluster by using the *Azure Container Networking Interface networking* configuration.

Below, you will create the virtual network for your AKS cluster. You will use this virtual network and specify the networking model when you deploy the cluster.

1. First, create a virtual network and subnet. Pods deployed in your cluster will be assigned an IP from this subnet. Run the following command to create the virtual network.

```Azure CLI
az network vnet create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $VNET_NAME \
    --address-prefixes 10.0.0.0/8 \
    --subnet-name $SUBNET_NAME \
    --subnet-prefix 10.240.0.0/16
```

2.Next, retrieve and store the subnet ID in a Bash variable by running the command below.

```Azure CLI
SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNET_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
```

## Create the AKS cluster

With the new virtual network in place, you can create your new cluster. There are two values you need to know before running the ```az aks create``` command. The first is the version of the latest, non-preview Kubernetes version available in your selected region, and the second is a unique name for your cluster.

1. To get the latest, non-preview Kubernetes version you use the ```az aks get-versions``` command. Store the value that returns from the command in a Bash variable named ```VERSION```. Run the command below the retrieve and store the version number.

```Azure CLI
SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNET_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
```

2. The AKS cluster name must be unique. Run the following command to create a Bash variable that holds a unique name.

```Bash
AKS_CLUSTER_NAME=aksworkshop-$RANDOM
```

3. Run the following command to output the value stored in ```$AKS_CLUSTER_NAME```. Note this for later use. You'll need it to reconfigure the variable in the future, if necessary.

```Bash
echo $AKS_CLUSTER_NAME
```

4. Run the following ```az aks create``` command to create the AKS cluster running the latest Kubernetes version. This command can take a few minutes to complete.

```Azure CLI
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER_NAME \
--vm-set-type VirtualMachineScaleSets \
--load-balancer-sku standard \
--location $REGION_NAME \
--kubernetes-version $VERSION \
--network-plugin azure \
--vnet-subnet-id $SUBNET_ID \
--service-cidr 10.2.0.0/24 \
--dns-service-ip 10.2.0.10 \
--docker-bridge-address 172.17.0.1/16 \
--generate-ssh-keys
```

## Test cluster connectivity by using kubectl

```kubectl``` is the main Kubernetes command-line client you use to interact with your cluster and is available in Cloud Shell. A cluster context is required to allow ```kubectl``` to connect to a cluster. The context contains the cluster's address, a user, and a namespace. Use the az aks get-credentials command to configure your instance of ```kubectl```.

1. Retrieve the cluster credentials by running the command below.

```Azure CLI
az aks get-credentials \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_CLUSTER_NAME
```

2. You can see what was deployed by listing all the nodes in your cluster. Use the ```kubectl``` get nodes command to list all the nodes.

```Bash
kubectl get nodes
```

You'll see a list of your cluster's nodes. Here's an example:

```Ouput
NAME                                STATUS   ROLES   AGE  VERSION
aks-nodepool1-24503160-vmss000000   Ready    agent   1m   v1.15.7
aks-nodepool1-24503160-vmss000001   Ready    agent   1m   v1.15.7
aks-nodepool1-24503160-vmss000002   Ready    agent   1m   v1.15.7
```

## Create a Kubernetes namespace for the application

A namespace in Kubernetes creates a logical isolation boundary. Names of resources must be unique within a namespace, but not across namespaces. If you don't specify the namespace when you work with Kubernetes resources, the default namespace is implied.

Create a namespace for your ratings application.

1. List the current namespaces in the cluster.

```Bash
kubectl get namespace
```

You'll see a list of namespaces similar to this output.

```Ouput
NAME              STATUS   AGE
default           Active   1h
kube-node-lease   Active   1h
kube-public       Active   1h
kube-system       Active   1h
```

2. Use the ```kubectl``` create namespace command to create a namespace for the application called **ratingsapp**.

```Bash
kubectl create namespace ratingsapp
```

You'll see a confirmation that the namespace was created.

```Output
namespace/ratingsapp created
```


 
