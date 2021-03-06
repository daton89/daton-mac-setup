# SSH

## Create the RSA Key Pair

The first step is to create the key pair on the client machine \(there is a good chance that this will just be your computer\):

```bash
ssh-keygen -t rsa
```

## Store the Keys and Passphrase

Once you have entered the Gen Key command, you will get a few more questions:

```bash
Enter file in which to save the key (/Users/tony/.ssh/id_rsa):
```

You can press enter here, saving the file to the user home \(in this case, my example user is called daton\).

```bash
Created directory '/Users/tony/.ssh'.
Enter passphrase (empty for no passphrase):
```

It's up to you whether you want to use a passphrase The entire key generation process looks like this:

```bash
ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/tony/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/tony/.ssh/id_rsa.
Your public key has been saved in /Users/tony/.ssh/id_rsa.pub.
The key fingerprint is:
4a:dd:0a:c6:35:4e:3f:ed:27:38:8c:74:44:4d:93:67 tony@Antonios-MacBook-Pro.local
The key's randomart image is:
+--[ RSA 2048]----+
|          .oo.   |
|         .  o.E  |
|        + .  o   |
|     . = = .     |
|      = S = .    |
|     o + = +     |
|      . o + o .  |
|           . o   |
|                 |
+-----------------+
```

The public key is now located in `/Users/tony/.ssh/id_rsa.pub`

The private key \(identification\) is now located in `/Users/tony/.ssh/id_rsa`

## Add your SSH key to the ssh-agent

Run the following commands to make sure that the `ssh-agent`is running.

```bash
eval `ssh-agent
```

If you're running macOS Sierra 10.12.2 or later, you will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain:

```bash
Host *
  AddKeysToAgent yes  
  UseKeychain yes  
  IdentityFile ~/.ssh/id_rsa
```

No matter what operating system version you run you need to run this command to complete this step:

```bash
ssh-add -K ~/.ssh/id_rsa

# you can check your added key with:
ssh-add -l
```

## Host Key Warning

If you happened to destroy a server directly prior to creating the one that you are connecting to, you may see a message like this:

```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
...
```

If this is the case, your new server probably has the same IP address as the old, destroyed server, but a different host SSH key. This is fine, and you can remove the warning, by deleting the old server's host key from your system, by running this command:

```bash
ssh-keygen -R [your.ip.address.here]
```

Now try connecting to your server again.

## SSH Best Practices 

When you set up SSH, you create a key pair that contains a private key \(saved to your local computer\) and a public key \(uploaded to a remote server\). This server uses the key pair to authenticate anything the associated account can access. This two-way mechanism prevents man-in-the-middle attacks.

This first key pair just created is your default SSH identity. I suggest to use it to manage your servers. If you need to manage GitHub or BitBucket accounts you need more than a default identity, you can [set up additional keys](https://confluence.atlassian.com/bitbucket/set-up-additional-ssh-keys-271943168.html).

{% hint style="info" %}
For security reasons, we recommend that you generate a new SSH key and replace the existing key on your account at least once a year.
{% endhint %}

## More resources 

{% embed url="https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-digitalocean-droplets" %}



