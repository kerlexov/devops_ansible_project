# Create CX11 VM (CentOS Stream 8) on Hetzner with separated 10GB volume with root SSH credentials and private network

# Create devops user
    $ useradd devops

# Configure passwordless sudo for devops user on test VM
    $ usermod -aG wheel devops

    Edit line below to /etc/sudoers
    %wheel  ALL=(ALL)	NOPASSWD: ALL

    Ensure that values below match in /etc/ssh/sshd_config
    PermitRootLogin prohibit-password
    PubkeyAuthentication yes
    AuthorizedKeysFile	.ssh/authorized_keys
    AllowUsers devops
    PasswordAuthentication no
    ChallengeResponseAuthentication no
    GSSAPIAuthentication yes
    GSSAPICleanupCredentials no
    UsePAM yes

# Generate SSH keys for devops user

    $ ssh-keygen

    Add generated public key to .ssh/authorized_keys.


# Run playbook

    $ ansible-playbook 