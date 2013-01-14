# 配置开发环境

---
## WNMP环境

---
### 安装NMP

本过程将会安装PHPSys和更换指定版本的PHP，PHPSys包含了memcached、MySQL、nginx、php等常用工具，并提供了便捷的控制界面。

假设安装目录为*c:\wnmp*。

1. [下载](http://www.phpnow.cn/Download.html)PHPSys软件包
1. 解压缩到安装目录
1. 更换默认PHP版本（可选）
    1. [下载](http://www.php.net/downloads.php)希望版本的**压缩包**
    2. 解压缩到PHPSys安装目录，目录名为"php+版本号"，例如*php5.4.9*
    3. 修改安装目录下的config.cmd文件，将php_version的值改成PHP目录名的版本号，比如5.4.9
1. 运行"服务器管理.cmd"控制各种服务

---
### 安装PHP持续集成工具集

推荐统一使用Pear工具进行安装，比较简便易行。

1. 安装[Pear](http://pear.php.net/)
1. 安装[Phing](http://www.phing.info/)
1. 安装[PHPUnit](http://phpunit.de/)
1. 安装[PHP_CodeSniffer](http://pear.php.net/PHP_CodeSniffer)
1. 安装[PHP Copy/Paste Detector](http://github.com/sebastianbergmann/phpcpd)
1. 安装[PHP_Depend](http://pdepend.org/)
1. 安装[PHP Mess Detector](http://phpmd.org/)
1. 安装[phploc](http://github.com/sebastianbergmann/phploc)
1. 安装[PHP_CodeBrowser](https://github.com/Mayflower/PHP_CodeBrowser)

---
### 安装和配置PHPStorm

1. 安装PHPStorm软件
1. 配置Phing执行路径，菜单：File->Settings->Phing，本例中为：C:\wnmp\php5.4.9\phing.bat
1. 配置Code Sniffer执行路径，菜单：File->Settings->PHP->Code Sniffer，本例中为：C:\wnmp\php5.4.9\phpcs.bat
1. 配置Code Sniffer检查的代码风格类型，菜单：File->Settings->Inspections->PHP->PHP Code Sniffer validation->Coding standard = PEAR
1. 其他要求（PHPStorm默认配置已经支持，但要保证不能改动）
    1. 字符编码UTF-8
    1. TAB制表符用四个空格代替
    1. 行尾结束符为\n