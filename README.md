# argo-task
A short pipeline that builds, pushes and deploys ArgoCD in a K8s cluster



# Deploy ArgoCD to a Kubernetes cluster

I chose to run this all in an EKS cluster, so I've created a temp account in AWS in which I've created a cluster (eu-west-1).

For the purpose of the task, I also used GitHub actions as my CI system for the pipeline part. that consists of 2 main parts -
 
          build & push a docker image to some registry (In this case - ECR of course)
          
          Helm deploy to a mildly customized public argo-cd helm chart
         

I will send in a seperate email the credentials for this AWS account, and also add further exaplanation regarding how to access Argo app.

    
BTW - Until now, I hven't found a way to make helm run smoothly in github actions, it's egony, I tend to forget that GitHub Actions is still in its youth.
Though, I did manage to run the rest in a GitHub Action workflow, and then I ran those commands from my local machine - 

         helm repo add argo-cd https://argoproj.github.io/argo-helm
         helm dep update charts/argo-cd/
         helm install argo-cd charts/argo-cd/
         
In this **argo-task** repo I have overriden the docker image this manifest works with, with the one I've uploaded to ECR.
It is shown in charts/argo-task/values.yml.

I've encoutered many issues along the way with documentation referring to old versions of this remote Helm chart, and also some IAM configuration (Mainly EKS related) stuff that didn't go so well in the beginning, though I'm glad I've learned many cool stuff nontheless. 


# Bonus 1 - DNS:
For that purpose I would use an nginx ingress controller (Or an ALB/NLB) and attach route53 to it, alongside an external DNS pod per each service.
So, whenever a service is added, updated or deleted, route53 will be automatically aligned with this knowledge.


# Bonus - Monitoring:
Well, it's a known fact that K8s and prometheus are really good friends, so it sounds like a good place to start with.
There's usually an Exporter for specific apps, or resource types where prometheus can collect metrics that might help us seeing the big picture better. Argo exposes some metrics regarding the app itself and also regarding the cluster itself.
Grafana could also be added the gang as a great dashboarder, Prometheus AlertManager could be added for notifications to slack, pagerduty, mail, etc.
   
