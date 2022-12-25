# Kcert Tutorial
A easy to follow tutorial to have an automatic https cert created for your public web url. This uses excellent util by https://github.com/nabsul/kcert  

# Assumption

* You have a public DNS for your website
* Use are using ingress controller like nginx
* You have kubectl access to the cluster  

# Installation

1. **Kcert Setup**
    * > git clone https://github.com/agileguru/kcert-tutorial.git
    * > cd kcert-tutorial
    * > kubectl create -f kcert/kcert.yml

1. **Kcert Check**
    * > kubectl get all -n kcert
        ```
        NAME                        READY   STATUS    RESTARTS   AGE
        pod/kcert-6ffbb9bf9-47979   1/1     Running   0          15h

        NAME            TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)           AGE
        service/kcert   ClusterIP   10.52.12.2   <none>        80/TCP,8080/TCP   15h

        NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
        deployment.apps/kcert   1/1     1            1           15h

        NAME                              DESIRED   CURRENT   READY   AGE
        replicaset.apps/kcert-6ffbb9bf9   1         1         1       15h
        ```
1. **Ingress Controller setup ( if not done already )**
    * > helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
    * > helm repo update
    * > helm install nginx-ingress ingress-nginx/ingress-nginx
    * > kubectl delete -A ValidatingWebhookConfiguration nginx-ingress-ingress-nginx-admission
    
1. **Create ingress**
    * > kubectl create -f ingress/kcert-demo.yaml
    * > kubectl get secrets -n kcert 
        ```
        NAME                     TYPE                                  DATA   AGE
        demo-doit-research-com   kubernetes.io/tls                     2      15h
        ```

1. **Check Your app**
    * Open Your App in the browser
    * Automatic redirect to https
    * Certificate issued by https://letsencrypt.org/


    
