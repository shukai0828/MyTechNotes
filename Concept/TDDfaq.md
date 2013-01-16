# TDD基本概念和常见问题

---
## What is TDD ?

TDD表示测试驱动开发（Test-Driven Development）。尽管名字里有“测试”二字，但是这个概念其实更倾向与软件设计而不是测试。它并没有替代任何其他测试阶段，比如集成测试、功能测试或者系统测试。TDD可以让开发者交付“可工作的简洁代码”，它依赖自动化、易操作的单元测试环境来执行测试代码。

>TDD stands for Test-Driven Development. Despite the name, it's more about software design than about testing. It does not replace any other test phase, such as integration, functional or system test. It just allows developers to deliver "clean code that works".
TDD relies on automated Unit Tests that allow executing the code in a controlled environment.

TDD是极限编程的基石，不过其并不仅仅适用于极限编程范畴，它可以被任何其他软件工程过程使用，无论这个过程是敏捷的还是非敏捷的。需要注意的是现在极限编程把这个概念命名为“程序员测试”而不是“单元测试”。

>TDD is the cornerstone of eXtreme Programming. However, it is independent from that method and can be used with any other development process, agile or not. Notice that eXtreme Programming now names them Programmer Tests instead of Unit Tests.

---
## The TDD cycle

TDD是一个迭代递增的开发技术，其名字就暗示着在写正式代码前编写测试代码。一次完成一个测试，首先让测试代码运行失败（因为还没有目标正式代码），然后再编写能够让这个测试代码运行通过的正式目标代码。

>TDD is an iterative and incremental development technique ; it implies writing the test code before the production code, one test at a time, verifying that the test fails before writing the code that will make it pass.

失败 -> 成功 -> 重构，这是TDD的三个环节。

    失败：写一个运行失败的测试
    成功：写尽量少的目标代码让这个测试通过
    重构：提升代码的质量，移除重复的代码、确保代码符合程序员的意图

>red - green - refactor. This is the TDD mantra.

>- red: write a test that fails；
>- green - write just enough code to make it pass；
>- refactor - improve the quality of the code: remove duplication and verify the code expresses the programmer intent.

“失败”和“成功”步骤非常重要，因为它们测试了单元测试自身：首先让测试失败，然后使其成功，表明这个单元测试确实测试了某些东西。

>The red and green steps are very important as they allow testing the test: failing the test first and then having a green is an evidence that it's actually testing something.

## TDD terminology（术语）

**单元/Unit**

单元可以代表很多事物，指被测试的对象，可以是函数、方法、类、闭包、函数集等等。
 
>The term unit is voluntary vague. It's the thing (function, method, class, closure, set of functions ...) being tested.

**测试用例/Testcase**

测试目标代码某个行为的测试函数或测试方法。

>Function or method that tests one behavior of the code

**测试套件/Testsuite**

测试用例的集合，一般都用“固件”分组。

>Set of Testcases, typically grouped by fixture.

**固件/Fixture**

一个或多个测试用例的执行环境，固件通常通过setUp()方法产生，通过tearDown()销毁。（固件类似于常说的上下文环境）

>Execution Environment for one or more testcases. Fixtures are usually generated via a setUp() method and destroyed in tearDown().

**断言/Assertion**

用于比较实际值和期望值的方法或者宏。

>Function or macro allowing to compare the expected value against the actual one.

**setUp and tearDown**

setUp()是xUnit中测试用例类（TestCase）的一个方法，可以在你的测试类中被重新定义，用来创建你的测试类需要的执行环境（固件）来运行测试类中的所有测试用例。tearDown()方法恰恰相反，它被用来清除测试用的执行环境。

setUp()和tearDown()分别在每个测试用例之前和之后被调用。

>setUp() is a method of the TestCase class in jUnit that can be redefined in your Test class and used to create the execution environment for all test cases in the class. TearDown() is the opposite of setUp(). It is called to cleanup the test environment.

>setUp() and tearDown() are called before and after every test case.

**重构/Refactoring**

重构表示对源代码进行调整以提升代码的设计，但是不改变它本来的行为。

>Refactoring is a source code manipulation to improving the design of the code, without altering its external behavior.

**模拟对象/Mock object**

一个实现了跟正式代码相同接口的对象，或者是一个正式代码的子类对象，它呈现了可预期的行为。模拟对象被用来替代依赖于昂贵资源（网络、数据库、磁盘等）的对象。

>An object implementing the same interface as, or subclassing a class of the production code, and exhibiting a deterministic behavior. Mock objects can be used to replace objects that rely on expensive resources (network, DB, disks ... )

**红色和绿色进度条/Red bar and green bar**

一般跟IDE关联，现实了测试用例的执行进度，当测试失败时从绿色变成红色。

>This comes from the graphical version of JUnit, where progression bar shows the execution of the tests, and goes from green to red when a test fails .

**测试优先/Test-first**

“测试优先编程”是“测试驱动开发”的另外一个名字，一般用于当设计已经完成、几乎不需要重构的场合。

>Test-First-Programming is another name for Test Driven Development. It could be used when the design has been defined first, and there is almost no refactoring.

---
## xUnit Frameworks

TDD一般都包含在被称为单元测试框架的体系中，框架使单元测试代码的编写和执行变得容易。

每一个编程语言都有自己的xUnit版本，甚至连Unix shell也有，比如[ShUnit](http://shunit.sourceforge.net/)、[shUnit2](http://shunit2.sourceforge.net/)。

Ron Jeffries在XProgramming.com维护了一个[单元测试框架列表](http://www.xprogramming.com/software.htm)，在维基百科上也有[另外一个框架列表](http://en.wikipedia.org/wiki/List_of_unit_testing_frameworks)。

>TDD typically involves using what's called an Unit Test Framework. It just enables easily writing and executing unit tests.

>Every programming language has its xUnit version, even Unix shells, see ShUnit and shUnit2.

>Ron Jeffries maintains a list of frameworks on XProgramming.com, and there is another one on Wikipedia.
</code>

---
## Questions

TDD方面经常被问起的问题。

**测试用例的结构是什么？**

使用3A组合组织你测试用例的结构：Arrange、Act、Assert。

    Arrange: 建立测试类的固件
    Act: 调用你需要测试的函数或方法
    Assert: 用断言验证代码的行为是正确的

你也能使用其他断言确保最后的断言有效。

>**What is the structure of a test ?**

>Structue your tests with the triple 'A': Arrange, Act, Assert.

>- Arrange: establish the fixture for the test class
>- Act: invoke the function (method) you're testing
>- Assert: assert to verify the behavior of the code is correct

>You can also assert before to act to ensure the final assertion was effectively due to the action.

**每个测试用例有多少个断言比较好？**

有些人建议每个测试包含一个断言以使测试更简单：每个测试一个断言。其实这是我们都一致同意的原则的另外一个说法，这个原则是：每个测试只测试一个事情。。

>**How many assertions per testcase ?**

>Some recommends to have one assertion per test to make the tests simpler.
"One Assert per Test" is simply a proxy for a principle we can probably all agree on: "Each test should test one thing".
</code>

**要不要模拟对象？**

如果你自底向上编码，应当能够避免模拟（mock）对象。虽然如此，这些模拟对象应当手写出来或者由构建链的工具创建出来。例如，可以参看[easyMock.org](http://www.easymock.org/)。

参考[mockObjects.com](http://www.mockobjects.com/)关于这方面的介绍和各种语言的实现列表。

参考[mocks aren't stubs](http://martinfowler.com/articles/mocksArentStubs.html)关于模拟和桩(stub)之间差异的讨论。

或参考[Mock Roles, not objects](http://www.mockobjects.com/files/mockrolesnotobjects.pdf)。

>**To mock or not to mock ?**

>If you code bottom-up, then you should be able to avoid mock objects. Nevertheless those can be handwritten, or generated by a tool in the build chain, see, for example, easyMock.org.

>Refer to mockObjects.com for an introduction and a list of implementations in various languages.

>Refer this article by Martin Fowler, mocks aren't stubs, for a discussion differenciating between mocks and stubs.
See also Mock Roles, not objects.

**交互测试 VS 状态测试**

这是TDD的两个风格，交互测试严重依赖于模拟(mock)对象而状态测试基于对象的状态。

>**Interaction testing vs. state testing**

>Those are two styles of TDD, interaction testing heavily relies on mock objects while state testing is based on ... object states.

**我正在提取一个新的类，我应该为它创建新的测试吗？**

该问题已经被争论过多次了，你可以为它写新的测试，但这不是必须的。

共识是既然这个新类已经被初始的类测试过了，你就能安全地提取这个新类而不写测试。然而如果你需要通过其他客户端重用这个新类，你就需要为新客户端的使用添加新的测试。

>**I'm extracting a new class, shall I create new tests for it ?**

>This question was debated several time on the TDD list. You do not have to write new tests for the extracted class, but you can...

>The consensus is that you can safely extract a class without writing new tests since it is already tested thru the initial class. However if you extracted the class to reuse it via another client, then you might want to add new tests targetting the extracted class for your new client class may use it another way.

**我怎样测试private方法？**

有这样几个观点：

1. 不要测试他们，在对public方法进行测试时已经间接测试了private方法
2. 把他们提取成一个新类，然后再参考上面提到的相关建议确定是否进一步测试
3. 把他们变成protected方法，然后测试他们的派生类
4. 根据开发语言或框架而不同，依赖反射或宏对他们进行调用

>**How do I test private methods ?**

>There are several schools here:

>1. Do not test them, there are tested thru the public methods of the class.
>2. Extract them to a new class (and see above)
>2. Make them protected and have your test derived from the class
>2. Depending on your language and frameworks, rely on reflection capability, or on macros to invoke them

**怎么开始测试开发？**

首先就是要写一个测试。

>**Where do I start ?**

>Write a test first ;o)

**从哪里找到好的TDD示例？**

用Java语言写的 [bowling game](http://www.objectmentor.com/resources/articles/xpepisode.htm)演示了一些设计技巧，这些设计理念可以被用到其它语言中。

>**Where can I find a good example of TDD ?**

>The [bowling game](http://www.objectmentor.com/resources/articles/xpepisode.htm) demonstrates emergent design (in Java); it's also available in Haskell, C# ...

**自顶向下还是自底向上？**

自底向上进行TDD需要创建大块的测试内容，而自顶向下可以逐步推进、分而治之。

自顶向下提供了很好的操控性，自底向上更加抽象了。

>**Top-down or bottom-up ?**

>TDDing bottom-up is creating building blocks while top-down is more of a divide-and-conquer strategy.

>Top-down gives control while bottom-up gives abstraction.

**我是否应该测试getter和setter？**

如果你在用TDD进行严格的感知（类似于作为代码质量的监控？存疑），不要添加任何不会失败的测试，这些存取器会被测试覆盖到。而且你并不是在测试你的编程语言本身，因此不必对其进行测试，除非它困扰着你，让你夜不能寐。

>**Should I write tests for my getters and setters ?**

>If you're applying TDD stricto senso, never adding any line of code without a failing test, then all your accessors are covered by tests. Moreover, you're not testing your language, so you do not have to test them. Finally, test them if this is haunting your nights.

**TDD是否打破了OOP的原则，比如“封装”？**

如果你仅仅为了测试需要而把某些方法或属性改成public类型，此时其实预示着应当抽象一个新的类了。你想要暴露出来的方法或属性放到一个独立的类里会更合适，因为这样做符合单一职责原则。原来的类可以把相关职责委托给这个新类在当前类里的private实例。

>**Doesn't TDD break OOP rules, for e.g. encapsulation?**

>When you feel the need to make things public only for testing, the code is telling you to sprout out a new class. The fields or methods that you want to expose will fit better into a separate class, of which they are the primary responsibility; the current class can delegate, then, those responsibilities to a private instance of the new class.

**模式（和反模式）**

介绍几个跟单元测试有关的几个模式：

1. 学习测试：写一个测试来验证或发现一个功能如何运转
1. 红色进度：下班之前，写一个失败的测试，它会在第二天帮助你尽快进入状态
1. 自行分流：测试类也实现被测试类继承的接口，这会使测试类跟被测试方法交互。这个方法是mock对象的一个可选方式。
1. 三角测量：一旦你有至少两个测试的时候就可以开始写实现代码了。
1. 在你真正实现目标代码之前，假装你已经实现他们了
1. 测试隔离：单元测试之间应该是相互隔离的，一个单元测试的结果不应该影响其它单元测试的结果
1. 伪造崩溃：传递一个特殊的对象是测试满足错误条件来抛出异常
1. 清洁提交：在测试还处于失败的情况下不要提交代码，知道你完成了开发和测试

一些[相反的意见](http://blog.james-carr.org/?p=44)和[wiki](http://tdd-antipatterns.net/)

>**Patterns (and anti-patterns)**

>Kent Beck's book (see below) about TDD introduces several patterns related to Unit testing:

>1. Learning test: writing a test to verify, or discover, how a function works.
>1. Red bar: before to leave tour office, write a failing test that will help you restart faster the next day.
>1. Shelf shunt: the test class also implements an interface of the class under test so that the tested method interacts with the test class. This is an alternative to mock objects.
>1. Triangulation: start the implementation once you have at least two tests to guide you.
>1. Fake it 'til you make it
>1. Isolated test: the unit tests shall be isolated so that one test does cannot impact the result of the others.
>1. Crash test dummy: pass a special object that throw exceptions to test for error conditions.
>1. Broken test and Clean check-in: leave a failing test until you are really done. Never check-in when a test is failing.
>1. ...

>A long list of TDD anti-patterns and set up a wiki.

**非敏捷环境的TDD**

即使你公司的软件过程要求你首先进行详细的设计并形成文档，以便在在开始编码前进行评审和确认，你也可以用测试先行的方式利用TDD的优点，也就是说即使有了设计，但在被允许开始编码的时候先进测试。

>**TDD in a non-agile environment**

>Even if your company process mandates you to detail the design in a document that needs to be reviewed and approved before you can start coding, you can take advantage of TDD in the form of Test First Programming. That is once you have your design and are allowed to start coding, do it test first.

**TDD和数据库-如何测试需要访问数据库的代码**

有两种方式，首先mock一个类访问数据库，或者使用tearDown进行数据回滚以便实现“测试隔离”。

>**TDD and databases-How to test-drive code that access a database ?**

>There are two possibilities: first you can mock the classes accessing the DB, or you can use transations to rollback your requests at teardown time to isolate tyour tests.

**TDD和遗产代码**

Michael Feathers定义遗产代码为“没有测试的代码”，参考"Working Effectively with Legacy Code"这本书上跟此类代码打交道的提示和技巧。

>**TDD and legacy code**

>Michael Feathers defines legacy code as "code without tests". Refer to his book "Working Effectively with Legacy Code" for tips and techniques on how to to deal with such code.

**TDD vs. DBB**

BDD可能是下一代的TDD，或者叫“TDD done well”

>**TDD vs. BDD**

>BDD could be nextgen TDD, or "TDD done well".

**测试是否需要被重构？**

是的，测试也是代码。

>**Should the tests be refactored ?**

>Yes, tests are just code.

**我如何测试抽象类**

如果你严格地运用TDD，你的测试应该就已经覆盖了你的抽象类。否则，你可以使用[抽象测试用例](http://c2.com/cgi/wiki?AbstractTestCases)。

>**How do I test an abstract class ?**

>If you applied TDD rigourously, it is already covered by your tests.Otherwise, you can use an [abstract test case](http://c2.com/cgi/wiki?AbstractTestCases).

---
## Rules of thumb

如果一个测试具备如下特征，那么它就不是一个单元测试：

1. 访问数据库
1. 通过网络进行通信
1. 操作文件系统
1. 不能像其它单元测试那样正确运转
1. 你必须对环境做一些特殊配置（比如修改配置文件）才能运行

>A test is not a unit test if:

>     It talks to the database
>     It communicates across the network
>     It touches the file system
>     It can't run correctly at the same time as any of your other unit tests
>     You have to do special things to your environment (such as editing config files) to run it.

能够做如下事情的测试不算坏事，这类测试通常具备一定价值，可以被统一写在同一个单元测试集合里。然而，非常有必要将这些测试跟真正的单元测试隔离开，以便在我们做出改变后能够使用真正的单元测试集合进行快速测试验证。

1. 测试可能会中断的每一个可能
1. 从来不写没有失败测试的代码
1. 为眼前设计，为未来编码
1. DRY
1. 消除任何形式的重复
1. YAGNI：适可而止。不要试图预测代码可能的设计方式，因为你很有可能是错的，添加了不必要的复杂度。

>Tests that do such things aren't bad. Often they are worth writing, and they can be written in a unit test harness. However, it is important to be able to separate them from true unit tests so that we can keep a set of tests that we can run fast whenever we make our changes).

>     Test everything that could possibly break
>     Never write a line of code without a failing test
>     Design for today, code for tomorrow
>     Once And Only Once or DRY - Don't Repeat Yourself
>     Remove any form of duplication
>     YAGNI: You Ain't Gonna Need It. - Do not try to foresee in which direction the code should be designed as you're likely to be wrong, or to add uneeded complexity.

---
## On the negative side

**成本**

TDD难学难用，它的存在导致了跟开发至少对等的代码开发。然而，单元测试代码确实很简单，由它组成的自动化测试组件对保证重构安全提供了保障。

>**On cost**

>TDD is hard to learn and takes a lifetime to master. It produces up to twice as much code as production code. However, unit tests code is much simpler.
But the automatic test suite it creates is a real safety net when it comes to refactoring.

---
## References

Links

    [TDD mailing list](http://groups.yahoo.com/group/testdrivendevelopment/)
    http://www.testdriven.com
    http://www.refactoring.com
    [The way of Testivus](http://pantras.free.fr/articles/testivus.html) ([long version](http://www.agitar.com/downloads/TheWayOfTestivus.pdf)).
    [jUnit FAQ](http://junit.sourceforge.net/doc/faq/faq.htm)

Books

    TDD By Example, Kent Beck, 2002
    Refactoring, Martin Fowler Beck, 1999
    TDD: a practical Guide, Dave Astels, 2003
    Working Effectively with Legacy Code, Michael Feathers, 2004
    Refactoring to Patterns, Joshua Kerievsky, 2004
    xUnit Test Patterns, Gerard Meszaros, 2007
---
## 参考资料

* [Test Driven Development FAQ](http://pantras.free.fr/tddfaq.html)