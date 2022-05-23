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
- 

# What is Container Orchestration?
- helps us in managing containers

