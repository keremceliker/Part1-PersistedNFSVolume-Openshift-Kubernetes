# Part 1 - Introduction & Configuration Storage Class & Persistent Volumes (PV/PVC) on OpenShift Advanced Container Platform / Kubernetes

*Written by Kerem ÇELİKER*
- Linkedin: **`linkedin.com/in/keremceliker`**
- Twitter: **`@CloudRss`**
- Blog: **`www.keremceliker.com`**



First of all, if you are on the Red Hat side, you can easily setup this using NFS-Ganesha on Gluster FS or Ceph FS

I definetely tested the Persistent Volume with NFS method with so many Vendors such as Qumulo, Pure Storage, Scality, Cohesity, Nutanix File, Isilon, Hitachi and Rubrik. It works seamlessly with all of them but version and software updates make differences as you know. That's why my reviews don't bind Vendors, they're based on my own testing and technical experience...

However, with other vendors such as the link below that I shared last time in linkedin post, I will show how you can do these operations on Red Hat Openshift on VMware vSAN (NativeFS)


I provided you I was going to introduce on to Qumulo last time. But you can do it with similar methods with other vendors. However, the Level of Difficulty to which this work is Easy is relative to each by Vendors :)

Anyway..Firstly you must start to Create NFS Export on Qumulo Storage

Honestly, It's easy understand to use and manage to Qumulo Dashboard. That's why I decided will not provide step-by-step on it how to create NFS-Export, Please kindly follow the link.

https://care.qumulo.com/hc/en-us/articles/360000723928-Create-an-NFS-Export

Notice: If you needed assistance on it, Ping me or Contact Qumulo Regional Care Support.

Im gonna be taking a look at persistent volumes what they are how we can use a persistent volume to store data in Openshift. Now Im gonna to take a look at a real life hands-on example.

Let's forget about pods kubernetes and containers for a second, please :)

What is state is normally just some form of data that our application needs in order to function now a container or pod or an application is just a process... There are 2 types of process that can run we can have a Stateless process and a Stateful process...

Stateless Process:

Stateless process is a process that does not rely on state or data in order to function. It does not store any state or data in memory or the filesystem and stateless usually like micro-services can come and go as they keep we can destroy the process and recreate the process without impacting for your users.

Statefull Process:

Statefull process relies on state in order to function they store states in only two places one is in the pure memory and the other is on disk. Memory allows fast access to your data and state and is usually used for caching application like ElasticSearch, Twistlock, PostgreSQL, Redis or Dynatrace w/MySQL and datastores rely on states in order to function and they store this either in memory for fast access but persistent they store it on disk the file system. It allows the database to come and go restore its state from disk. This meant its heavily reliance on the state in order to function.

The filesystem is the only way for state to persist among reboot. So when a process a dies and gets re-created it reads that state back from the filesystem...

What makes containers different to other processes ?

Container is just a process when rights to the file system like a database writing RDF ON MDF for whatever sort of file to the filesystem. It just writes to the file system of the host OS. Now the difference between a container and a process is that a container usually its own file system. When docker creates a container creates a virtual file system and attaches it to the that container. That's why it creates a virtual file system and attaches it to that container.

So unlike process on a host that have access to the whole file system containers have their own file system. So in container gets destroyed and recreated it loses the file system and the file system gets recreated against of files on lost.

Therefore the container file system is not persisted during restarts...


The life cycle of PersistentVolumeClaim/PersistentVolume resources is roughly divided into four stages

Provision: Create a PersistentVolume resource and the corresponding storage resource in the storage scheme used by this PersistentVolume

Bind: Establish a one-to-one correspondence between the most suitable PerisistentVolume and the PerisistentVolumeClaim created by the user.

Attach: If a pod uses this PerisistentVolumeClaim, then Attach the PerisistentVolume resource that is bound with this PerisistentVolumeClaim to the Node where the pod is located

Mount: Finally complete the remaining initialization steps of this PerisistentVolume on this machine, and mount it to a certain path for the actual use of the subsequent started container.

So once the use of PersistentVolumeClaim is abnormal (the pod using pvc cannot be started because the pvc initialization is unsuccessful), it is difficult for us to troubleshoot the problem. So the launch of this tool can help us quickly determine the problem of PersistentVolumeClaim.

I know its a little bit more complicated is the storage class but in Part 2, I'll be conveying in the simplest way how this is configured and used for sure.




References :

https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/




