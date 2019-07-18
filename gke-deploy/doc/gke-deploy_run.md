## gke-deploy run

Execute both prepare and apply phase

### Synopsis

Deploy to GKE in two phases, which will do the following:

Prepare Phase:
  - Modify Kubernetes config YAMLs:
    - Set the digest of images that match the [--image|-i] flag, if provided.
    - Add app.kubernetes.io/name=[--app|-a] label, if provided.
    - Add app.kubernetes.io/version=[--version|-v] label, if provided.

Apply Phase:
  - Apply Kubernetes config YAMLs to the target cluster with the provided namespace.
  - Wait for deployed resources to be ready before exiting.


```
gke-deploy run [flags]
```

### Examples

```
  # Modify configs and deploy to GKE cluster.
  gke-deploy run -f configs -i gcr.io/my-project/my-app:1.0.0 -a my-app -v 1.0.0 -o modified -n my-namespace -c my-cluster -l us-east1-b

  # Deploy to GKE cluster that kubectl is currently targeting.
  gke-deploy run -f configs

  # Deploy to GKE cluster that kubectl is currently targeting without supplying any configs. Have gke-deploy generate base configs for your application using an image, app name, and service port.
  gke-deploy run -i nginx -a nginx -x 80
```

### Options

```
  -a, --app string         Application name of the Kubernetes deployment.
  -c, --cluster string     Name of GKE cluster to deploy to.
  -x, --expose int         Creates a Service resource that connects to a deployed resource using a selector that matches the label with key as 'app.kubernetes.io/name' and value provided by --app. The port provided will be used to expose the deployed resource (i.e., port and targetPort will be set to the value provided in this flag).
  -f, --filename string    Config file or directory of config files to use to create the Kubernetes resources (file or files in directory must end with ".yml" or ".yaml"). If this field is not provided, base configs will be created: Deployment with image provided by --image and HorizontalPodAutoscaler.
  -h, --help               help for run
  -i, --image string       Image to be deployed.
  -L, --label strings      Label(s) to add to Kubernetes resources (k1=v1). Labels can be set comma-delimited or as separate flags. If two or more labels with the same key are listed, the last one is used.
  -l, --location string    Region/zone of GKE cluster to deploy to.
  -n, --namespace string   Namespace of GKE cluster to deploy to. (default "default")
  -o, --output string      Target directory to store modified Kubernetes resource configs. (default "./output")
  -p, --project string     Project of GKE cluster to deploy to. If this field is not provided, the current set GCP project is used.
  -t, --timeout duration   Timeout limit for waiting for resources to finish applying. (default 5m0s)
  -V, --verbose            Prints underlying commands being called to stdout.
  -v, --version string     Version of the Kubernetes deployment.
```

### SEE ALSO

* [gke-deploy](gke-deploy.md)	 - Deploy to GKE

###### Auto generated by spf13/cobra on 17-Jul-2019