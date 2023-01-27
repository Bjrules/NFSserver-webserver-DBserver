#### This project implements NETWORK FILE SYSTEM (NFS) on a <REHL> server  with three other web servers sharing the same file!
[Project Diagram](Screenshot_20230123_100807.png)
 ![Attching Volume](Screenshot_20230114_231413.png%0D) 
 ![Attaching volume to ec2 instance](Screenshot_20230114_231427.png)
 ![lsblk to inspect what block devices are attached to the server  then df -h to check info about the disk](Screenshot_20230114_231836.png)
 ![use sudo gdisk with p,n,w,y prompts then lsblk to check the success](Screenshot_20230114_232505.png)
 ![sudo yum install lvm2 to install logical volume management](Screenshot_20230114_232532.png)
 !['sudo pvcreate /dev/xvdf1' to create physical volumes and also did same for other partitions /dev/xvdg1 /dev/xvdh1](Screenshot_20230114_232802.png)
 !['sudo pvs' to seethe physical volumes and  'sudo vgcreate tooling-box-data-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1' to create a volume group](Screenshot_20230114_233356.png)
 !['sudo vgs' to see the volume group and also   'sudo lvcreate -n lv-opt -L 9G tool-box-data-vg' and also for lv-apps and lv-opts then use 'sudo lvs' to view the logical volumes](Screenshot_20230114_234112.png)

 ![sudo vgdisplay -v #view complete setup - VG, PV, and LV  sudo lsblk](Screenshot_20230114_234254.png)

 ![complete set-up](Screenshot_20230114_234242.png)

 !['sudo mkfs -t xfs /dev/tool-box-data-vg/apps-lv-opt' 'sudo mkfs -t xfs /dev/tool-box-data-vg/lv-apps' 'sudo mkfs -t xfs /dev/tool-box-data-vg/lv-logs'  to format the three logical volumes with xfs filesystem 'sudo mkdir -R /mnt/apps'  sudo mkdir -R /mnt/logs'  'sudo mkdir -R /mnt/opt'](Screenshot_20230114_235526.png)

 ![mounting and syncing ](Screenshot_20230114_235702.png)
 ![mounting and syncing](Screenshot_20230114_235953.png)

![installing , starting and enabling NFS server](Screenshot_20230115_000356.png)

![setting permmissions and chonging ownershinp so that the mount points which are /mnt/app /mnt/opt /mnt/logs can be accesible, restarts nfs.server and edit /etc/exports](Screenshot_20230115_001540.png)

![setting permmissions and chonging ownershinp so that the mount points which are /mnt/app /mnt/opt /mnt/logs can be accesible, restarts nfs.server and edit /etc/exports](Screenshot_20230115_001909.png)

![sudo vi /etc/exports](Screenshot_20230115_001916.png)
![check if they are on the same CIDR](Screenshot_20230115_001951.png)

![sudo exportfs -arv](Screenshot_20230115_002038.png)

![Alt text](Screenshot_20230115_002157.png)

![Alt text](Screenshot_20230115_002404.png)
![Configuring security rules for Accessibility ](Screenshot_20230115_002812.png)

##### SET UP THE DB SERVER with creating a user 'webaccess' and creating a Database 'tooling'
![Installing MySQL](Screenshot_20230115_003646.png)

![Installing MySQL](Screenshot_20230115_003918.png)

![Creating tooling Database](Screenshot_20230115_004531.png)

![Granting Permissions](Screenshot_20230115_010329.png)

![installing  mySQLClient on webserver NB: configure security group on DB server to accept from the  web-server-IP-Address ](Screenshot_20230115_010455.png%0D) 

![login in remotely to MYSQL-SERVER from the webserver](Screenshot_20230115_010912.png)

![](Screenshot_20230115_010939.png)

![Alt text](Screenshot_20230118_230226.png)

#### Set up webserver on REHL Install and configure Httpd


1. install nfs-client on webserver using : sudo yum install nfs-utils nfs4-acl-tools -y

![Alt text](Screenshot_20230118_230237.png)

2. sudo mkdir /var/www

3. sudo mount -t nfs -o rw,nosuid 172.31.85.124:/mnt/apps /var/www
   
4. 
![use sudo blkid first then edit the /etc/fstab file](Screenshot_20230119_002935.png) ![sudo vi /etc/fstab to ensure persistence after reboot ](Screenshot_20230120_001152.png)

![remember to mount for logs and opt aswell](Screenshot_20230120_001207.png)
 
 ![installing httpd and the dependencies](Screenshot_20230119_003102.png)

 ### NB: I forked the repo from dare.io git account to my repo then i used: git clone https://github.com/Bjrules/tooling-website-NFS.git to my local folder which i later Zipped and sent to my webserver via 'scp -i nfs-client.pem tooling.zip ec2-user@172.31.83.95:/home/ec2-user

 ![Dependencies installation](Screenshot_20230119_004336.png) 
 
 ##### editing the tooling-db.sql script file and executing it on the Database 

  ![screenshot](Screenshot_20230123_003339.png)
  

 
![Success](Screenshot_20230123_003352.png)

###### i also set the Http protocol security rule on the webserver to be able to view it in browser
![Alt text](Screenshot_20230123_003451.png)
![Alt text](Screenshot_20230123_003502.png)

THe End

The Threshold.



