### Debugging_Openstack_with_Pycharm-Pro5

-----

In this archive, I will guide configuration to debug Neutron project by Pycharm 5 professional . And configuration with other projects are similar to Neutron project.

#### Step 1: Setup environment

We need two machines and topology as below:

<img class="image__pic js-image-pic" src="http://i.imgur.com/hVGNksP.png" alt="" id="screenshot-image">

- Machine 1 (called "Pycharm-Pro5"): Installing Pycharm-Pro5.

- Machine 2 (called "VM"): Installing Openstack-AIO by Devstack.

*Note:* 

- We will use Devstack to install Openstack-AIO. This is [local.conf](https://github.com/NguyenHoaiNam/Debuging_Openstack_with_Pycharm-Pro5/blob/master/local.conf) file.

#### Step 2: Configuration Pycharm on Pycharm-Pro5

##### Step 2.1: Setup Deverlopment by clicking Tools --> Deployment --> Configuration then click "+" to create a "Devstack"

<img class="image__pic js-image-pic" src="http://image.prntscr.com/image/27222f597a0142d4820597d1a6ef4ed5.png" alt="" id="screenshot-image">

- (1): Type of connect to VM. We will choose SFTP.

- (2): The address of VM.

- (3): The account of VM.

- (4): The password of VM.

*Note*: In this step, we should check to connect to VM by choice "Test SFTP connection..."

Then we jump "Mappings" tab. To configure mapping between Pycharm-Pro5 and VM is like image:

<img class="image__pic js-image-pic" src="http://i.imgur.com/NVfR55X.png" alt="" id="screenshot-image">

- (5): This is local path on Pycharm-Pro5.

- (6): This is path on VM.

Click OK.

##### Step 2.2: Setup project by clicking File --> Settings then choose "Project: neutron" (in this case, I am setting debug with neutron project, with other projects are similar.)


Choice "Project Interpreter" to add an interpreter remote by choice "Add remote":

<img class="image__pic js-image-pic" src="http://i.imgur.com/jxd7NT8.png" alt="" id="screenshot-image">

After choice "Add remote", we have image:

<img class="image__pic js-image-pic" src="http://i.imgur.com/DYQhW7x.png" alt="" id="screenshot-image">

Change "Deployment configuration" then click "ssh://stack@10.10.10.30:22" to connect to VM. In this time, we will receive message "Successfully ...."

<img class="image__pic js-image-pic" src="http://i.imgur.com/efOR8ol.png" alt="" id="screenshot-image">

We need to wait a time so that Pycharm download packet from VM.


##### Step 2.3: Configuration Python Debugger. In "Settings", we choose "Build, Execution, Deployment" --> "Python Debugger" then select "Gevent compatible"

<img class="image__pic js-image-pic" src="http://i.imgur.com/mQohhvJ.png" alt="" id="screenshot-image">


After done, we click OK.

#### Step 3: Configuration debug with Neutron prject

In this step, I will configure debug with neutron-server. With other component or other project, they are similar.

##### Step 3.1: Create tab debug by clicking Run --> Edit Configurations then create a neutron-server debug like that:

<img class="image__pic js-image-pic" src="http://i.imgur.com/8oHtJwY.png" alt="" id="screenshot-image">

##### Step 3.2: Configuration API-worker on VM

Because Pycharm-Pro5 debug only one process so we have to configure on VM so that neutron-server run only one process.

Edit configure file /etc/neutron/neutron.conf. At first line we change api_workers = -1

(note that in nova api configuration, the config for only one process api worker is osapi_worker = 1. The nova API daemon does not accept negative value)

##### Step 3.3: After changing configuration file, turn off neutron-server process on VM. (Hint: you can use rejoin-stack to do that).

#### Step 4: Start debugging

After finishing all steps. We can start debug by click "debug" button. Have fun !!!

**Optional**: If you want to locally debugging your openstack neutron, please apply monkey patch for eventlet for collecting debug information from openstack process. In neutron, edit file __init__.py in neutron/common/eventlet_utils.py and modify line 32 from: 

```python
eventlet.monkey_patch()
```
to:
```python
eventlet.monkey_patch(os=False, thread=False)
```

Happy debugging !
