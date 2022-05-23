# tekton-may-2022

# Hypervisor ( Virtualization Technology )
- helps you in running 2 or more Operating Systems side by side on the same machine
- Intel Processor
  - the virtualization feature is called VT-X
- AMD Processor
  - the virtualization feature is called AMD-V
- Popular Hyversior Softwares
 - VMWare
   - Workstation ( Type 2 Hypervisor runs on top of Host OS )
   - Player ( Type 2 Hypervisor runs on top of Host OS )
   - Fusion ( Mac OS-X) - Type2
   - vSphere ( Bare Metal Hypervisor ) - Type 1
 - Oracle
   - VirtualBox ( Type2 )
 - Parallels ( Mac OS-X )
 - Microsoft
   - Hyper-V
 - Virtual Machines ( Guest OS )
     - hosts a full functional operating system
     - requires dedicated hardware resources
       - dedicated CPU Cores
       - dedicated RAM
       - dedicated Storage
     - has dedicated OS Kernel
  
# Container Technology
- an application virtualization technology
- containers are nothing but application process that runs in a separate namespace
- containers shares the hardware resources on the OS where they are running
  - shares OS kernel
  - shares CPU Core
  - shared RAM
  - shares Storage ( HDD/SSD )
- lightweight virtualization technology unlike Hypervisor

## What makes people compare containers with virtual machine?
- containers just like VMs has their own IP Address
- containers just like VMs has their own network stack
- containers just like VMs has their own shell/command prompt
- it is for these reasons people tend to compare a container with a VM
- but containers are mere application process. Container are not OS.
- while VMs are a fully functional Operating System

# Container Engines
- Docker is one of most popular Container Engine
- CRI-O
- containerd
- LXC
- Podman is also gaining popularity ( used by RedHat OpenShift )

# What is Container Orchestration Platform ?
- helps us in managing containers
- self healing platform
- also helps in making the deployed applications Highly Available ( HA )
- also helps in scaling up/down your application on demand
- in built monitoring capabilities
  - automatically monitors the health of your application and heals them when required
  - load balancing
- supports different types of services ( internal and external services )
- helps in application rolling update
  - upgrading your application from one version to other without any down-time

## What are the various container orchestration platforms available?
- Docker SWARM
   - only support Docker container engine
- Google Kubernetes
   - supports many different container engines including Docker
- RedHat OpenShift
   - supports many different container engines including Docker
- AWS EKS ( Managed Kubernetes from Amazon - SaaS )
- Azure AKS ( Managed Kubernetes from Microsoft - SaaS )
- AWS ROSA ( Managed RedHat OpenShift from Amazon - SaaS  )
- Azure OpenShift Service ( Managed RedHat OpenShift from Microsoft - SaaS )

# Lab Setup
Dell Server ( Server 1 )
RAM - 512 GB RAM
64 Physical Cores 
6TB HDD Storage
Used by 8 participants

Dell Server ( Server 2 )
RAM - 512 GB RAM
64 Physical Cores 
Used by 7 participants
6TB HDD Storage
