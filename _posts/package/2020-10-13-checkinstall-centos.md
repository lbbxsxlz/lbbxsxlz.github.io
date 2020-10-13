---
layout: post
title:  "install checkinstall in centos"
comments: true
categories: package
date:   2020-10-13 16:20:54
---

[ref1](https://www.cnblogs.com/moceanliu/p/4933263.html)
[ref2](https://serverfault.com/questions/152704/checkinstall-failed-with-root-rpmbuild-has-no-source-directory)

## 下载checkinstall源码
点击[此处](https://asic-linux.com.mx/~izto/checkinstall/)

## 修改代码编译
```
tar zxvf checkinstall-1.6.2.tar.gz
cd checkinstall-1.6.2.tar.gz
``` 

直接运行make 会出现以下错误
installwatch.c:2942: error: conflicting types for ‘readlink’
/usr/include/unistd.h:828: note: previous declaration of ‘readlink’ was here
installwatch.c:3080: error: conflicting types for ‘scandir’
/usr/include/dirent.h:252: note: previous declaration of ‘scandir’ was here
installwatch.c:3692: error: conflicting types for ‘scandir64’
/usr/include/dirent.h:275: note: previous declaration of ‘scandir64’ was here
make[1]: *** [installwatch.o] Error 1

需要修改installwatch.c的源码，具体如下：

　在第101行：

```
static int (*true_scandir)(    const char *,struct dirent ***,
                 int (*)(const struct dirent *),
                 int (*)(const void *,const void *));
```
　　改成

```
static int (*true_scandir)(    const char *,struct dirent ***,
                 int (*)(const struct dirent *),
                 int (*)(const struct dirent **,const struct dirent **));
```

　　第121行：

```
static int (*true_scandir64)(    const char *,struct dirent64 ***,
                 int (*)(const struct dirent64 *),
                 int (*)(const void *,const void *));
```
　　改成

```
static int (*true_scandir64)(    const char *,struct dirent64 ***,
                 int (*)(const struct dirent64 *),
                 int (*)(const struct dirent64 **,const struct dirent64 **));
```

　　第2941行：

```
#if (GLIBC_MINOR <= 4)
```
　　改成

```
#if (0)
```

　　第3080行：

```
int scandir(    const char *dir,struct dirent ***namelist,
         int (*select)(const struct dirent *),
         int (*compar)(const void *,const void *)    ) {
```
　　改成

```
int scandir(    const char *dir,struct dirent ***namelist,
         int (*select)(const struct dirent *),
         int (*compar)(const struct dirent **,const struct dirent **)    ) {
```

　　第3692行：

```
int scandir64(    const char *dir,struct dirent64 ***namelist,
         int (*select)(const struct dirent64 *),
         int (*compar)(const void *,const void *)    ) {
```
　　改成

```
int scandir64(    const char *dir,struct dirent64 ***namelist,
         int (*select)(const struct dirent64 *),
         int (*compar)(const struct dirent64 **,const struct dirent64 **)    ) {
```

此时可以make通过。

## 修改checkinstall脚本
行495：

```
CHECKINSTALLRC=${CHECKINSTALLRC:-${INSTALLDIR}/checkinstallrc}
```
　　改成

```
CHECKINSTALLRC=${CHECKINSTALLRC:-${INSTALLDIR}/lib/checkinstall/checkinstallrc}
```
　　行2466：

```
$RPMBUILD -bb ${RPM_TARGET_FLAG}${ARCHITECTURE} "$SPEC_PATH" &> ${TMP_DIR}/rpmbuild.log
```
　　改成
```
$RPMBUILD -bb ${RPM_TARGET_FLAG}${ARCHITECTURE} --buildroot $BROOTPATH "$SPEC_PATH" &> ${TMP_DIR}/rpmbuild.log
```
此时即可执行make install

## 修改/usr/local/lib/checkinstall/checkinstallrc文件
```
INSTYPE=""
```
	改成
```
INSTYPE="R"
```

## 修复解决问题中的错误
在checkinstall生成rpm包的过程中，报错内容为：

　　ERROR: ld.so: object '/usr/local/lib64/installwatch.so' from LD_PRELOAD cannot be preloaded: ignored.

通过以下命令解决
```

echo "/usr/local/lib64" >/etc/ld.so.conf.d/installwatch.conf
ln -s /usr/local/lib/installwatch.so /usr/local/lib64/installwatch.so
ldconfig
```

## 验证
下载hello测试包,然后使用checkinstall生成RPM包
```
wget http://ftp.gnu.org/gnu/hello/hello-2.10.tar.gz
tar zxvf hello-2.10.tar.gz
cd hello-2.10;./configure;make
checkinstall -y  --backup=no --install=no --pkgname=Core_zlib --pkgversion=1.0 --pkgrelease=`date +"%Y%m%d%H"`  --pkggroup=IPDGroup --maintainer=li_binbin1@dahuatech.com --provides=Intellif --pakdir .
```

## 错误修复
/root/rpmbuild has no SOURCES directory. Please write the path to
the RPM source directory tree:
用以下命令修复问题

```
mkdir -p /root/rpmbuild/SOURCES
```

至此，用checkinstall生成RPM包圆满成功。
