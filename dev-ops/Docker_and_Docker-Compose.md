# Docker and docker-compose
Docker and Docker Compose are powerful tools for containerizing applications and managing multi-container applications, respectively. Here are some best practices for using them:

1. **Use Official Images**: Whenever possible, use official Docker images for your base images. They are well-maintained and often receive security updates promptly.

2. **Keep Images Small**: Large images take longer to download and consume more disk space. Use multi-stage builds, avoid unnecessary packages, and clean up after installing packages to keep your images small.

3. **One Process per Container**: Each container should have only one responsibility. If your application consists of multiple processes, consider splitting them into separate containers.

4. **Use .dockerignore**: Just like .gitignore, .dockerignore file can help you exclude files that are not necessary for building a Docker image, such as local environment configs, logs, and node modules.

5. **Don't Use Latest Tag**: The latest tag can lead to unpredictable results because it's not clear which version of the image will be pulled. Always specify an explicit version for your base images.

6. **Use Environment Variables for Configuration**: Docker provides built-in support for environment variables to configure your containers. This allows you to avoid hard-coding configuration values into your Dockerfile or image.

7. **Use Docker Compose for Multi-Container Applications**: Docker Compose makes it easy to manage applications that consist of multiple containers. Define your services, networks, and volumes in a docker-compose.yml file, and manage them all with a single command.

8. **Use Networks and Volumes**: Docker networks provide isolation and communication between containers, and Docker volumes provide persistent storage. Use them instead of linking containers and storing data in the container's filesystem.

9. **Health Checks**: Implement health checks in your application and use Docker's HEALTHCHECK instruction to let Docker know how to test if your application is working correctly.

10. **Keep Your Images Up-to-Date**: Regularly rebuild your images to pick up security updates in base images and dependencies. Consider using a tool like Dependabot to automate this.

11. **Use Labels**: Docker labels provide a way to add metadata to your images, containers, volumes, and networks. They can be used for organization, documentation, or automation.

12. **Don't Run as Root**: For security reasons, don't run your application as root in the container. Instead, create a user in your Dockerfile and switch to that user.
# Questions
1. Containerization vs Virtualization. Explain difference
2. What is dockerfile and image? What is entrypoint? How to build image?
3. What does it mean layers in terms of docker image?
4. How to mount file system to your docker container?
5. How to execute code within container which is run?
6. Which volume types docker support?
7. What is multistage build? Explain usecases.
8. What is docker-compose? Explain usecases.
9. What is docker-compose file? How to run docker-compose?
10. How to specify dependency between componetns inside docker-compose file?
11. What is docker networks? Explain usecases.
12. How to use docker-compose for different environments? (docker-compose overrides)
13. Explain difference between networks: bridge vs host vs overlap
14. What is docker plugins? Explain usecases.
15. How to share your images? What is docker registry? How to publish your image?
# Answers
1. Containerization vs Virtualization: Virtualization involves running multiple operating systems on a single physical server. Each operating system runs on a virtual machine that emulates a complete hardware system, from processor to network card. In contrast, containerization involves encapsulating an application in a container with its own operating environment. This is a lightweight alternative to a full virtual machine, and allows applications to be run on any system without worrying about dependencies.

2. Dockerfile is a text file that contains the instructions to build a Docker image. It defines what goes on in the environment inside your container. An image is a lightweight, stand-alone, executable package that includes everything needed to run a piece of software. The ENTRYPOINT of a Dockerfile is the command that will be run when a container is started from the image. To build an image, you use the `docker build` command.

3. Layers in a Docker image represent each instruction in the Dockerfile that modifies the filesystem. Each layer is only a set of differences from the layer before it. Layers are stacked on top of each other to form a Docker image.

4. To mount a file system to your Docker container, you can use the `-v` or `--mount` flag with the `docker run` command. This allows you to map a directory or file from the host machine to the container.

5. To execute code within a running Docker container, you can use the `docker exec` command followed by the container ID and the command you want to run.

6. Docker supports three types of volumes: host, anonymous, and named. Host volumes are directories from the host machine that are mounted into the container. Anonymous volumes are created automatically by Docker and are not given an explicit name. Named volumes are manually created by users and have a specific name assigned to them.

7. Multistage build is a feature in Docker that allows you to build an image in multiple stages, each with its own base image and instructions. This can help to reduce the size of the final image by excluding unnecessary tools and intermediate files.

8. Docker Compose is a tool for defining and running multi-container Docker applications. It uses a YAML file to specify the services, networks, and volumes for your application, and provides a set of commands to manage the application as a whole.

9. A Docker Compose file is a YAML file that defines the services, networks, and volumes for a multi-container Docker application. You can run Docker Compose using the `docker-compose up` command.

10. To specify dependencies between services in a Docker Compose file, you can use the `depends_on` option. This ensures that the dependent services are started before the service that depends on them.

11. Docker networks provide isolation and communication between containers. They can be used to segment the network for your application, control communication between containers, and provide a way for containers to discover each other.

12. To use Docker Compose for different environments, you can use multiple Docker Compose files and override the configuration as needed. You can specify multiple files with the `-f` option when running `docker-compose` commands.

13. Docker supports several network drivers, each with its own use cases. The bridge network is the default network for standalone containers. The host network adds a container on the host’s network stack, and is only available for swarm services on Docker 17.06 and higher. The overlay network is for services to communicate across multiple Docker daemons, which means that it is for swarm services or for stack deployments.

14. Docker plugins are extensions that add new capabilities to the Docker engine. This can include new storage drivers, network drivers, or even new commands. They can be used to integrate Docker with other tools or to add features that are not included in the core Docker engine.

15. To share your Docker images, you can push them to a Docker registry. A Docker registry is a storage and distribution system for Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can push an image to a registry using the `docker push` command.