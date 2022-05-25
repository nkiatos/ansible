# Ansible playbook to deploy Apache Airflow

sudo su
cd /opt
git pull https://github.com/nkiatos/ansible.git
# Can run as root or create new user to run ansible

# Creating ansible user
useradd ansadmin

chown -R ansadmin:ansadmin /opt/ansible

su ansadmin

cd /opt/ansible

# Install python3

# Run ansible playbook
ansible-playbook -i inventories/hosts configure_airflow_main.yml --check



Helpful URLs
https://github.com/kyungw00k/ansible-airflow

https://github.com/idealista/airflow-role
