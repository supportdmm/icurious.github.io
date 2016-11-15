---
layout: post
category: Info
title: 【OpenCV自学笔记】Day1 如何打开一张图像
date: 2016-11-15 18:00:00.000000000 +08:00
tags: icurious, post
---

>版权声明：本文为 @iCurious
的原创文章，可以转载，但请务必注明作者和出处！！！
原文链接：|[blog.csdn.net/icurious](http://blog.csdn.net/icurious) | [www.blankspace.cn](http://www.blankspace.cn)|[www.cnblogs.com/icurious/](http://www.cnblogs.com/icurious/)|

---

## 摘要
本文主要介绍如何使用OpenCV创建窗口，并打开图像，以原色彩空间和灰度方式显示。
>Talk is cheap, show me the code!


## 正文
在这之前，你必须下载OpenCV，按照自己的电脑系统下载相应的版本。网址：[opencv.org](http://opencv.org)。然后就是在相应的系统环境和IDE下配置OpenCV，实际相当于Java中的导包，使得别人造好的轮子可以为自己所用。关于OpenCV的配置，可以参考其余教程。博主将会在后期[OpenCV自学笔记]Day0 中提供详细而通俗的配置教程，尽请期待。


废话不多说，直接上源码：



```
#include<iostream>
#include<opencv.hpp>
#include<opencv2/opencv.hpp>
using namespace std;
using namespace cv;

int main()
{
       Mat in_image, out_image;
       //读取原始图像
       in_image = imread("｛图片名称｝.{图片格式,如jpg,png等}" , IMREAD_UNCHANGED);
       if (in_image.empty())
       {
             cout << "错误，无法打开图片" ;
        }
       //创建两个具有图像名称的窗口
       const char *SrcTitle = "原图";
       const char *DstTitle = "处理图";

       namedWindow(SrcTitle, WINDOW_AUTOSIZE);
       namedWindow(DstTitle, WINDOW_AUTOSIZE);

       //在创建的窗口中显示图片
       imshow(SrcTitle, in_image);
       cvtColor(in_image, out_image, COLOR_BGR2GRAY);

      imshow(DstTitle, out_image);

      //imwrite(DstTitle,in_image);
      waitKey();
      return 0;
}
```

##效果

![picture](http://img.blog.csdn.net/20161112211120389) 


通过本文我们学会了**imread**函数打开图片。
其更详细的说明如下：

```
CV_EXPORTS_W Mat imread( const String& filename, int flags = IMREAD_COLOR );

/** @brief Loads a multi-page image from a file. (see imread for details.)

@param filename Name of file to be loaded.
@param flags Flag that can take values of @ref cv::ImreadModes, default with IMREAD_ANYCOLOR.
@param mats A vector of Mat objects holding each page, if more than one.
*/
```

flag指读取图像的颜色，并在imgcodecs.hpp头文件中由如下枚举类型定义和解释：

```
//! Imread flags
enum ImreadModes {
       IMREAD_UNCHANGED  = -1, //!< If set, return the loaded image as is (with alpha channel, otherwise it gets cropped).
       IMREAD_GRAYSCALE  = 0,  //!< If set, always convert image to the single channel grayscale image.
       IMREAD_COLOR      = 1,  //!< If set, always convert image to the 3 channel BGR color image.
       IMREAD_ANYDEPTH   = 2,  //!< If set, return 16-bit/32-bit image when the input has the corresponding depth, otherwise convert it to 8-bit.
       IMREAD_ANYCOLOR   = 4,  //!< If set, the image is read in any possible color format.
       IMREAD_LOAD_GDAL  = 8   //!< If set, use the gdal driver for loading the image.
     };

CV_EXPORTS_W void imshow(const String& winname, InputArray mat);

```

更多函数的使用和说明，以及OpenCV图像处理将在后续的文章中介绍。谢谢阅读。


>版权声明：本文为 @iCurious
的原创文章，可以转载，但请务必注明作者和出处！！！
原文链接：|[blog.csdn.net/icurious](http://blog.csdn.net/icurious) | [www.blankspace.cn](http://www.blankspace.cn)|[www.cnblogs.com/icurious/](http://www.cnblogs.com/icurious/)|
