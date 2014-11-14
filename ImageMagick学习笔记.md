# ImageMagick学习笔记

------
> * 影响文件大小的参数




### 影响文件大小的参数
图片的大小一般由profile和quality来决定。
quality：图片的品质越高图片占用空间越大。
profile：记录图片的一些描述信息。

### 制作gif图片
```shell
convert -delay 50 0.jpg 1.jpg -delay 100 2.jpg 3.jpg 4.jpg dest.gif
```

[1]: http://www.netingcn.com/category/imagemagick
[2]: http://elf8848.iteye.com/blog/382528
[3]: http://stackoverflow.com/questions/15769623/imagemagick-convert-pdf-to-jpeg-has-poor-text-quality-after-upgrading-imagemagic?answertab=active#tab-top
[4]: http://www.zouyesheng.com/imagemagick.html
