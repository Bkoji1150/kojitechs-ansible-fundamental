# kojitechs-ansible-fundamental
kojitechs-ansible-fundamental

## Download ssh key from ssm
```sh
aws ssm get-parameters \
    --output=text \
    --region us-east-1 \
    --with-decryption \
    --names jenkins-agent-bootstrap-ssh-key \
    --query "Parameters[*].{Value:Value}[0].Value" > private-key private-key
chmod 0600 private-key
eval "$(ssh-agent -s)
```
## Test
```
/usr/local/bin/ansible-playbook -i aws_ec2.yaml ping_playbook.yaml
```
## Ansible host
ansible-pull ping_playbook.yaml \
    -U https://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@github.com/Bkoji1150/kojitechs-ansible-fundamental.git 

