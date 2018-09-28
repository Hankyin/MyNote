[TOC]

# 概论

颜色由红绿蓝三色合成

颜色深度：每个像素所占的二进制位数，颜色深度越大所能表示的颜色数目越多。



# 图像存储格式

## 黑白图像

二值图像，1位

灰度图像：8位

## 8位索引图像

除了图像，还有一个颜色的索引表。

图片中的像素值对应颜色索引表中一个具体的rgb值，最多256色

当索引表中的rgb分量相等时，就会形成灰度图像。

## 真彩色

真彩色的颜色深度是24位，rgb三通道各用一个字节

# BMP格式

1. 位图文件头BITMAPFILEHEADER

   含有BMP文件类型，文件大小和位图起始位置

   ```c
   typedef struct tagBITMAPFILEHEADER
   {
       WORD bfType;//位图文件的类型，必须为BM(1-2字节）
       DWORD bfSize;//位图文件的大小，以字节为单位（3-6字节，低位在前）
       WORD bfReserved1;//位图文件保留字，必须为0(7-8字节）
       WORD bfReserved2;//位图文件保留字，必须为0(9-10字节）
       DWORD bfOffBits;//位图数据的起始位置，以相对于位图（11-14字节，低位在前）
       //文件头的偏移量表示，以字节为单位
   }__attribute__((packed)) BITMAPFILEHEADER;
   ```

2. 位图信息头BITMAPINFOHEADER

   BMP位图信息头数据用于说明位图的尺寸等信息。

   ```c
   typedef struct tagBITMAPINFOHEADER{
   DWORD biSize;//本结构所占用字节数（15-18字节）
   LONG biWidth;//位图的宽度，以像素为单位（19-22字节）
   LONG biHeight;//位图的高度，以像素为单位（23-26字节）
   WORD biPlanes;//目标设备的级别，必须为1(27-28字节）
   WORD biBitCount;//每个像素所需的位数，必须是1（双色），（29-30字节）
   //4(16色），8(256色）16(高彩色)或24（真彩色）之一
   DWORD biCompression;//位图压缩类型，必须是0（不压缩），（31-34字节）
   //1(BI_RLE8压缩类型）或2(BI_RLE4压缩类型）之一
   DWORD biSizeImage;//位图的大小(其中包含了为了补齐行数是4的倍数而添加的空字节)，以字节为单位（35-38字节）
   LONG biXPelsPerMeter;//位图水平分辨率，每米像素数（39-42字节）
   LONG biYPelsPerMeter;//位图垂直分辨率，每米像素数（43-46字节)
   DWORD biClrUsed;//位图实际使用的颜色表中的颜色数（47-50字节）
   DWORD biClrImportant;//位图显示过程中重要的颜色数（51-54字节）
   }__attribute__((packed)) BITMAPINFOHEADER;
   ```

3. 位图颜色表RGBQUAD

   颜色表用于说明位图中的颜色，它有若干个表项，每一个表项是一个RGBQUAD类型的结构，定义一种颜色。

   ```c
   typedef struct tagRGBQUAD{
   BYTE rgbBlue;//蓝色的亮度（值范围为0-255)
   BYTE rgbGreen;//绿色的亮度（值范围为0-255)
   BYTE rgbRed;//红色的亮度（值范围为0-255)
   BYTE rgbReserved;//保留，必须为0
   }__attribute__((packed)) RGBQUAD;
   ```

# 图像处理编程基础

常用图像处理工具

opencv，cximage，matlab，cimg, freeimage,halcon,

开源项目

openbr 开源人脸识别,easypr开源车牌识别



## 图像的显示

扫描显示，

渐显渐隐，将rgb值除以一个数可以让图片变淡。

马赛克显示，将图片分割成小块，然后随机显示小块

