# Enterprise Addons

This repository contains [Kubernetes](https://kubernetes.io) addon applications deployed and managed by [Kubeaddons](https://github.com/mesosphere/kubeaddons).

`Addon` resources here are utilized by [D2iQ](https://d2iq.com) managed [Kubernetes](https://kubernetes.io) deployments (such as [Konvoy](https://d2iq.com/solutions/ksphere/konvoy)).


Instructions:

1.) This repo is a catalog that can be used for Kommander. Fork this repo and make your own.

2.) Edit (root of this repo) repository.yaml to match the url of your new repo

3.) Under the addons folder, add new helm charts for whatever you want to add to your catalog. See the minecraft example for more info. This is a bit of work...

4.) Go to kommander and create a project
    When a project is created in kommander, it will create:
     A new namespaced  called kommander-<projectname>
     A resource called AddonRepository (which you need to edit with the github url of the catalog you want to use)


5.) Create a yaml  file like this:

apiVersion: kubeaddons.mesosphere.io/v1beta1
kind: AddonRepository
metadata:
  annotations:
  name: kubeaddons-enterprise
spec:
  priority: "1"
  ref: master
  url: <url of your github forked repo>
  
  
 6.) Apply the  yaml against the namespace of your project
  
       kubectl apply -n kommander-<projectname> -f repository.yaml
  
  7.) If you want to refresh the items in the catalog, if you push new changes to your github repo
  
    kubectl delete -n kommander-<projectname> -f repository.yaml
    kubectl apply -n kommander-<projectname> -f repository.yaml

   

  
  




