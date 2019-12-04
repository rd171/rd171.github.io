---
layout: post
title:  "ubuntu-在Ubuntu上交叉编译用于ARM板子的fftw3"
date:   2019-12-4 19:00:00 +0200
categories: ubuntu
---
### 1、切换到root账户
```
sudo -i
```
### 2、下载fftw3源码并解压到
http://www.fftw.org/fftw-3.3.8.tar.gz   
### 3、路径切换到FFTW3库源码目录
```
cd /home/kevin/BM/code/fftw-3.3.8
```
### 4、导入ARM板的SDK编译环境
```
. /opt/phytec-yogurt/BSP-Yocto-i.MX6-PD18.1.1/environment-setup-cortexa9hf-neon-phytec-linux-gnueabi
```  
本例使用的phytec公司的cortexa9板子，SDK安装在Ubuntu系统的/opt/phytec-yogurt目录中，所以使用上面的路径。注意：“. /opt/”点号与后面的斜杠有一个空格   
### 5、配置FFTW3库
```
./configure --prefix=/opt/fftw3 --host=arm-linux --enable-shared=yes --enable-double
```
--prefix=/opt/fftw3        指定编译后生成文件的目录   
--host=arm-linux           指定目标系统类型   
--enable-shared=yes        是否生成.so文件   
--enable-double            使用双精度浮点   
### 6、编译
```
make
```
### 7、生成
```
make install
```
至此会在Ubuntu系统的/opt/fftw3目录生成库文件   
### 8、app中引用fftw3库
在xxx.pro文件中增加如下内容：   
```
INCLUDEPATH += /opt/fftw3/include
LIBS        += -L"/opt/fftw3/lib" -lfftw3
```
### 9、将fftw3库文件拷贝到arm板上
将/opt/fftw3/lib/libfftw3.so.3.5.8拷贝到arm板的lib目录，并重命名为libfftw3.so.3
### 10、app中使用fftw3库
```
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include "fftw3.h"
#include <QVector>

MainWindow::MainWindow(QWidget *parent) :
    QMainWindow(parent),
    ui(new Ui::MainWindow)
{
    ui->setupUi(this);

    /*FFT*/
    fftw_complex *in, *out;
    fftw_plan p;
    int N= 8;
    int i;
    in = (fftw_complex*) fftw_malloc(sizeof(fftw_complex) * N);
    out = (fftw_complex*) fftw_malloc(sizeof(fftw_complex) * N);
    for( i=0; i < N; i++)
    {
        in[i][0] = 1.0;
        in[i][1] = 2.0;
    }

    p = fftw_plan_dft_1d(N,in,out, FFTW_FORWARD, FFTW_ESTIMATE);


    fftw_execute(p); /* repeat as needed*/

    fftw_destroy_plan(p);
    fftw_free(in);
    fftw_free(out);
}

MainWindow::~MainWindow()
{
    delete ui;
}
```
