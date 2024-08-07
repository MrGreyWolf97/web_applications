To setup GitHub SSH keys and use them on both Ubuntu or Windows, follow these steps:

1. Create a GitHub SSH key pair with the [_ssh-keygen_ command](https://www.techtarget.com/searchsecurity/tutorial/Use-ssh-keygen-to-create-SSH-key-pairs-and-more?_gl=1*1grmfds*_ga*MjAwMjY2ODMyOS4xNzE1NTI0NjEx*_ga_TQKE4GS5P9*MTcxNTUyODg1NS4yLjAuMTcxNTUyODg1NS4wLjAuMA..).
2. Copy the value of the public SSH key to the clipboard.
3. Login to GitHub and navigate to your account settings.
4. Click on the link for SSH and GPG keys.
5. Click _Add Key_ to register the public SSH key with your account.
6. Name the key and paste the copied value into the text field.
7. Save your changes.
8. In your Git client, use the SSH-based GitHub URL to clone your repo.

---
### [Create SSH key pair](obsidian://open?vault=obsidian_thee_grey&file=SSH%20%26%20ssh-keygen)
In Ubuntu and Windows, the SSH keys you generate for GitHub must go in a folder named _.ssh_ under the user’s home directory. Perform the [GitHub SSH key create](https://searchitoperations.techtarget.com/tutorial/Create-an-SSH-key-with-GitHub-for-network-access?_gl=1*171klkt*_ga*MjAwMjY2ODMyOS4xNzE1NTI0NjEx*_ga_TQKE4GS5P9*MTcxNTU1MDExMS4zLjAuMTcxNTU1MDExMS4wLjAuMA..) operation in this folder:

```shell
cd ~/.ssh
```

Use the _ssh-keygen_ command to [create GitHub SSH key pairs](https://www.techtarget.com/searchsecurity/tutorial/Use-ssh-keygen-to-create-SSH-key-pairs-and-more):

```shell
ssh-keygen -t ed25519 -C "enrico.cestino@live.it"
```

The operation then prompts you to choose a location in which to save the public and private keys. Just click _Return_ to leave them in the _.ssh_ folder. The SSH command looks here when a connection attempt is made to a remote server.

The _ssh-keygen_ command also asks you to protect your GitHub SSH key with an optional passphrase. It’s permissible to leave the passphrase blank, so click _Return_ when prompted.

### Connect to GitHub with SSH

The purpose of the parameters used with the GitHub _ssh-keygen_ command are as follows:

- The -o flag forces the tool to generate SSH keys with the OpenSSH format.
- The -t flag specifies the type of SSH keys to create.
- The -C flag allows for comments that get added as metadata at the end of the public key.

By default, the public and private GitHub SSH keys are placed in a folder named _.ssh_ under the user’s home directory.

1. You will need to paste the contents of your public SSH key into GitHub.
   On Ubuntu you can _cat_ the file to view its contents in the Ubuntu Terminal and then copy it. On Windows, just open the file with a text editor.
2. Configure the GitHub SSH key in the settings of your online account.
   Log into GitHub, navigate to your account settings, and find the link named “SSH and GPG keys.”
   Click on this link to create a new GitHub SSH key.
   Provide a unique name and paste the value of the private GitHub SSH key you copied earlier.

---
## [Adding your SSH key to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key.

1. Start the ssh-agent in the background.
    
    ```shell
    $ eval "$(ssh-agent -s)"
    > Agent pid 59566
    ```
    
    Depending on your environment, you may need to use a different command. For example, you may need to use root access by running `sudo -s -H` before starting the ssh-agent, or you may need to use `exec ssh-agent bash` or `exec ssh-agent zsh` to run the ssh-agent.
    
2. Add your SSH private key to the ssh-agent.
    
    If you created your key with a different name, or if you are adding an existing key that has a different name, replace _id_ed25519_ in the command with the name of your private key file.
    
    ```shell
    ssh-add ~/.ssh/id_ed25519
    ```
    
3. Add the SSH public key to your account on GitHub. For more information, see "[Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)."

---
##### Resources
- [Full guide](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/GitHub-SSH-Key-Setup-Config-Ubuntu-Linux)
- [Github guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- 