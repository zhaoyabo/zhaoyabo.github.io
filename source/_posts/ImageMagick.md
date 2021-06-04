---
title: ImageMagick
date: 2021-06-04 11:49:51
tags: Image
---

windows 批量压缩图片

<!-- more -->

```
@echo off
for /f "delims=" %%i in ('dir /b /s %1') do (
	"D:\software\ImageMagick-7.0.9-Q16/magick.exe"  %%i -quality 95 %%i.jpg
	echo %%i
	del %%i
)
pause
```

影响图片大小（占用空间）主要取决于图片的profile和quality。

quality：图片的品质，品质越高，占用的空间越大。适当降低品质能很大程度的减少图片的尺寸。一般来说，从品质100降到85，基本上肉眼很难区别其差别，但尺寸上减少很大。imagemagick通过通过 -quality 来设置。

profile：记录图片一些描述信息。例如相机信息（光圈，相机型号）、photoshop元数据，颜色表等信息。它占用的空间可以从几KB到几百KB，甚至可能更大。ImageMagicK可以通过两种方式来去掉这些信息。+profile “*” 　或　-strip


需要注意的是，上面的ImageMagick的安装路径是我本机的路径，如果你需要使用这个脚本，需要将上面的路径该为自己的。这个脚本的执行过程是，首先遍历指定的目录(执行时提供的参数)，然后用ImageMagick优化这个图片，并给这个文件改名，然后删除原文件。

我把这个脚本命名为batch-images-optimize.bat，假设我将所有的图片都放入了my-images目录里，执行的命令是这样的：

```
batch-images-optimize.bat my-images
```


