`Ad-Hoc commands are one-liner ansible commands that performs one task on the target host.`
`It allows you to execute simpleone-line task against one or group of hosts defined on the inventory file configuration.`

Ad-Hoc commands everything will be performed in controller mechine, and that will be triggered in host servers.

ansible will be better practice to perform all tasks from user own inventory.

bhujatha# ansible all -a "touch /tmp/annapa"
(it will create a foleder in all hosts which configured in bhujatha inventory)

check file are create or not in hosts
bhujatha# ansible all -a "ls -l /tmp"
 (it lists all files i tmp location in hosts server)
 
 
 check ram utilization of resource
 bhujatha# ansible all -a "free -m"
 
 bhujatha# ansible localhost -a "free -m"
 
 installing apache at hosts server
 ---
 bhujatha#ansible all -b  -a  "apt-get install -y apache2"
 
 check in hosts wheter it is going to install or not
 -
 hosts server-->ps -ef|grep apache2
 
 check from controller
 bhujatha# ansible all -b -K -a "apt-get install -y apache2"
 
 
 check apache is accessable or not
 ---
 bhujatha# ansible all -a "curl localhost"
 
 insatll docker in root(hosts)
 ---
 bhujatha# ansible all -a "sh /root/labs/docker/install/installDocker.sh"
 
 error--> Failed
 can't open /root/labs/docker/install/installDocker.sh non-zero return code
 i.e not possibel to run script at root(hosts) mechine
 
 
 Solution:(use module)
 --
 bhujatha# ansible all -b script -a "/root/labs/docker/install/installDocker.sh"
 
 
 
 
 
 
 modules:
 -------
 ex: by default we can't run script on remote mechine from local mechine.
 in order to resolve this modules came into pictures
 there are around 3387 modules available in ansible.
 ex: script 
 	setup: it represent remote mechine details. 
 
 view modules list >> ansible-doc --list
 move list to another file: ansible-doc --list > moduleslist
 		check count --> cat moduleslist |wc -l
		o/p:3387


				
 
 
 
 
 
 
 
 
 
 
 
  




## Ansible Ad-Hoc Commands to use when SSH Keys configured with target hosts

```
how to run ansible ad-hoc commands ( default inventory )

	ansible all -m setup
        ansible qa -m ping
        ansible dev -m shell -a "free -m"
        ansible iat -m copy -a "src=/tmp/naresh.txt dest=/tmp"
        ansible prod -m file -a "path=/tmp/helousername.txt state=touch"

how to run ansible ad-hoc with custom inventory

	ansible all -i /path/to/inventory ping
        ansible dev -i /path/to/inventory -m copy -a "src=/tmp/new.txt dest=/tmp"

how to run ansible ad-hoc with super user (root)

        ansible all -i /path/to/inventory -b ping
        ansible dev -i /path/to/inventory -m copy -a "src=/tmp/new.txt dest=/tmp" -b
```

## Ansible Ad-Hoc Commands to use when No SSH  Keys configured with target hosts

```
how to run ansible ad-hoc commands ( default inventory ) with uid/pwd

	ansible all -m setup -u username -k 
        ansible qa -m ping -u username -k
        ansible dev -m shell -a "free -m" -u username -k
        ansible iat -m copy -a "src=/tmp/naresh.txt dest=/tmp" -u username -k 
        ansible prod -m file -a "path=/tmp/helousername.txt state=touch" -u username -k

how to run ansible ad-hoc with custom inventory & uid/pwd

	ansible all -i /path/to/inventory -u username -k
        ansible dev -i /path/to/inventory -m copy -a "src=/tmp/new.txt dest=/tmp" -u username -k

how to run ansible ad-hoc with super user (root) with uid/pwd

        ansible all -i /path/to/inventory -b -u username -k -K
        ansible dev -i /path/to/inventory -m copy -a "src=/tmp/new.txt dest=/tmp" -b -u username -k -K
```
