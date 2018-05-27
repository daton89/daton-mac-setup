# Node.js

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine.

### Installation {#installation}

#### Using Homebrew {#using-homebrew}

```text
brew install node
```

#### Manage multiple Node Version with nvm {#using-node-version-manager-nvm}

Download and install [nvm](https://github.com/creationix/nvm) by running:

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash
```

Then download Node and select your version by running:

```bash
source ~/.bashrc        # source your bashrc/zshrc to add nvm to PATH
command -v nvm          # check the nvm use message
nvm install node        # install most recent Node stable version
nvm ls                  # list installed Node version
nvm use node            # use stable as current version
nvm ls-remote           # list all the Node versions you can install
nvm alias default node  # set the installed stable version as the default Node
```

See the [documentation](https://github.com/creationix/nvm#installation) for information.

#### Switch automatically the Node and NPM version 

Make sure you have set the `default` alias for nvm - e.g.: `nvm alias default 8.11.2`

```bash
git clone https://github.com/dijitalmunky/nvm-auto.git ~/.oh-my-zsh/custom/plugins/nvm-auto
```

Add `nvm-auto` to your plugins in `~/.zshrc`.

Add a call to the `nvm_auto_switch` function **after** NVM is initialized in your `.zshrc` file.

Source `.zshrc` in your current shell or restart your shell.

### npm usage {#npm-usage}

To install a package:

```text
npm install <package> # Install locally
npm install -g <package> # Install globally
```

To install a package and save it in your project's `package.json` file:

```text
npm install <package> --save
```

To see what's installed:

```text
npm list [-g]
```

To find outdated packages:

```text
npm outdated [-g]
```

To upgrade all or a particular package:

```text
npm update [-g] [<package>]
```

To uninstall a package:

```text
npm uninstall [-g] <package>
```

### Yarn

For project with a lot of dependencies, or particular dependencies, we should probably use yarn. 

**Homebrew**

You can install `Yarn` through the [Homebrew](https://brew.sh/). This will also install `Node.js` if it is not already installed.

```bash
brew install yarn
```

If you use [nvm](https://github.com/creationix/nvm) or similar, you should exclude installing `Node.js` so that nvm’s version of `Node.js` is used.

```bash
brew install yarn --without-node
```

**Path Setup**

If you chose manual installation, the following steps will add Yarn to path variable and run it from anywhere.

Note: your profile may be in your `.profile`, `.bash_profile`, `.bashrc`, `.zshrc`, etc.

1. Add this to your profile: `export PATH="$PATH:/opt/yarn-[version]/bin"` \(the path may vary depending on where you extracted Yarn to\)
2. In the terminal, log in and log out for the changes to take effect

To have access to Yarn’s executables globally, you will need to set up the `PATH` environment variable in your terminal. To do this, add ``export PATH="$PATH:`yarn global bin`"`` to your profile.

**Upgrade Yarn**

Yarn will warn you if a new version is available. To upgrade Yarn, you can do so with Homebrew.

```bash
brew upgrade yarn
```

Test that Yarn is installed by running:

```bash
yarn --version
```

{% hint style="info" %}
**Problems?** If you are unable to install Yarn with any of these installers, please search through GitHub for an existing issue or open a new one.

[Search for an existing issue](https://github.com/yarnpkg/yarn/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aopen%20%22Installation%20Problem%22%20in%3Atitle%20) · [Open a new issue](https://github.com/yarnpkg/yarn/issues/new?title=Installation%20Problem:%20[title]&body=%0A**Which%20operating%20system%20are%20you%20using:**%0A%0A%0A**Please%20describe%20the%20steps%20you%20took%20when%20trying%20to%20install%20Yarn%20and%20what%20went%20wrong:**%0A%0A)
{% endhint %}

#### Usage

Now that you have Yarn installed, you can start using Yarn. Here are some of the most common commands you’ll need.

**Starting a new project**

```text
yarn init
```

**Adding a dependency**

```text
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
```

**Adding a dependency to different categories of dependencies**

Add to `devDependencies`, `peerDependencies`, and `optionalDependencies` respectively:

```text
yarn add [package] --dev
yarn add [package] --peer
yarn add [package] --optional
```

**Upgrading a dependency**

```text
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```

**Removing a dependency**

```text
yarn remove [package]
```

**Installing all the dependencies of project**

```text
yarn
```

or

```text
yarn install
```

**Additional Reading**

[How do I use Yarn? There are basic workflows for both creating and consuming Yarn packages that will help you get productive quickly.](https://yarnpkg.com/en/docs/yarn-workflow)

[CLI CommandsYarn is executed through a rich set of commands allowing package installation, administration, publishing, and more.](https://yarnpkg.com/en/docs/cli/)



