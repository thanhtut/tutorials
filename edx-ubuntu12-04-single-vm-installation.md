This installation process starts from a plain Ubuntu 12.04 freshly installed. Make sure it has at least 2GB of RAM or at least 20 GB of disk space. Otherwise random error will popped out like MySQL servery dying. 

#Note 02 The installation scripts will disable password authentication edit " /etc/ssh/sshd_config" and change "PasswordAuthentication yes" after you finish installation script or else you will be locked out if it is a remote system.. If you want that feature or it might log you out if the server is remote! 

Update the repository and update all the packages 

sudo apt-get upgrade -y sudo apt-get update -y 

Install required software 

sudo apt-get install -y build-essential software-properties-common python-software-properties curl git-core libxml2-dev libxslt1-dev python-pip python-apt python-dev sudo pip install --upgrade pip sudo pip install --upgrade virtualenv 

Download the Playbook and Ansible configuration for Birch release and install requirements 

cd /var/tmp 

git clone -b named-release/birch https://github.com/edx/configuration 

cd /var/tmp/configuration 

sudo pip install -r requirements.txt 

 

#See fix 01 (on the right) to fix possible git No Authentication Method Error 

"To allow password based SSH authentication, edit the common role inside of configuration/playbooks/roles/common/defaults/main.yml and set COMMON_SSH_PASSWORD_AUTH to "yes"" 

#Fix 02 for reference to private repository 

https://groups.google.com/forum/#!topic/openedx-ops/L_0orWLIc6Y 

Comment out this line "- name: install python custom-requirements" in "roles/minos/tasks/main.yml" 

#Fix 03 for installing python-scocial-auth dependency 

/edx/app/insights/venvs/insights/bin/activate 

sudo /edx/app/insights/venvs/insights/bin/pip install python-social-auth 

#Fix 04 Remove some uncompleteable tasks. Harmless to do so! // ไม่ต้องทำก็ได้ 

sudo vim roles/insights/tasks/main.yml 

#- name: run r.js optimizer #  shell: > #    chdir={{ insights_code_dir }} #    . {{ insights_nodeenv_bin }}/activate && {{ insights_node_bin }}/r.js -o build.js #  sudo_user: "{{ insights_user }}" 

#Note 01 If any tasks keep giving errors they can be commented out depending on what kind of task it is. Most of them won't impact the functionality we use in anyway. 

 #Note 02 The installation scripts will disable password authentication edit " /etc/ssh/sshd_config" and change "PasswordAuthentication yes" after you finish installation script or else you will be locked out if it is a remote system.. If you want that feature or it might log you out if the server is remote! 

 Finally run install script 

cd /var/tmp/configuration/playbooks && sudo env SSH_AGENT_PID=$SSH_AGENT_PID SSH_AUTH_SOCK=$SSH_AUTH_SOCK ansible-playbook -c local ./edx_sandbox.yml -i "localhost," 

sudo  my-script or sudo -E

See fix 01 

When running playbook, it will encounter problem with git: protocol (not over https) 

It is because the public key and private key between your computer and github need to be configured. Follow these steps (Especially "Verify your public key section" 

https://help.github.com/articles/error-permission-denied-publickey/  

To generate ssh key 

cd ~/.ssh && ssh-keygen  

cat id_rsa.pub  

After key has been added enter "ssh -vT git@github.com" to verify. It should end without any error. 
