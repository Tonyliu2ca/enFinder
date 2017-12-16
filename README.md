# enFinder

###历史：
2017-12.15： 更新说明，添加开启SIP的说明。


从macOS 10.13.2版本开始，中文版将Finder翻译为“访达”，就翻译本身来说，还是不错的，但是有些人不太习惯于这个新词语。这个脚本就是用于在Finder和访达之间切换的

# 注意
因为会改变系统完整性保护（SIP）所保护的目录内的文件，所以在运行前，必须先禁止SIP，运行后可以再打开SIP。

# 使用
### 原理
其实原理很简单，就是讲Finder和Dock等等所有有关Finder和访达的文档等都转译一下。
从“访达”到“Finder”的转化，它会搜索访达后，做一个原始备份，然后替换为Finder
从“Finder”转化为“访达”，它只是判断如果原始备份文件存在则恢复原始备份。

# 使用script
传递 “English”，则：从“访达”到“Finder”的转化
传递“Chinese”，则：从“Finder”转化为“访达”

# 声明：
Copyright Tony Liu 2017, All rights reserved
不适合于商业使用
'''源码适用于GPLv3

# 使用build
作为一种方便快捷的实践方式，我们通过用如下的方式来制作一个用户友好的GUI程序，这样方便于普通用户使用。

### 相关技术
为了可以让脚本可以跟GUI交互，我们使用了下面两种技术：
1. 将一个脚本转化为.app程序，虽然我们介绍使用appify（https://gist.github.com/mathiasbynens/674099），其实原理很简单，只不过用它可以简化步骤。
2. 能与脚本交互的GUI程序: Pashua。具体与bash的交互可以看（https://github.com/BlueM/Pashua-Binding-Bash）

### enFinder.app
在这里它的主程序enFinder是一个用于与Pashua和EnglishFinder交流的流程控制程序，同事完成管理员密码验证的工作。
但是李敏不包含pashua的程序部分

### enFinder.dmg
是一个发布版本的dmg文件