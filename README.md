# HW5- Software Engineering

<b>Playbook files:</b>

1. [Ansible Playbook for setting up the task] (https://github.com/sohankunkerkar/SE_HW5/blob/master/ansible_play.yaml)
2. [EC2 Ansible Playbook] (https://github.com/sohankunkerkar/SE_HW5/blob/master/amazon.yaml)

<b>Steps for running ansible playbooks</b><br>

1. First create a vagrantfile by executing the followng command i.e. `vagrant init`
2. Edit the contents as follows for creating the two VMs ansible and web:
```
Vagrant.configure("2") do |config|

  config.vm.define "ansibleserver" do |ansibleserver|
  	ansibleserver.vm.box = "ubuntu/trusty64"
  	ansibleserver.vm.hostname = "ansibleserver"
  	ansibleserver.vm.network "private_network", ip: "192.168.33.15"
  end


  config.vm.define "slave" do |slave|
  	slave.vm.box = "ubuntu/trusty64"
  	slave.vm.hostname = "slave"
  	slave.vm.network "private_network", ip: "192.168.33.25"
  	slave.vm.network "forwarded_port", guest: 80, host: 8082
  end

end

```
3. Then we need to perform `vagrant up`.
4. Perform `vagrant ssh ansibleserver` and then execute below command
```     
sudo apt-get update
sudo apt-get -y install git make vim python-dev python-pip libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev
```
5. Install ansible
`sudo pip install ansible`

6. Create the required [inventory] (https://github.com/sohankunkerkar/SE_HW5/blob/master/inventory) and [ansible config] (https://github.com/sohankunkerkar/SE_HW5/blob/master/ansible.cfg) files.
7. Create the [playbook] (https://github.com/sohankunkerkar/SE_HW5/blob/master/ansible_play.yaml) with the tasks.
8. Then execute the ansible playbook.
9. See if all the tasks have been completed in the command prompt.
10. Check in the slave machine if the forvever is running by executing following command  `forever start`
11. Then run [Ec2 Playbook ](https://github.com/sohankunkerkar/SE_HW5/blob/master/amazon.yaml) to see if the virtual machine is getting created on EC2.
