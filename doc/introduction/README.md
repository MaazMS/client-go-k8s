## Introduction  
1. if you're writing the software which is talk to k8s cluster and using go then use client-go.  
1. client go is official for client go for k8s.   
1. It is built and maintain by api machinery.   

## client-go  
1. create go.mod file 

```mod
require (
	k8s.io/api v0.19.1
	k8s.io/apimachinery v0.19.1
	k8s.io/client-go v0.19.1
)
```

## The Client-go Library  
1. The Kubernetes programming interface in Go mainly consists(to be formed or made up of) of the `k8s.io/client-go library`  
1. client-go is a typical web service client library that supports all API types that are officially part of Kubernetes.  
1. It can be used to execute the usual REST verbs: Create, Get, List, Update, Delete, Patch.   
1. Each of these REST verbs are implemented using the “The HTTP Interface of the API Server”.  
1. for each Kubernetes 1.x.y release, there is a client-go release with a matching tag kubernetes-1.x.y.  
1. ![]()    

## Kubernetes API Types  
1. The Kubernetes API Go types for objects like pods, services, and deployments are located in their own repository.     
1. It is accessed as k8s.io/api in Go code.   
1. The actual Go types are contained in a types.go file (e.g.,k8s.io/api/core/v1/types.go).      
1. ![]()  

## API Machinery 
1. There is a third repository called API Machinery,   
1. It is used as k8s.io/apimachinery in Go.   
1. It includes all the generic building blocks to implement a Kubernetes-like API.   
1. API Machinery is not restricted to container management, so, for example, it could be used to build APIs for an online shop
or any other business-specific domain.  
1. ![]() 

## Creating and Using a Client    
1. Now we know all the building blocks to create a Kubernetes client object, which means we can access resources in a       
   Kubernetes cluster.    
1. Assuming you have access to a cluster in your local environment (i.e., kubectl is properly set up and credentials are  
   configured), the following code illustrates how you can use client-go in a Go project:     
   
```go
import (
metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
"k8s.io/client-go/tools/clientcmd"
"k8s.io/client-go/kubernetes"
)
kubeconfig = flag.String("kubeconfig", "~/.kube/config", "kubeconfig file")
flag.Parse()
config, err := clientcmd.BuildConfigFromFlags("", *kubeconfig)
clientset, err := kubernetes.NewForConfig(config)
pod, err := clientset.CoreV1().Pods("book").Get("example", metav1.GetOptions{})
```
   
1. clientcmd holds the required code to configuring connection to the cluster using kubeconfig as well as about modification to kubeconfig.   
1. `kubernetes.NewForConfig` in order to create the actual Kubernetes client set.   
   It’s called a client set because it contains multiple clients for all native Kubernetes resources.  

clientcmd.BuildConfigFromFlags. We omitted the mandatory error handling throughout this code, but the err variable would     
normally contain, for example, the syntax error if a kubeconfig is not well formed. As syntax errors are common in Go code,    
such an error ought to be checked for properly, like so:     
```go
config, err := clientcmd.BuildConfigFromFlags("", *kubeconfig)
if err != nil {
fmt.Printf("The kubeconfig cannot be loaded: %v\n", err
os.Exit(1)
}
```

When running a binary inside of a pod in a cluster, the kubelet will automatically mount a service account into the container at
/var/run/secrets/kubernetes.io/serviceaccount.  
It replaces the kubeconfig file just mentioned and can easily be turned into a rest.Config via the `rest.InClusterConfig()` method.   

```go
config, err := rest.InClusterConfig()
if err != nil {
// fallback to kubeconfigkubeconfig := filepath.Join("~", ".kube", "config")
if envvar := os.Getenv("KUBECONFIG"); len(envvar) >0 {
kubeconfig = envvar
}
config, err = clientcmd.BuildConfigFromFlags("", kubeconfig)
if err != nil {
fmt.Printf("The kubeconfig cannot be loaded: %v\n", err
os.Exit(1)
}
}
```
