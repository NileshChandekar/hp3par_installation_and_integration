# HP3PAR Installation and Deployment with Integration of Packstack-10/RHOSP-10/RHOSP-13

Tested and working on all above Openstack Environemnt. 

## Warning

For RHOSP-13, HP3Par lefthand is not supported as its a containerized environment.  
There are some tweak to make it work. 

We will not take you throught the process of Packstack-10/OSP10/13 installation.


What's included
---------------
* Hp3Par Installtion on KVM
* Static IP Configuration of Hp3Par
* CMC Installtion on Lubuntu (as CMC required GUI, we decided to take light weight GUI)
* Connect CMC with Hp3Par
* User Management, RAID Creation, 
* Integration of Hp3Par with Openstack (Packstack-10/RHOSP-10 & RHOSP-13) 
* Testing

Prerequisites
--------------------------
* To Begin with installation make sure you fulfill the following prerequisites
  - Minimum of one node to add into cluster 
  - Node Specifications: 4Gb RAM, 3*10GB Disk(which should be added once VSA node is ready)
  - Hpe LeftHand setup tar file 
    - HPE_StoreVirtual_KVM_VSA_and_StoreVirtual_FOM_Installer_TA688-10554.tgz
    - 
  
Hp3Par Installation steps
--------------------------
* First Check if you enough space for /var/lib/libvirt/images atleast of 150GB
* Open the virt-manager of you base machine.
* Click on File->New Virtual Machine 
* Choose Fourth option `Import existing disk image` and then click on *Forwad*



CMC Installation steps
--------------------------



Integration with Openstack Environemnt :-
------------------------------------------



Packstack Integration :-
------------------------


RHOSP-10 Integration :- 
-----------------------

 
RHOSP-13 Integration :- 
-----------------------

