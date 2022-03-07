---
title: "Setting up SSH Public Key authentication"
date: 2022-03-06T12:38:02-05:00
draft: false
github_link: "https://github.com/Rojaun-Dev"
author: "Rojaun"
tags:
  - SSH
  - PKI 
bg_image: ""
description: ""
toc:
---

The [SSH protocol](https://www.ssh.com/ssh/protocol/) supports many different methods of authentication. One of the most important and useful of these is Public Key authentication this can facilitate more secure connections and allow for easy and secure automation!

## What is SSH Public Key authentication?

Instead of a password, SSH Public key authentication allows for the use of a cryptographic key pair for validation. This helps to mostly prevent/mitigate completely [brute force attacks](https://www.kaspersky.com/resource-center/definitions/brute-force-attack), as well as allow for the implementation of automated passwordless logins.

## How does it work?

The SSH public key authentication has four steps:

1. The private and public keys are generated.
2. The public key is moved to the server we want to ssh into without a password.
3. The server stores the key and adds it to its lists of approved public keys.
4. The server will now allow anyone who can prove ownership of the corresponding private key access.

## Generating SSH Key Pairs

Okay, so now that we know how it works we need to find out how to create and apply our very own key pairs.

#### On Linux, the basic instructions are as follows

1. Login to the computer you will be using to connect to the server and use the SSH command to generate a key pair using the -t flag to specify the use of the RSA algorithm

> `$ ssh-keygen -t rsa`

2. You will be prompted to provide a directory (for the keypair to be saved to) to accept the default filename and location just press enter.

> `Output`
> `Enter file in which to save the key (/home/test/.ssh/id_rsa)`

3. The second prompt from `ssh-keygen` command will request that you enter a passphrase this is optional but it is highly recommended the security of a PKI authentication system relies on the Private key STAYING PRIVATE !! If a private key with no passphrase fall into malicious hands, they will be able to log in to any server configured with the corresponding public key
4. Next you will need to copy the Public Key to your server, this can be done using [SFTP](https://www.ssh.com/academy/ssh/sftp) or [SCP](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/) (for example, /home/test/.ssh/id_rsa.pub) to your account on the remote system (for example, server@testserver.com); for example, using command-line SCP:

> `scp /home/test/.ssh/id_rsa.pub server@testserver.com`

You'll be prompted for your account password. Your public key will be copied to your home directory (and saved with the same filename) on the remote system.

5. Once the command completes, you will be able to log into the server via SSH without being prompted for a password. However, if you had set a passphrase earlier while creating your SSH key, you will be asked to enter the passphrase. Please note however this is your local `ssh` client asking you to decrypt the private key, and _NOT_ the remote server asking for a password.

### And that's how you setup SSH Public Key authentication !!! In my next article, I'll be demonstrating a technique that can be used to steal SSH Private Keys 😉

### *Stay Tuned*