---
layout: post
title:  "Installing Sublime Text Editor on Ubuntu"
date:   2018-05-31 10:00:00 -0300
categories: tutorial sublime
---
Lets install using the terminal. Execute the follows commands:
```
# echo "deb https://download.sublimetext.com/ apt/stable/" | tee /etc/apt/sources.list.d/sublime-text.list
# wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | apt-key add -
# apt update
# apt install sublime-text
```

## Installing the Package Control
Open the sublime text and click in `Tools > Install Package Control...`.

## Installing a package
Click in `Preferences > Package Control > Package Control: Install Package`.

Type the name of package and click on it.

## Some iteresting packages

| Name                                                                                            | Description                   | Common commands      |
|:------------------------------------------------------------------------------------------------|:------------------------------|:---------------------|
| [HTML5](https://packagecontrol.io/packages/HTML5)                                               | Snippets for HTML5.           | html5                |
| [HTML Snippets](https://packagecontrol.io/packages/HTML%20Snippets)                             | Snippets for HTML.            | doctype, meta, lorem |
| [Java​Script & NodeJS](https://packagecontrol.io/packages/JavaScript%20%26%20NodeJS%20Snippets) | Snippets for Javscript.       | cl, gi, fn           |
| [HTMLBeautify](https://packagecontrol.io/packages/HTMLBeautify)                                 | Autoformat HTML code          | Ctrl+Alt+Shift+F     |
| [Markdown Table Formatter](https://packagecontrol.io/packages/Markdown%20Table%20Formatter)     | Autoformat tables in markdown | Ctrl+Alt+Shift+T     |
| [CodeFormatter](https://packagecontrol.io/packages/CodeFormatter)                               | Autoformat your code          | Ctrl+S               |
| [phpfmt](https://packagecontrol.io/packages/phpfmt)                                             | Autoformat PHP. (need php).   | Use CodeFormatter    |
| [SublimeCodeIntel](https://packagecontrol.io/packages/SublimeCodeIntel)                         | Autocomplete code.            |                      |
| [Bracket​Highlighter](https://packagecontrol.io/packages/BracketHighlighter)                    | Bracket and tag highlighter.  |                      |

