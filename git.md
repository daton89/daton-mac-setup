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

We suggest to use an SSH Key for each account.

### Check for existing SSH keys

First, we need to check for existing SSH keys on your computer. We do this by running:

```bash
ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

Check the directory listing to see if you have files named either `id_rsa.pub` or `id_dsa.pub`. If you already have this you need to use a different name for your new  SSH Key.

### Generate a new SSH key

```bash
ssh-keygen -t rsa 
# Generating public/private rsa key pair.
# Enter file in which to save the key
(/Users/tony/.ssh/id_rsa): /Users/tony/.ssh/daton89_github
```

{% hint style="info" %}
To create a key with a name or path other than the default, specify the full path to the key. For example, to create a key called `my-new-ssh-key`, enter a path like the one shown at the prompt:  `(/Users/tony/.ssh/id_rsa): /Users/tony/.ssh/daton89_github`
{% endhint %}

Change the default location and name and press enter.

Enter and re-enter a passphrase when prompted. The command creates your identity with its public and private keys. 

Now list the contents of `~/.ssh` to view the key files.

```bash
ls ~/.ssh
config id_rsa id_rsa.pub daton89_github daton89_github.pub
```

### Add your SSH key to the ssh-agent

Run the following commands to make sure that the `ssh-agent`is running.

```bash
eval 'ssh-agent'
```

No matter what operating system version you run you need to run this command to complete this step:

```bash
ssh-add -K ~/.ssh/daton89_github
# Identity added: /Users/tony/.ssh/daton89_github (/Users/tony/.ssh/daton89_github)
```

To make sure that your key was added to the agent you can run:

```bash
ssh-add -l
```

### Copy and add the public key to your GitHub account

The last step is to let GitHub know about your SSH key. Run this command to copy your key to your clipboard:

```bash
pbcopy < ~/.ssh/daton89_github.pub
```

Then go to GitHub and [input your new SSH key](https://github.com/settings/ssh/new). Paste your key in the "Key" text box and pick a name that represents the computer you're currently using.

#### More Resources

{% embed data="{\"url\":\"https://help.github.com/articles/generating-ssh-keys\",\"type\":\"link\",\"title\":\"Generating SSH Keys · GitHub Help\",\"icon\":{\"type\":\"icon\",\"url\":\"https://help.github.com/favicon.ico\",\"aspectRatio\":0},\"caption\":\"Official GitHub documentation\"}" %}

## Adding an SSH Key in your BitBucket account

You can generate and add your Key to ssh-agent with the same process used for GitHub. For add  your public key to your account you need to follow these steps:

1. From Bitbucket, choose **Bitbucket settings** from your avatar in the lower left. The **Account settings** page opens.
2. Click **SSH Keys.**
3. In your terminal copy the public key with this command: `pbcopy < ~/.ssh/<your pub key name>.pub`
4. From BitBucket, click **Add key**.
5. Enter a **Label** for the Key.
6. Paste the copied public key into the **SSH Key** field.
7. Click **Save**.
8. Return to your terminal window and verify your configuration and username by entering the following command: `ssh -T git@bitbucket.org`
   1. The command message tells you which of your Bitbucket accounts can log in with that key.
   2. If you get an error message with `Permission denied (publickey)`, check the [Troubleshoot SSH issues](https://confluence.atlassian.com/bitbucket/troubleshoot-ssh-issues-271943403.html) page for help.

Now that you've got an SSH key set up, use the SSH URL the next time you [clone a repository](https://confluence.atlassian.com/bitbucket/clone-a-repository-223217891.html). If you already have a repository that you cloned over HTTPS, [change the remote URL for your repository](https://confluence.atlassian.com/bitbucket/change-the-remote-url-to-your-repository-794212774.html) to use its SSH URL.



#### More Resources

{% embed data="{\"url\":\"https://confluence.atlassian.com/bitbucket/set-up-an-ssh-key-728138079.html\",\"type\":\"link\",\"title\":\"Set up an SSH key - Atlassian Documentation\",\"icon\":{\"type\":\"icon\",\"url\":\"https://s3.amazonaws.com/cac-static-assets-prod/3.15.2/dist/common/images/favicon.png\",\"width\":32,\"height\":32,\"aspectRatio\":1}}" %}



