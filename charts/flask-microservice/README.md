# Helm Chart for Flask Apps on Kubernetes

--- 
This chart was forked from Shiny Repo which was created by Julian and then modified a bit.    
Original documentation may be be found [here.](https://git.photonicdata.science/shiny-on-k8s/helm-chart)

--- 
## What is this ?

This repository contains the Helm Chart to deploy a dockerized Flask Server (e.g. built with this [repository](https://git.photonicdata.science/flask-on-kubernetes/docker-template) to the Photonic Data Science Kubernetes Cluster.

## Why do I need this ?

Deploying your Flask Server applications to Kubernetes is an easy way to give users access to the power of R analysis scripts. Using our Kubernetes cluster, you don't have to worry about setting up the servers etc. for that - it is all handled for you. Using our simple GUI frontend [Rancher](https://rancher.k8s.photonicdata.science) you can deploy your app without any Kubernetes or networking knowledge.

## How do I use this ?

1. Write & Dockerize a Flask Server Application

Follow the Guidelines described in this [Repository](https://git.photonicdata.science/flask-on-kubernetes/docker-template) to create a dockerized Flask Server application to deploy to our cluster.

2. Request Access to the Rancher GUI to deploy App to Kubernetes

Contact [Julian](mailto:julian.hniopek@uni-jena.de) or [Nazar](mailto:nazar.stefaniuk@uni-jena.de) to get limited access to our Kubernetes Management system. You'll only be able to install the Flask Server in the flask namespace. If you need more access, please discuss with us.

3. Deploy your app to Kubernetes

    1. Log in to [Rancher](https://rancher.k8s.photonicdata.science)
    2. Navigate to the fa16 cluster (left Sidebar).
    3. Select `Apps & Marketplace --> Charts` in the new sidebar. You'll see all available charts on the cluster, but if you try to install any of them other than the Flask Chart, it'll fail. Search for "Flask-on-Kubernetes" using the filter function and click on it. 
    4. Click on install
    5. Select a name for your application. It has to be lowercase and can include `-`
    6. Fill in the `Values.yaml` file on the next page
        * `DockerSecret` should be `pds-registry` if you pull from the Photonic Data Science registry. If you pull from a public registry without authentication keep empty. If you want to use a different registry with authentication, please contact [Julian](mailto:julian.hniopek@uni-jena.de) or [Nazar](mailto:nazar.stefaniuk@uni-jena.de).
        * `FlaskAppImage` should be the image you want to use in the format `registry/image:tag`
        * `AppURL` should be the URL you want to serve from. Use any `*.k8s.photonicdata.science` URL. Make sure, it isn't already taken :)
    7. Click on Install and navigate to your `AppURL` to watch the application work

### Helm Installation

After you click install, Rancher will automatically trigger a Helm based pipeline to install the application. You can see the status of your app under `Apps & Marketplace --> Installed Apps`. After a while, it should show as `deployed`. If not, you can go to `Apps & Marketplace --> Recent Operations`, which will list all recently run Helm processes. Find your process and you can click the three dots on the far right to view the logs. Most often, the problem is some typo in the `values.yaml` file.

### Docker Container

Similar to the Troubleshooting described [here](https://git.photonicdata.science/flask-on-kubernetes/docker-template), you can also access the Docker logs via Rancher. For that, navigate to `Apps & Marketplace --> Installed Apps`, find you application and click on its name. On the next page, click on the name of the deployment ([your-app-name]-deployment). On the next page, you can then find the pod, which actually contains your application. To view the logs, click on the three dots and select "view logs".

### Update you aplication
Create and push your new docker image. You may have always the same tag with you image, for example "latest". 
The Kybernetes system will alway pull you image on start. So to updare your application you need to delete old deployment part. 
Similar to previous section, click on the name of the deployment ([your-app-name]-deployment). Click on the three dots and select "delete". 
This will start deletion process of your application with old version and in the same time it should start creating new application with pulling your new image. 
