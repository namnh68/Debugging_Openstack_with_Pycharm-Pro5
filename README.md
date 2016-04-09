### Debuging_Openstack_with_Pycharm-Pro5
Guide configure debug Openstack with Pycharm-Pro5

-----

In this archive, I will guide configuration to debug Neutron project. And debugging other projects are similar.

#### Step 1: Setup environment

We need two machines and topology as below:

<img class="image__pic js-image-pic" src="http://i.imgur.com/hVGNksP.png" alt="" id="screenshot-image">

- Machine 1 (called "Pycharm-Pro5"): Installing Pycharm-Pro5.

- Machine 2 (called "VM") : Installing Openstack-AIO by Devstack.

Note: 

- You can install Openstack via Devstack by clone Devstack repo then create local.conf [here] and run command `./stack.sh`

#### Step 2: Configuration Pycharm on Pycharm-Pro5

##### Step 2.1: Setup Deverlopment by clicking Tools --> Deployment --> Configuration then click "+" to create a "Devstack"

<img class="image__pic js-image-pic" src="http://image.prntscr.com/image/27222f597a0142d4820597d1a6ef4ed5.png" alt="" id="screenshot-image">

- (1): Type of connect to VM. We choose SFTP.

- (2): The address of VM.

- (3): The account of VM.

- (4): The password of VM.

Note: In this step, we should check to connect to VM by choose "Test SFTP connection..."

Then we jump "Mappings" tab. To configure mapping between Pycharm-Pro5 and VM like image:

<img class="image__pic js-image-pic" src="http://i.imgur.com/NVfR55X.png" alt="" id="screenshot-image">

- (5): This is local path on Pycharm-Pro5.

- (6): This is path on VM.

Click OK.

##### Step 2.2: Setup project by clicking File --> Settings then choose "Project: neutron" (in this case, I am setting debug with neutron project, with other projects are similar)


Choose "Project Interpreter" to add an interpreter remote by choose "Add remote":

<img class="image__pic js-image-pic" src="http://i.imgur.com/jxd7NT8.png" alt="" id="screenshot-image">

After choose "Add remote", we have image:

<img class="image__pic js-image-pic" src="http://i.imgur.com/DYQhW7x.png" alt="" id="screenshot-image">

Change "Deployment configuration" then click "ssh://stack@10.10.10.30:22" to connect to VM. In this time, we will response "Successfully ...." then click OK

<img class="image__pic js-image-pic" src="http://i.imgur.com/efOR8ol.png" alt="" id="screenshot-image">

We need to wait a time to Pycharm download packet from VM.


##### Step 2.3: Configuration Python Debugger. In "Settings", we choose "Build, Execution, Deployment" --> "Python Debugger" then select "Gevent compatible"

<img class="image__pic js-image-pic" src="http://i.imgur.com/mQohhvJ.png" alt="" id="screenshot-image">


After done, we click OK.

#### Step 3: Configuration debug with Neutron prject

In this step, I will configure debug with neutron-server. With other component or other project, they are similar.

##### Step 3.1: Create tab debug by clicking Run --> Edit Configurations then create a neutron-server debug like that:

<img class="image__pic js-image-pic" src="http://i.imgur.com/8oHtJwY.png" alt="" id="screenshot-image">

##### Step 3.2: Configuration API-worker on VM

Because Pycharm-Pro5 debug only one process so we have to configure on VM other that neutron-server run only one process.

Edit configure file /etc/neutron/neutron.conf. At first line we change api_workers = -1

##### Step 3.3: After change file configure, turn off process neutron-server on VM. (Hide: you can use rejoin-stack to do that).

#### Step 4: Start debug

After finished all steps. We can start debug by click "bug". Have fun !!!