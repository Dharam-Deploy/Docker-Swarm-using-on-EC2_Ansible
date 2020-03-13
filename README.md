# Docker-Swarm setup on EC2 instance using-Ansible

Step 1:
Make AWS account than,
Launch 2 ubuntu EC2 instance Download keys [like Docker_M.pem and Docker_S.pem]
with VPC port Enabled 2377
>> Add Rule -> 
1- Custom TCP Rule enable port 2377 [for docker swarm communication]  
2- All ICMP IPv4 [to ping instances]

Step 2:
Download ansible and configure it accordingly on your workstaion
>> vim /etc/ansible/ansible.cfg ->
do modification according to given ansible.cfg file
Make ansible inventory file like hosts file given

*[here replace the x.x.x.x with your master instance public ip and y.y.y.y with your slave instance publiv ip in hosts file]

Step 3:
Run the ansible playbooks.

>> ansible-playbook docker_swarm.yml
* This file will initilize docker swarm on the manager node and add worker node for the docker swarm

>> Don't need to run docker_setup.yml
* This is already imported in docker_swarm.yml file so when we run docker_swarm.yml then docker_setup.yml will automatically run.
* This file will do the required configuration on the instances like installing docker engine and will launch a container on worker node.

Step 4:
Check the setup.
To check the setup go to the manager node by 
* ssh -i Docker_M.pem[your key] ubuntu@x.x.x.x[your master ip]
>> And run->
* sudo docker node ls
>> OR
* sudo docker info

# Hence your Setup is done

* For professional practice: Devide the ansible playbook into roles [recommended]
