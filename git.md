# Git

## Installation

If you installed Xcode from the you should skip this task, otherwise run:

```bash
brew install git
```

When done, to test that it installed properly you can run:

```bash
git --version
```

And `which git` should output `/usr/local/bin/git`.

Next, we'll define your Git user \(should be the same name and email you use for [GitHub](https://github.com/)\):

```bash
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
```

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method \(versus SSH\). To prevent `git` from asking for your username and password every time you push a commit you can cache your credentials by running the following command, as described in the [instructions](https://help.github.com/articles/caching-your-github-password-in-git/).

```bash
git config --global credential.helper osxkeychain
```

## Adding an SSH key in your GitHub account

The instructions below are referenced from [the official documentation](https://help.github.com/articles/generating-ssh-keys).

### Check for existing SSH keys

First, we need to check for existing SSH keys on your computer. We do this by running:

```bash
ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

Check the directory listing to see if you have files named either `id_rsa.pub` or `id_dsa.pub`. If you don't have either of those files then read on, otherwise skip the next section.

### Generate a new SSH key

For security reason you can't use the same key between accounts. You must create new keys for each individual account that you want to use. 

```bash
ssh-keygen -t rsa 
# Generating public/private rsa key pair.
# Enter file in which to save the key
(/Users/tony/.ssh/id_rsa): /Users/tony/.ssh/daton89_github
```

{% hint style="info" %}
To create a key with a name or path other than the default, specify the full path to the key. For example, to create a key called `my-new-ssh-key`, enter a path like the one shown at the prompt:  `(/Users/tony/.ssh/id_rsa): /Users/tony/.ssh/daton89_github`
{% endhint %}

Press the Enter or Return key to accept the default location.

Enter and re-enter a passphrase when prompted. The command creates your default identity with its public and private keys. 

Now list the contents of `~/.ssh` to view the key files.

```bash
ls ~/.ssh
id_rsa id_rsa.pub daton89_github daton89_github.pub
```

### Add your SSH key to the ssh-agent

Run the following commands to make sure that the `ssh-agent`is running.

```bash
eval `ssh-agent
```

No matter what operating system version you run you need to run this command to complete this step:

```bash
ssh-add -K ~/.ssh/daton89_github
```

### Copy and add the public key to your GitHub account

The last step is to let GitHub know about your SSH key. Run this command to copy your key to your clipboard:

```bash
pbcopy < ~/.ssh/id_rsa.pub
```

Then go to GitHub and [input your new SSH key](https://github.com/settings/ssh/new). Paste your key in the "Key" text box and pick a name that represents the computer you're currently using.

#### More Resources

{% embed data="{\"url\":\"https://help.github.com/articles/generating-ssh-keys\",\"type\":\"link\",\"title\":\"Generating SSH Keys · GitHub Help\",\"icon\":{\"type\":\"icon\",\"url\":\"https://help.github.com/favicon.ico\",\"aspectRatio\":0},\"caption\":\"Official GitHub documentation\"}" %}

## Adding an SSH Key in your BitBucket account



#### More Resources

{% embed data="{\"url\":\"https://confluence.atlassian.com/bitbucket/set-up-an-ssh-key-728138079.html\",\"type\":\"link\",\"title\":\"Set up an SSH key - Atlassian Documentation\",\"icon\":{\"type\":\"icon\",\"url\":\"https://s3.amazonaws.com/cac-static-assets-prod/3.15.2/dist/common/images/favicon.png\",\"width\":32,\"height\":32,\"aspectRatio\":1}}" %}



