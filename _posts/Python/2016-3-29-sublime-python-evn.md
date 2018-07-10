---
layout: post
title: Sublime Text 3 中搭建 Python 开发环境
categories: Python
description: sublime python 使用
keywords: python,sublime
---

　　在 [Sublime Text 3](https://www.sublimetext.com/3)中配置Python IDE 的时候发现,基于 [REPL](https://github.com/wuub/SublimeREPL) 打开的 Python Console 不能直接在编辑代码时候直接用快捷键直接把代码送入 Console 中进行测试,复制一段代码再粘贴过去很不方便,想要用快捷键完成就得自己动手了。

### 在 sublime 中设置快捷键绑定

* 依次打开 Preferences > Key Bindings-User
* 加入以下代码,其中我设置的快捷键为 `Ctrl+Enter` ,很方便!

```bash
[
{ "keys": ["ctrl+enter"], "command": "repl_transfer_current", "args": {"scope": "lines"}, "context":
[
{ "key": "selector", "operator": "equal", "operand": "source.python", "match_all": true }
]
},
{
"word_wrap": true,
"wrap_width": 80,
}

]
```

### 打开 SublimeREPL 时候出现 environment failed 错误解决

* 错误如下:

```bash
SublimeREPL: obtaining sane environment failed in getenv()
Check console and 'getenv_command' setting 
WARN: Falling back to SublimeText environment
```

* 解决办法依次打开Preferences > Package Settings > SublimeREPL > Settings - User
* 加入下列代码就不会再提示上面的错误了

```bash
{
"getenv_command": false
}

```


### 参考资料

* [SublimeREPL issues](https://github.com/wuub/SublimeREPL/issues/342)
