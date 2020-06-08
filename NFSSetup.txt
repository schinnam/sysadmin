For our infrastructure in Stratos Datacenter we have a requirement to serve our website code from a common/shared location that can be shared among all app nodes. For this we came up with a solution to use NFS (Network File System) server that can store the data and we can mount the share among our app nodes. The dedicated NFS server going to be our storage server. To accomplish this task do the following given steps:


Install required NFS packages on storage server.

Configure storage server to act as an NFS server.

Make a NFS share /webapp on storage server.

Install and configure NFS client packages on all app nodes and configure them to act as NFS client.

Mount /webapp directory on all app nodes at /var/www/code directory (Create the directories if don't exist).

Start and enable required services.


 Solution:
 https://www.tecmint.com/install-nfs-server-on-centos-8/
 
 https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/deployment_guide/s1-nfs-server-config-exports#:~:text=The%20%2Fetc%2Fexports%20file%20controls,remote%20hosts%20and%20specifies%20options.&text=In%20this%20structure%2C%20replace%20%3Cexport,for%20that%20host%20or%20network.
 
 Install NFS Server
 vi /etc/exports
 /app  172.16.238.10(sync,rw) 172.16.238.10(sync,rw) 172.16.238.10(sync,rw)
 
 exportfs -arv
 mount | grep nfs
 
 Client:
 showmount -e 172.16.238.15
   >> Export list for 172.16.238.15:
   >> /app 172.16.238.12,172.16.238.11,172.16.238.10
 mkdir -p /var/www/appdata
 mount -t nfs  172.16.238.15:/app /var/www/appdata/
 
 
