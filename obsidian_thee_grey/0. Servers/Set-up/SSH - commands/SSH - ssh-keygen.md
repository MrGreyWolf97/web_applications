# [SSH](https://www.techtarget.com/searchsecurity/tutorial/Use-ssh-keygen-to-create-SSH-key-pairs-and-more?_gl=1*1ya7gz7*_ga*MjAwMjY2ODMyOS4xNzE1NTI0NjEx*_ga_TQKE4GS5P9*MTcxNTUyNDYxMC4xLjAuMTcxNTUyNDYxMC4wLjAuMA..)
Logging into remote systems with [SSH](https://www.techtarget.com/searchsecurity/definition/Secure-Shell) implementations is secure by default -- but those connections are secured only in that they use the [TLS](https://www.techtarget.com/searchsecurity/definition/Transport-Layer-Security-TLS) protocol to encrypt network protocol exchanges.
SSH can be made even more secure by using it to authenticate communicating hosts through the exchange of [public keys](https://www.techtarget.com/searchsecurity/definition/public-key) -- keys that are created using the ssh-keygen command.
### Why generate SSH keys?

SSH can be used without a prior exchange of publ ic key pairs, and those uses can be reasonably secure.
The best approach for securely [authenticating](https://www.techtarget.com/searchsecurity/definition/authentication) SSH sessions, however, is to create a ==public key pair for the local computer and copy the public key file to the remote SSH server==.
Only a user with authenticated permission should be able to copy files to the server.
If local users do not have sufficient permission, they can request that a system administrator of the remote host copy the files for them.

Putting a public key file on an SSH server enables the user associated with the public key to securely log in to the SSH server. This is done by having users authenticate their ownership of the public key by demonstrating they control the [private key](https://www.techtarget.com/searchsecurity/definition/private-key) of the public key pair.
### How SSH works

SSH depends on [public key authentication](https://www.techtarget.com/searchitoperations/tip/PKI-authentication-explained-The-basics-for-IT-administrators) to negotiate a secure connection between an SSH client and an SSH server.
SSH is often used to make an ad hoc connection between the client and the remote server without a previously created public key pair, for example, with a command like this:

```
ssh 192.0.2.44 -l <user-account>
```

The ssh command includes the IP address of the remote server and the -l option, which specifies a valid user account on the remote server.
Once the SSH connection is established, users are prompted to enter the password for their user accounts.

This prompt is followed by the fingerprint of the server and a prompt to continue connecting. ==The fingerprint is a secure hash of the server's public key, which is stored in a file in the SSH directory.==

> [!tips] SSH keys
> On Linux systems, the default location for SSH keys is in the user's personal directory in the file _~/.ssh/known_hosts_. 
> On Windows systems, the default file location is in the user's personal directory in the file _C:\Users\username\.ssh\known_hosts_.


---
# [Generating SSH key pair](https://www.techtarget.com/searchsecurity/tutorial/Use-ssh-keygen-to-create-SSH-key-pairs-and-more?_gl=1*1ya7gz7*_ga*MjAwMjY2ODMyOS4xNzE1NTI0NjEx*_ga_TQKE4GS5P9*MTcxNTUyNDYxMC4xLjAuMTcxNTUyNDYxMC4wLjAuMA..)
The `ssh-keygen` command is a component of most SSH implementations used to generate a public key pair for use when authenticating with a remote server.
In the typical use case, users generate a new public key and then copy their public key to the server using SSH and their login credentials for the remote server.

By default, ssh-keygen creates an [RSA](https://www.techtarget.com/searchsecurity/definition/RSA) key pair and stores the public key in a public key file named _.ssh/id_rsa.pub_ and a private key file named _.ssh/id_rsa_.

Key generation begins with something like the following command:

```
ssh-keygen -t rsa
```

- Generates a public key pair.
- "Enter passphrase" -> the user can enter a key passphrase to protect access to the private key.
> [!tip]
  > Using a passphrase enhances security, and a passphrase is recommended for sensitive applications.
  > If a key is not passphrase-protected, an attacker who gains access to the user's system would also gain direct access to possibly sensitive remote systems.
  > ==In some cases, it may be acceptable to press enter for no passphrase in response to this prompt.==
- The private key, also known as _identification_, is stored in a file named _id_rsa_ in the _.ssh_ directory of the user's home directory 
  _HOME$/_ in **Windows**
  _~/_ in **Linux, Unix-based OSes**
- The public key is saved in a file with the same name as the private key but with the extension .pub producing a file named _pub_ in the same directory.
- The key fingerprint is created and displayed. 
> [!tip]
> The fingerprint is a short sequence of bytes generated with a [cryptographic hash function](https://www.techtarget.com/searchsecurity/definition/cryptographic-checksum) applied to the generated key. SSH implementations can use fingerprints to authenticate the public key.
> The fingerprint includes any comments applied to the key pair.
> The fingerprint also identifies the hashing algorithm used to create the public key.
> In this case, the algorithm is Secure Hash Algorithm 256, or SHA-256, with a digest composed of 256 bits.
- A randomart image is displayed.
  This is an image consisting of American Standard Code for Information Interchange, or ASCII, characters based on the data in the key fingerprint. The key's randomart image is intended to enable humans to visually determine whether fingerprints for different servers are identical or not. The bits in the fingerprint are treated like instructions for an [algorithm that outputs](https://blog.benjojo.co.uk/post/ssh-randomart-how-does-it-work-art) the randomart image.

---
#### ==`ssh-keygen`== 
The ssh-keygen command creates two files, one **public** and one **private**, for the local computer.
The two files are named:

1. **_id-rsa_** -> contains the private key of the pair.
   This file should never be shared or copied to any remote system unless it is a system under the key pair holder's control.
3. **_id-rsa.pub_** -> contains the public key of the pair.
   This file can be shared and copied to other systems, especially when the user plans to log in to those systems using SSH.

The file name for other key types use, by default, the form of `~/.ssh/id_[key type]` -- specified to be in the _.ssh_ directory of a user's Unix-based account -- so the default file names for each different type of key include the following:

| **Key type**                | **Public key file name** | **Private key file name** |
| --------------------------- | ------------------------ | ------------------------- |
| DSA                         | _~/.ssh/id_dsa.pub_      | _~/.ssh/id_dsa_           |
| RSA                         | _~/.ssh/id_rsa.pub_      | _~/.ssh/id_rsa_           |
| ECDSA                       | _~/.ssh/id_ecdsa.pub_    | _~/.ssh/id_ecdsa_         |
| Ed25519 (Edwards-curve DSA) | _~/.ssh/id_ed25519.pub_  | _~/.ssh/id_ed25519_       |

Copying the public key file to a server -- or to multiple servers -- is the next step to getting automatic strong authentication when connecting to remote SSH servers.

