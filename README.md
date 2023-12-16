# litmus-recipes

This repo can be used from basic local setup of litmus to Makefiles for testing the changes.

I'm using minikube for running a local cluster

## Installation of Litmus with frontend
For running whole litmus i.e all the components from operator to frontend you can refer to the [docs](https://docs.litmuschaos.io/). but here are some of the steps:
```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
```
```shell
helm install my-release bitnami/mongodb --values deploy/mongo-vaules.yml -n litmus --create-namespace
```

```shell
kubectl apply -f https://raw.githubusercontent.com/litmuschaos/litmus/master/mkdocs/docs/3.0.0/litmus-cluster-scope-3.0.0.yaml
```
## Installtion of Litmus for testing the experiments/changes/components

This section can be used for testing the changes in the some of the components like operator, exporter, runner.
These steps are taken from the [operator's repo](https://github.com/litmuschaos/chaos-operator/tree/master/deploy)

### Applying the RBACs
```shell
k apply -f deploy/rbac.yaml -n litmus
```

### Installing crds
```shell
k apply -f deploy/chaos_crds.yaml
```

### Verifying
```shell
 k get crds | grep 'litmus'
chaosengines.litmuschaos.io       2023-12-15T22:57:53Z
chaosexperiments.litmuschaos.io   2023-12-15T22:57:53Z
chaosresults.litmuschaos.io       2023-12-15T22:57:53Z

```
### Installing Operator
Operator is needed for running the experiments/runner
```shell
k apply -f deploy/operator.yaml
```
A Operator Pod should show. Check it by running:
```shell
k get po -n litmus
```

### Installing a dummy application
While using the experiments, we need a dummy application, for now I'm just using a nginx app.(Please check the labels, namespace of your app,and litmus components)
```shell
k apply -f deploy/app.yaml
```
A nginx pod should show up.

### Running experiments

Please refer to [experiment](./experiments/) directory for installing and running the specific experiment



