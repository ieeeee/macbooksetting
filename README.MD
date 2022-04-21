``` shell
cd /System/Library/CoreServices/SystemFolderLocalizations/zh_CN.lproj 
sudo chmod -R 777 *
open .     # 在文件夹中打开，以便之后操作
```

如果加了sudo命令还是无法给权限请开启Rootless功能，开启方法：

- 重启电脑并按住 cmd + R 键。进入恢复模式。
- 顶部的菜单 栏Utilities > Terminal 打开终端。
- 键入命令 csrutil disable 重启即可。

开启之后再做之前操作。

打开 SystemFolderLocalizations.strings 文件。看内容是否乱码，如果是乱码则为二进制文件，需要下面2步转换，如果不是乱码可以跳过下面两步。

转化二进制文件为JSON或者XML文件(二选一)。 
``` shell
plutil -convert json SystemFolderLocalizations.strings # 转化为JSON文件
plutil -convert xml1 SystemFolderLocalizations.strings # 转化为XML文件
```

然后修改添加自己的英/中文(key-value)。

例如我们新建一个Projects但是要显示中文的“项目”。 
```
{"Desktop": "桌面", ...., "Projects": "项目"}
```

```
...
<key>Desktop</key>
<string>桌面</string>
...
<key>Projects</key>
<string>项目</string>
```

当然，修改完成之后如果原文件是二进制，需要转化回去: 

```
plutil -convert binary1 SystemFolderLocalizations.strings
```

最后，去我们的文件夹下面如例子中的Projects。 

```
cd ......./Projects # cd 到目录Projects下
touch .localized # 新建一个.localized空文件 默认会隐藏
pkill Finder # 重启Finder 
```

然后重启后的finder中就可以看到Projects变成"项目"了。

作者：极乐君
链接：https://juejin.cn/post/6844903466507173902
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。