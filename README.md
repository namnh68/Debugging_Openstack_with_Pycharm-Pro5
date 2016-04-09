### Debuging_Openstack_with_Pycharm-Pro5
Guide configure debug Openstack with Pycharm-Pro5

-----

In this archive, I will guide configuration to debug Neutron project. And debugging other projects are similar

Step 01: Setup environment


We need two machines and topology as below:

--image--

Machine 01 (call Pycharm-Pro5): Installing Pycharm-Pro5

Machine 02 (call VM) : Installing Openstack-AIO by Devstack

### Step 2: Configuration Pycharm on Pycharm-Pro5

#### 2.1: Setup Deverlopment by clicking Tools --> Deployment --> Configuration then click "+" to create a "Devstack"

--image--

(1): Type of connect to VM. We choose SFTP
(2): The address of VM
(3): The acount of VM
(4): The password of VM

Then we jump "Mappings" tab. To configure mapping between Pycharm-Pro5 and VM like picture


Then click OK.

#### 2.2 Setup project by clicking File --> Settings then choose "Project: neutron" (in this case, I am setting debug with neutron project, with other projects are similar)


Then choose "Project Interpreter" to add a interpreter remote by choose "Add remote" and follow these step


Change "Deployment configuration" then click "ssh://stack@10.10.10.30:22" to connect to VM. In this time, we will response "Successfully ...." then click OK


We need to wait a time to Pycharm download packet from VM


#### 2.3 Configuration Python Debugger. In "Settings", we choose "Build, Execution, Deployment" --> "Python Debugger" then select "Gevent compatible"

--image--


After done, we click OK

### Step 3: Configuration debug with Neutron prject

In this step, I will configure debug with neutron-server. With other component or other project, they are similar

#### 3.1 Create tab debug by clicking Run --> Edit Configurations then create a neutron-server debug like that:

--image--


#### 3.2 Configuration API-worker on VM

Because Pycharm-Pro5 deubug just one process so we have to configure on VM other that neutron-server run only one process

Edit configure file /etc/neutron/neutron.conf. At first line we change api_workers = -1

#### 3.3 After change file configure, turn off process neutron-server on VM. (Hide: you can use rejoin-stack to do that)

### Step 4: Start bebug

After finished all step. We can start dubug. Have fun !!!