# argo-task
A short pipeline that builds, pushes and deploys ArgoCD in a K8s cluster


# argo-task
A short pipeline that builds, pushes and deploys ArgoCD in a K8s cluster




# Deploy ArgoCD to a Kubernetes cluster

I chose to run this all in an EKS cluster, so I've created a temp account in AWS in which I've created a cluster (eu-west-1).

For the purpose of the task, I also used GitHub actions as my CI system for the pipeline part. that consists of 2 main parts -
 
          build & push a docker image to some registry (In this case - ECR of course)
          
          Helm deploy to a mildly customized public argo-cd helm chart
         

I will send in a seperate email the credentials for this AWS account, and also add further exaplanation regarding how to access Argo app.

    
BTW - Until now, I hven't found a way ot make helm run through github actions, it's egony, I tend to forget Actions is still in its youth.
Though, I did manage to run the rest in a GitHub Action workflow, and then I ran those commands from my local machine - 

         helm repo add argo-cd https://argoproj.github.io/argo-helm
         helm dep update charts/argo-cd/
         helm install argo-cd charts/argo-cd/
   
