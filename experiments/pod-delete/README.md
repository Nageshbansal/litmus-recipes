# Pod-delete Experiment
This is the basic use case of the pod-delete experiment. Please refer to the [litmus-docs](https://litmuschaos.github.io/litmus/experiments/categories/pods/pod-delete#minimal-rbac-configuration-example-optional) for more information.

#### I'm using the nginx app (it can be found in the [deploy/app.yaml](../../deploy/app.yaml))

### Installing RBACs
```shell
k apply -f pod-delete-rbac.yaml
```
### Installing Experiment
```shell
k apply -f pod-delete.yaml
```
NOTE: the go-runner can be changed in this config

### Running the experiment
```shell
k apply -f pod-chaos.yaml
```
NOTE: Tunables can be configured in this config

