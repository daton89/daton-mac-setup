# VS Code

## Installation

You can get `Visual Studio Code` from his [official site](https://code.visualstudio.com/). Once downloaded, drag and drop the application file into your **Applications** folder.

{% hint style="info" %}
Instead of downloading and installing `VSCode` manually, you can use `Homebrew` `brew cask install visual-studio-code`
{% endhint %}

## Installation of a Font

We are following the article [Multiple Fonts: Alternative to Operator Mono in VSCode](https://medium.com/@zamamohammed/multiple-fonts-alternative-to-operator-mono-in-vscode-7745b52120a0)

1. Download and install both [FiraCode](https://github.com/tonsky/FiraCode) and [FlottFlott](http://www.dafont.com/flottflott.font) \(or another cursive alternative if you want\)
2. Install VSCode Extension: [Custom CSS and JS Loader](https://marketplace.visualstudio.com/items?itemName=be5invis.vscode-custom-css)
3. Save [styles.css](https://gist.githubusercontent.com/mohammedzamakhan/03be8cb8bcab53b09772db4d09b7d32e/raw/6d86ae0b78c54810130091304c51e8614f4f4199/styles.css) on your desktop
4. Update the User settings \([settings.json](https://gist.githubusercontent.com/mohammedzamakhan/e8f10b5d759c01e1b9d7de7bccc3832c/raw/538b4e4b4d44af31e1b8ac3420f884d84c3d139b/settings.json)\) in VSCode. **\(note: don’t forget to change the path “ vscode\_custom\_css.imports”\)**

```javascript
// Place your settings in this file to overwrite the default settings
{
    "editor.fontFamily": "Fira Code",
    "editor.fontLigatures": true,
    "vscode_custom_css.imports": ["file:///Users/daton/Desktop/styles.css"]
}
```

Replace your User from the path of custom css import.

![The result should look like this.](.gitbook/assets/1_ehwritlj5wtgd3vbbiwglq.png)

## More resources 

{% embed data="{\"url\":\"https://vscodecandothat.com/\",\"type\":\"link\",\"title\":\"VS Code Can Do That?\",\"icon\":{\"type\":\"icon\",\"url\":\"https://vscodecandothat.com/static/favicon.ico\",\"aspectRatio\":0}}" %}



