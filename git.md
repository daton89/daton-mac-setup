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

### SSH Config for GitHub {#ssh-config-for-github}

The instructions below are referenced from [the official documentation](https://help.github.com/articles/generating-ssh-keys).

#### Check for existing SSH keys {#check-for-existing-ssh-keys}

First, we need to check for existing SSH keys on your computer. We do this by running:

```bash
ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```

Check the directory listing to see if you have files named either `id_rsa.pub` or `id_dsa.pub`. If you don't have either of those files then read on, otherwise skip the next section.

#### Generate a new SSH key {#generate-a-new-ssh-key}

If can follow the previous [SSH](https://daton.gitbook.io/daton-mac/~/edit/primary/git) step to generate an ssh key.

#### Add your SSH key to the ssh-agent {#add-your-ssh-key-to-the-ssh-agent}

Run the following commands to add your SSH key to the `ssh-agent`.

```bash
eval "$(ssh-agent -s)"
```

If you're running macOS Sierra 10.12.2 or later, you will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain:

```text
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

No matter what operating system version you run you need to run this command to complete this step:

```bash
ssh-add -K ~/.ssh/id_rsa
```

#### Adding a new SSH key to your GitHub account {#adding-a-new-ssh-key-to-your-github-account}

The last step is to let GitHub know about your SSH key. Run this command to copy your key to your clipboard:

```bash
pbcopy < ~/.ssh/id_rsa.pub
```

Then go to GitHub and [input your new SSH key](https://github.com/settings/ssh/new). Paste your key in the "Key" text box and pick a name that represents the computer you're currently using.

