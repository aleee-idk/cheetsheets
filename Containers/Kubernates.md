
# Table of Contents

1.  [Terminology:](#orgdf30003)
2.  [Commands:](#orgcce9771)
    1.  [Get information:](#orge9038a1)
    2.  [Create componnent:](#org06a4439)
    3.  [Debugg pods:](#org8b982f9)
    4.  [Commands:](#org96f10c1)
        1.  [Run command inside container:](#org2fcada9)
    5.  [Use config file:](#org741c571)
3.  [Configuration file:](#org20e0d65)
4.  [Tips and Tricks:](#orgcb502c7)



<a id="orgdf30003"></a>

# Terminology:

-   Kubernates components:
    -   Node: Physical machine
    -   Pod: Smallest unit of B8s, abstraction over container, usually 1 application per pod.
    -   Service: permanent IP address, load balancer.
        -   External Service: Open to the host machine and further.
            for this kubernates use Ingress
        -   Internal Service: just to kubernates network.
    -   Ingress: route traffic into the cluster.
    -   ConifgMap: External configuration of the application, variables like URL&rsquo;s, users, etc. But not for credentials.
    -   Secret: External configuration of the sensible data of the aplication, like credentials.
    -   Volumes: Attached physical storage to the pod, localy or remotly.
    -   Deployment: blueprint for app pods, the deployments are creater, not pods. deployments are pods abstraction.
    -   statefullset: component for apps like database, manage the pods.
-   Minikube: 1 node K8s that runs in a VirtualBox.
-   Kubectl: CLI for K8s clusters.


<a id="orgcce9771"></a>

# Commands:

All commands are run with *&ldquo;kubectl &#x2026;&rdquo;*
Example: &ldquo;kubectl create *name* &#x2013;image=/image/&rdquo;
All the flag listed below can be used together.


<a id="orge9038a1"></a>

## Get information:

-   get all
-   get pod
-   get services
-   get deployment
-   describe *pod*
-   describe service *service*


<a id="org06a4439"></a>

## Create componnent:

create *component*
create deployment *name* &#x2013;image/image/


<a id="org8b982f9"></a>

## Debugg pods:

logs *pod name*


<a id="org96f10c1"></a>

## Commands:


<a id="org2fcada9"></a>

### Run command inside container:

exec -it *pod name* &#x2013; *command*


<a id="org741c571"></a>

## Use config file:

apply -f *file name*


<a id="org20e0d65"></a>

# Configuration file:

\*\*


<a id="orgcb502c7"></a>

# Tips and Tricks:

-   Enter the container of the pod: *exec -it pod<sub>name</sub> &#x2013; \\/bin\\/container<sub>shell</sub>*

Use inspect to check the container shell

-   Deployment for state\*LESS\* apps and statefulset for state\*FULL\* apps or databases.
-   Database are ofthen hosted outside of K8s cluster.
-   the image refers to a docker image from dockerhub repository.

