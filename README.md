## Memory-Checker Helm Chart

This repository contains a Helm chart for a Kubernetes CronJob that monitors and restarts the top 10 memory-consuming pods in your cluster. The CronJob uses `kubectl top pod` command to get the list of pods and then restarts their corresponding deployments.

### Installation

First, clone this repository:

```sh
git clone https://github.com/NicolasKarnick/memory-checker.git
cd memory-checker
```

Then, to install the Helm chart with the release name `my-release`:

```sh
helm install my-release .
```

### Configuration

The following table lists the configurable parameters of the Memory-Checker chart and their default values which are set in `values.yaml`:

| Parameter           | Description                                        | Default                          |
|---------------------|----------------------------------------------------|----------------------------------|
| `image.repository`  | Memory-Checker image repository                    | `bitnami/kubectl`                |
| `image.tag`         | Memory-Checker image tag                           | `latest`                         |
| `image.pullPolicy`  | Memory-Checker image pull policy                   | `Always`                         |
| `schedule`          | Cron schedule                                      | `"0 4 * * *"`                    |
| `restartPolicy`     | Job restart policy                                 | `OnFailure`                      |
| `args`              | Arguments passed to the CronJob                    | `kubectl top pod ...` script     |

Modify the `values.yaml` file to change the default configuration.

You can also specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```sh
helm install my-release . --set schedule="0 5 * * *"
```

This will set the CronJob to run at 05:00 every day.

For more information on configuring the CronJob, see the Kubernetes [CronJob documentation](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/).
