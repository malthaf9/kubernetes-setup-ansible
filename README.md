# 🚀 Kubernetes Initialization with Ansible Role
This repo contains an Ansible role designed to initialize and set up a Kubernetes cluster on a target server.

# 📜 Overview
This Ansible role automates the steps required to set up a Kubernetes cluster. It performs tasks such as:

Installing Kubernetes packages (kubeadm, kubelet, kubectl)
Setting up necessary configurations
Running kubeadm init to initialize the cluster

# 🛠️ Prerequisites
Before running this role, ensure that you have:

Ansible installed on your local machine.
SSH access to your target server(s) configured.
A properly set up inventory file with the target server(s).
Ensure that the target server has sufficient system resources for Kubernetes installation.
# 🏗️ Requirements
You must have the following tools and dependencies:

Ansible >= 2.x
A compatible OS (Ubuntu/Debian or CentOS/RHEL) on the target server(s). In my case i use Ubuntu
📂 Directory Structure
The repository has the following directory structure:

plaintext
Copy code
.
├── ansible-role/
│   └── k8s-init/
│       ├── tasks/
│       │   └── main.yml
│       ├── defaults/
│       │   └── main.yml
│       └── templates/
│           └── kubeadm-config.yaml.j2
├── inventory/
│   └── hosts
├── playbook.yml
└── README.md

# 🖥️ How to Use
1. Clone the Repository
First, clone the repository:

bash
Copy code
git clone git@github.com:malthaf9/kubernetes-setup-ansible.git
cd kubernetes-setup-ansible

2. Set Up Your Inventory
Edit the inventory/hosts file to include your target server(s):

ini
Copy code
[all]
k8s-master ansible_host=<TARGET_SERVER_IP> ansible_user=<SSH_USER>
Replace <TARGET_SERVER_IP> with the IP address of your target server and <SSH_USER> with the SSH username you use to connect.

3. Run the Playbook
Execute the Ansible playbook to initialize Kubernetes:

bash
Copy code
ansible-playbook -i inventory playbook.yml
🧩 Playbook Details
playbook.yml
The playbook contains the following logic:

yaml
Copy code
- name: Initialize Kubernetes
  hosts: all
  become: true
  roles:
    - k8s-init
# ✨ Role Features
The role performs these steps:

-> Installs Kubernetes packages using package managers (apt or yum) depending on the target server's OS.
-> Runs kubeadm init to initialize Kubernetes.
-> Sets up kubectl configuration for the user.
-> Ensures that the cluster is in a ready state for further operations.

🔑 Variables
You can override default variables by creating a vars.yml file or using the --extra-vars flag:

Example:
Create a vars.yml with your custom configurations:

yaml
Copy code
kubernetes_version: "1.x.x"
Run the playbook with custom variables:

bash
Copy code
ansible-playbook -i inventory playbook.yml --extra-vars "@vars.yml"


# 🤝 Contributing
If you find any issues, have suggestions, or would like to contribute, feel free to open an issue or create a pull request!

# 💬 Questions/Feedback
If you have questions, feedback, or need assistance, contact me via GitHub Issues.

# 🎉 Happy Deploying! 🚀
Kubernetes is ready for action. 🐳 Let's manage your clusters with ease!
