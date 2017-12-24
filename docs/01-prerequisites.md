# Prerequisites

## Installing the Client Tools (OSX)

This tutorial assumes OSX will be used as the client workstation to carry out the installation. However it should be pretty straight forward to use Linux and install the required pre-prerequisites.

## Install CFSSL

The `cfssl` and `cfssljson` command line utilities will be used to provision a [PKI Infrastructure](https://en.wikipedia.org/wiki/Public_key_infrastructure) and generate TLS certificates.

### OS X
```
brew install cfssl
```

### Verification

Verify `cfssl` version 1.2.0 or higher is installed:

```
cfssl version
```

> output

```
Version: 1.2.0
Revision: dev
Runtime: go1.6
```

> The cfssljson command line utility does not provide a way to print its version.

## Install kubectl

The `kubectl` command line utility is used to interact with the Kubernetes API Server. Download and install `kubectl` from the official release binaries:

### OS X

```
brew install kubectl
```

### Verification

Verify `kubectl` version 1.9.0 or higher is installed:

```
kubectl version --client
```
> output
```
Client Version: version.Info{Major:"1", Minor:"9", GitVersion:"v1.9.0", GitCommit:"925c127ec6b946659ad0fd596fa959be43f0cc05", GitTreeState:"clean", BuildDate:"2017-12-15T21:07:38Z", GoVersion:"go1.9.2", Compiler:"gc", Platform:"darwin/amd64"}
```

# Provisioning Compute Resources

Kubernetes requires a set of machines to host the Kubernetes control plane and the worker nodes where containers are ultimately run.

Since this tutorial does not specify a specific Cloud or Infrastructure provider, it assumed the end user is capable of creating standard VM's with the following specification:

**Master Node**
1 * Master Node (3 for HA)
2 vCPU
8GB Mem
50GB Localdisk
Single network card

* Ensure the Master node(s) are named "master-1", "master-2" etc...
**Worker Nodes**
3 * Worker Nodes
2 vCPU
8GB Mem
50GB Localdisk
Single network card
* Ensure the Worker node(s) are named "worker-1", "worker-2" etc...


**Additional settings/notes:**
* Turn off swap on all Nodes
* Turn off the firewall and selinux

**Note**: You can leave the Firewall and SE-Linux running and enable the relevant ports and profiles. However this is out of scope for this document.

## Networking

The Kubernetes [networking model](https://kubernetes.io/docs/concepts/cluster-administration/networking/#kubernetes-model) assumes a flat network in which containers and nodes can communicate with each other. In cases where this is not desired [network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/) can limit how groups of containers are allowed to communicate with each other and external network endpoints.

> Setting up network policies is out of scope for this tutorial.

Next: [Provisioning Compute Resources](03-compute-resources.md)

## DNS

Make sure DNS is configured for the VM's you created. 
