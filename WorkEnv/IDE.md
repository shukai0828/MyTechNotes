# PHP集成开发环境的安装和配置 #
---

我们统一使用Jetbrains公司的PHPStorm作为集成开发环境，PHPStorm的好处blabla......


## 前置准备 ##
---

1. 预安装配置[PHP基础开发环境][1]
1. 下载[PhpStorm][2]，本教程基于PhpStorm7进行配置

## 安装和配置PHPStorm ##
---

1. 安装PHPStorm软件，使用默认配置即可，打开PhpStrom，通过菜单File->Settings界面按照下列方式进行配置

1. 配置Phing执行路径，Project Settings->Phing，选中已安装的phing脚本：

        C:\xampp\php\phing.bat

    并点击“应用”按钮。

1. 配置Code Sniffer执行路径，Project Settings->PHP->Code Sniffer：

        C:\xampp\php\phpcs.bat

    并点击“应用”按钮。

1. 配置Mess Detector执行路径，Project Settings->PHP->Mes Detector：

        C:\xampp\php\phpmd.bat

    并点击“应用”按钮。

1. 配置Code Sniffer检查的代码风格类型，Project Settings->Inspections->PHP->PHP Code Sniffer validation->Coding standard：

        PEAR

    选择之前需要点击右边的“刷新”按钮，选中后点击“应用”按钮。

1. 配置Mess Detector的检查项，Project Settings->Inspections->PHP->PHP Mess Detector validation->Options，选中如下四个选项：

        Code Size Rules
        Design Rules
        Naming Rules
        Unused Code Rules

2. 去掉拼写检查，解除Project Settings->Inspections->Spelling的选中状态

1. 配置IDE自动检查的Code Style风格为PEAR，Project Settings->Code Style->PHP->Set From...->Predefined Style：

        PEAR

1. 配置部分编辑器特征，Project Settings->Code Style->General

        Line separator (for new files): Unix and OS X '\n' // unix换行符
        Right margin (columns): 120 // 最大行长度标识线
        DO NOT use tab character // 不使用TAB符号
        Tab size: 4
        Indent: 4
        Continuation indext: 8

1. 配置UTF-8编码（根据实际项目决定），Project Settings->File Encodings

        IDE encoding: UTF-8
        Project encoding: UTF-8
        Default encoding for properties file: UTF-8

1. 跟RD项目平台对接，Project Settings->Task->Servers，增加一个Redmine服务：

        Server URL: http://rd.staff.xdf.cn
        Username: zhaoshukai
        Password: ******
        ProjectID: tool
        Use http authentication: checked

## 配置XDebug ##
---

### 本地调试 ###
---

### 远程调试 ###
---



## 开发环境跟持续集成环境的快速对照方式 ##
---

1. 使用IDE的代码检查命令，只能查看代码规范
    1. 在PHPStorm的Inspections中选中PHP Code Sniffer validation，菜单：File->Settings->Inspections->PHP
    1. 执行菜单：Code->Inspect Code，可以看到代码检查的结果

1. 使用Phing自动构建
    1. 在项目目录下创建build目录
    1. 在build目录下创建build.xml，根据需要设定各种构建目标
    1. 将build.xml绑定为Phing文件
    1. 在Phing工具窗口中执行各种构建目标并查看结果



  [1]: DEV.md "PHP基础开发环境的安装"
  [2]: http://www.jetbrains.com/phpstorm/download/ "PhpStorm"