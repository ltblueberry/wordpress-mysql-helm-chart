# Kubernetes WordPress + MySQL helm chart

The simplest example of a helm chart for WordPress and MySQL (**chart** directory).

Also, original manifests provided for using via **kubectl** (**original-manifests** directory).

This demo was used with GCP Kubernetes cluster.

# Dependencies

* **gcloud** ([installation guide is here](https://cloud.google.com/sdk/docs/quickstarts/))
* **kubectl** ([installation guide is here](https://kubernetes.io/docs/tasks/tools/install-kubectl/))
* **helm** ([installation guide is here](https://helm.sh/docs/intro/install/))

# Setup cluster
To start using gcloud utility execute next command
```sh
gcloud init
```

Execute the next command to sign in
```sh
gcloud auth login
```

Select your GCP project (if you have one) or create a new one (you can do it via GCP Web Interface)
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
2) Execute next commands **from repository directory**

*check that all templates are valid*
```sh
helm template .
```
*install chart*
```sh
helm install . --generate-name
```
3) Check your WordPress service **External IP** address with next command (may take some time)
```sh
kubectl get service -n demo-application
```
*By-default namespace that used in the chart called **demo-application**. If you changed it, make sure you define the proper namespace in **kubectl get** command.*

Now you can check this IP address with web-browser

# Helm Variables
Defined in [values.yaml](https://github.com/ltblueberry/wordpress-mysql-helm-chart/blob/develop/values.yaml)

| Name              | Default Value       |Difinition   |
|-----------------------|---------------------|---------------------|
| `namespace` | `demo-application` |Kubernetes namespace|

## `wordpress`:
| Name              | Default Value       |Difinition   |
|-----------------------|---------------------|---------------------|
| `deployment.image` | `wordpress:4.8-apache` |Docker image for Wordpress|
|`deployment.replicaCount` | `1` |Number of Pods to run
|`service.type` |` LoadBalancer` |Kubernetes Service type
|`service.port` | `80 `|Publishing port

## `mysql`:
| Name              | Default Value       |Difinition   |
|-----------------------|---------------------|---------------------|
| `deployment.image` | `mysql:5.6` |Docker image for MySQL|
|`deployment.replicaCount` | `1` |Number of Pods to run
|`service.type` |` ClusterIP` |Kubernetes Service type
|`service.port` | `3306 `|Publishing port
|`pvc.accessMode` | `ReadWriteOnce `|PVC Access mode
|`pvc.storage` | `2Gi `|PVC Storage size

# Uninstall
1) Execute the next command to get the list of helm releases
```sh
helm list
```
2) Execute the next command to uninstall helm release by RELEASE_NAME
```sh
helm uninstall RELEASE_NAME
```

## License

**[MIT License](LICENSE)**

Copyright (c) 2020 [ltblueberry](https://github.com/ltblueberry)