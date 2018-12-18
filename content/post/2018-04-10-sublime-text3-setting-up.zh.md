---
title: sublime text 3 初始配置
date: '2018-04-10'
tags:
  - "sublime text 3"
slug: sublime-text-3-setting-up
---

ST3插件大大增强了其功能，`Package Control`可以方便的搜索、安装、卸载插件，`` ctrl + ` ``调出控制台，复制下面代码按回车安装。<!--more-->

```python
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' +
'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; 
ipp = sublime.installed_packages_path(); urllib.request.install_opener( 
urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = 
urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', 
'%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating 
download (got %s instead of %s), please try manual install' % (dh, h)) if dh 
!= h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

## 颜色主题

**主题预览**: ST3有许多第三方的主题插件，[Colorsublime](https://github.com/Colorsublime/Colorsublime-Plugin)用于安装和卸载主题，并且提供预览功能。

- `command+shift+p`
- `Select Colorsublime: Install Theme`

**主题切换**:[sublime-text-theme-switcher-menu](https://github.com/chmln/sublime-text-theme-switcher-menu)插件用于快速切换主题（包括颜色主题），不需要手动选择设置主题，`command + ship + p`调出命令面板，选择即可

- `UI: Select Theme`
- `UI: Select Color Scheme`

## Markdown

**功能增强**:[MarkdownEditing](https://github.com/SublimeText-Markdown/MarkdownEditing),提供了语法高亮，颜色主题，自动配对（如`_`和`*`),以及一些其他功能。

**预览**:[MarkdownPreview](https://www.jianshu.com/p/aa30cc25c91b)预览markdown

- `alt + m`：预览
- `command + b`：编译为html


