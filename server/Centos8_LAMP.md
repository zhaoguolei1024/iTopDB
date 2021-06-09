服务器版本：Centos8

服务器运维环境：LAMP

PHP版本：7.4.6

Mysql版本：8.0.20

Apache版本：2.4.37

iTop安装包下载地址：https://sourceforge.net/projects/itop/

当前版本：iTop-2.7.0-2-5689.zip

网站域名：xxx.xxx.xxx

外网IP：xxx.xxx.xxx.xxx

内网IP：xxx.xxx.xxx.xxx

服务器配置：16C 32G  500G（有点高，实际上用不上）

![image-20200619185916983](../assets/image-20200619185916983.png)

![image-20200619190007113](../assets/image-20200619190007113.png)

![image-20200619190039158](../assets/image-20200619190039158.png)

![image-20200619190056371](../assets/image-20200619190056371.png)

![image-20200619190115624](../assets/image-20200619190115624.png)

PHP安装LDAP扩展 

```
cd /data/lnmp1.7/src && tar jxvf php-7.4.6.tar.bz2 && cd php-7.4.6/ext
cd ldap
```

```
安装前建议先执行 /usr/local/php/bin/php -m (此命令显示目前已经安装好的PHP模块)看一下，要安装的模块是否已安装。然后下载当前PHP版本的源码并解压。

大部分php扩展/模块的安装就是三个步骤，在源码目录下执行：
/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
有些模块可能会稍微有差异，具体看模块的安装文件就可以。
```

![image-20200619190235750](../assets/image-20200619190235750.png)

```
yum install openldap

yum install openldap-devel
```

![image-20200619190300113](../assets/image-20200619190300113.png)

```
cp -frp /usr/lib64/libldap* /usr/lib/
```

![image-20200619190323695](../assets/image-20200619190323695.png)

![image-20200619190339303](../assets/image-20200619190339303.png)

```
lnmp restart
```

![image-20200619190403138](../assets/image-20200619190403138.png)

![image-20200619190416638](../assets/image-20200619190416638.png)

![image-20200619190432884](../assets/image-20200619190432884.png)

![image-20200619190444019](../assets/image-20200619190444019.png)

![image-20200619190458750](../assets/image-20200619190458750.png)

![image-20200619190538169](../assets/image-20200619190538169.png)

![image-20200619190606552](../assets/image-20200619190606552.png)

![image-20200619190614164](../assets/image-20200619190614164.png)

![image-20200619190628337](../assets/image-20200619190628337.png)

![image-20200619190641045](../assets/image-20200619190641045.png)

![image-20200619190721677](../assets/image-20200619190721677.png)

![image-20200619190759402](../assets/image-20200619190759402.png)

![image-20200619190909946](../assets/image-20200619190909946.png)

![image-20200619191153574](../assets/image-20200619191153574.png)

```
yum install -y graphviz
```

![image-20200619191217223](../assets/image-20200619191217223.png)

![image-20200619191230334](../assets/image-20200619191230334.png)

![image-20200619191240360](../assets/image-20200619191240360.png)

![image-20200619191542191](../assets/image-20200619191542191.png)

![image-20200619191600271](../assets/image-20200619191600271.png)

![image-20200619191608974](../assets/image-20200619191608974.png)

![image-20200619191624113](../assets/image-20200619191624113.png)

![image-20200619191646547](../assets/image-20200619191646547.png)

![image-20200619191701013](../assets/image-20200619191701013.png)

![image-20200619191712794](../assets/image-20200619191712794.png)

![image-20200619191729509](../assets/image-20200619191729509.png)