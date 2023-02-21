# channel_v3_daily

## ■ 用途

使用 Sublime Text 时，有时需要下载插件以丰富编辑器功能，这就需要用到官方组件 `Package Control` （可理解为包管理器，类似apt/dpkg之于Ubuntu/Debian、rpm之于RedHat、yum之于CentOS、pip之于Python、npm之于Node.js），但该组件默认是没有安装的，然而安装需要访问 Sublime Text 官网。然后，即使安装了 `Package Control` 组件，在使用该组件搜索插件时也需要访问 Sublime Text 官网。但国内网络无法访问其官网，那么下载插件也就无从谈起。

本项目借助 Github Actions 从 Sublime Text 官网获取最新 `channel_v3.json`（每天检查1次是否更新）和最新 `Package Control` (每月检查1次是否更新)，然后存放到本仓库，以便于国内网络访问。至于有偶尔访问 Github 也会抽抽，后续可以考虑用国内的 Gitee 定时copy本仓库，以彻底解决访问困难的问题。

## ■ 用法

### ● 安装 Package Control

若已安装则跳过这一步（点击菜单 `Preferences` ，如果下拉菜单中有 `Package Control`则代表已经安装）

#### ○ 在线安装
  
  1. 根据你使用 Sublime Text 的版本复制下面的代码
```python3
# Sublime Text 3
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'https://github.com/HBLong/channel_v3_daily/raw/master/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
```python
# Sublime Text 2
import urllib2,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'https://github.com/HBLong/channel_v3_daily/raw/master/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```
  2. 通过菜单 `View` > `Show Console` 或 快捷键 `Ctrl`+`` ` `` 调出控制台
  3. 在控制台输入框粘贴后按回车键执行
  
#### ○ 离线安装
  
  1. 下载 [Package Control插件压缩包](https://github.com/sdokio/channel_v3_daily/raw/master/Package%20Control.sublime-package) 以备后用
  1. 通过菜单 `Preferences` > `Browse Packages`打开插件文件所在文件夹
  1. 进入目录 `../Installed Packages` ，即先进入父级文件夹，再进入 `Installed Packages` 文件夹
  1. 将第一步所得 `Package Control插件压缩包` 复制到该文件夹
  1. 重启 Sublime Text

### ● 换源

#### ○ 在线源

  1. 通过菜单 `Preferences` > `Package Settings` > `Package Control` > `Settings` 打开自定义配置文件
  1. 添加 `"channels": ["https://raw.githubusercontent.com/sdokio/channel_v3_daily/master/channel_v3.json"],` 后保存即可
```json
{
  "bootstrapped": true,
	"channels":
	[
		"https://raw.githubusercontent.com/sdokio/channel_v3_daily/master/channel_v3.json"
	],
	"in_process_packages":
	[
	],
	"installed_packages":
	[
		"ConvertToUTF8",
		"Package Control"
	]
}
```


#### ○ 离线源（不建议，因为插件信息不会随各插件作者更新而更新）

  1. 下载 [channel_v3.json](https://github.com/sdokio/channel_v3_daily/raw/master/channel_v3.json) 到本地，如 **C:\Users\Administrator\Downloads\channel_v3.json**
  1. 通过菜单 `Preferences` > `Package Settings` > `Package Control` > `Settings` 打开自定义配置文件
  1. 添加 `"channels": ["C:\Users\Administrator\Downloads\channel_v3.json"],` 后保存即可

  完成换源后即可使用快捷键 `Ctrl`+`Shift`+`P` 调用 `Package Control: Install Package` ，然后就可以愉快地搜索/下载插件了。

