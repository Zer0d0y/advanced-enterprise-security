vi /etc/ssh/sshd_config

# What ports, IPs and protocols we listen for
Port 10022

Protocol 2
# HostKeys for protocol version 2
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_dsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key

#Privilege Separation is turned on for security
UsePrivilegeSeparation yes

# Lifetime and size of ephemeral version 1 server key
KeyRegenerationInterval 3600
ServerKeyBits 1024

# Logging
SyslogFacility AUTH
LogLevel INFO

# Authentication:
LoginGraceTime 120
PermitRootLogin no
StrictModes yes
PasswordAuthentication no
ChallengeResponseAuthentication no
RSAAuthentication yes
PubkeyAuthentication yes
MaxAuthTries 4
PermitEmptyPasswords no
PermitUserEnvironment no
Ciphers aes128-ctr,aes192-ctr,aes256-ctr

# Don't read the user's ~/.rhosts and ~/.shosts files
IgnoreRhosts yes

# For this to work you will also need host keys in /etc/ssh_known_hosts
RhostsRSAAuthentication no

# similar for protocol version 2
HostbasedAuthentication no

# Disable X11 Forward
X11Forwarding no

# Allow client to pass locale environment variables
AcceptEnv LANG LC_*

# File Transfer
Subsystem sftp /usr/lib/openssh/sftp-server

# Idle Log Out Timeout Interval 
ClientAliveInterval 600
ClientAliveCountMax 0

# Banner
Banner /etc/issue

# use PAM
UsePAM yes
