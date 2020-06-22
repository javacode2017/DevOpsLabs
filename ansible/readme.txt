Things to know before working with ansible
	
	1) ansible is agentless ( means, we do not need to run any agent on remote servers for communication )
	
	2) ansible follows push model ( means we push the configuration from ansible controller to remote servers )
	
	3) ansible uses SSH protocol to communicate with remote servers
	
	4) ansible uses below methods for remote servers authentication
	
			password based
			key based

Ansible controller ( is the machine/host/server where we install ansible ) 

	/etc/ansible default directory ( we have two important file in it )
	
		hosts ( default inventory file in which we can mention remote servers we want to apply/push the changes to)	

we can put our entries here. i.e we can add host details here
		
		ansible.cfg  ( default ansible configuraton - can be used to customize as per our need )
		
hosts
=====
vi hosts(like this open hosts file)

10.10.10.10
20.20.20.20

How to connect with hosts:
==========================
there are two types of authentication
1.password based
2.key based

1 .Password based authentication
================================
as we configured hosts in host file, we can't ping them by default.

>>ansible all -m ping -u devops -k
here devops -->user name of the remote server which i configured in hosts
-k --> it will ask hosts password 
 
 
 --> to connect the hosts server need to disable host_key_checking = False , in config.xml file
 
 -->now we can able to connect with hosts
 
 >> ansible all -m ping -u devops -k
 
 2. key based authentication
 ============================
 on mastr mechine
 
 >>ssh-keygen
 
 when i use this , it will create token for the current user only.(i.e it is a root user)
 
 So, create token on specific user
 >>ssh-keygen
 
 when we run this it will create folder in 
 /home/devops/.ssh/id_rsa (private) 
 and 
 /home/devops/.ssh/id_rsa.pub(public)
 
 So, inorder to connect host mechine  need to copy public folder in hosts mechine.
 
 >>ssh-copy-id host_server_ip
 ex: ssg-cop-id 10.10.10.10
 
 
 connecting
==============
>> ansible all -m ping



Configuration specific to user
=================================
multiple users are working on same host, bcoz of one user change it mighr effect to all user changes.
So, need to configure the host for different users.

step 1:
 create own folder
 >> mkdir bhuatha
 cd bhujatha
 vi inv
 
 // here create own group
 [aws]
10.10.101.10
2.0.20.20
==


==
try to ping hosts from own folder
bhujatha>ansible all -m ping -u devops -k
bhujatha>>rm /etc/ansible/hosts
>>ansible all -m ping -u devops -k 

o/p : No inventory was parsed...(no hosts available)
but, if 
>> ansible all -i /root/bhujatha/inv -m ping -u devops -k
>>ansible aws -i /root/bhujatha/inv -m ping -u devops -k

make own root as default
==========================
configure changes will happen in config.xml

>> cd /etc/ansible/
ansible>>ls -l

>>vi ansible.cfg

// from these file need to change default inventory location
inventory  =  /etc/root/.


>>cp ansible.cfg  /root/bhujatha
>>cd /root/bhujatha
bhujatha>>ansible --version











 
 
 




Ansible Terminlogy 

	1) ansible ad-hoc commands ( single task that can be executed against remote servers )
	
	2) ansible playbooks  ( set of instructions written in a .yml file to execute against remote servers  )
	
	3) ansible facts ( information about remote servers collected ansible before running any task )
	
	4) ansible modules ( are the units of work that ansible ships to remote servers for executing the tasks )
	
	5) ansible role ( to break a playbook into multiple files. This simplifies writing complex playbooks, and it makes them easier to reuse )
	
		look at: https://docs.ansible.com/ansible/latest/reference_appendices/glossary.html     for more terms used in ansible. 
		
