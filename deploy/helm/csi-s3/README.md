# Helm chart for csi-s3

This chart adds S3 volume support to your cluster.

## Install chart

- Helm 2.x: `helm install [--set secret.accessKey=... --set secret.secretKey=... ...] --namespace kube-system --name csi-s3 .`
- Helm 3.x: `helm install [--set secret.accessKey=... --set secret.secretKey=... ...] --namespace kube-system csi-s3 .`

After installation succeeds, you can get a status of Chart: `helm status csi-s3`.

## Delete Chart

- Helm 2.x: `helm delete --purge csi-s3`
- Helm 3.x: `helm uninstall csi-s3 --namespace kube-system`

## Configuration

By default, this chart creates a secret and a storage class. You should at least set `secret.accessKey` and `secret.secretKey`
to your [Yandex Object Storage](https://cloud.yandex.com/en-ru/services/storage) keys for it to work.

The following table lists all configuration parameters and their default values.

| Parameter                                           | Description                                                            | Default                                                |
| --------------------------------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------ |
| `storageClass.create`                               | Specifies whether the storage class should be created                  | true                                                   |
| `storageClass.name`                                 | Storage class name                                                     | csi-s3                                                 |
| `storageClass.singleBucket`                         | Use a single bucket for all dynamically provisioned persistent volumes |                                                        |
| `storageClass.mounter`                              | Mounter to use. Either geesefs, s3fs or rclone. geesefs recommended    | geesefs                                                |
| `storageClass.mountOptions`                         | GeeseFS mount options                                                  | `--memory-limit 1000 --dir-mode 0777 --file-mode 0666` |
| `storageClass.reclaimPolicy`                        | Volume reclaim policy                                                  | Delete                                                 |
| `storageClass.annotations`                          | Annotations for the storage class                                      |                                                        |
| `secret.create`                                     | Specifies whether the secret should be created                         | true                                                   |
| `secret.name`                                       | Name of the secret                                                     | csi-s3-secret                                          |
| `secret.accessKey`                                  | S3 Access Key                                                          |                                                        |
| `secret.secretKey`                                  | S3 Secret Key                                                          |                                                        |
| `secret.endpoint`                                   | Endpoint                                                               | https://storage.yandexcloud.net                        |
| `secret.region`                                     | Region                                                                 |                                                        |
| `tolerations.all`                                   | Tolerate all taints by the CSI-S3 node driver (mounter)                | false                                                  |
| `tolerations.node`                                  | Custom tolerations for the CSI-S3 node driver (mounter)                | []                                                     |
| `tolerations.controller`                            | Custom tolerations for the CSI-S3 controller (provisioner)             | []                                                     |
| `hostNetwork.node`                                  | Run the CSI-S3 node driver (mounter) with host network                 | false                                                  |
| `hostNetwork.controller`                            | Run the CSI-S3 controller (provisioner) with host network              | false                                                  |
| `resourceLimits.node.registrar.cpuRequests`         | CPU requests for the node driver registrar sidecar                     | 100m                                                   |
| `resourceLimits.node.registrar.cpuLimits`           | CPU limits for the node driver registrar sidecar                       | 1                                                      |
| `resourceLimits.node.registrar.memory`              | Memory requests and limits for the node driver registrar               | 64Mi                                                   |
| `resourceLimits.node.csi.cpuRequests`               | CPU requests for the CSI-S3 node plugin                                | 100m                                                   |
| `resourceLimits.node.csi.cpuLimits`                 | CPU limits for the CSI-S3 node plugin                                  | 1                                                      |
| `resourceLimits.node.csi.memory`                    | Memory requests and limits for the CSI-S3 node plugin                  | 64Mi                                                   |
| `resourceLimits.controller.provisioner.cpuRequests` | CPU requests for the provisioner sidecar                               | 100m                                                   |
| `resourceLimits.controller.provisioner.cpuLimits`   | CPU limits for the provisioner sidecar                                 | 1                                                      |
| `resourceLimits.controller.provisioner.memory`      | Memory requests and limits for the provisioner                         | 64Mi                                                   |
| `resourceLimits.controller.csi.cpuRequests`         | CPU requests for the CSI-S3 controller plugin                          | 100m                                                   |
| `resourceLimits.controller.csi.cpuLimits`           | CPU limits for the CSI-S3 controller plugin                            | 1                                                      |
| `resourceLimits.controller.csi.memory`              | Memory requests and limits for the CSI-S3 controller                   | 64Mi                                                   |
