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

Hp3Par Installation steps
--------------------------
~~~
Overview
~~~

~~~
Install HPE StoreVirtual VSA on ANY new server from ANY server vendor.** StoreVirtual VSA transforms unused capacity inside your servers into a shared storage array.
You get fully featured shared storage without the cost and complexity of dedicated storage hardware.
Register now and try HPE software-defined storage for free for 3 years.
Your license will be activated when you install the software.

NOTE: StoreVirtual VSA performs optimally when you install the same software version on every server in the management group.
Previously installed free versions of StoreVirtual VSA software can be upgraded with the purchase of a full license.

New customers:

    Download the latest HPE StoreVirtual Free 1TB VSA
~~~

###Begin Installation

* First Check if you enough space for /var/lib/libvirt/images atleast of 150GB

    <img src="images/hpe01.png" />

* If not check for the size on /home, For example in my case I have only 50GB for my partition and 2.7T on my /home

* Create a directory named images inside /home and run all the commands given below

    ```
    cd /var/lib/libvirt
    rm -rf images
    mkdir /home/images
    chcon -t virt_image_t /home/images
    ln -s /home/images .
    ```

* Inside /home/images extract your HPE_StoreVirtual_KVM_VSA_and_StoreVirtual_FOM_Installer_TA688-10554.tgz

    ~~~
    tar -xvf HPE_StoreVirtual_KVM_VSA_and_StoreVirtual_FOM_Installer_TA688-10554.tgz
    ~~~
* Then extract KVM-VSA-12.7.00.0226_01.img.tgz which you get after running the above command.

    ~~~
    tar -xvf KVM-VSA-12.7.00.0226_01.img.tgz
    ~~~
* Open the virt-manager of you base machine.
* Click on File → New Virtual Machine
* Choose Fourth option `Import existing disk image` and then click on *Forwad*
* Click on File->New Virtual Machine

    <img src="images/hpe02.png" width="600" />
* Choose Fourth option `Import existing disk image` and then click on *Forwad*

    <img src="images/hpe03.png" width="600" />

    <img src="images/hpe04.png" width="600" />

* Input the value of ram and cpus
* It will take upto 15 - 20 minutes to setup the machine.
* Once you get the login screen type *start* and press *enter*, you will get the below screen.

    <img src="images/hpe05.png" width="600" />
* Press *Enter* to login

    <img src="images/hpe06.png" width="600" />

* Go in *Network TCP/IP Settings*

    <img src="images/hpe08.png" width="600" />

* Hit enter and select 2nd option to get ip automatically from dhcp, you can also set ip manual if you want

    <img src="images/hpe09.png" width="600" />
* Press *Enter*

    <img src="images/hpe10.png" width="600" />

* Finally you will get the. This ip needs to be given in CMC which we will see further

    <img src="images/hpe12.png" width="600" />

CMC Installation steps
--------------------------
* Open your lubuntu session
    - Make Sure you have CMC bin file with you
        ~~~
         HPE_StoreVirtual_Centralized_Management_Console_for_Linux_64_bit_BM480-10622.bin
        ~~~
* Run the binary file you will see the following window

    <img src="images/cmc01.png" width="600" />
* Click on next
* Accept the license agreement

    <img src="images/cmc02.png" width="600" />
* Go with typical installation set

    <img src="images/cmc03.png" width="600" />
* Just go on clicking next

    <img src="images/cmc04.png" width="600" />

    <img src="images/cmc05.png" width="600" />

    <img src="images/cmc06.png" width="600" />

    <img src="images/cmc07.png" width="600" />

    <img src="images/cmc08.png" width="600" />

    <img src="images/cmc09.png" width="600" />

    <img src="images/cmc10.png" width="600" />



* Go to the directory /opt/HPE/StoreVirtual/UI/

    <img src="images/cmc11.png" width="600" />
* Hit the following command

    ~~~
    ./HPE\ StoreVirtual\ Centralized\ Management\ Console
    ~~~
* The CMC Window will open, it looks like the below figure

    <img src="images/cmc12.png" width="600" />

* Click on Add and enter the VSA node ip address

    <img src="images/cmc13.png" width="600" />

    <img src="images/cmc14.png" width="600" />
* Now click on `Getting Started` at left side

    <img src="images/cmc15.png" width="600" />

* Click next

    <img src="images/cmc16.png" width="600" />

* Create New Management Group

    <img src="images/cmc17.png" width="600" />
* Add management group name

    <img src="images/cmc19.png" width="600" />

* Create user and set password for the user

    <img src="images/cmc20.png" width="600" />

* Add ntp server ip address in next window

    <img src="images/cmc21.png" width="600" />

    <img src="images/cmc22.png" width="600" />

* Add DNS Server

    <img src="images/cmc23.png" width="600" />

* Enter the mail server ip address/domain
    - [Note: In my case I have given dummy information]

    <img src="images/cmc24.png" width="600" />

    <img src="images/cmc25.png" width="600" />

    <img src="images/cmc26.png" width="600" />

* Select the type of cluster I do not have `multi-site` so going for     `standard`

    <img src="images/cmc27.png" width="600" />

* Enter the Cluster name over there

    <img src="images/cmc28.png" width="600" />

* Now its time to enter the virtual ip, you virtual ip should be reachable from any instance in same network

    <img src="images/cmc29.png" width="600" />

* Enter all the required details

    <img src="images/cmc30.png" width="600" />


* Wait for some time since it takes time to create a management group

    <img src="images/cmc31.png" width="600" />

* You will get something like this

    <img src="images/cmc32.png" width="600" />


* You can see your cluster at the left side of panel

    <img src="images/cmc33.png" width="600" />



Integration with Openstack Environemnt :-
------------------------------------------



Packstack Integration :-
------------------------


RHOSP-10 Integration :-
-----------------------


RHOSP-13 Integration :-
-----------------------

