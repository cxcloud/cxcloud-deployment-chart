# CX Cloud deployment chart

CX Cloud deployment chart is a Helm chart for deploying microservices easily into a Kubernetes cluster. The helm chart has support for the [AWS Load Balancer Controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/) and works well together with [Amazon EKS](https://aws.amazon.com/eks).

## Getting started

### Installing the chart

Add the repository:

```bash
helm repo add cxcloud https://cxcloud.github.io/helm-charts
```

Update repositories:

```bash
helm repo update
```

To install the chart with version `0.1.2` and release name `my-release` into the namespace `production`:

```bash
helm upgrade -i my-release cxcloud/cxcloud-deployment-chart \
  --version 0.1.2 \
  --namespace production
```

### Uninstalling the Chart

To uninstall the `my-release` deployment from namespace `kube-system`:

```bash
helm uninstall my-release --namespace kube-system
```

### Configuration

The following table list the configurable parameters of the chart and their default values.

| Parameter | Description | Default |
| --- | --- | --- |
| name | Name for the microservice | cxcloud |
| replicaCount | Amount of pods | 2 |
| image.repository | Repository for docker image  | 012345678901.dkr.ecr.eu-west-1.amazonaws.com/cxcloud-service |
| image.tag | Docker image tag | 0.1.0 |
| image.pullPolicy | Image pull policy | IfNotPresent |
| restartPolicy | The restartPolicy applies to all containers in the Pod | Always |
| service.type | Service Type | ClusterIP |
| service.ports | Port configuration map | http default configuration |
| service.ports.http | Name of the port configuration | http |
| service.ports.port | Exposed Kubernetes port | 80 |
| service.ports.targetPort | Application port, service send requests to this port | 8080 |
| service.ports.protocol | Application protocol | TCP |
| awsLbController.enabled | Enable AWS LoadBalancer Controller | true |
| awsLbController.groupName | specifies the group name that this Ingress belongs to | cxcloud |
| awsLbController.groupOrder | specifies the order across all Ingresses within IngressGroup | 0 |
| awsLbController.host | Host name for routing rules | "" |
| awsLbController.path | Application path for routing rules | /* |
| awsLbController.listenPorts.http | Specifies the http port that ALB used to listen on | "80" |
| awsLbController.listenPorts.https | Specifies the https port that ALB used to listen on | "" |
| awsLbController.redirectToHTTPSPort | Redirect http traffic to the https port | false |
| awsLbController.targetType | Specifies how to route traffic to pods. You can choose between instance and ip | ip |
| awsLbController.scheme | Specifies whether your LoadBalancer will be internet facing | internal |
| awsLbController.certificateArn | specifies the ARN of one or more certificate managed by AWS Certificate Manager | "" |
| awsLbController.healthCheck.path | specifies the HTTP path when performing health check on targets | / |
| awsLbController.healthCheck.port | specifies the port used when performing health check on targets | 80 |
| awsLbController.healthCheck.successCodes | specifies the HTTP status code that should be expected when doing health checks against the specified health check path | 200 |
| awsLbController.healthCheck.interval | specifies the interval (in seconds) between health check of an individual target | 10 |
| awsLbController.healthCheck.timeout | specifies the timeout (in seconds) during which no response from a target means a failed health check | 10 |
| awsLbController.healthCheck.healthyThreshold | specifies the consecutive health checks successes required before considering an unhealthy target healthy | 2 |
| awsLbController.healthCheck.unhealthyThreshold | specifies the consecutive health check failures required before considering a target unhealthy | 2 |
| awsLbController.annotations | Additional AWS Load Balancer Controller [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/guide/ingress/annotations/) | {} |
| healthChecks | Kubernetes health check probes for pods | {} |
| rollingUpdate | Default rolling update strategy | maxSurge: 25%, maxUnavailable: 25% |
| env | Pod environment variables as maps | {} |
| resources | CPU and memory resources object for pods | limits and requests objects |
| nodeSelector | Kubernetes node selection constraint | {} |
| tolerations | Tolerations are applied to pods, and allow (but do not require) the pods to schedule onto nodes with matching taints | [] |
| affinity | constrain which nodes your pod is eligible to be scheduled on | {} |

## License

MIT © [CXCloud](https://docs.cxcloud.com)
