---
title: vscode配置
date: 2019-09-05 04:41:29
category: ["工具"]
tags: ["前端工具","vscode"]
comments: true
---

# 插件 #

1. `Beautify`
2. `chinese Language`
3. `open in browser`
4. `Vetur`
5. `minapp`

<!--more-->

# `settings.json` #

```json
{
    "window.zoomLevel": 1,
    "markdown.preview.fontSize": 16,
    "[html]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "[javascript]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "[json]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "editor.wordWrap": "on",
    "files.associations": {
        "*.tpl": "html",
        ".easymockrc": "json"
    },
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    "vetur.format.defaultFormatterOptions": {
        "js-beautify-html": {
            "wrap_attributes": "force-aligned"
        }
    }
}
```


