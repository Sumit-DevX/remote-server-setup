# remote-server-setup

## Overview
This project demonstrates how to configure secure SSH key-based authentication between a host machine and a remote Linux server.


For this project, a Linux Mint host computer and a virtual Ubuntu Server operating system running on VirtualBox were used. This project includes two SSH key pairs, setting up the remote Linux server to accept these key pairs, and establishing a secure connection to the Linux server.

## HOST MACHINE
- Linux Mint

## REMOTE SERVER
- Ubuntu Server running on Virtual Box

## Procdures

PHASE1 - Generate ssh key pairs in host machine

Here I created two ssh key pairs using the command:
'''bash 
    ssh-keygen -t ed25519 -f "~/.ssh/key_file_name"
'''
Explanation
- ssh-keygen
    I used this command to generate SSH authentication keys.
- -t
    This option specifies the type of cryptographic algorithm to use for the key pair.
    In this project, I used the ed25519 algorithm.
- -f
    This option specifies the filename and storage location for the generated key files.

After running the command, SSH generated:

A private key
A corresponding public key

The generated key files were stored inside the ~/.ssh directory

PHASE2 - Copy the two newly created ssh PUBLIC keys to the remote 
server

After sucessfully creating the two new ssh key pairs, I copied the PUBLIC keys from the path "~/.shh" by using the command

'''bash 
    ssh-copy-id -i ~/.ssh/public_key_file username@server-ip
'''

Explanation
- ssh-copy-id
    I used this command to copy a local public SSH key to the remote server.
- -i
    This option specifies the identity file (public key) that should be copied.


PHASE3 - Verify passwordless SSH login

After copying the public keys to the remote server, I tested passwordless SSH login using the following command:

'''bash 
    ssh -o IdentityOnly=yes -i ~/.ssh/private_key_file username@server-ip
'''

Explanation
- -i
    I used this option to specify which private key file should be used for authentication.
- -o IdentitiesOnly=yes
    I added this option to ensure that SSH used only the specified private key instead of automatically trying previously loaded SSH keys from the SSH agent or default SSH configurations.

This verification step helped me confirm that:

The correct SSH key pair was being used
The remote server trusted the corresponding public key
Passwordless SSH authentication was working successfully
