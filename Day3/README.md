# Day 3

## You may like these blogs
https://developers.redhat.com/blog/2019/01/15/podman-managing-containers-pods#podman_pods__what_you_need_to_know
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/building_running_and_managing_containers/assembly_working-with-pods_building-running-and-managing-containers
https://blog.neuvector.com/article/advanced-kubernetes-networking

## Install Code Ready Containers on your System
##### ℹ️ Installing Code Ready Containers in Linux
:x: Please do not try this in our lab environment as it will corrupt our OpenShift cluster installation.  These instructions are here to help you in setting up OpenShift in your personal laptop/desktop post the training for your self-learning purposes only.

```
cd /home/alchemy/Downloads
tar xvf crc-linux-amd64.tar.xz
cd crc-linux-1.38.0-amd64
./crc setup
```

The expected output is
<pre>
jegan@ubuntu:~/Downloads/crc-linux-1.38.0-amd64$ <b>./crc setup</b>
INFO Checking if running as non-root              
INFO Checking if running inside WSL2              
INFO Checking if crc-admin-helper executable is cached 
INFO Checking for obsolete admin-helper executable 
INFO Checking if running on a supported CPU architecture 
INFO Checking minimum RAM requirements            
INFO Checking if crc executable symlink exists    
INFO Checking if Virtualization is enabled        
INFO Checking if KVM is enabled                   
INFO Checking if libvirt is installed             
INFO Checking if user is part of libvirt group    
INFO Checking if active user/process is currently part of the libvirt group 
INFO Checking if libvirt daemon is running        
INFO Checking if a supported libvirt version is installed 
INFO Checking if crc-driver-libvirt is installed  
INFO Installing crc-driver-libvirt                expose
INFO Checking crc daemon systemd service          
INFO Setting up crc daemon systemd service        
INFO Checking crc daemon systemd socket units     
INFO Setting up crc daemon systemd socket units   
INFO Checking if AppArmor is configured           
INFO Updating AppArmor configuration              
INFO Using root access: Updating AppArmor configuration 
[sudo] password for jegan: 
INFO Using root access: Changing permissions for /etc/apparmor.d/libvirt/TEMPLATE.qemu to 644  
INFO Checking if systemd-networkd is running      
INFO Checking if NetworkManager is installed      
INFO Checking if NetworkManager service is running 
INFO Checking if dnsmasq configurations file exist for NetworkManager 
INFO Checking if the systemd-resolved service is running 
INFO Checking if /etc/NetworkManager/dispatcher.d/99-crc.sh exists 
INFO Writing NetworkManager dispatcher file for crc 
INFO Using root access: Writing NetworkManager configuration to /etc/NetworkManager/dispatcher.d/99-crc.sh 
INFO Using root access: Changing permissions for /etc/NetworkManager/dispatcher.d/99-crc.sh to 755  
INFO Using root access: Executing systemctl daemon-reload command 
INFO Using root access: Executing systemctl reload NetworkManager 
INFO Checking if libvirt 'crc' network is available 
INFO Setting up libvirt 'crc' network             
INFO Checking if libvirt 'crc' network is active  
INFO Starting libvirt 'crc' network               
INFO Checking if CRC bundle is extracted in '$HOME/.crc' 
INFO Checking if /home/jegan/.crc/cache/crc_libvirt_4.9.12.crcbundle exists 
INFO Extracting bundle from the CRC executable    
INFO Ensuring directory /home/jegan/.crc/cache exists 
INFO Extracting embedded bundle crc_libvirt_4.9.12.crcbu:moneybag:ndle to /home/jegan/.crc/cache 
INFO Uncompressing crc_libvirt_4.9.12.crcbundle   
crc.qcow2: 11.69 GiB / 11.69 GiB [------------------------------------------------------] 100.00%
oc: 117.16 MiB / 117.16 MiB [-----------------------------------------------------------] 100.00%
Your system is correctly setup for using CodeReady Containers, you can now run 'crc start' to start the OpenShift cluster
</pre>

##### ℹ️ Starting your local CRC OpenShift Cluster
:x:  Please don't attempt this in our training lab.

```
./crc start
```
The expected output is
<pre>
[jegan@tektutor crc-linux-1.38.0-amd64]$ <b>./crc start</b>
INFO Checking if running as non-root              
INFO Checking if running inside WSL2              
INFO Checking if crc-admin-helper executable is cached 
INFO Checking for obsolete admin-helper executable 
INFO Checking if running on a supported CPU architecture 
INFO Checking minimum RAM requirements            
INFO Checking if crc executable symlink exists    
INFO Checking if Virtualization is enabled        
INFO Checking if KVM is enabled                   
INFO Checking if libvirt is installed             
INFO Checking if user is part of libvirt group    
INFO Checking if active user/process is currently part of the libvirt group 
INFO Checking if libvirt daemon is running        
INFO Checking if a supported libvirt version is installed 
INFO Checking if crc-driver-libvirt is installed  
INFO Checking crc daemon systemd socket units     
INFO Checking if systemd-networkd is running      
INFO Checking if NetworkManager is installed      
INFO Checking if NetworkManager service is running 
INFO Checking if /etc/NetworkManager/conf.d/crc-nm-dnsmasq.conf exists 
INFO Checking if /etc/NetworkManager/dnsmasq.d/crc.conf exists 
INFO Checking if libvirt 'crc' network is available 
INFO Checking if libvirt 'crc' network is active  
INFO Starting CodeReady Containers VM for OpenShift 4.9.12... 
INFO CodeReady Containers instance is running with IP 192.168.130.11 
INFO CodeReady Containers VM is running           
INFO Check internal and public DNS query...       
INFO Check DNS query from host...                 
INFO Verifying validity of the kubelet certificates... 
INFO Starting OpenShift kubelet service           
INFO Waiting for kube-apiserver availability... [takes around 2min] 
INFO Waiting for user's pull secret part of instance disk... 
INFO Starting OpenShift cluster... [waiting for the cluster to stabilize] 
INFO All operators are available. Ensuring stability... 
INFO Operators are stable (2/3)...                
INFO Operators are stable (3/3)...                
INFO Adding crc-admin and crc-developer contexts to kubeconfig... 
Started the OpenShift cluster.
penShift Installer Provisioned Ins
The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: B8XxM-aY9yz-zhwJY-5HU7d

Log in as user:expose
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  $ eval $(crc oc-env)
  $ oc login -u developer https://api.crc.testing:6443
[jegan@tektutor crc-linux-1.38.0-amd64]$ 
</pre>
when the crc prompts for pull secret, you need to paste the content of pull-secret.txt and hit enter.

##### ℹ️ Troubleshooting CRC start
:x:  Please don't attempt this in our training lab.

It is commonly noticed that ./crc start command fails many times. 

Make sure

1. Virtualization is enabled (VT-X/AMD-V)
2. You have sufficient RAM in the system atleast 16GB or more
3. You have alteast 8 vCPU in your system

Try to stop and startAgreement

```
./crc stop
./crc start
```

##### ℹ️ Login to CRC Cluster as a developer via CLI
:x:  Please don't attempt this in our training lab.

```
eval $(./crc oc-env)
oc login -u developer https://api.crc.testing:6443
```

##### ℹ️ Login to CRC Cluster as an administrator via CLI
:x:  Please don't attempt this in our training lab.

```
eval $(./crc oc-env)
oc login -u kubeadmin https://api.crc.testing:6443
```

# What is a Kubernetes/OpenShift Service?

- Service represents a group of similar Pods( Pods from same Deployment )
- all the pods in a Service will have same labels
- label selector is used to identify the Pods that belong to a particular service
- Service offers load-balancing to the group of Pods (Pods from same Deployment )
- You can create a Service for a group of nginx Pods
- You can create another Service for a group of tomcat Pods
- Yet another for mysql Pods

# What is an Ingress?
- ingress is a routing rule
- Ingress is a Kubernetes feature which also works in OpenShift
- For example
  www.tekutor.org - This should take me to Home Page
  www.tektutor.org/login - This url should invoke Login service
  www.tektutor.org/logout - This url should invoke Logout service
  www.tektutor.org/blog - This url should invoke the blog service

If you notice above, based on the url path, the call is routed to different services within the website

For Ingress to work in Kubernetes/OpenShift, we need an Ingress Controller.

Ingress Controller if present in the OpenShift/Kubernetes Cluster, it listens for new Ingress rules created
in the Cluter.
Whenever it detects new Ingress/updated Ingress rules, the Ingress Controller picks the ingress rules
and configures the Load Balancer to perform the routing to the corresponding service.

1. Load Balancer ( Nginx, HAProxy, etc., )
2. Ingress Controller 
   - In Managed OpenShift Service from AWS/AZure,Ingress Controller comes out of the box
5. Ingress Rule ( This is defined by Web Developer/DevOps Engineer )

# What is a route?
- OpenShift feature which isn't present Kubernetes
- In OpenShift, every service is generally created as clusterip service
- If service will be accessed externally, then a route will be created for the clusterIP service.
- If the service is accessed only within the cluster, then no route is created
- route only forwards the call to a single service
