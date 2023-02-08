# Create CX11 VM (CentOS Stream 8) on Hetzner with separated 10GB volume with root SSH credentials and private network

# Create devops user
    $ useradd devops

# Generate SSH keys for devops user
    $ ssh-keygen

# Configure passwordless sudo for devops user on test VM
   Edit line below to /etc/sudoers
    %wheel  ALL=(ALL)	NOPASSWD: ALL

    $ usermod -aG wheel devops
    
    Copy pub key to this location
    mkdir /home/devops/.ssh
    touch /home/devops/.ssh/authorized_keys

    Ensure that values below match in /etc/ssh/sshd_config
    PermitRootLogin prohibit-password
    PubkeyAuthentication yes
    AuthorizedKeysFile	.ssh/authorized_keys
    AuthorizedKeysFile	/home/devops/.ssh/authorized_keys
    AllowUsers devops
    PasswordAuthentication no
    ChallengeResponseAuthentication no
    GSSAPIAuthentication yes
    GSSAPICleanupCredentials no
    UsePAM yes

    systemctl restart sshd.service

# Run playbook

    $ ansible-playbook --ask-vault-pass playbook.yml -vvvv