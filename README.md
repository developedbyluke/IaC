-   [Infrastructure as Code (IaC)](#infrastructure-as-code-iac)
    -   [What is it](#what-is-it)
    -   [Why use it](#why-use-it)
    -   [When to use it](#when-to-use-it)
    -   [Where to use it](#where-to-use-it)
    -   [Tools Available](#tools-available)
-   [Ansible](#ansible)
    -   [What is Ansible:](#what-is-ansible)
    -   [Benefits of using Ansible:](#benefits-of-using-ansible)
    -   [Who is using IaC and Ansible](#who-is-using-iac-and-ansible)
-   [Setting up Ansible](#setting-up-ansible)
    -   [Prerequisites](#prerequisites)
    -   [Steps](#steps)

### Infrastructure as Code (IaC)

#### What is it

Infrastructure as Code (IaC) is the practice of managing and provisioning infrastructure resources through machine-readable definition files, rather than manual configuration or interactive configuration tools. It involves writing code to define, deploy, and manage infrastructure components such as servers, networks, storage, and other cloud resources.

#### Why use it

It ensures consistent and repeatable routines for provisioning and tearing down infrastructure, reducing manual processes, and enhancing the speed and reliability of infrastructure deployments.

#### When to use it

Use IaC when you need to automate the setup, change, or removal of infrastructure, especially in environments that change often or are scaled frequently.

#### Where to use it

IaC is utilized in cloud environments, data centers, and anywhere infrastructure needs to be managed as code. It is essential for DevOps practices, facilitating continuous integration and continuous delivery (CI/CD) workflows.

#### Tools Available

-   **Terraform:** Open-source tool that works with many cloud providers for infrastructure provisioning.
-   **Ansible:** Open-source tool for software provisioning, configuration management, and application deployment.
-   **Chef:** Provides a way to define infrastructure as code to automate server configuration and management.
-   **Puppet:** Manages infrastructure as code, automating the provisioning, configuration, and management of servers.
-   **AWS CloudFormation:** Service for AWS users to define and provision AWS infrastructure using code.

### Ansible

#### What is Ansible:

Ansible is an open-source automation tool for software provisioning, configuration management, and application deployment. It uses YAML syntax for expressing automation jobs in plain terms.

#### Benefits of using Ansible:

-   **Simplicity:** Easy to learn and use because of its use of YAML for defining automation jobs.
-   **Agentless:** Does not require any agent software installed on remote nodes, making it easier to manage.
-   **Efficiency:** Uses SSH for communication with no extra servers or daemons needed, reducing the overhead on the network.
-   **Flexibility:** Can manage both Unix-like systems and Windows systems from a single control machine.

#### Who is using IaC and Ansible

Many organizations across various industries have adopted Infrastructure as Code practices and tools like Ansible.

**Netflix**: Netflix extensively uses IaC to manage its large-scale infrastructure on AWS. They have developed their own IaC tool called Spinnaker.

**Airbnb**: Airbnb uses Terraform to manage its infrastructure across multiple cloud providers and regions.

**Slack**: Slack utilizes Terraform to provision and manage its AWS infrastructure, ensuring consistency and reliability.

**Uber**: Uber employs Ansible for configuration management and infrastructure provisioning across its global infrastructure.

**Red Hat**: Red Hat, the company behind Ansible, uses Ansible extensively for managing its own infrastructure and provides enterprise support for Ansible to its customers.

Many other companies, from startups to large companies, have adopted IaC practices and tools to streamline their infrastructure management and deployment processes.

### Setting up Ansible

#### Prerequisites

-   [x] Two EC2 instances (one as Ansible controller and one as agent node)
-   [x] Security group with port 22 open for SSH on both instances

#### Steps

1. **Install Ansible on the controller node:**

```bash
sudo apt update
sudo apt install ansible
```

2. **Configure the Ansible controller:**

Edit the Ansible configuration file `/etc/ansible/ansible.cfg` to set the inventory file location and other settings.

```bash
sudo nano /etc/ansible/ansible.cfg
```

Add the following lines to the configuration file:

```yaml
[defaults]
remote_user = ubuntu
private_key_file = /path/to/your/private-key.pem
```

3. **Edit inventory file:**

Edit the inventory file `/etc/ansible/hosts` to define the hosts that Ansible will have control over. These are the IP addresses of the agent nodes.

```bash
sudo nano /etc/ansible/hosts
```

Add the IP addresses of the agent nodes to the inventory file:

```yaml
[agents]
ec2_instance ansible_host=agent_ip_address
```

4. **Test the Ansible setup:**

Run the `ping` command to check if Ansible can communicate with the agent node.

```bash
sudo ansible all -m ping
```

There should be a successful `pong` response from the agent node.
