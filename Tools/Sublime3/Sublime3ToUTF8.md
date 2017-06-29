# Sublime3 GBK编码转UTF8插件安装方法
## 安装Package Control
> 想要在Sublime3安装插件需要先安装包管理工具**Package Control**，在Sublime下按下`Ctrl+~`,在弹出的输入框中输入如下安装命令,然后回车安装:

```
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

复制上述命令，注意整体复制。
```
> 如果想为Sublime2安装或者由于版本更新导致上述命令不起作用可访问[**官网帮助文档**](https://packagecontrol.io/installation)获取最新的安装命令。

## 安装ConvertToUTF8插件
> 在Sublime下按`Ctrl+Shift+P`在弹出框中搜索**Install Package**插件并点击安装，之后在弹出框中搜索**ConvertToUTF8**插件并安装，至此Sublime3就会自动转换非UTF8编码的字符了。


## 附： [Sublime3 下载地址](http://www.sublimetext.com/3)
