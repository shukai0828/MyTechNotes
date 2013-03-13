# PHP持续集成环境的配置 #
---

## Jenkins安装和配置 ##
---

## PHP工具集的安装和配置 ##
---

工具集安装请参考IDE.md。

特殊配置：
* PHP Mess Dector
  1. 圈复杂度检查从10降到7，修改pear/data/PHP_PMD/resources/rulesets/codesize.xml里CyclomaticComplexity的属性reportLevel值为7
  1. 类方法代码长度从100降到40，修改pear/data/PHP_PMD/resources/rulesets/codesize.xml里ExcessiveMethodLength的属性minimum值为40