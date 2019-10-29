## vscode个性化配置 


### 插件目录
```
 - HTML css Support
 - HTML Snippets
 - HTMLHint
 - Auto Rename Tag
 - Dark-Dracula Theme
 - Document This
 - Dracula Official
 - filesize
 - Gulp Snippets
 - IntelliJ IDEA KeyBindings
 - jQuery Code Snippets
 - npm
 - Npm Intellisense
 - Open in Browser
 - Path Intellisense
 - Prettier
 - Vetur
 - vscode wxml
 - vscode-fileheader
```
### 用户设置
```
{
    "terminal.integrated.shell.windows": "C:\\Windows\\Sysnative\\cmd.exe",
    "window.menuBarVisibility": "default",
    "workbench.iconTheme": "vscode-icons",
    "files.associations": {
        "*.wpy": "vue"
    },
    "editor.minimap.enabled": true,
    "prettier.singleQuote": true,
    "prettier.tabWidth": 4,
    "git.enableSmartCommit": true,
    "editor.quickSuggestions": {
        "strings": true
    },
    "element-helper.version": "2.0",
    "explorer.confirmDelete": false,
    "editor.formatOnSave": false,
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    "window.zoomLevel": 0,
    "editor.fontFamily": "PingFang SC",
    "editor.fontSize": 18,
    "markdown.styles": [ 
        "file:///C:/Users/WYP/.vscode/vscode-markdown.css"
         ]
}
```
#### 配置文件
* vscode-markdown.css  

```

@charset "ust-8";

/**
 * vscode-markdown.css
 *
 */

h1, h2, h3, h4, h5, h6, p, blockquote {
    margin: 0;
    padding: 0;
    color: #0f0f0f;
}

body {
    font-family: "PingFang SC", "Hiragino Sans GB", Helvetica, Arial, sans-serif;
    padding: 1em;
    margin: auto;
    max-width: 42em;
    color: #0f0f0f;
    background-color: #EFE8BC;
    margin: 10px 13px 10px 13px;
}

table {
    margin: 10px 0 15px 0;
    border: 1px solid #000;
    background-color: #2f6fab;
    border-collapse: collapse;
}

td, th {
    color: #ffffff;
    padding: 3px 10px;
}

th { padding: 5px 10px; }

a { color: #0069d6; }

a:hover {
    color: #0050a3;
    text-decoration: none;
}

a img { border: none; }

p { margin-bottom: 9px; }

h1, h2, h3, h4, h5, h6 {
    line-height: 36px;
}

h1 { margin-bottom: 18px; font-size: 30px; }

h2 { font-size: 24px; }

h3 { font-size: 18px; }

h4 { font-size: 16px; }

h5 { font-size: 14px; }

h6 { font-size: 13px; }

hr {
    margin: 0 0 19px;
    border: 0;
    border-bottom: 1px solid #ccc;
}

blockquote{
    color:#292525;
    margin:0;
    padding-left: 3em;
    border-left: 0.5em solid #EEE ;
    font-family: "STKaiti", georgia, serif;
}

code, pre {
    font-family: Monaco, Andale Mono, Courier New, monospace;
    font-size: 12px;
}

code {
    background-color: #ffffe0;
    border: 1px solid orange;
    color: rgba(0, 0, 0, 0.75);
    padding: 1px 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    border-radius: 3px;
}

pre {
    display: block;
	background-color: #f8f8f8;    
    border: 1px solid #2f6fab;
    border-radius: 3px;
    overflow: auto;
    padding: 14px;
    white-space: pre-wrap;
    word-wrap: break-word;
}

pre code {
    background-color: inherit;
    border: none;    
    padding: 0;
}

sup {
    font-size: 0.83em;
    vertical-align: super;
    line-height: 0;
}

* {
    -webkit-print-color-adjust: exact;
    color: #0f0f0f;
}

@media screen and (min-width: 914px) {
    body {
        width: 854px;
        margin: 10px auto;
    }
}

@media print {
    body, code, pre code, h1, h2, h3, h4, h5, h6 {
        color: black;
    }
    table, pre {
        page-break-inside: avoid;
    }
}

```