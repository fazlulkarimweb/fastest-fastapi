## Why You Need Faster FastAPI

Let's imagine you're starting a FastAPI project and someone hands you a boilerplate code to kickstart your development. You may wonder why you should consider using it instead of starting from scratch. Well, here are six benefits that make it worth your consideration:

1. ⚡ **Unmatched Speed**: This FastAPI implementation is blazingly fast, thanks to its use of the latest PyPy interpreter instead of traditional Python. The code is optimized for maximum performance, and you can hardly make it any faster. At best with a few hours of tweaking, you can achieve the same lightning-fast results, which you can avail instantly,

2. 🐳 **Simplified Dockerization**: While setting up a basic Dockerfile for a Python and FastAPI project is straightforward, things can get messy and error-prone when incorporating PyPy. Fortunately, we've already prepared a well-structured Dockerfile that perfectly integrates PyPy. By leveraging our Dockerfile, you don't have to spend time reinventing the wheel.

3. 🚀 **Production-Ready Foundation**: Building a production-ready codebase often requires countless hours of effort. By forking or using this boilerplate code as a foundation, you save an immense amount of time. The code is already optimized, follows best practices, and is ready to be deployed to a production environment with minimal modifications.

4. 💻 **Real-Time Development and Testing**: Imagine writing your code and instantly seeing the results. With this boilerplate, it's possible. When you save your code in VSCode, the entire application is automatically Dockerized, pushed to a local Kind Kubernetes cluster, and made accessible through port-forwarding. You can view your application in real-time on your laptop, exactly as your customers would see it from server. Handling with poetry is not needed. You see what your customers or peer developers will see without time-consuming deployment testing. If it works in a machine, it will wor everywhere.

5. ☁️ **Kubernetes-First Approach**: If you want to develop with a focus on Kubernetes deployment, this boilerplate is tailored for you. It allows you to write your code and immediately observe how it behaves in a production Kubernetes cluster. Whether you fork the code or download it, you can start development right away with Kubernetes in mind, except juggling with random yaml k8 files. Because, we wrote a production ready helm chart for you.

6. 🌟 **Industry Best Practices**: Rest assured that the codebase you'll be working with is the same one used in production environments. We've followed industry best practices throughout its microservices oriented development, ensuring code quality, scalability, and maintainability.

By considering these benefits, you can leverage this faster FastAPI boilerplate to accelerate your development process and deliver high-quality, performant applications.


## Prerequisites

To create you developer environment to start this project you will need to have this in your operation system. Install these developer tools first. 


### Installation Links

Here are the installation links for the required tools to run this project:

- **Helm**:
  - Official Helm installation: [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)
- **Skaffold**:
  - Official Skaffold installation: [https://skaffold.dev/docs/install/](https://skaffold.dev/docs/install/)
- **Kind**:
  - Official Kind installation: [https://kind.sigs.k8s.io/docs/user/quick-start/](https://kind.sigs.k8s.io/docs/user/quick-start/)
- **Docker**:
  - Docker installation: [https://www.docker.com/get-started](https://www.docker.com/get-started)
- **kubectl**:
  - Kubernetes official installation: [https://kubernetes.io/docs/tasks/tools/](https://kubernetes.io/docs/tasks/tools/)

Please refer to these links for detailed instructions on installing each tool based on your operating system.


## Getting Started

Once you have installed all the necessary tools, follow these steps to proceed:

1. 🐳 Open Docker Desktop.
2. 🖥️ Open a terminal.
3. 📂 Navigate to the directory where the project is located.
4. ⚙️ Create a `kind` cluster for the first time. After creating it, you won't need to do it again. To create a `kind` cluster, run the following command in the terminal:
   ```bash
   kind create cluster --name faster-fastapi
   ```
5. ▶️ From the terminal, start the app by running the command:
   ```bash
   skaffold dev
   ```
6. 🌐 Visit `localhost:8080` in your web browser to see the changes.

Now, open the `fastapi/app/main.py` file:

```python
# Start developing from here. When you save a line of code, see the changes automatically in `localhost:8080`.

from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def hello_world():
    return {"Hello": "World"}
```

You can begin developing your FastAPI application from the specified file. Whenever you save a line of code, you will see the changes automatically reflected in `localhost:8080`. Happy coding!

---

## FAQ and other Features ✨

### How to add more python library? 📚
Add your python library to the `requirements.txt` file. Rest assured, no local installation is needed. 🐍

### How to set up environment variables? ⚙️
Of course, you need environment variables. We follow the best practices. Considering the CI/CD pipeline scenario, we store the environment variables for both development and production environments in the following files. Please edit both files. 🌐

- `fastapi/dev.env.yaml` for development environments
- `fastapi/prod.env.yaml` for production environments

```yaml
secrets:
  ENVVARIABLE1: "envvalue1"
  ENVVARIABLE2: "envvalue2"
```

Here you can add your environment variables. Later, you will find these environment variables in your FastAPI application. All variables are stored using Kubernetes secrets with the help of Helm. ⚓️

In a more serious production environment, where you don't want to store environment variables in the codebase, you can set more secret environment variables on the fly from your CI/CD pipeline. 💻

```bash
helm upgrade --install --set-json='secret={"envkey1":"envvalue1","envkey2":"envvalue2"}' -f ./fastapi/prod.env.yaml fastapi ./fastapi/helm-chart
``` 

### How to enable auto scaling in production Kubernetes cluster? ⚖️
It's easy. You just have to update the `fastapi/production.env.yaml` file. 🚀

```yaml
resources:
  limits:
    cpu: 250m # 25% of 1 CPU core
    memory: 256Mi
  requests:
    cpu: 250m # 25% of 1 CPU core
    memory: 256Mi

autoscaling:
  enabled: true
  minReplicas: 1
  maxReplicas: 100 # Edit the max replica you want
  targetCPUUtilizationPercentage: 80
  # targetMemoryUtilizationPercentage: 80
```

### How will I add custom Kubernetes YAML? 📄

First, create a Kubernetes YAML file in the `k8-yaml-files` directory. Then update the `skaffold.yaml` file like this. 🔧

```yaml
manifests:
  rawYaml:
    - ./k8-yaml-files/namespace.yaml # For creating namespaces
    - ./k8-yaml-files/dockerconfigjson.yaml # For creating image pull secrets 
    - ./k8-yaml-files/ingress-nginx.yaml # For creating ingress-nginx
```

### How to add an image pull secret in production? 🤐

Update the `prod.env.yaml` file with the following entry. 🔒

```yaml
imagePullSecrets: [{ name: dockerconfigjson-github-com }]
```

Refer to the above section to add the `dockerconfigjson` YAML. 

### How to add custom image name and tag in CI/CD pipeline 

With Helm, it's easy. Just set the variables. 

```shell
helm upgrade --install --set image.repository=fastapi --set image.tag=latest -f ./fastapi/prod.env.yaml fastapi ./fastapi/helm-chart
```

### How to change ports ⚓️

The default port is `8080`. If you want to change it to `9090`, you need to perform three tasks. 🔄

1. Change the `Dockerfile` to `EXPOSE 9090/tcp`.
2. Add the following to your

`prod.env.yaml` and `dev.env.yaml` files:

```yaml
service:
  type: ClusterIP
  port: 9090
```

3. In your `skaffold.yaml` file, add the following section.

```yaml
portForward:
  - resourceType: deployment
    resourceName: fastapi 
    port: 9090
    address: 0.0.0.0
    localPort: 9090
``` 

### How to increase replica in production? 📦
By default, the `replicaCount` is 1. To increase it, add the following line to your `prod.env.yaml` and `dev.env.yaml` files. 

```yaml
replicaCount: 3
```

### What to do if I need more customization? ✨

Go to `fastapi/helm-chart/values.yaml` and tweak it according to your needs. 🛠️ 

Contributions are welcome as well. We are also open to discussion.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)


<!-- Here is the content converted to Markdown:

---

## Install helm
Install Helm on your system. 

## Helm use case
Use Helm to manage your FastAPI application.

```shell
helm create fastapi
```

## Rename
Rename the folder to "helm-chart".

## Manage secrets
Create a secret YAML file. Make sure to edit the `fastapi.fullname`.

Update the secret values in the `values.yaml` file.

Change the `deployments.yaml` file to include the following:

```yaml
envFrom:
  - secretRef:
      name: {{ include "fastapi.fullname" . }}-secrets
```

## Manage Ports
Change the `service.type.port` to `8080` or your desired port.

Also, update the `service.yaml` file:

```yaml
spec.ports.targetPort: {{ .Values.service.port }}
```

Update the `deployment.yaml` file as well:

```yaml
spec.template.spec.containers.ports.containerPort: {{ .Values.service.port }}
```

Make sure to change the liveness and readiness ports in the deployment file as well.
 -->
