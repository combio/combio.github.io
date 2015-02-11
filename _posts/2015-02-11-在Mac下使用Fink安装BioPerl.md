---
layout: post
title: 在Mac下使用Fink安装BioPerl
tags: [生物信息学, bioperl, perl, Fink]
---

在Mac上使用Fink安装bioperl，记录一下步骤。实际上一开始打算直接从源码安装bioperl，但是运行测试的时候总是失败4000多项。虽然bioperl官网说了少量的错误无关紧要，但是这18000多项测试失败了4000多项，应该不能算是少量了吧。好不容易Google到了[blaststation.com](http://www.blaststation.com/freestuff/en/howtoBioPerlMac.html#1010)使用Fink安装的文章。十分感谢他们的工作，在一步步照做后，直接成功了（时间有点长，一下午，不过他们给付费用户提供了编译好的安装包）。

####准备工作

1. 安装Xcode 6.1或更新版本。Xcode可以直接从App Store中免费下载。
2. 安装Xquartz，下载地址[http://xquartz.macosforge.org/landing/](http://xquartz.macosforge.org/landing/)。
3. 安装JDK，下载地址[http://support.apple.com/kb/DL1572](http://support.apple.com/kb/DL1572)。实际上没有安装的，只要在终端运行javac就会自动弹出下载框，Apple在这方面做的真心方便。

####安装步骤

1 . 下载Fink的安装脚本，将它保存为**install.sh**:[https://github.com/fink/scripts/blob/master/srcinstaller/Install%20Fink.tool](https://github.com/fink/scripts/blob/master/srcinstaller/Install%20Fink.tool)
2 . 在终端运行**install.sh**。

```bash
$ sh install.sh
```

整个安装过程非常漫长，并且会问许多问题，千万别运行脚本后就做其它事情去了。对于这些问题，如果不理解的话，直接按回车或者输入`Y`就行了。

3 .使用Fink安装BioPerl。Fink是一个包管理器，它提供了类似于Debian Linux的apt-get管理工具。它主要是用来将Unix或Linux下的一些开源项目移植到Mac下。默认情况下Fink工具被安装在`/sw`目录下。

- 更新fink软件仓库。

```bash
$ /sw/bin/fink update-all
```

- 安装bioperl 5.16.2，系统默认的perl 5.18.2对BioPerl的一些模块不兼容，最好是安装perl 5.16.2（bioperl安装时，自动下载）。

```bash
$ sudo /sw/bin/apt-cache search bioperl-pm5162
$ sudo /sw/bin/apt-get install bioperl-pm5162
```

- 安装完后会有一个`/sw/bin/perl5.16.2`出现，为了方便起见我们可以给它建立一个连接。

```bash
$ sudo ln -s /sw/bin/perl5.16.2 /sw/bin/perl
```

- 编写BioPerl程序并运行（需要重启一下终端），在Perl代码前应该使用下面的说明。

```perl
#!/sw/bin/perl 
```

到这里就可以放心的使用BioPerl了。我也要开始学习BioPerl的使用了，后面的文章会详细记录学习的过程。