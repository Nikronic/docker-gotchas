## Docker
Docker is an open platform for developing, shipping, and running applications. 

Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. 

Docker provides tooling and a platform to manage the **lifecycle** of your containers:
-   Develop your application and its supporting **components using containers**.
-   The container becomes the **unit for distributing and testing** your application.
-   When you’re ready, **deploy** your application into your production environment, **as a container** or an orchestrated service. This works the same whether your production environment is a local data center, a cloud provider, or a hybrid of the two.

**Docker’s portability and lightweight** nature also make it easy to dynamically manage workloads, **scaling up or tearing down** applications and services as business needs dictate, in near real time.

Docker Architecture is based on client(`docker`)-server(`dockerd`) model:
![[architecture.svg]]
*docker architecture*


## Image
Container image contains the container’s filesystem, and contains everything needed to run an application - all dependencies, configurations, scripts, binaries, etc. Simply put, an _image_ is a read-only template with instructions for creating a Docker container.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a **Dockerfile** with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. **When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt.** This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

## Container
Simply put, a container is a sandboxed process on your machine that is isolated from all other processes on the host machine. Simply put, a container is a runnable instance of an image. 

## The underlying technology
Docker uses a Linux kernel technology called `namespaces` to provide the isolated workspace called the _container_. When you run a container, Docker creates a set of _namespaces_ for that container.

These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.

## References
1. [Docker overview | Docker Documentation](https://docs.docker.com/get-started/overview/#docker-objects)
2. [Overview | Docker Documentation](https://docs.docker.com/get-started/)
3. 