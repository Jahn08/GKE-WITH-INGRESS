# GKE-WITH-INGRESS

The repository demonstrates how to deploy an application from container image using Google Kubernetes Engine (GKE). [WEB-TIMER](https://github.com/Jahn08/WEB-TIMER) is exploited as a containerised application.

## Getting Started

To start with, you have to install the next tools:
1. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl) - the Kubernetes command-line tool. Set up yaml files can be applied to a cluster by using a command: *kubectl apply -f <path_to_yaml_file>*
2. [Google Cloud SDK](https://cloud.google.com/sdk/install). Right after installing the component it's possible to [configure it and create your cluster](https://cloud.google.com/kubernetes-engine/docs/quickstart) - the credentials for *kubectl* will then be updated automatically. Otherwise, if you create your cluster through the GKE web UI, you will have to fetch the credentials on your own: *gcloud container clusters get-credentials <cluster-name>*
3. You might also need [kompose](https://kompose.io/) to convert your existent docker-compose.yml file into service and pod files. 

## Pod

### Secrets

[app-pod.yaml](https://github.com/Jahn08/GKE-WITH-INGRESS/blob/master/app-pod.yaml) refers to secrets (the *secretKeyRef* element) provided in [secret.yaml](https://github.com/Jahn08/GKE-WITH-INGRESS/blob/master/secret.yaml). All the secret values are rpesented as base64 encoded values. Thus, it's going to be the very first file to apply to your cluster: *kubectl apply -f secret.yaml*
To encode a text value in Linux: *echo -n "you_secret_value" | base64*. Conversely, decoding: *echo -n "base64_encoded_value" | base64 --decode*

### Readiness/Liveness Probes

[Readiness and liveness probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) can be used in parallel for the same container. Using both can ensure that traffic does not reach a container that is not ready for it (the readiness probe), and that containers are restarted when they fail (the liveness probe).

