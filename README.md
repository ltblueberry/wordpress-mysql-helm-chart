# Kubernetes Wordpress + MySQL helm chart

The simpliest example of helm chart for Wordpress and MySQL (**chart** directory).

Also, original manifests provided for using via **kubectl** (**original-manifests** directory).

This demo was used with GCP Kubernetes cluster.

# Dependencies

* **gcloud** ([installation guide is here](https://cloud.google.com/sdk/docs/quickstarts/))
* **kubectl** ([installation guide is here](https://kubernetes.io/docs/tasks/tools/install-kubectl/))

# Setup cluster
To start using gcloud utility execute next command
```sh
gcloud init
```

Execute next command to sign in
```sh
gcloud auth login
```

Select your GCP project (if you have one) or create new one (you can do it via GCP Web Interface)
```sh
gcloud projects list
gcloud config set project <YOUR_PROJECT_ID>
```

**Finally, we can setup demo cluster**
```sh
gcloud container clusters create demo-cluster --zone europe-west4-a
```

***kubectl** will be automatically configured to your created cluster*

You can check your demo-cluster status with next command
```sh
kubectl get nodes
```

# Usage

1) Clone this git repository
```sh
git clone git@github.com:ltblueberry/wordpress-mysql-helm-chart.git
```
2) Execute next commands from repository directory
```sh
kubectl create -f original-manifests/namespace.yaml
kubectl create -f original-manifests/mysql
kubectl create -f original-manifests/wordpress
```
*All manifests configured with namespace called **demo-application***

3) Check your wordpress service **External IP** address with next command (may take some time)
```sh
kubectl get service -n demo-application
```

Now you can check this IP address with web-browser


## License

**[MIT License](LICENSE)**

Copyright (c) 2020 [ltblueberry](https://github.com/ltblueberry)