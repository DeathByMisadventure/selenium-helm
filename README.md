# Selenium-Grid Helm Chart

A Helm chart for creating a Selenium grid server in Kubernetes

![Version: 4.29.0](https://img.shields.io/badge/Version-4.29.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 4.29.0-20250303](https://img.shields.io/badge/AppVersion-4.29.0--20250303-informational?style=flat-square)

**Homepage:** <https://github.com/DeathByMisadventure/selenium-helm>

## Why this chart?

The official [Selenium-Grid helm chart](https://github.com/SeleniumHQ/docker-selenium/blob/trunk/charts/selenium-grid/README.md)
works great of course and is fully featured, with things like autoscaling and other features.  The chart includes 6 different
helm dependencies.  It's pretty complex.

Don't need all those capabilities?  That's why this chart exists.

## Installing the chart

To install the selenium-grid helm chart, you can run:

```bash
# Clone the project
git clone https://github.com/DeathByMisadventure/selenium-helm.git

# Install basic grid
helm install selenium-grid .

# Or install full grid (Router, Distributor, EventBus, SessionMap and SessionQueue components separated)
helm install selenium-grid --set isolateComponents=true .
```

## Updating Selenium-Grid release

Once you have a new chart version, you can update your selenium-grid running:

```bash
helm upgrade selenium-grid .
```

## Uninstalling Selenium Grid release

To uninstall:

```bash
helm uninstall selenium-grid
```

## Configuration

## Values

| Key | Type | Description |
|-----|------|-------------|
| busConfigMap.annotations | object | Custom annotations for configmap |
| busConfigMap.name | string | Name of the configmap |
| chromeNode.annotations | object | Annotations for chrome-node pods |
| chromeNode.dshmVolumeSizeLimit | string | Size limit for DSH volume mounted in container (if not set, default is "1Gi") |
| chromeNode.enabled | bool | Enable chrome nodes |
| chromeNode.extraEnvFrom | string | Custom environment variables by sourcing entire configMap, Secret, etc. for chrome nodes |
| chromeNode.extraEnvironmentVariables | string | Custom environment variables for chrome nodes |
| chromeNode.imageName | string | Image of chrome nodes |
| chromeNode.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| chromeNode.labels | object | Labels for chrome-node pods |
| chromeNode.nodeSelector | object | Node selector for chrome-node container |
| chromeNode.ports | list | Port list to enable on container |
| chromeNode.replicas | int | Number of chrome nodes |
| chromeNode.resources | object | Resources for chrome-node container |
| chromeNode.securityContext.allowPrivilegeEscalation | bool |  |
| chromeNode.securityContext.capabilities.drop[0] | string |  |
| chromeNode.securityContext.readOnlyRootFilesystem | bool |  |
| chromeNode.securityContext.runAsNonRoot | bool |  |
| chromeNode.securityContext.seccompProfile.type | string |  |
| chromeNode.seleniumPort | int | Selenium port (spec.ports[0].targetPort in kubernetes service) |
| chromeNode.seleniumServicePort | int | Selenium port exposed in service (spec.ports[0].port in kubernetes service) |
| chromeNode.service.annotations | object | Custom annotations for service |
| chromeNode.service.enabled | bool | Create a service for node |
| chromeNode.service.type | string | Service type |
| chromeNode.tolerations | list | Tolerations for chrome-node container |
| components.distributor.annotations | object | Custom annotations for Distributor pod |
| components.distributor.imageName | string | Distributor image name |
| components.distributor.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.distributor.nodeSelector | object | Node selector for Distributor container |
| components.distributor.port | int | Distributor port |
| components.distributor.resources | object | Resources for Distributor container |
| components.distributor.serviceAnnotations | object | Custom annotations for Distributor service |
| components.distributor.serviceType | string | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.distributor.tolerations | list | Tolerations for Distributor container |
| components.eventBus.annotations | object | Custom annotations for Event Bus pod |
| components.eventBus.imageName | string | Event Bus image name |
| components.eventBus.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.eventBus.nodeSelector | object | Node selector for Event Bus container |
| components.eventBus.port | int | Event Bus port |
| components.eventBus.publishPort | int | Port where events are published |
| components.eventBus.resources | object | Resources for event-bus container |
| components.eventBus.serviceAnnotations | object | Custom annotations for Event Bus service |
| components.eventBus.serviceType | string | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.eventBus.subscribePort | int | Port where to subscribe for events |
| components.eventBus.tolerations | list | Tolerations for Event Bus container |
| components.extraEnvFrom | string | Custom environment variables by sourcing entire configMap, Secret, etc. for all components |
| components.extraEnvironmentVariables | string | Custom environment variables for all components |
| components.router.annotations | object | Custom annotations for router pod |
| components.router.imageName | string | Router image name |
| components.router.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.router.livenessProbe | object | Liveness probe settings |
| components.router.nodeSelector | object | Node selector for router container |
| components.router.port | int | Router port |
| components.router.readinessProbe | object | Readiness probe settings |
| components.router.resources | object | Resources for router container |
| components.router.serviceAnnotations | object | Custom annotations for router service |
| components.router.serviceType | string | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.router.tolerations | list | Tolerations for router container |
| components.sessionMap.annotations | object | Custom annotations for Session Map pod |
| components.sessionMap.imageName | string | Session Map image name |
| components.sessionMap.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.sessionMap.nodeSelector | object | Node selector for Session Map container |
| components.sessionMap.port | int | Session Port |
| components.sessionMap.resources | object | Resources for Session Map container |
| components.sessionMap.serviceAnnotations | object | Custom annotations for Session Map service |
| components.sessionMap.serviceType | string | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.sessionMap.tolerations | list | Tolerations for Session Map container |
| components.sessionQueue.annotations | object | Custom annotations for Session Queue pod |
| components.sessionQueue.imageName | string | Session Queue image name |
| components.sessionQueue.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.sessionQueue.nodeSelector | object | Node selector for Session Queue container |
| components.sessionQueue.port | int | Queue Port |
| components.sessionQueue.resources | object | Resources for Session Queue container |
| components.sessionQueue.serviceAnnotations | object | Custom annotations for Session Queue service |
| components.sessionQueue.serviceType | string | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.sessionQueue.tolerations | list | Tolerations for Session Queue container |
| customLabels | object | Custom labels for k8s resources |
| edgeNode.annotations | object | Annotations for edge-node pods |
| edgeNode.dshmVolumeSizeLimit | string | Size limit for DSH volume mounted in container (if not set, default is "1Gi") |
| edgeNode.enabled | bool | Enable edge nodes |
| edgeNode.extraEnvFrom | string | Custom environment variables by sourcing entire configMap, Secret, etc. for edge nodes |
| edgeNode.extraEnvironmentVariables | string | Custom environment variables for edge nodes |
| edgeNode.imageName | string | Image of edge nodes |
| edgeNode.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| edgeNode.labels | object | Labels for edge-node pods |
| edgeNode.nodeSelector | object | Node selector for edge-node container |
| edgeNode.ports | list | Port list to enable on container |
| edgeNode.replicas | int | Number of edge nodes |
| edgeNode.resources | object | Resources for edge-node container |
| edgeNode.securityContext.allowPrivilegeEscalation | bool |  |
| edgeNode.securityContext.capabilities.drop[0] | string |  |
| edgeNode.securityContext.readOnlyRootFilesystem | bool |  |
| edgeNode.securityContext.runAsNonRoot | bool |  |
| edgeNode.securityContext.seccompProfile.type | string |  |
| edgeNode.seleniumPort | int | Selenium port (spec.ports[0].targetPort in kubernetes service) |
| edgeNode.seleniumServicePort | int | Selenium port exposed in service (spec.ports[0].port in kubernetes service) |
| edgeNode.service.annotations | object | Custom annotations for service |
| edgeNode.service.enabled | bool | Create a service for node |
| edgeNode.service.type | string | Service type |
| edgeNode.tolerations | list | Tolerations for edge-node container |
| firefoxNode.annotations | object | Annotations for firefox-node pods |
| firefoxNode.dshmVolumeSizeLimit | string | Size limit for DSH volume mounted in container (if not set, default is "1Gi") |
| firefoxNode.enabled | bool | Enable firefox nodes |
| firefoxNode.extraEnvFrom | string | Custom environment variables by sourcing entire configMap, Secret, etc. for firefox nodes |
| firefoxNode.extraEnvironmentVariables | string | Custom environment variables for firefox nodes |
| firefoxNode.imageName | string | Image of firefox nodes |
| firefoxNode.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| firefoxNode.labels | object | Labels for firefox-node pods |
| firefoxNode.nodeSelector | object | Node selector for firefox-node container |
| firefoxNode.ports | list | Port list to enable on container |
| firefoxNode.replicas | int | Number of firefox nodes |
| firefoxNode.resources | object | Resources for firefox-node container |
| firefoxNode.securityContext.allowPrivilegeEscalation | bool |  |
| firefoxNode.securityContext.capabilities.drop[0] | string |  |
| firefoxNode.securityContext.readOnlyRootFilesystem | bool |  |
| firefoxNode.securityContext.runAsNonRoot | bool |  |
| firefoxNode.securityContext.seccompProfile.type | string |  |
| firefoxNode.seleniumPort | int | Selenium port (spec.ports[0].targetPort in kubernetes service) |
| firefoxNode.seleniumServicePort | int | Selenium port exposed in service (spec.ports[0].port in kubernetes service) |
| firefoxNode.service.annotations | object | Custom annotations for service |
| firefoxNode.service.enabled | bool | Create a service for node |
| firefoxNode.service.type | string | Service type |
| firefoxNode.tolerations | list | Tolerations for firefox-node container |
| global.seleniumGrid.imageTag | string | Image tag for all selenium components |
| global.seleniumGrid.nodesImageTag | string | Image tag for browser's nodes |
| hub.annotations | object | Custom annotations for Selenium Hub pod |
| hub.extraEnvFrom | string | Custom environment variables by sourcing entire configMap, Secret, etc. for selenium-hub |
| hub.extraEnvironmentVariables | string | Custom environment variables for selenium-hub |
| hub.imageName | string | Selenium Hub image name |
| hub.imagePullPolicy | string | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| hub.labels | object | Custom labels for Selenium Hub pod |
| hub.livenessProbe | object | Liveness probe settings |
| hub.nodeSelector | object | Node selector for selenium-hub container |
| hub.port | int | Selenium Hub port |
| hub.publishPort | int | Port where events are published |
| hub.readinessProbe | object | Readiness probe settings |
| hub.resources | object | Resources for selenium-hub container |
| hub.securityContext.allowPrivilegeEscalation | bool |  |
| hub.securityContext.capabilities.drop[0] | string |  |
| hub.securityContext.readOnlyRootFilesystem | bool |  |
| hub.securityContext.runAsNonRoot | bool |  |
| hub.securityContext.seccompProfile.type | string |  |
| hub.serviceAnnotations | object | Custom annotations for Selenium Hub service |
| hub.serviceType | string | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| hub.subscribePort | int | Port where to subscribe for events |
| hub.tolerations | list | Tolerations for selenium-hub container |
| ingress.annotations | object | Additional ingress annotations |
| ingress.className | string | Ingress class type |
| ingress.enabled | bool | Enable ingress |
| ingress.hostname | string |  |
| ingress.path | string |  |
| ingress.tls | list |  |
| isolateComponents | bool | Deploy Router, Distributor, EventBus, SessionMap and Nodes separately |
