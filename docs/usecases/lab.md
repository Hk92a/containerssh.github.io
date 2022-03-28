title: Dynamic lab environment

## Problem

In a lab environment you want to give SSH access to several people: students, contractors, etc. There are several requirements:

1. **Authentication:** Each user should be able to log in with their own username and password or SSH key, and only get access to their own environment.
2. **Resource restriction:** The environment should be resource-restricted, one user should not be able to use up all system resources.
3. **Cleanup:** When a user logs out the environment should be cleaned up.
4. **Monitoring:** The activities of the user should be monitored.

## How a traditional setup looks like

1. **Authentication:** Authentication is done by creating system users, either directly or via a PAM integration. SSH key-based authentication is difficult or impossible to manage, depending on the requirements.
2. **Resource restriction:** Resource restrictions are difficult or even impossible to implement.
3. **Cleanup:** The environment is not cleaned up after a user, the servers need to be reinstalled frequently.
4. **Monitoring:** Basic login monitoring is provided by the system, more advanced logging is difficult.

## How ContainerSSH helps

1. **Authentication:** ContainerSSH natively talks to an external authentication provider via webhooks.
2. **Resource restriction:** Each user container can be configured with resource restrictions for CPU, memory, disk IO, and network, depending on the capabilities of the backend (Docker, Kubernetes, etc).
3. **Cleanup:** ContainerSSH launches ephemeral containers that are removed when the user logs out. Persistent volumes can be mounted for each user dynamically.
4. **Monitoring:** ContainerSSH has a detailed audit log that is able to record everything that goes on via SSH, including file transfers.

## How to build it

As a first step, decide on a backend: Kubernetes is more scalable, but requires more work to get going. Docker is less scalable, but provides more capabilities for resource restriction out of the box.

Once you have 