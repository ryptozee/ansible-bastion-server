## Ansible-Based Bastion Host Setup and Management

### 1. Verified Environment
- **Operating System**: CentOS 7
- **Ansible Version**: 2.9.10

Before starting, ensure that Ansible is installed and a root SSH key is generated:

```bash
yum install epel-release ansible -y
ssh-keygen -t rsa -f ~/.ssh/id_rsa -N ''
```

### 2. Host Configuration

#### 2.1 Modify `hosts.ini` as Needed

- The `hosts.ini` file defines the target machines for Ansible operations.
  - The first machine listed acts as the **Ansible server**, also referred to as the **Fortress Machine Manager**.
  - The `addnew` section is used for **new servers** added later.

#### 2.2 Default Hosts Template

- A default hosts template is located at `/etc/ansible/inventory/default-hosts.ini`. This template is designed for ordinary users and should be modified according to your needs.

### 3. Variables

- Variables are defined in `group_vars/all.yml`. Modify this file as needed to set up custom variables for your environment.

### 4. Features

1. **Batch synchronization of the root user key**:
   - Syncs the root SSH key from the bastion machine to target servers for root user management.

2. **Batch synchronization of the sudo user key**:
   - Syncs the sudo user’s SSH key to target servers for the management of ordinary users with sudo privileges.

3. **Batch addition of ordinary users**:
   - Adds multiple ordinary users across the servers using Ansible.

4. **Quick setup of a simple bastion host**:
   - Automatically deploys a basic bastion server setup.

### 5. How to Use

#### Checking Connectivity

To verify that Ansible can reach all hosts defined in `hosts.ini`, run the following command:

```bash
ansible -i hosts.ini all -m ping
```

If the command successfully pings the target machines, your `hosts.ini` configuration is correct.

#### Running the Playbook

To run the Ansible playbook, use the following command:

```bash
ansible-playbook -i hosts.ini start.yml
```

### 6. Adding a New Server

1. Add the new server under the `addnew` section in `hosts.ini`.

2. Run the following command to apply the configuration to the new server:

```bash
ansible-playbook -i hosts.ini -l addnew start.yml -t addmanager
```
