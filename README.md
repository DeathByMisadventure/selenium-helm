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

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| busConfigMap.annotations | object | `{}` | Custom annotations for configmap |
| busConfigMap.name | string | `"selenium-event-bus-config"` | Name of the configmap |
| chromeNode.annotations | object | `{}` | Annotations for chrome-node pods |
| chromeNode.dshmVolumeSizeLimit | string | `"1Gi"` | Size limit for DSH volume mounted in container (if not set, default is "1Gi") |
| chromeNode.enabled | bool | `true` | Enable chrome nodes |
| chromeNode.extraEnvFrom | string | `nil` | Custom environment variables by sourcing entire configMap, Secret, etc. for chrome nodes |
| chromeNode.extraEnvironmentVariables | string | `nil` | Custom environment variables for chrome nodes |
| chromeNode.imageName | string | `"selenium/node-chrome"` | Image of chrome nodes |
| chromeNode.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| chromeNode.labels | object | `{}` | Labels for chrome-node pods |
| chromeNode.nodeSelector | object | `{}` | Node selector for chrome-node container |
| chromeNode.ports | list | `[5553]` | Port list to enable on container |
| chromeNode.replicas | int | `1` | Number of chrome nodes |
| chromeNode.resources | object | `{"limits":{"cpu":"1","memory":"500Mi"},"requests":{"cpu":".1","memory":"200Mi"}}` | Resources for chrome-node container |
| chromeNode.securityContext.allowPrivilegeEscalation | bool | `false` |  |
| chromeNode.securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| chromeNode.securityContext.readOnlyRootFilesystem | bool | `false` |  |
| chromeNode.securityContext.runAsNonRoot | bool | `true` |  |
| chromeNode.securityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| chromeNode.seleniumPort | int | `5900` | Selenium port (spec.ports[0].targetPort in kubernetes service) |
| chromeNode.seleniumServicePort | int | `6900` | Selenium port exposed in service (spec.ports[0].port in kubernetes service) |
| chromeNode.service.annotations | object | `{}` | Custom annotations for service |
| chromeNode.service.enabled | bool | `true` | Create a service for node |
| chromeNode.service.type | string | `"ClusterIP"` | Service type |
| chromeNode.tolerations | list | `[]` | Tolerations for chrome-node container |
| components.distributor.annotations | object | `{}` | Custom annotations for Distributor pod |
| components.distributor.imageName | string | `"selenium/distributor"` | Distributor image name |
| components.distributor.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.distributor.nodeSelector | object | `{}` | Node selector for Distributor container |
| components.distributor.port | int | `5553` | Distributor port |
| components.distributor.resources | object | `{}` | Resources for Distributor container |
| components.distributor.serviceAnnotations | object | `{}` | Custom annotations for Distributor service |
| components.distributor.serviceType | string | `"ClusterIP"` | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.distributor.tolerations | list | `[]` | Tolerations for Distributor container |
| components.eventBus.annotations | object | `{}` | Custom annotations for Event Bus pod |
| components.eventBus.imageName | string | `"selenium/event-bus"` | Event Bus image name |
| components.eventBus.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.eventBus.nodeSelector | object | `{}` | Node selector for Event Bus container |
| components.eventBus.port | int | `5557` | Event Bus port |
| components.eventBus.publishPort | int | `4442` | Port where events are published |
| components.eventBus.resources | object | `{}` | Resources for event-bus container |
| components.eventBus.serviceAnnotations | object | `{}` | Custom annotations for Event Bus service |
| components.eventBus.serviceType | string | `"ClusterIP"` | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.eventBus.subscribePort | int | `4443` | Port where to subscribe for events |
| components.eventBus.tolerations | list | `[]` | Tolerations for Event Bus container |
| components.extraEnvFrom | string | `nil` | Custom environment variables by sourcing entire configMap, Secret, etc. for all components |
| components.extraEnvironmentVariables | string | `nil` | Custom environment variables for all components |
| components.router.annotations | object | `{}` | Custom annotations for router pod |
| components.router.imageName | string | `"selenium/router"` | Router image name |
| components.router.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.router.livenessProbe | object | `{"enabled":true,"failureThreshold":10,"initialDelaySeconds":10,"path":"/readyz","periodSeconds":10,"successThreshold":1,"timeoutSeconds":10}` | Liveness probe settings |
| components.router.nodeSelector | object | `{}` | Node selector for router container |
| components.router.port | int | `4444` | Router port |
| components.router.readinessProbe | object | `{"enabled":true,"failureThreshold":10,"initialDelaySeconds":12,"path":"/readyz","periodSeconds":10,"successThreshold":1,"timeoutSeconds":10}` | Readiness probe settings |
| components.router.resources | object | `{}` | Resources for router container |
| components.router.serviceAnnotations | object | `{}` | Custom annotations for router service |
| components.router.serviceType | string | `"NodePort"` | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.router.tolerations | list | `[]` | Tolerations for router container |
| components.sessionMap.annotations | object | `{}` | Custom annotations for Session Map pod |
| components.sessionMap.imageName | string | `"selenium/sessions"` | Session Map image name |
| components.sessionMap.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.sessionMap.nodeSelector | object | `{}` | Node selector for Session Map container |
| components.sessionMap.port | int | `5556` | Session Port |
| components.sessionMap.resources | object | `{}` | Resources for Session Map container |
| components.sessionMap.serviceAnnotations | object | `{}` | Custom annotations for Session Map service |
| components.sessionMap.serviceType | string | `"ClusterIP"` | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.sessionMap.tolerations | list | `[]` | Tolerations for Session Map container |
| components.sessionQueue.annotations | object | `{}` | Custom annotations for Session Queue pod |
| components.sessionQueue.imageName | string | `"selenium/session-queue"` | Session Queue image name |
| components.sessionQueue.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| components.sessionQueue.nodeSelector | object | `{}` | Node selector for Session Queue container |
| components.sessionQueue.port | int | `5559` | Queue Port |
| components.sessionQueue.resources | object | `{}` | Resources for Session Queue container |
| components.sessionQueue.serviceAnnotations | object | `{}` | Custom annotations for Session Queue service |
| components.sessionQueue.serviceType | string | `"ClusterIP"` | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| components.sessionQueue.tolerations | list | `[]` | Tolerations for Session Queue container |
| customLabels | object | `{}` | Custom labels for k8s resources |
| edgeNode.annotations | object | `{}` | Annotations for edge-node pods |
| edgeNode.dshmVolumeSizeLimit | string | `"1Gi"` | Size limit for DSH volume mounted in container (if not set, default is "1Gi") |
| edgeNode.enabled | bool | `true` | Enable edge nodes |
| edgeNode.extraEnvFrom | string | `nil` | Custom environment variables by sourcing entire configMap, Secret, etc. for edge nodes |
| edgeNode.extraEnvironmentVariables | string | `nil` | Custom environment variables for edge nodes |
| edgeNode.imageName | string | `"selenium/node-edge"` | Image of edge nodes |
| edgeNode.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| edgeNode.labels | object | `{}` | Labels for edge-node pods |
| edgeNode.nodeSelector | object | `{}` | Node selector for edge-node container |
| edgeNode.ports | list | `[5553]` | Port list to enable on container |
| edgeNode.replicas | int | `1` | Number of edge nodes |
| edgeNode.resources | object | `{"limits":{"cpu":"1","memory":"500Mi"},"requests":{"cpu":".1","memory":"200Mi"}}` | Resources for edge-node container |
| edgeNode.securityContext.allowPrivilegeEscalation | bool | `false` |  |
| edgeNode.securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| edgeNode.securityContext.readOnlyRootFilesystem | bool | `false` |  |
| edgeNode.securityContext.runAsNonRoot | bool | `true` |  |
| edgeNode.securityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| edgeNode.seleniumPort | int | `5900` | Selenium port (spec.ports[0].targetPort in kubernetes service) |
| edgeNode.seleniumServicePort | int | `6900` | Selenium port exposed in service (spec.ports[0].port in kubernetes service) |
| edgeNode.service.annotations | object | `{}` | Custom annotations for service |
| edgeNode.service.enabled | bool | `true` | Create a service for node |
| edgeNode.service.type | string | `"ClusterIP"` | Service type |
| edgeNode.tolerations | list | `[]` | Tolerations for edge-node container |
| firefoxNode.annotations | object | `{}` | Annotations for firefox-node pods |
| firefoxNode.dshmVolumeSizeLimit | string | `"1Gi"` | Size limit for DSH volume mounted in container (if not set, default is "1Gi") |
| firefoxNode.enabled | bool | `true` | Enable firefox nodes |
| firefoxNode.extraEnvFrom | string | `nil` | Custom environment variables by sourcing entire configMap, Secret, etc. for firefox nodes |
| firefoxNode.extraEnvironmentVariables | string | `nil` | Custom environment variables for firefox nodes |
| firefoxNode.imageName | string | `"selenium/node-firefox"` | Image of firefox nodes |
| firefoxNode.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| firefoxNode.labels | object | `{}` | Labels for firefox-node pods |
| firefoxNode.nodeSelector | object | `{}` | Node selector for firefox-node container |
| firefoxNode.ports | list | `[5553]` | Port list to enable on container |
| firefoxNode.replicas | int | `1` | Number of firefox nodes |
| firefoxNode.resources | object | `{"limits":{"cpu":"1","memory":"500Mi"},"requests":{"cpu":".1","memory":"200Mi"}}` | Resources for firefox-node container |
| firefoxNode.securityContext.allowPrivilegeEscalation | bool | `false` |  |
| firefoxNode.securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| firefoxNode.securityContext.readOnlyRootFilesystem | bool | `false` |  |
| firefoxNode.securityContext.runAsNonRoot | bool | `true` |  |
| firefoxNode.securityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| firefoxNode.seleniumPort | int | `5900` | Selenium port (spec.ports[0].targetPort in kubernetes service) |
| firefoxNode.seleniumServicePort | int | `6900` | Selenium port exposed in service (spec.ports[0].port in kubernetes service) |
| firefoxNode.service.annotations | object | `{}` | Custom annotations for service |
| firefoxNode.service.enabled | bool | `true` | Create a service for node |
| firefoxNode.service.type | string | `"ClusterIP"` | Service type |
| firefoxNode.tolerations | list | `[]` | Tolerations for firefox-node container |
| global.seleniumGrid.imageTag | string | `"4.29.0-20250303"` | Image tag for all selenium components |
| global.seleniumGrid.nodesImageTag | string | `"4.29.0-20250303"` | Image tag for browser's nodes |
| hub.annotations | object | `{}` | Custom annotations for Selenium Hub pod |
| hub.extraEnvFrom | string | `nil` | Custom environment variables by sourcing entire configMap, Secret, etc. for selenium-hub |
| hub.extraEnvironmentVariables | string | `nil` | Custom environment variables for selenium-hub |
| hub.imageName | string | `"selenium/hub"` | Selenium Hub image name |
| hub.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy (see https://kubernetes.io/docs/concepts/containers/images/#updating-images) |
| hub.labels | object | `{}` | Custom labels for Selenium Hub pod |
| hub.livenessProbe | object | `{"enabled":true,"failureThreshold":10,"initialDelaySeconds":10,"path":"/readyz","periodSeconds":10,"successThreshold":1,"timeoutSeconds":10}` | Liveness probe settings |
| hub.nodeSelector | object | `{}` | Node selector for selenium-hub container |
| hub.port | int | `4444` | Selenium Hub port |
| hub.publishPort | int | `4442` | Port where events are published |
| hub.readinessProbe | object | `{"enabled":true,"failureThreshold":10,"initialDelaySeconds":12,"path":"/readyz","periodSeconds":10,"successThreshold":1,"timeoutSeconds":10}` | Readiness probe settings |
| hub.resources | object | `{"limits":{"cpu":"1","memory":"500Mi"},"requests":{"cpu":".5","memory":"300Mi"}}` | Resources for selenium-hub container |
| hub.securityContext.allowPrivilegeEscalation | bool | `false` |  |
| hub.securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| hub.securityContext.readOnlyRootFilesystem | bool | `false` |  |
| hub.securityContext.runAsNonRoot | bool | `true` |  |
| hub.securityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| hub.serviceAnnotations | object | `{}` | Custom annotations for Selenium Hub service |
| hub.serviceType | string | `"ClusterIP"` | Kubernetes service type (see https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) |
| hub.subscribePort | int | `4443` | Port where to subscribe for events |
| hub.tolerations | list | `[]` | Tolerations for selenium-hub container |
| ingress.annotations | object | `{}` | Additional ingress annotations |
| ingress.className | string | `"nginx"` | Ingress class type |
| ingress.enabled | bool | `true` | Enable ingress |
| ingress.hosts[0] | string | `"selenium-hub.localdev.me"` |  |
| ingress.path | string | `"/"` |  |
| ingress.tls | list | `[]` |  |
| isolateComponents | bool | `false` | Deploy Router, Distributor, EventBus, SessionMap and Nodes separately |
