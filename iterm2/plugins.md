# Plugins

Now is time to setup some useful plugins for iTerm.

## zsh-autosuggestions

[_Fish_](http://fishshell.com/)_-like fast/unobtrusive autosuggestions for zsh._

It suggests commands as you type, based on command history. This is my favourite plugin, it will save you a lot of time spent in typing commands in our terminal.

### Installing with Oh My Zsh

1. Clone [this](https://github.com/zsh-users/zsh-autosuggestions) repository into `$ZSH_CUSTOM/plugins` \(by default `~/.oh-my-zsh/custom/plugins`\)

   ```bash
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   ```

2. Add the plugin to the list of plugins for Oh My Zsh to load \(open `~/.zshrc`\):

   ```text
   plugins=(zsh-autosuggestions)
   ```

3. Start a new terminal session.

![](../.gitbook/assets/2018-05-27-13.29.41.gif)

For other types of installation go [here](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md).

## Syntax highlighting

This package provides syntax highlighting for the shell zsh. It enables highlighting of commands whilst they are typed at a zsh prompt into an interactive terminal. This helps in reviewing commands before running them, particularly in catching syntax errors.

### Installing with Oh My Zsh

1. Clone this repository in oh-my-zsh's plugins directory:

   ```bash
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```

2. Activate the plugin in `~/.zshrc`:

   ```bash
    plugins=( [plugins...] zsh-syntax-highlighting)
   ```

3. Source `~/.zshrc` to take changes into account:

   ```bash
    source ~/.zshrc
   ```

## Enable natural text selection

By default, word jumps \(`option + →` or `option + ←`\) and word deletions \(`option + backspace`\) do not work. 

To enable these, go to "iTerm =&gt; Preferences =&gt; Profiles =&gt; Keys =&gt; Load Preset... =&gt; Natural Text Editing"

![](../.gitbook/assets/2018-05-27-13.37.12.gif)

## How to Customize Your Command Prompt

For further customisation of your prompt, you can follow a great guide here: [https://code.tutsplus.com/tutorials/how-to-customize-your-command-prompt--net-24083](https://code.tutsplus.com/tutorials/how-to-customize-your-command-prompt--net-24083)

