Install helm
Install Docker
Install kind
Install skaffold

Helm use case
helm create api

# Rename
Then rename the folder to helm-chart

# Manage secrets
Create a secret yaml. Don't forget to edit the api.fullname

Update the secret values in values.yaml

Change the deployments.yaml. Add 
          envFrom:
            - secretRef:
                name: {{ include "api.fullname" . }}-secrets


# Manage Ports
Change the service.type.port to 8080 or your desiarable port

Change the service.yaml file as well 
spec.ports.targetPort: {{ .Values.service.port }}

Change the deployment.yaml file as well 
spec.template.spec.containers.ports.containerPort: {{ .Values.service.port }}
Change the liveness readiness port as well from the deployment as well


