# 0x01、PC-lint是什么
PC-Lint是一款C/C++软件代码静态分析工具，不仅可以检查一般的语法错误，还可以检查潜在的错误，比如数组访问越界、内存泄漏、使用未初始化变量、使用空指针等。在单元测试前使用PC-Lint来检查代码，可以提前发现程序中的潜在的错误，提高代码的质量。
C/C++的静态检查工具主要有PC-lint、Coverity、Fortify等，后面两种都偏重量级，Coverity还需要提交结果到服务器。PC-lint小巧方便，历史悠久，使用广泛，虽然被诟病为误报率高，但还是一个很有价值，值得随身携带的工具。特别是合理的配置选项减少误报之后，更是可以大幅提高查错、排错的效率。
PC-Lint9出来也老长时间了。
# 0x02、PC-lint安装
PC-Lint官网为http://www.gimpel.com/ ，这货是收费的，需要购买下载。下载后解压后如下图：
<p align="center">
  <img alt="解压图" src="Docs/images/PC-lint/files.png">
</p>
安装时，一路next即可。安装最后会询问是否进行其他配置，暂时不用配置即可！。
PC-Lint等升级稍微麻烦点，需要命令行执行响应的命令。进入官网，http://www.gimpel.com/html/ptch90.htm，可以看到提供的升级包，升级包需要使用官方提供的工具lpatch升级。升级方式如下：
##下载官方的升级包和lpatch工具
<p align="center">
  <img alt="解压图" src="Docs/images/PC-lint/updates_files.png">
</p>
##更新前先查看当前版本
<p align="center">
  <img alt="解压图" src="Docs/images/PC-lint/ver.png">
</p>
将下载的文件放到一个目录中，启动cmd
<p align="center">
  <img alt="解压图" src="Docs/images/PC-lint/updates_setup.png">
</p>
##根据当前版本，执行命令即可（如果是a，就如图执行）
<p align="center">
  <img alt="解压图" src="Docs/images/PC-lint/updates_setup_2.png">
</p>
重复（3）更新所有文件即可！