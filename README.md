# enFinder

从macOS 10.13.2版本开始，中文版将Finder翻译为“访达”，就翻译本身来说，还是不错的，但是有些人不太习惯于这个新词语。这个脚本就是用于在Finder和访达之间切换的

# 注意
因为会改变系统完整性保护（SIP）所保护的目录内的文件，所以在运行前，必须先禁止SIP，运行后可以再打开SIP。

# 使用
##原理
其实原理很简单，就是讲Finder和Dock等等所有有关Finder和访达的文档等都转译一下。
从“访达”到“Finder”的转化，它会搜索访达后，做一个原始备份，然后替换为Finder
从“Finder”转化为“访达”，它只是判断如果原始备份文件存在则恢复原始备份。

##使用script
传递 “English”，则：从“访达”到“Finder”的转化
传递“Chinese”，则：从“Finder”转化为“访达”

# 声明：
Copyright Tony Liu 2017, All rights reserved
不适合于商业使用
源码适用于GPLv3
