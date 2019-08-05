# ANSIBLE HANDS-ON

### Our task:

#### Reboot Ubuntu Linux machine using shell or command module and wait for it to come back.

### You will need:

    1.  Ansible
    2.  A remote host
        Example: 34.244.168.125
    3.  a *.pem file to connect to your AWS instance.
    3.  Loads of fun!
------
### Let's start
1. Install Ansible (if you haven't already)
    If you are not sure, you can check whether Ansible is installed by running:
        $ ansible --version

- [Install XCode](https://developer.apple.com/xcode/)
        
        sudo easy_install pip
        sudo pip install ansible --quiet

    That's it!

2. Initial setup. This will create a demo directory, a config file for Ansible, will populate your inventory with your remote host adress and will place your public ssh key in the Authorized_keys file in your remote host.

        $ git clone git@github.ecs-digital.co.uk:ECSD/hsbc_patching_pod.git && 
        cd hsbc_patching_pod/ansible-demo

        $ vi yuliya_ans.pem                   # Paste here the key that was shared with you.
        $ chmod 400 yuliya_ans.pem

        $ ./setup.sh <your_db_host>


3. Let's check out connectivity with the host. Run:

        $ ansible all -i ./ansible_inventory -u ubuntu -m ping

4. Write a playbook.

    We will put together a simple playbook to update our remote host. 
    Create a file `update.yml` and paste the following. Careful with the spaces - YAML is fussy! 
    
    HINT: You can copy the file you have cloned from the repo. 

        ---
        - hosts: db_hosts
          tasks:
            - name: Update all packages on a Debian/Ubuntu
              apt:
                update_cache: yes
                upgrade: dist


5. Run the playbook

    ansible-playbook  -i ./ansible_inventory update.yml

6. Write the upgrade playbook
    Copy the `update_kernel.yml` 

7. Run the playbook

    ansible-playbook  -i ./ansible_inventory update_kernel.yml

-----------
#### Additional notes on setup:

##### If you already have Homebrew installed on your mac, then 

    ```brew install ansible```


# Thanks for participating!