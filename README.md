# Ansible playbook to deploy Apache Airflow

sudo su
cd /opt
git pull https://github.com/nkiatos/ansible.git

# Install python3
sudo yum install python3

# Can run as root or create new user to run ansible

# Creating ansible user
useradd ansadmin

chown -R ansadmin:ansadmin /opt/ansible

su ansadmin

cd /opt/ansible


# Set up to deploy from Ansible Master to Node


<b> ansible master </b>
ssh-keygen

<b> ansible node </b>
sudo useradd ansadmin
sudo passwd ansadmin

Create the ansadmin sudoers file
sudo touch /etc/sudoers.d/10-ansible-user
sudo echo 'ansadmin ALL=(ALL)      NOPASSWD: ALL' >> /etc/sudoers.d/10-ansible-user

Update /etc/ssh/sshd_config 
PasswordAuthentication yes
#PasswordAuthentication no
sudo systemctl restart sshd

<b> ansible master </b>
su ansadmin
ssh-copy-id node ip


# Run ansible playbook
ansible-playbook -i inventories/hosts configure_airflow_main.yml --check

# To do:
# Set up firewalld
sudo firewall-cmd --zone=public --add-port=8080/tcp

sudo firewall-cmd --zone=public --add-port=80/tcp

sudo firewall-cmd --runtime-to-permanent

sudo firewall-cmd --reload

# Helpful URLs
https://github.com/kyungw00k/ansible-airflow

https://github.com/idealista/airflow-role

https://towardsdatascience.com/how-to-run-apache-airflow-as-daemon-using-linux-systemd-63a1d85f9702
