<h1>I. Introduction:</h1>
In today's IT landscape, effective management of infrastructures and applications is critical for stability, security, and speedy software deployments. Ansible, an open-source automation tool, offers simplicity, flexibility, and scalability, enabling Infrastructure as Code (IaC) principles. Our project aims to leverage Ansible to automate the entire software deployment lifecycle, including server configuration, application deployment, updates, and monitoring. Benefits include error reduction, environment standardization, traceable configurations, and scalable infrastructure deployment. Ansible's ease of use ensures rapid adoption across team members, fostering continuous improvement and robust infrastructure. We believe this modern approach will significantly enhance agility and performance in our IT environment.

<h1>II. Objectives:</h1>
The Ansible-based security automation project aims to:

1. Automate security configurations across servers, VMs, and network devices.
2. Standardize security settings for consistency and risk reduction.
3. Manage patches and updates seamlessly for enhanced security.
4. Monitor and respond to security events promptly and automatically.
5. Automate identity and access management for efficiency.
6. Conduct automated security audits for compliance and reporting.
7. Integrate with other security tools to bolster overall security.
8. Automatically document security configurations for traceability and compliance.

These objectives drive proactive security measures, minimize manual errors, and fortify IT infrastructure against threats.

<h1>III. Ansible Foundations:</h1>

1. Agentless Architecture: Ansible operates without agents, utilizing SSH for secure communication and simplifying deployment.
2. Inventory Management: Hosts are listed in an inventory file, allowing organized interaction with physical servers, VMs, or cloud instances.
3. Configuration File: ansible.cfg sets global parameters, customizing Ansible behavior per project needs.
4. Module Usage: Modules execute specific tasks like software installation or file copying, enabling playbook automation.
5. Playbook Understanding: YAML-based playbooks describe tasks to perform on inventory hosts, ensuring consistent system states.
6. Task and Handler Management: Tasks define actions, while handlers respond to specific events, enabling precise infrastructure management.
7. Ad-Hoc Commands: Ansible permits quick operations on hosts without full playbooks.
8. Facts Gathering: Ansible collects host information for conditional decision-making in playbooks.
9. SSH Connection: Ansible uses SSH for secure communication with hosts, ensuring encrypted connections.
10. Control Host and Server Interaction: The Control Host orchestrates operations, storing playbooks and managing remote servers (hosts), including physical, virtual, or cloud instances.

      <img width="688" alt="image" src="https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/2ff8fcc8-39de-4c4c-a999-735952a717b7">


<h1>IV. OpenSSH Management:</h1>

1. Setup and Activation:
   - Update package list: `sudo apt update`
   - Install OpenSSH server: `sudo apt install openssh-server`
   - Start SSH service: `sudo service ssh start`
   - Enable SSH service: `sudo systemctl enable ssh`

2. SSH Key Generation:
   - Generate SSH key pair: `ssh-keygen -t ed25519 -C "ansible"`
   - The public key is stored in `authorized_keys`

3. Public Key Sharing:
   - Share public key: `ssh-copy-id -i ~/.ssh/ansible.pub <IP Address>`

4. Connection Verification:
   - Connection using keys: `ssh -i ~/.ssh/<key_name> <IP Address>`
   - Connection using passwords: `ssh <IP Address>`

![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/78342e37-9417-48a9-be87-35e505c85b41)


<h1>V. Ansible Configuration: Ad-Hoc Commands</h1>

1. Ansible Installation:
   - Update: `sudo apt update`
   - Install Ansible: `sudo apt install ansible`

2. Inventory File Creation:
   - Contains IP addresses of all managed machines.

3. Functionality Validation:
   - `ansible all --key-file ~/.ssh/ansible -i inventory -m ping`
     - `all`: Targets all hosts defined in the inventory.
     - `-i inventory`: Specifies the path to the inventory file.
     - `-m ping`: Uses the "ping" module.
     - `--key-file ~/.ssh/ansible`: Specifies the path to the SSH private key.

4. Configuration File Creation:
   - Specifies default parameters for Ansible operation: use the inventory file for targets and `~/.ssh/ansible` for the private key.
   - The configuration file must be named `ansible.cfg` and placed closer than the default configuration file installed with Ansible.

5. Verification: Ping Command
   - `ansible all -m ping`: Tests connectivity and availability of all hosts specified in the inventory using the "ping" module and configuration file parameters.

6. Information Gathering: Facts
   - `ansible all -m gather_facts --limit 192.168.10.3`
   - Collects information on server machines, targeting a specific machine `<192.168.10.3>`.

7. Ad-Hoc Commands:
   - `ansible all -m apt -a update_cache=true --become --ask-become-pass`
     - Instructs Ansible to become a user with elevated privileges (usually root) (`--become`) to update the package cache (`-a update_cache=true`).
     - `--ask-become-pass` prompts the Ansible user for the root password.
   - For CentOS machine `<192.168.10.6>`, which uses the 'yum' module, the command fails. However, the update is successful for all other Ubuntu machines. The second command is suitable for CentOS.

<h1>VI. Playbooks:</h1>

1.  **Execute Playbook:**

   ansible-playbok --ask-become-pass <playbook_name.yml>
    
3.  **Example Playbook: Updating Cache and Installing Apache:**
   - This playbook updates the package index and installs Apache2 on specified hosts.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/6978e3bc-a89e-41f6-a0cb-542da24615fe)


3. **Customizing Playbooks:**
   - **Tags:** Mark parts of the playbook for selective execution.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/1be44fc7-f426-437f-8a3f-462bae175a4a)

   - **Configuration Variables:** Allow customization and code reuse.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/68b4785d-db4c-4a30-b547-a0614e4bf95c)
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/9bbd9221-2285-4c6a-b426-bf6fcbb37507)


   - **Conditions (when):** Add conditions to execute tasks.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/dcfb8830-f9ac-4b0a-9daa-f79b2c28094c)

   - **Groups:** Facilitate management of operations on multiple hosts.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/78bd3e7b-8b92-4c3a-98cd-108ec928d4d6)
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/827638e4-7e3b-43b7-8d26-efcdb5addc6d)



4. **Playbook: Configuration Removal:**
   - Removes the Apache2 package from a specific machine.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/edd8917c-f655-423e-a9cc-44282adbc6b4)


5. **Playbook: File Copies:**
   - Copies an HTML file to web servers.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/4ec8507e-f128-4246-b4fd-dfafcaecf9c7)


6. **Playbook: File Access Rights Management:**
   - Modifies access rights for a specified file.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/56bc45e4-e766-4c3a-bff1-59c6a4c84c71)


7. **Playbook: File Management:**
   - Installs Terraform on workstations.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/fbd25eae-24fe-480e-836c-e4d04b4aa61f)


8. **Playbook: Service Management:**
   - Installs and starts the HTTPD service on CentOS.
     
    ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/95301ff0-be14-44c0-b5d2-2fac5da95cb3)


9. **Playbook: Adding Users:**
   - Creates a new user, adds an SSH key, and grants sudo privileges.
     
     ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/0fa46190-bbf0-496c-af83-f52ddf46bf5e)

10. **Playbook: Role-Based Access Control (RBAC):**
    - Applies different roles to specific host groups.
      
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/68cfa109-3a9e-4488-8a38-a910a2556ec2)
      •	base Role:
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/a6d024c6-31c6-4924-a57c-be3a8ee894e6)
      •	db_servers Role:
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/98817ccc-48b3-49bb-9ccf-2a4e443e596e)
      •	file_servers Role:
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/343f0697-787e-4303-9248-2861dac9de4b)
      •	workstations Role:
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/798ef801-cfd8-4943-96c7-8ed1916e9b8d)
      •	web_servers Role:
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/f3f7faa3-979c-4469-ac66-491d76c1e48b)
      • site.yml:
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/e5011401-82ef-4b1c-ab01-a1a37fa34b94)

11. **Playbook: Firewall Management:**
    - Configures UFW (Uncomplicated Firewall) on Ubuntu and firewalld on CentOS.
      
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/17fa7893-08ea-45d2-abf8-4b7b5c7b6595)


12. **Playbook: SELinux Configuration:**
    - Configures SELinux on a specific machine.
      
      ![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/b552945c-1f35-4935-a12f-4b0991d34b88)

<h1>VII. Ansible Logging:</h1>

Implementing logging mechanisms in Ansible ensures complete traceability of all changes made to systems. This crucial feature captures in detail every action taken during playbook execution, ensuring complete visibility into configuration changes.
To automatically log the results of each Ansible playbook execution to a file after each run, the log_path module is used in the Ansible configuration file (ansible.cfg). This module specifies the location to save the log file.
![image](https://github.com/marwa2412/Ansible-deployment-and-automation-IaC-/assets/86896531/2a652198-5829-4b90-b2e5-164683e4a106)

Once this module is added to the configuration file, Ansible logging begins.

<h1>VIII. Conclusion:</h1>

In conclusion of this Automation of Security Enhancement with Ansible project, it is evident that the technical and methodological approach employed provides a robust solution for maintaining security within a complex infrastructure. Key concepts such as configuration management, Role-Based Access Control (RBAC), and automation of security tasks demonstrate significant advancements in risk management and compliance.

Ansible playbooks, as orchestration scripts, ensure consistent implementation of security policies, thereby eliminating potential variations associated with manual administration. The judicious use of inventory and groups facilitates management at scale, adapting configurations to the specific roles of different virtual machines.

Role-Based Access Control (RBAC) with Ansible strengthens security by enabling fine-grained management of permissions, restricting access to sensitive resources based on user responsibilities. This granular approach ensures enhanced defense against internal and external threats.

The establishment of rigorous testing and continuous monitoring of compliance ensures that configurations remain aligned with the defined security baseline. The logging mechanisms integrated into Ansible provide precise traceability of changes, simplifying security audits and investigations in case of incidents.

In summary, this project illustrates how Ansible stands as a cornerstone in the toolkit of security professionals, offering intelligent automation and precise control to ensure the sustainability of security standards within the organizational infrastructure.
