# SSH

## Step One—Create the RSA Key Pair

The first step is to create the key pair on the client machine \(there is a good chance that this will just be your computer\):

```bash
ssh-keygen -t rsa
```

## Step Two—Store the Keys and Passphrase

Once you have entered the Gen Key command, you will get a few more questions:

```bash
Enter file in which to save the key (/daton/.ssh/id_rsa):
```

You can press enter here, saving the file to the user home \(in this case, my example user is called daton\).

```bash
Enter passphrase (empty for no passphrase):
```

It's up to you whether you want to use a passphrase The entire key generation process looks like this:

```bash
ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/daton/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /daton/.ssh/id_rsa.
Your public key has been saved in /daton/.ssh/id_rsa.pub.
The key fingerprint is:
4a:dd:0a:c6:35:4e:3f:ed:27:38:8c:74:44:4d:93:67 daton@a
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

The public key is now located in `/daton/.ssh/id_rsa.pub`

The private key \(identification\) is now located in `/daton/.ssh/id_rsa`

## More resources 

{% embed data="{\"url\":\"https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-digitalocean-droplets\",\"type\":\"link\",\"title\":\"How To Use SSH Keys with DigitalOcean Droplets \| DigitalOcean\",\"description\":\"This guide is for Mac OS X and Linux users. Learn how to use SSH Keys with DigitalOcean Droplets.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.digitalocean.com/favicon.ico\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://www.digitalocean.com/assets/community/default\_community\_sharing-65c1cc547375d6e37cc45195b3686769.png\",\"width\":1024,\"height\":536,\"aspectRatio\":0.5234375}}" %}



