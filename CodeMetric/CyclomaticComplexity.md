#圈复杂度 - Cyclomatic Complexity

---

##概念

循环复杂度（Cyclomatic complexity）也称为条件复杂度，是一种软件度量，是由老托马斯·J·麦凯布（英语：Thomas J. McCabe, Sr.）
在1976年提出，用来表示程序的复杂度，其符号为VG或是M。“循环复杂度”的名称有时会让人误解，因为此复杂度不只计算程序中的循环
（循环）个数，也包括条件及分支个数。

---
##算法

圈复杂度(Cyclomatic Complexity)是一种代码复杂度的衡量标准。它可以用来衡量一个模块判定结构的复杂程度，数量上表现为独立现行
路径条数，也可理解为覆盖所有的可能情况最少使用的测试用例数。圈复杂度大说明程序代码的判断逻辑复杂，可能质量低且难于测试和
维护。程序的可能错误和高的圈复杂度有着很大关系。

它的计算方法很简单，计算公式为：V(G)=e-n+2。其中，e表示控制流图中边的数量，n表示控制流图中节点的数量。其实，圈复杂度的计
算还有更直观的方法，因为圈复杂度所反映的是“判定条件”的数量，所以圈复杂度实际上就是等于判定节点的数量再加上1，也即控制流
图的区域数，对应的计算公式为：V(G)=区域数=判定节点数+1。

对于多分支的CASE结构或IF-ELSEIF-ELSE结构，统计判定节点的个数时需要特别注意一点，要求必须统计全部实际的判定节点数，也即每
个ELSEIF语句，以及每个CASE语句，都应该算为一个判定节点。判定节点在模块的控制流图中很容易被识别出来，所以，针对程序的控制
流图计算圈复杂度V(G)时，最好还是采用第一个公式，也即V(G)=e-n+2；而针对模块的控制流图时，可以直接统计判定节点数，这样更为
简单。

---
##意义

* 在缺陷成为缺陷之前 捕获它们。
* 研究显示，平均每人在其大脑中大约能够处理 7（±2）位数字。这就是为什么大多数人可以很容易地记住电话号码，但却很难记住大
于 7 位数字的信用卡号码、发射次序和其他数字序列的原因。
* 过去几年的各种研究已经确定：圈复杂度（或 CC）大于 10 的方法存在很大的出错风险。
* 许多研究发现循环复杂度和缺陷个数有高度的正相关：循环复杂度最高的模组及方法，其中的缺陷个数也最多。
* 圈复杂度是代码复杂度的一个好的指示器；此外，它还是用于开发人员测试的一个极好的衡量器。一个好的经验法则是创建数量与将被
测试代码的圈复杂度值相等的测试用例。
*  在持续集成环境中，可以随时间变化评估方法的复杂度和成长度。如果某一方法的 CC 值在不断增长，那么您有两个响应选择：
	* 确保相关测试的健康情况仍然表现为减少风险。
	* 评估重构方法减少任何长期维护问题的可能性。
*  因为圈复杂度是如此好的一个代码复杂度指示器，所以测试驱动的开发 (test-driven development) 和低 CC 值之间存在着紧密相关
的联系。在编写测试时，开发人员通常倾向于编写不太复杂的代码，因为复杂的代码难以测试。如果您发现自己难以编写某一代码，那么
这是一种警示，表示正在测试的代码可能很复杂。在这些情况下，TDD 的简短的 “代码、测试、代码、测试” 循环将导致重构，而这将
继续驱使非复杂代码的开发。
* 在使用遗留代码库的情况下，测量圈复杂度特别有价值。
* 有助于分布式开发团队监视 CC 值，甚至对具有各种技术级别的大型团队也是如此。确定代码库中类方法的 CC 并连续监视这些值将使
您的团队在复杂问题出现时抢先处理它们。

---
##示例

* 圈复杂度为 2

<pre>
<code>
public String case1(int num) {
    String string = null;

    if (num == 1) {
        string = "String";
    }

    return string.substring(0);
}
</code>
</pre>

* 圈复杂度为 6

<pre>
<code>
public String case2(int index, String string) {
    String returnString = null;
    if (index < 0) {
         throw new IndexOutOfBoundsException("exception <0 ");
    }

    if (index == 1) {
         if (string.length() < 2) {
             return string;
         }

       returnString = "returnString1";
    } else if (index == 2) {
         if (string.length() < 5) {
             return string;
       }
       returnString = "returnString2";
    } else {
         throw new IndexOutOfBoundsException("exception >2 ");
    }

    return returnString;
}
</code>
</pre>

---
##PHPMD

[PHP Mess Detector](http://phpmd.org)是一种代码质量检查工具，支持[5大类31小类](http://phpmd.org/rules/index.html)的质量检查：

1. Code Size Rules
    1. CyclomaticComplexity: Complexity is determined by the number of decision points in a method plus one for the method
    entry. The decision points are 'if', 'while', 'for', and 'case labels'. Generally, 1-4 is low complexity, 5-7 indicates
    moderate complexity, 8-10 is high complexity, and 11+ is very high complexity.
    2. NPathComplexity
    3. ExcessiveMethodLength
    4. ExcessiveClassLength
    5. ExcessiveParameterList
    6. ExcessivePublicCount
    7. TooManyFields
    8. TooManyMethods
    9. ExcessiveClassComplexity
2. Controversial Rules
    1. Superglobals
    2. CamelCaseClassName
    3. CamelCasePropertyName
    4. CamelCaseMethodName
    5. CamelCaseParameterName
    6. CamelCaseVariableName
3. Design Rules
    1. ExitExpression
    2. EvalExpression
    3. GotoStatement
    4. NumberOfChildren
    5. DepthOfInheritance
    6. CouplingBetweenObjects
4. Naming Rules
    1. ShortVariable
    2. LongVariable
    3. ShortMethodName
    4. ConstructorWithNameAsEnclosingClass
    5. ConstantNamingConventions
    6. BooleanGetMethodName
5. Unused Code Rules
    1. UnusedPrivateField
    2. UnusedLocalVariable
    4. UnusedPrivateMethod
    5. UnusedFormalParameter

---
##用重构降低圈复杂度

从[Refactoring](http://refactoring.com/)网站看到的93种重构方式，也可学习《重构：改善既有代码的设计》：

1. Add Parameter
1. Change Bidirectional Association to Unidirectional
1. Change Reference to Value
1. Change Unidirectional Association to Bidirectional
1. Change Value to Reference
1. Collapse Hierarchy
1. Consolidate Conditional Expression
1. Consolidate Duplicate Conditional Fragments
1. Convert Dynamic to Static Construction by Gerard M. Davison
1. Convert Static to Dynamic Construction by Gerard M. Davison
1. Decompose Conditional
1. Duplicate Observed Data
1. Eliminate Inter-Entity Bean Communication (Link Only)
1. Encapsulate Collection
1. Encapsulate Downcast
1. Encapsulate Field
1. Extract Class
1. Extract Interface
1. Extract Method
1. Extract Package by Gerard M. Davison
1. Extract Subclass
1. Extract Superclass
1. Form Template Method
1. Hide Delegate
1. Hide Method
1. Hide presentation tier-specific details from the business tier (Link Only)
1. Inline Class
1. Inline Method
1. Inline Temp
1. Introduce A Controller (Link Only)
1. Introduce Assertion
1. Introduce Business Delegate (Link Only)
1. Introduce Explaining Variable
1. Introduce Foreign Method
1. Introduce Local Extension
1. Introduce Null Object
1. Introduce Parameter Object
1. Introduce Synchronizer Token (Link Only)
1. Localize Disparate Logic (Link Only)
1. Merge Session Beans (Link Only)
1. Move Business Logic to Session (Link Only)
1. Move Class by Gerard M. Davison
1. Move Field
1. Move Method
1. Parameterize Method
1. Preserve Whole Object
1. Pull Up Constructor Body
1. Pull Up Field
1. Pull Up Method
1. Push Down Field
1. Push Down Method
1. Reduce Scope of Variable by Mats Henricson
1. Refactor Architecture by Tiers (Link Only)
1. Remove Assignments to Parameters
1. Remove Control Flag
1. Remove Double Negative by Ashley Frieze and Martin Fowler
1. Remove Middle Man
1. Remove Parameter
1. Remove Setting Method
1. Rename Method
1. Replace Array with Object
1. Replace Assignment with Initialization by Mats Henricson
1. Replace Conditional with Polymorphism
1. Replace Conditional with Visitor by Ivan Mitrovic
1. Replace Constructor with Factory Method
1. Replace Data Value with Object
1. Replace Delegation with Inheritance
1. Replace Error Code with Exception
1. Replace Exception with Test
1. Replace Inheritance with Delegation
1. Replace Iteration with Recursion by Dave Whipp
1. Replace Magic Number with Symbolic Constant
1. Replace Method with Method Object
1. Replace Nested Conditional with Guard Clauses
1. Replace Parameter with Explicit Methods
1. Replace Parameter with Method
1. Replace Record with Data Class
1. Replace Recursion with Iteration by Ivan Mitrovic
1. Replace Static Variable with Parameter by Marian Vittek
1. Replace Subclass with Fields
1. Replace Temp with Query
1. Replace Type Code with Class
1. Replace Type Code with State/Strategy
1. Replace Type Code with Subclasses
1. Reverse Conditional by Bill Murphy and Martin Fowler
1. Self Encapsulate Field
1. Separate Data Access Code (Link Only)
1. Separate Query from Modifier
1. Split Loop by Martin Fowler
1. Split Temporary Variable
1. Substitute Algorithm
1. Use a Connection Pool (Link Only)
1. Wrap entities with session (Link Only)


---
##参考资料

* [追求代码质量: 监视圈复杂度](https://www.ibm.com/developerworks/cn/java/j-cq03316/)
* [循环复杂度](http://zh.wikipedia.org/wiki/%E5%9C%88%E8%A4%87%E9%9B%9C%E5%BA%A6)
* [圈复杂度](http://baike.baidu.com/view/3553594.htm)
* [代码质量-圈复杂度及其计算](http://wobfei.iteye.com/blog/706875)
* [Refactoring](http://refactoring.com/catalog/index.html)
