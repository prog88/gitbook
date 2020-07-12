# GPG 

## Install GPG

## Generate a GPG Key

1. Run the following command:

```
gpg --full-gen-key
```

2. A prompt ask you to choose between 1-4 key type:

```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 1
```

2. It is recommended to choose at least `4096`:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048) 4096
Requested keysize is 4096 bits
```

3. Specify GPG key expiration:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
```

4. Asking for confirmation (y/N):

```
Is this correct? (y/N) y
```

5. Double checking your info to validate or edit:

```
GnuPG needs to construct a user ID to identify your key.

Real name: <your_real_name>
Email address: <your_email>
Comment:
You selected this USER-ID:
    "<your_real_name> <your_email>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
```

6. Listing GPG Keys:

```
gpg --list-secret-keys --keyid-format LONG <your_email>
```

It will prompt information such as the following:

```
sec   rsa4096/BC4F4B77228120E9 2020-05-30 [SC]
      FBC35FE19353F84DAD4640B6BC4F4B77228120E9
uid                 [ultimate] <comment> <your_email>
ssb   rsa4096/4FF81D971F73F011 2020-05-30 [E]
```

7. Export public key ID

Copy the value equivalent of `BC4F4B77228120E9` (replace your key ID as listed on step6)

```
gpg --armor --export BC4F4B77228120E9
```

## Signing git commits

0. Add the ID to your Git configuration file `config` or `.gitconfig` (example: `BC4F4B77228120E9`):

```
[user]
  name = <your_name>
  email = <your_email>
  signingkey = <same_id_key_used_on_step7>
```

1. Commit can be signed by adding the following `-S` flag

```
git commit -S -m "your commit description message"
```

2. Case if you don't want to bother with `-S` flag

```
git config --global commit.gpgsign true
```

## Tips & Tricks 

For OSX add the following command on your `.<type>rc` file. (`.bashrc` | `.zshrc`)

```
# ioctl issue for signing GPG OSX
export GPG_TTY=$(tty)
```
