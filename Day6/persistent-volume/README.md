## Things to consider while storing data
- applications that persistent data shouldn't use Pod storage, as Pods might be removed by OpenShift as part of
  scale up/down
- applications that persistent data should use external storage like NFS shared folders, Amazon S3, etc.,
- In OpenShift, applications that require storage they have to request OpenShift via PersistentVolumeClaim
- Administrators generally create PersistentVolume of different size, access mode, storage class, etc.,
- When applications request for Persistent Volume storage via PersistentVolumeClaim, OpenShift will scan through
  the cluster looking for a matching Persistent Volume that matches the size, access and storage class(if any). 
  When OpenShift finds a matching PersistentVolume it binds the Persistent Volume with the respective Claim, allowing
  the application to use the storage
  
## Let's deploy mysql that uses external NFS storage

Let's create the Persistent Volume of size 500MB from one of the NFS shared folder
```
cd ~/tekton-may-2022
git pull
cd Day6

oc apply persistent-volume/mysql-pv.yml
```

Let's now create a Persistent Volume Claim that mysql deployment can use
```
cd ~/tekton-may-2022
git pull
cd Day6

oc apply persistent-volume/mysql-pvc.yml
```

Let's finally deploy the mysql application
```
cd ~/tekton-may-2022
git pull
cd Day6

oc apply persistent-volume/mysql-deploy.yml
```
