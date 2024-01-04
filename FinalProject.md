## Jenkins_Ansible_Integration_Project

###### Write Terraform Script to Provision the following Infrastructure
Here are some key points 
- terraform `fmt` mean it will rearrabge the code in a neat way.
- explain terraform state show and terraform state list.
- "terraform output" is the command to get the outputs

     


* First write settings block and then provider block.
* Create  a private or Custom Network:
        - Create a Vpc
        - Create a Subnet(Public one)
        - Create an IGW and Attach it to a VPc
        - Create a RouteTable
        - Create a Route
        - Create or do a Subnet Association.
        - Create a security Group which allows port 22,80,8080,9000 for now
* Create a 3 servers
        - One for Ansible
        - Second one for Jenkins_Master
        - Third One for Jenkins_Slave

##### Ansible_Server Setup
* Ansible Installation in the Ansible Server will be done through terraform script itself.
* Create a hosts file in Ansible Server and add the private ips and the variables the machines in the same file like below:

      {

        [jenkins-master]
        10.0.10.26
        [jenkins-master:vars]
        ansible_user=ubuntu
        ansible_ssh_private_key_file=/home/ubuntu/project-key.pem

        [jenkins-slave]
        10.0.10.186
        [jenkins-slave:vars]
        ansible_user=ubuntu
        ansible_ssh_private_key_file=/home/ubuntu/project-key.pem

        [sonarqube]
        10.0.10.252
        [sonarqube:vars]
        ansible_user=ubuntu
        ansible_ssh_private_key_file=/home/ubuntu/project-key.pem   
      }



*with this video 66 coved as part of the final project*

##### Jenkins_Master Setup
**create an ansible playbook to install jenkins on Jenkins_Master**
* 1-jenkins-master-setup.yaml.
```bash
---
- name: installing Jenkins on jenkins master node
  hosts: jenkins-master
  become: true
  tasks:
  - name: Update system packages
    apt:
      update_cache: yes
      upgrade: yes
  - name: get jenkins the key
    apt-key:
      url: https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
      state: present
  - name: get the jenkins repo
    apt_repository:
      repo: deb https://pkg.jenkins.io/debian-stable binary/
      state: present
  - name: install java-11
    apt:
      name: openjdk-11-jre
      state: present
  - name: install jenkins
    apt:
      name: jenkins
      state: present
  - name: cat the initial passwrodword file 
    shell: cat /var/lib/jenkins/secrets/initialAdminPassword
    register: initial_admin_password
  - name: Display the initialpassword 
    debug:
      var: initial_admin_password.stdout_lines
  
# This file conetent we will copy to 1-jenkins-master-setup.yaml file in the ansible server 
# ansible-playbook -i hosts 1-jenkins-master-setup.yaml , so that jenkins master setup will be done
```
* ansible-playbook -i hosts 1-jenkins-master-setup.yaml.

##### Jenkins_Slave Setup
**Create an ansible playbook to setup the Jenkins_Slave**
* 2-jenkins-slave-setup.yaml.
* ansible-playbook -i hosts 1-jenkins-slave-setup.yaml.

