# How to Set up SSH

1. What is SSH
2. Advantages of ssh-key authentication
3. How to generate ssh-key 
4. How to configure generated ssh keys
5. Use-case 1: GitHub
6. Use-case 2: Remote server
7. References

## 1. What is SSH 

  SSH stands for Secure Shell, by which users can manage systems or transfer of files from computer to computer. Users  can access to remote machines by username + password or ssh key. I personally prefer ssh-key authentication to traditional login authentication since you can use ssh-key to authenticate yourself not only on remote computers, but also on GitHub and so on. 

## 2. Advantages of ssh-key authentication

  The use of multiple SSH keys to grant secure server access to multiple individuals affords three advantages over assigning separate user accounts with traditional login credentials.

- Grants access to multiple parties without sharing passwords.
- Simplifies permission management; all parties log in as the same user and thereby share permissions.
- Allow for easy access revocation as needed.

## 3. How to generate ssh-key 

  There are multiple algorithms to generate ssh-key: RSA, DSA, ECDSA, and EdDSA. Mostly used algorithm is RSA (the default option for ssh-keygen), but EdDSA is newer and provides the highest security level compared to key length.

simply: 
`ssh-keygen -t ed25519 -C "john@example.com" `
or more securely:
`ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "john@example.com" `

- **-t** specifies the type of key to create, in our case the Ed25519.
- **-f** specifies the filename of the generated key file. 
- **-C** specifies a comment.

## 4. How to configure generated ssh keys

You need to use ssh-agent, which is a helper program that keeps track of user's identity keys and their passphrases. Make sure ssh-agent is running:
`eval "$(ssh-agent -s)" `

Add a host onto "~/.ssh/config":
```
Host myRemoteServer
  HostName 198.222.111.33
  User john
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```


Finally, add your SSH key to the agent:

option1 (Mac user):
If you're using macOS Sierra 10.12.2 or later, you will need to modify your ~/.ssh/config file to automatically load keys into the ssh-agent and store passphrases in your keychain.
```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

`ssh-add -K ~/.ssh/id_ed25519 `

option2 (linux user):
And then, add your newly generated Ed25519 key to SSH agent
`ssh-add ~/.ssh/id_ed25519 ` 
or add all generated keys to SSH agent
`ssh-add `  

## 5. Use-case 1: GitHub

First,
`pbcopy < ~/.ssh/id_ed25519.pub `

Click my profile image -> Settings -> In the "Access" section of the sidebar, click  SSH and GPG keys -> Click New SSH key or Add SSH key -> paste the copied key into "Key" field.

## 6. Use-case 2: Remote server

First of all, copy the public key to the remote server:
`ssh-copy-id -i ~/.ssh/id_ed25519.pub john@198.222.111.33 `

And then:
`ssh john@198.222.111.33 `
or:
`ssh myRemoteServer `

## 7. References

- [Generate a new ssh key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Add a new ssh-key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- [Secure Shell](https://www.techtarget.com/searchsecurity/definition/Secure-Shell)
- [How to create users in linux using user add command](https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/)
- [Upgrade your ssh key to ed25519](https://medium.com/risan/upgrade-your-ssh-key-to-ed25519-c6e8d60d3c54)
- [Using the ssh config file](https://linuxize.com/post/using-the-ssh-config-file/)
- [ssh-copy-id](https://www.ssh.com/academy/ssh/copy-id)

