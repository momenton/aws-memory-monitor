# Ansible Playbooks to install ec2-cloudwatch memory and disk monitoring

- PreRequsites
    - AWS_ACCESS_KEY and AWS_SECRET_KEY to be loaded as environment variables.
    - Administrator or similar role availalbe in AWS to create IAM instance profile if needed on AWS
    - `Ansible` (2.9.0) or higher installed with ansible requirements like python 3.8
    - `SSH keys` for ec2 instances
    - ensure that the ssh user is able to switch to `root` user
- How To
    - #### Configure Ansible Playbooks and other info
        - Variables for what to monitor like Memory or Disk is maintained in group_vars folder
        - cron job expression is also maintained in group_vars folder and this can vary from 1 minute range to 59 minutes
        - Playbooks or tasks are setup to be run on Amazon Linux2, Ubuntu, CentOS or RHEL Distros and assuming these to be latest. If you want support for older versions of these distros, please reach out
        - These playbooks take the hostname or IP as parameters during the run. If using hostname, ensure these are resolving from the host where you run these playbooks from

    - #### Running Ansible playbooks
        - `Generic command to run`
            ```
            ansible-playbook  -v -i inventory/hosts playbooks/install_aws_monitoring.yaml  -u <ec2 user name> -c paramiko -e working_host=<IP or hostname of ec2 instance > --private-key=~/Downloads/<ec2-keypair>.pem 
            ```
        - `running in check mode or dry-run`
            ```
            ansible-playbook  -v -i inventory/hosts playbooks/install_aws_monitoring.yaml  -u ubuntu  -c paramiko -e working_host=52.63.254.239 --private-key=~/Downloads/momenton-mel-sydney.pem  --check
            ```
        - `running to check what tasks will be run`
            ```
            ansible-playbook  -v -i inventory/hosts playbooks/install_aws_monitoring.yaml  -u ubuntu  -c paramiko -e working_host=52.63.254.239 --private-key=~/Downloads/momenton-mel-sydney.pem  --list-tasks
            ```
        - `running or installing the scripts`
            ```
            ansible-playbook  -v -i inventory/hosts playbooks/install_aws_monitoring.yaml  -u ubuntu  -c paramiko -e working_host=52.63.254.239 --private-key=~/Downloads/momenton-mel-sydney.pem
            ```


