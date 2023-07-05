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

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)


<!-- Install helm
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

 -->
