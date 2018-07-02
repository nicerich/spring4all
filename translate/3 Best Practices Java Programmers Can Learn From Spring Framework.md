# Java程序员可以从Spring框架中学习的3个最佳实践

> 原文：[3 Best Practices Java Programmers Can Learn From Spring Framework](https://dzone.com/articles/3-best-practices-java-programmers-can-learn-from-s)
>
> 译者： [nicerich](https://github.com/nicerich)
>
> 校对： 


看一看Spring的源代码，你便可以看到设计spring框架的构思。我们从Spring中寻找到一些最佳实践可供Java开发人员学习。

## 导读

毫无疑问，Spring Framework是最流行的Java框架之一，并且通过提供诸如依赖注入和控制反转等特性，使得创建真实的企业级Java应用程序变得非常简单。

但说实话，Spring不仅仅是一个DI和IOC框架。通过提供一个有用的抽象层，它可以进一步简化许多Java的API，例如JDBC，JMS，Java Mail等。用了Spring的JdbcTempalte和其他实用程序类会让JDBC的开发工作变得非常简单。它们消除了Java开发人员在执行SQL语句和处理ResultSets以获取他们想要的Java对象方面所面临的大部分障碍。

所以，当你学习Spring的时候，你不仅可以学会如何使用它，还可以学到一些关于“如何用Java编写更好的代码”和“从整体视角进行面向对象编程”的实用思想。

在本文中，我将分享我在学习Spring时遇到的一些最佳实践，主要来源于阅读Craig Walls经典的《Spring in Action》一书以及我个人对Spring的经验。

这本书对我有特别巨大的影响，因为Craig优秀的写作风格和他在spring中解释每一个概念的方式（都让我学到很多）。如果你还没有阅读，我强烈将其推荐给你 - 这是完全值得你付出时间和金钱去学习的。

说到这，就不再过多浪费你的时间了，我准备了三个我学到的最佳实践给大家，并建议每个Java程序员都要意识到它并在Java编写代码时应用它。



## 1.面向接口编程

这是我在阅读《Head First Design Patterns》时首先学习的一个旧的OOP指南。这种OOP设计原则的主要目的是减少两类之间的耦合，从而提高灵活性。

Spring严格遵循这一面向对象的准则，并经常公开接口给关键类，例如，特意创建JdbcOperation接口用以实现JdbcTemplate（译者：查看源码 public class JdbcTemplate extends JdbcAccessor implements JdbcOperations）。这种做法促进了不同层之间的松散耦合。

另一个很好的例子是一个Cache接口，它被用来提供缓存。所有其他缓存实现（例如EhCache，ConcurrentMapCache和NoOpCache）都实现此接口。

如果您的代码依赖于缓存接口而不是任何特定的实现，则可以切换缓存提供程序而不影响代码的其他部分。

下面是使用Collection框架演示的一个“java中面向接口编程”的简单代码示例。如果仔细观察，在本例中，我使用了一个接口而不是具体实现来声明Java中的变量，参数和返回类型的方法。
```
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;
/**
 * Program to demonstrate coding for interfaces in Java
 * @author WINDOWS 8
 *
 */
public class Hello {
  public static void main(String args[]) {
    // Using interface as variable types
    List<String> rawMessage = Arrays.asList("one", "two", "three");
    List<String> allcaps = toCapitalCase(rawMessage);
    System.out.println(allcaps);
  }
  /**
   * Using Interface as type of argument and return type
   */
  public static List<String> toCapitalCase(List<String> messages) {
    return messages.stream()
                    .map(String::toUpperCase)
                    .collect(Collectors.toList());
  }
}
```

这种编码风格是灵活的，并且在未来更容易改变。


## 2.支持在检查异常之上定义未经检查的异常

如果您使用过Spring Framework，那么您已经注意到Spring支持在已检查的异常之上定义未经检查的异常，最好的例子就是Spring JDBC。

Spring具有丰富的异常层次结构来描述从数据库连接和检索数据时可能会遇到的不同错误，但它们的根源是DataAccessException，而它是未经检查的。

Spring认为大多数错误都源于无法在catch块中纠正的原因，因此它决定让开发人员捕获该异常，而不是像Java那样强制进入它。结果是更干净的代码，没有空的catch块和更少的try-catch块。

这也是在处理Java中的错误和异常时的最佳实践之一。如果您对该主题感兴趣，那么您也可以查看我的《10 Java Exception best practice》以获取更多建议。

> 译者提醒：此段翻译比较拗口，自认为翻译不达标。基于理解进行说明，运行时异常（即未经检查的异常）发生时会自动强制执行整个逻辑工作单元的回滚，Spring的这个特性可以让开发者自定义特定异常并在合适的位置抛出，从而更容易地发现并改正问题。 

## 3.使用模板设计模式

Spring大量使用模板方法设计模式来简化事情。一个很好的例子就是JdbcTemplate，它在使用JDBC API的时候带走了很多痛苦。您只需要定义它需要的内容，Spring会处理剩下的进程。

可能您还不知道，模板模式会定义一个流程或算法，您虽无法更改此流程，但同时您可以根据自己的需求自定义步骤。

例如，在处理JDBC时，可以使用JdbcTemplate执行查询并获取所需的对象。您只需提供SQL，这在每种情况下（的实现）都是不同的，一样需要映射逻辑以将表中的行数据和对象一一对应起来。

这是一个很好的图表，很好地解释了模板模式。你可以看到每个人都有一些共同的任务，但是他们做了不同的工作，并且很好地被Template方法捕获。他们所需要做的就是定义他们的工作，通过自定义实现work（）的抽象方法。

![image](https://github.com/nicerich/spring4all/blob/master/translate/images/Template%20method%20pattern%20in%20Java%20example.png?raw=true)

除了JdbcTemplate之外，您还可以在整个Spring框架的API中找到很多其他的Template Method Pattern示例，例如JmsTemplate和RestTemplate，它们允许您从Java应用程序中使用REST API。

这就是你可以从Spring学到的一些Java最佳实践。Spring是一个很好的框架，他们的作者都是有经验的Java开发人员。通过使用Spring以您可以学到很多东西，还可以查看他们的代码，观察他们做出的决策以及他们是如何设计API的。Spring是开源的，这意味着你可以下载并查看它们的源代码。

我知道Spring是许多这样的最佳实践的集合，还有很多需要学习的东西，但是我发现这三个在Spring中随处可见，这对Spring框架的代码质量产生了巨大的影响。

总之，如果你遇到过从Spring学到的其他最佳实践，请随时与我们分享。




