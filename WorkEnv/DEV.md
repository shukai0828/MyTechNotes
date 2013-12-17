# PHP基础开发环境的安装 #
---

blabla......

我们统一使用开源的一体化基础开发工具包“[XAMPP Portable Lite] [1]”，之所以选择这个也是因为比较可控，不容易出现路径冲突的问题。

XAMPP Portable Lite 1.8.2包含如下组件：

- Apache 2.4.7,
- MySQL 5.5.34
- PHP 5.4.22
- phpMyAdmin 4.0.9
- XAMPP Control Panel 3.1.0

## 前置准备 ##
---

1. 确保系统中安装有“[Microsoft Visual C++ 2008 Redistributable] [2]”运行库，当前XAMPP包中引用的PHP版本需要这个运行库才能正确运转。
2. 删除当前系统下PATH环境变量对原有PHP路径的引用

### 下载和解压 ###
---

要求将XAMPP安装到C盘根目录下：

1. 获取压缩包的两个途径：
    1. 从官方下载XAMPP Portable Lite 1.8.2，（[7z版] [3] [ZIP版] [4]），不要求下载EXE版本，后续安装需要额外配置和安装Pear的其他包。
    2. 从我这里获取已经配置好的压缩包，只需要配置PHP和pear用到的路径即可。

1. 解压缩到C盘根目录下
	
        c:\xampp

1. 检查php.ini的引用路径，确保其加载的php.ini在xampp\php目录下
        C:\xampp\php> php --ini
        Loaded Configuration File:         C:\xampp\php\php.ini

1. 设置当前系统下PATH环境变量对PHP路径的引用：
        C:\xampp\php

如果使用我提供的完整配置包，还需要调整Pear目录配置，执行如下命令
        cd c:\xampp\php
	    pear config-set bin_dir  c:\xampp\php
	    pear config-set doc_dir  c:\xampp\pear\docs
	    pear config-set ext_dir  c:\xampp\php\ext
	    pear config-set php_dir  c:\xampp\php\pear
	    pear config-set cfg_dir  c:\xampp\php\pear\cfg
	    pear config-set data_dir c:\xampp\php\pear\data
	    pear config-set php_bin  c:\xampp\php\php.exe
	    pear config-set php_ini  c:\xampp\php\php.ini
	    pear config-set test_dir c:\xampp\php\pear\tests
	    pear config-set www_dir  c:\xampp\php\pear\www

使用我提供的完整配置包的话，到这里就可以结束了。如果想要自行配置，请继续后面的教程。

### 安装PEAR和其他包 ###
---

完善Pear，为代码检查和持续集成做准备。

XAMPP本身已经预先安装好了部分PEAR包，但其对安装目录的引用形式为“相对路径”，而且还缺部分比较关键的工具。而且如果不对Pear进行重新配置，原先曾经安装过的Pear会对正常使用产生干扰，这个干扰主要表现在IDE执行phing操作时产生各种路径错误。

1. 安装[Pear][10]，下载[go-pear.phar][11]到目录：
        c:\xampp\php

    执行
        C:\xampp\php> php go-pear.phar

        Are you installing a system-wide PEAR or a local copy?
        (system|local) [system] : local //输入local
        Please confirm local copy by typing 'yes' : yes //输入yes
        
        Below is a suggested file layout for your new PEAR installation.  To
        change individual locations, type the number in front of the
        directory.  Type 'all' to change all of them or simply press Enter to
        accept these locations.
        
         1. Installation base ($prefix)                   : C:\xampp\php
         2. Temporary directory for processing            : C:\xampp\php\tmp
         3. Temporary directory for downloads             : C:\xampp\php\tmp
         4. Binaries directory                            : C:\xampp\php
         5. PHP code directory ($php_dir)                 : C:\xampp\php\pear
         6. Documentation directory                       : C:\xampp\php\docs
         7. Data directory                                : C:\xampp\php\data
         8. User-modifiable configuration files directory : C:\xampp\php\cfg
         9. Public Web Files directory                    : C:\xampp\php\www
        10. Tests directory                               : C:\xampp\php\tests
        11. Name of configuration file                    : C:\xampp\php\pear.ini
        12. Path to CLI php.exe                           : C:\xampp\php
        
        1-12, 'all' or Enter to continue: //直接回车

        ...... // 安装过程
        
        Would you like to alter php.ini <C:\xampp\php\php.ini>? [Y/n] : Y //输入Y

        php.ini <C:\xampp\php\php.ini> include_path updated.
        
        Current include path           : .;\xampp\php\PEAR
        Configured directory           : C:\xampp\php\pear
        Currently used php.ini (guess) : C:\xampp\php\php.ini
        Press Enter to continue: //直接回车

    是否还需要执行如下设置路径的操作？存疑。实际案例中曾发现按照上述方式安装go-pear.phar后部分路径仍然没有变成c:\xampp\php下的具体目录的情况。

        cd c:\xampp\php
	    pear config-set bin_dir  c:\xampp\php
	    pear config-set doc_dir  c:\xampp\pear\docs
	    pear config-set ext_dir  c:\xampp\php\ext
	    pear config-set php_dir  c:\xampp\php\pear
	    pear config-set cfg_dir  c:\xampp\php\pear\cfg
	    pear config-set data_dir c:\xampp\php\pear\data
	    pear config-set php_bin  c:\xampp\php\php.exe
	    pear config-set php_ini  c:\xampp\php\php.ini
	    pear config-set test_dir c:\xampp\php\pear\tests
	    pear config-set www_dir  c:\xampp\php\pear\www

1. 调整php.ini中的部分路径，在文件中执行如下替换：
        \xampp\php => c:\xampp\php

1. 清除可能的pear缓存
        C:\xampp\php> pear clear-cache

1. 安装[Phing][12]
        C:\xampp\php> pear channel-discover pear.phing.info
        C:\xampp\php> pear install --alldeps phing/phing
    Phing的安装过程会默认安装它依赖的部分Pear包，其中部分包是我们的持续集成正在使用的：
        install ok: channel://pear.phpunit.de/Version-1.0.1
        install ok: channel://pear.phpunit.de/Git-1.2.0
        install ok: channel://pear.netpirates.net/fDOMDocument-1.4.2
        install ok: channel://pear.phpunit.de/PHP_CodeCoverage-1.2.13
        install ok: channel://pear.phpmd.org/PHP_PMD-1.5.0
        install ok: channel://pear.phpunit.de/PHPUnit_MockObject-1.2.3
        install ok: channel://pear.phpunit.de/PHPUnit-3.7.28

1. 安装[PHP_CodeSniffer][13]-1.4.8版本，首先卸载默认安装的最新版
        C:\xampp\php> pear uninstall PHP_CodeSniffer
    然后执行如下命令：
        C:\xampp\php>pear install PHP_CodeSniffer-1.4.8
        install ok: channel://pear.php.net/PHP_CodeSniffer-1.4.8


1. 安装[PHP Copy/Paste Detector][5]-1.4.3，最新版有问题
        C:\xampp\php> pear config-set auto_discover 1
        C:\xampp\php> pear install pear.phpunit.de/phpcpd-1.4.3

1. 安装[phploc][8]-1.7.4，最新版有问题
        C:\xampp\php> pear config-set auto_discover 1
        C:\xampp\php> pear install pear.phpunit.de/phploc-1.7.4

1. 安装[PHP_CodeBrowser][9]
        C:\xampp\php> pear channel-discover pear.phpqatools.org
        C:\xampp\php> pear install --alldeps phpqatools/PHP_CodeBrowser

1. 运行"xampp-control.exe"控制各种服务

### 特殊配置 ###
---

部分规则进行了改良调整，以符合目前在代码质量上的特殊要求。

* PHP Mess Dector
  1. 圈复杂度检查从10降到7，修改文件第28行：
            C:\xampp\php\pear\data\PHP_PMD\resources\rulesets\codesize.xml
将CyclomaticComplexity的属性reportLevel值调整为7

            <rule name="CyclomaticComplexity" since="0.1" message="">
                <description></description>
                <priority>3</priority>
                <properties>
                    <property name="reportLevel" description="" value="7"/>
                </properties>
            </rule>

  1. 类方法代码长度从100降到40，修改文件第116行：
            C:\xampp\php\pear\data\PHP_PMD\resources\rulesets\codesize.xml
将ExcessiveMethodLength的属性minimum值调整为40
            <rule name="ExcessiveMethodLength" since="0.1" message="">
                <description></description>
                <priority>3</priority>
                <properties>
                    <property name="minimum" description="" value="40"/>
                </properties>
            </rule>

* PHP CodeSniffer
  1. 修改PEAR代码风格默认行长度120，修改文件第15行：
            C:\xampp\php\pear\PHP\CodeSniffer\Standards\PEAR\ruleset.xml
将lineLimit的value值调整为120
             <rule ref="Generic.Files.LineLength">
              <properties>
               <property name="lineLimit" value="120"/>
               <property name="absoluteLineLimit" value="0"/>
              </properties>
             </rule>




[1]: http://www.apachefriends.org/en/xampp-windows.html#646 "XAMPP Portable Lite"
[2]: http://www.microsoft.com/en-us/download/details.aspx?id=5582  "Microsoft Visual C++ 2008 Redistributable"
[3]: http://www.apachefriends.org/download.php?xampp-portable-win32-1.8.2-3-VC9.7z    "XAMPP Portable Lite 1.8.2"
[4]: http://www.apachefriends.org/download.php?xampp-portable-win32-1.8.2-3-VC9.zip    "XAMPP Portable Lite 1.8.2"
[5]: http://github.com/sebastianbergmann/phpcpd "PHP Copy/Paste Detector"
[6]: http://pdepend.org/ "PHP_Depend"
[7]: http://phpmd.org/   "PHP Mess Detector"
[8]: http://github.com/sebastianbergmann/phploc "phploc"
[9]: https://github.com/Mayflower/PHP_CodeBrowser "PHP_CodeBrowser"
[10]: http://pear.php.net/manual/en/installation.getting.php "Getting and installing the PEAR package manager"
[11]: http://pear.php.net/go-pear.phar "go-pear.phar"
[12]: http://www.phing.info/docs/guide/stable/ch03s03.html "Setting-up Phing"
[13]: http://pear.php.net/PHP_CodeSniffer "PHP_CodeSniffer"