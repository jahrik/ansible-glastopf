# ansible-glastopf

Glastopf is a Python web application honeypot.

- [Glastopf GitHub](https://github.com/mushorg/glastopf)
- [KYT Glastopf Paper](http://honeynet.org/sites/default/files/files/KYT-Glastopf-Final_v1.pdf)

## Usage

Configure your targets in `inventory.ini` before running playbooks.

### Vagrant

```bash
vagrant up
ansible-playbook -i inventory.ini -l vagrant site.yml
```

### Raspberry Pi

```bash
ansible-playbook -i inventory.ini -l pi site.yml
```

### EC2 Instance

Ensure your AWS credentials are set and an SSH key is available.

```bash
ssh-keygen -f ~/.ssh/glastopf_rsa
ssh-add ~/.ssh/glastopf_rsa

export AWS_ACCESS_KEY_ID="your_access_key"
export AWS_SECRET_ACCESS_KEY="your_secret_key"

ansible-playbook -i ec2.py setup_ec2.yml
ansible-playbook -i ec2.py site.yml -u ubuntu
```

## Testing

```bash
uv sync
source .venv/bin/activate
yamllint .
ansible-lint
molecule test
```

### Honeypot Verification

Trigger a test RFI (Remote File Inclusion) vulnerability against the honeypot:

```bash
curl -X GET "http://<target_ip>/INTERNAL_TEST/vuln.php=http://raw.githubusercontent.com/jahrik/ansible-glastopf/master/malicious-file.txt"
```

The application logs should show:

```text
2016-11-10 11:17:48,658 (glastopf.glastopf) <target_ip> requested GET /INTERNAL_TEST/vuln.php%3Dhttp://raw.githubusercontent.com/jahrik/ansible-glastopf/master/malicious-file.txt on <target_ip>:80
2016-11-10 11:17:48,791 (glastopf.sandbox.sandbox) File successfully parsed with sandbox.
```
