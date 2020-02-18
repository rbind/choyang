---
title: CentOS 7 R 中安装 hdf5r 包
author: ''
date: '2020-02-18'
slug: centos-7-r-install-hdf5r
categories: []
tags: [R, linux]
---

环境： CentOS 7.7, R 3.6.0

在安装 hdf5r 包的时候，提示需要 hdf5-devel >= 1.8.13，而目前CentOS 7 中 
`yum` 只能安裝1.8.12版本，所以只能手动安装高版本的hdf5.

卸载yum安装旧版本后，从官网下载 hdf5-1.10.5安装

```sh
wget https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.5/src/hdf5-1.10.5.tar.gz
tar xvf hdf5-1.10.5.tar.gz
cd hdf5-1.10.5
./configure --prefix=/usr/local/hdf5
make
make check
sudo make install 
sudo make check-install
```

这时候安装hdf5r的时候提示请安装 hdf5r-devel，然后在
[这](https://github.com/hhoeflin/hdf5r/issues/94#issuecomment-453352921)和
[这](https://github.com/hhoeflin/hdf5r/issues/115#issuecomment-582485446)发现 
hdf5r 的安装依赖 `h5cc`,因为是自己安装的 hdf5，所以需要手动指定 `h5cc` 路径

```r
install.packages("hdf5r", configure.args="--with-hdf5=/usr/local/hdf5/bin/h5cc")
```

结果又出现下面错误：

```
Error: package or namespace load failed for ‘hdf5r’ in dyn.load(file, DLLpath = DLLpath, ...):
unable to load shared object '/home/caoyang/R/x86_64-redhat-linux-gnu-library/3.6/00LOCK-hdf5r/00new/hdf5r/libs/hdf5r.so': libhdf5_hl.so.100: cannot open shared object file: No such file or directory.
```
这表明加载包的时候不能识别 hdf5 的动态库,实际包已经安装好了，只是不能加载 hdf5 
动态库,需要手动配置 hdf5 动态库 libhdf5_hl.so.100，方法参考
[这](https://github.com/hhoeflin/hdf5r/issues/106#issuecomment-461117057)和
[这](https://stackoverflow.com/questions/41494585/setting-ld-library-path-from-inside-r?answertab=active#tab-top)，也就是通过在 `~/.Rprofile` 中添加

```
# echo "dyn.load('/usr/local/hdf5/lib/libhdf5_hl.so.100')" >> ~/.Rprofile 
dyn.load('/usr/local/hdf5/lib/libhdf5_hl.so.100')
```


或者  `~/.Renviron` 文件中设置 `LD_LIBRARY_PATH`为 `/usr/local/hdf5/lib`

```sh
echo LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/hdf5/lib >> ~/.Renviron
```

然后成功加载 `library(hdf5r)`
