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
1. ![]()  

## API Machinery 
1. There is a third repository called API Machinery,   
1. It is used as k8s.io/apimachinery in Go.   
1. It includes all the generic building blocks to implement a Kubernetes-like API.   
1. API Machinery is not restricted to container management, so, for example, it could be used to build APIs for an online shop
or any other business-specific domain.  
1. ![]() 

## Creating and Using a Client  
