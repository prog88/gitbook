# SSH

SSH is the secure shell protocol. It allows you to attach your terminal window to a remote server and execute commands in it.

# Generating new SSH key

## ED25519 SSH keys

ED25519 (SSH introduced in 2014 OpenSSH 6.5) 

```
ssh-keygen -t ed25519 -C "email@address.com"
```

It generate public/private ed25519 key pair in: `~/.ssh/id_ed25519)`

## RSA SSH keys

By default `ssh-keygen` command create an 1024-bit RSA key. _(Minimum recommended key size of `2048`)_.

```
ssh-keygen -o -t rsa -b 4096 -C "email@domain.com"
```

It generate public/private RSA key pair in: `~/.ssh/id_rsa`

## Update SSH key Passphrase 

Specify the SSH key you would like to change the passphrase.

```
ssh-keygen -p -f "~/.ssh/<path/to/ssh_key>"
```

# SSH Gitlab


## Public SSH Key

For OSX, buffer public key to clipboard by specify your specific key with `.pub` extension.

```
pbcopy < ~/.ssh/<your_generated_key>.pub
```

## Testing your key

Quick test by running the following command:
```
ssh -T <your_gitlab_domain>
```

Verbose version:
```
ssh -Tvvv <your_gitlab_domain>
```

## Specifying none default path 

To change non-default file path for SSH Key pair you can run this following command:
```
eval $(ssh-agent -s)
ssh-add <path to private SSH key>
```

## Configuration file

The case of multiple ssh key for different usage could be config in the file `~/.ssh/config`.

The followin case illustrate an usage of 3 keys for 3 differents domain of Git: 

```
# office domain
Host <user_office_git_domain>
  Hostname <domain>
  Preferredauthentications publickey
  IdentityFile ~/.ssh/office_id_rsa

# some client
Host <user_client_git_domain>
  Hostname <domain>
  Preferredauthentications publickey
  IdentityFile ~/.ssh/client_id_rsa
  
# personal
Host <user_personal_git_domain>
  Hostname <domain>
  Preferredauthentications publickey
  IdentityFile ~/.ssh/own_id_rsa
```

_FI: It can be multiple domains using the same key ( id_rsa | id_ed25519 )_

## Useful link

Going further with [Gitlab official documentation](https://docs.gitlab.com/ee/ssh/#multiple-accounts-on-a-single-gitlab-instance)


# SSH-AGENT

Now that you setup your ssh with a passphrase to add some level of security.

But you don't want the inconvenience to type your passphrase every single time you use your key.

When using git/ssh, you may have come across the following prompt:
```
Enter passphrase for key '/home/user/.ssh/id_rsa':
```

## Pitfalls

* Make sure your keys/agent are unload when you log off your machine. 

* Do not copy your `private keys` on somebody else computer which has root on.

* Do not run `ssh-agent` on somebody else computer which has root on.


## Trade-off (Security vs Convenience)

If you are tempted to add the following script on your `dotfile profile`.
You have to be aware that every instance of your Terminal will start a `ssh-agent process`

```
if [ -z "$SSH_AUTH_SOCK" ] ; then
    eval `ssh-agent`
    ssh-add
fi
```

* To remove current agent provide by `SSH_AGENT_PID` run:
```
eval `ssh-agent -k`
```

* To list running ssh-agent process (OSX):
```
ps x | grep ssh-agent
```

* Last tips for security would be to set a time to live using: `-s` bourne shell stdout, `-t 86400` for 24 hours. It could be less according to your security policy definition.
```
eval `ssh-agent -s -t 86400`
```