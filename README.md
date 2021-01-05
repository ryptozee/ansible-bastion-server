1, Verified environment:
Centos 7
ansible 2.9.10

# Need to install ansible first, and create a root public key
# yum install epel-release ansible -y
# ssh-keygen -t rsa -f ~/.ssh/id_rsa -N ''

2, About hosts
2. 1 Modify hosts.ini as needed
2. 2 hosts.ini first acts ansible server, fortress Machine Manager server
2. 2 addnew is a new server added later
2. 4 /etc/ansible/inventory/default-hosts.ini uses the default hosts template for ordinary users, modify as needed

3, vars variable definition, can be modified as needed
group_vars / all.yml

4. Realize function
4. 1 Batch synchronization of the bastion machine root user key to the server-mainly for the bastion machine root user operation management
4. 2 Batch synchronization of the bastion host sudo management user key to the server-mainly for the sudo user operation management of ordinary users of the bastion host
4. 3 Add ordinary users in batch
4. 4 Quickly build a simple bastion server

5. How to use
ansible -i hosts.ini all -m ping #If you can ping normally, there is no problem with hosts.ini configuration
ansible-playbook -i hosts.ini start.yml

6, add a new server
6. 1. First add hosts.ini addnew
6.2 ansible-playbook -i hosts.ini -l addnew start.yml -t addmanager