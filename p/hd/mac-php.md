## macos更换php方案
> macOS自带php的gd库有些问题，当用到imagettftext() 和 freetype 相关功能时会出问题

最近在使用thinphp的时候有需要用到`imagettftext`函数，而mac自带的php不支持此函数。于是想到以下方案来更换macos自带php(nginx+php).

- 关闭apache 
```ssh
  sudo apachectl stop
```
- 关闭mac自带的php-fpm
```ssh
找到/private/etc/php-fpm.conf并注释掉
mv /private/etc/php-fpm.conf /private/etc/php-fpm.conf.bak
```
- 配置nginx
```ssh
安装nginx，并配置nginx
```
- 安装php 
```ssh
浏览器打开 https://php-osx.liip.ch/#install
找到需要下载的版本，我这里安装的是7.1版本
然后在控制台执行shell脚本：curl -s https://php-osx.liip.ch/install.sh | bash -s 7.1
安装完后需要再环境变量中添加。我这里使用的是zshrc,命令如下：
vim ~/.zshrc
export PATH=/usr/local/php5/bin:$PATH
```
-配置php-fpm
```ssh
cd /usr/local/php5/etc
cp php-fpm.conf.default php-fpm.conf
cd /usr/local/php5/etc/php-fpm.d
cp www.conf.default www.conf
需要注意的是www.conf里的listen需要改为127.0.0.1:9000
启动php-fpm
先关闭之前开启的php-fpm
sudo killall php-fpm
再重新启动当前的php-fpm
cd /usr/local/php5/sbin
sudo php-fpm
```
ok,控制台输入php -v,查看到版本已修改
```ssh
PHP 7.1.31 (cli) (built: Aug 11 2019 21:05:57) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.1.31, Copyright (c) 1999-2018, by Zend Technologies
    with Xdebug v2.7.2, Copyright (c) 2002-2019, by Derick Rethans
```
新建一个测试站点，使用`phpinfo()`
```ssh
PHP Version 7.1.31
php-osx.liip.ch by Liip (originally developed by www.local.ch)
```
大功告成~