Cloud native computing uses an open source software stack to be:

* Containerized. Each part (applications, processes, etc) is packaged in its own container. This facilitates reproducibility, transparency, and resource isolation.
* Dynamically orchestrated. Containers are actively scheduled and managed to optimize resource utilization.
* Microservices-oriented. Applications are segmented into microservices. This significantly increases the overall agility and maintainability of applications.”

An approach that builds software applications as microservices and runs them on a containerized and dynamically orchestrated platform to utilize the advantages of the cloud computing model.


## Container
The basic idea of containers is to package your software with everything you need to execute it into one executable package, e.g., a Java VM, an application server, and the application itself. You then run this container in a virtualized environment and isolate the contained application from its environment.

The main benefit of this approach is that the application becomes independent of the environment and that the container is highly portable. 

## Orchestration
Deploying your application with all dependencies into a container is just the first step. It solves the deployment problems you had previously, but if you want to benefit from a cloud platform fully, you’re experiencing new challenges.

Starting additional or shutting down running application nodes based on the current load of your system isn’t that easy. You need to

* monitor your system
* trigger the startup or shutdown of a container
* make sure that all required configuration parameters are in place
* balance the load between the active application instances
* share authentication secrets between your containers

Doing all of that manually requires a lot of effort and is too slow to react to unexpected changes in system load. You need to have the right tools in place that automatically do all of this. This is what the different orchestration solutions are built for. A few popular ones are Docker Swarm, Kubernetes, Apache Mesos and Amazon’s ECS.
