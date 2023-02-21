# channel_v3_daily

## 用途

使用 Sublime Text 时，有可能需要下载插件以丰富编辑器功能，就需要安装官方插件 `Package Control` ，然后借助该插件就可以下载所需插件了。但由于国内有时无法访问 Sublime Text 官方网站，而无论是安装官方插件 `Package Control` 还是搜索其它插件都需要访问官方网站，导致无法安装插件。

本项目借助Github Actions从 `https://packagecontrol.io/channel_v3.json` 拉取最新 `channel_v3.json`（每天1次）和最新 `Package Control.sublime-package` (每月1次)，并存到本仓库，以解决 Sublime Text 3 包管理器的默认源无法访问的问题。

## 用法

### 安装 Package Control

若已安装则跳过这一步（点击菜单 `Preferences` ，如果下拉菜单中有 `Package Control`则代表已经安装，否则未安装）

  #### 在线安装
  
  1. 通过菜单 `View` > `Show Console` 或 快捷键 `Ctrl`+`` ` `` 调出控制台
  2. 根据 Sublime Text 版本复制下面的代码
  ```python3
  # Sublime Text 3
  import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'https://github.com/HBLong/channel_v3_daily/raw/master/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
  ```
  
  ```python
  # Sublime Text 2
  import urllib2,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'https://github.com/HBLong/channel_v3_daily/raw/master/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
  ```
  3. 在控制台输入框粘贴后按回车键运行
  
  #### 离线安装
  
  1. 下载 [Package Control插件压缩包](https://github.com/sdokio/channel_v3_daily/raw/master/Package%20Control.sublime-package) 以备后用
  2. 通过菜单 `Preferences` > `Browse Packages`打开插件文件所在文件夹
  3. 进入目录 `../Installed Packages` ，即先进入父级文件夹，再进入 `Installed Packages` 文件夹
  4. 将第一步所得 `Package Control插件压缩包` 复制到该文件夹
  5. 重启 Sublime Text

### 换源

#### 在线使用

1. 通过菜单 `Preferences` > `Package Settings` > `Package Control` > `Settings - User` 打开自定义配置文件
2. 添加 `"channels": ["https://raw.githubusercontent.com/sdokio/channel_v3_daily/master/channel_v3.json"],` 后保存即可

#### 离线使用（不建议，因为此刻之后的插件更新信息需要重新完成以下步骤）

1. 下载 [channel_v3.json](https://github.com/sdokio/channel_v3_daily/raw/master/channel_v3.json) 到本地，如 **C:\Users\Administrator\Downloads\channel_v3.json**
2. 通过菜单 `Preferences` > `Package Settings` > `Package Control` > `Settings - User` 打开自定义配置文件
3. 添加 `"channels": ["C:\Users\Administrator\Downloads\channel_v3.json"],` 后保存即可

完成换源后即可重新尝试唤起 `Package Control: Install Package` 搜索插件了。

