# 傻瓜包模式

[一键安装](https://lnmp.org/install.html)

# 分步安装

`PS: 省略Linux部分`
## Nginx安装
1. 首先讲的是比较多centos安装方法如链接[http://www.nginx.cn/install](http://www.nginx.cn/install)所示

其中还有几个相关工具的最新版本链接：
- [pcre](ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/)
- [zlib](http://zlib.net/) [https://nchc.dl.sourceforge.net/project/libpng/zlib/1.2.11/zlib-1.2.11.tar.gz](https://nchc.dl.sourceforge.net/project/libpng/zlib/1.2.11/zlib-1.2.11.tar.gz)或者[http://zlib.net/zlib-1.2.11.tar.gz(US)](http://zlib.net/zlib-1.2.11.tar.gz)
- [openssl](https://www.openssl.org/source/)
- [Nginx](https://nginx.org/en/download.html)建议从`Stable version`寻找你所需要的

2. 第二种当然是‘骚套路’咯(通过repo文件方式)。

#### 截取修改自[https://www.qiansw.com/yum-lnmp.html](https://www.qiansw.com/yum-lnmp.html)，在此表示感谢
### 首先访问[官方文档](https://nginx.org/en/linux_packages.html#stable)获取repo文件
根据文档修改你所需要的内容，如下:由于我的是centos7所以`baseurl=http://nginx.org/packages/OS/OSRELEASE/$basearch/`改成了`baseurl=http://nginx.org/packages/centos/7/$basearch/`,当然你如果是其他系统请根据文档修改链接并进行其他的相关操作
```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```
### 安装
`yum install -y nginx`即可安装稳定版Nginx
### 启动Nginx
`service nginx start`为启动Nginx，`chkconfig nginx on`设置Nginx为开机启动

## 安装MySQL
### yum安装。MySQL可以直接通过yum安装MySQL server
`yum install -y mysql mysql-server`
### 启动服务
`service mysqld start`如果您的MySQL版本已经切换成了mariadb则可以通过`service mariadb start`
### 默认mysql开机启动(自行选择对应的服务)
```
chkconfig mysqld on
chkconfig mariadb on
```

## PHP安装
刚开始直接执行安装`yum install -y php-cli php-fpm`发现版本就5.4的太老旧了所以又找了一下找到了如下更新内容
#### 以下摘自[https://blog.csdn.net/li_lening/article/details/80950014](https://blog.csdn.net/li_lening/article/details/80950014),在此表示感谢
```
yum provides php   #自带的只有5.4版本
rpm -Uvh https://mirror.webtatic.com/yum/el7/epel-release.rpm         #更新源
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
yum remove php-common -y     #移除系统自带的php-common
yum install -y php72w php72w-opcache php72w-xml php72w-mcrypt php72w-gd php72w-devel php72w-mysql php72w-intl php72w-mbstring   #安装依赖包
php -v                    #版本变为7.2
 
yum provides php-fpm      #因为我是准备搭建lnmp，所以安装php-fpm，这里会提示多个安装源，选择7.2版本的安装就可以了
yum install php72w-fpm.x86_64 -y
```

## Nginx更改配置
### 更改默认路径
`vim /etc/nginx/conf.d/default.conf`
修改
```
    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
```
成
```
    location / {
        root   /var/www/html;   #自定义默认路径
        index  index.html index.htm;
    }
```
### 支持php
更改
```
#location ~ \.php$ {
#    root           html;
#    fastcgi_pass   127.0.0.1:9000;
#    fastcgi_index  index.php;
#    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
#    include        fastcgi_params;
#}
```
成
```
location ~ \.php$ {
    root           /var/www/html;   #自定义默认路径
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  /var/www/html$fastcgi_script_name;
    include        fastcgi_params;
}
```
然后执行`nginx -s reload`或者`service nginx reload`