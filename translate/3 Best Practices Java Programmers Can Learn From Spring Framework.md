# Java程序员可以从Spring框架中学习的3个最佳实践

> 原文：[3 Best Practices Java Programmers Can Learn From Spring Framework](https://dzone.com/articles/3-best-practices-java-programmers-can-learn-from-s)
>
> 译者： [nicerich](https://github.com/nicerich)
>
> 校对： 


看一看Spring的源代码，你便可以看到设计spring框架的构思。我们从Spring中寻找到一些最佳实践可供Java开发人员学习。

## 广告略

毫无疑问，Spring Framework是最流行的Java框架之一，通过提供诸如依赖注入  和  控制反转等特性，创建真实世界的企业级Java应用程序变得非常简单  。

但说实话，Spring不仅仅是另一个DI和IOC框架。通过提供一个有用的抽象层，它可以进一步简化许多Java的API，例如JDBC，JMS，Java Mail等。使用Spring的JdbcTempalte和其他实用程序类使用JDBC更容易。它们消除了Java开发人员在执行SQL语句和处理ResultSets以获取他们想要的Java对象方面所面临的大部分障碍。

所以，当你学习Spring的时候，你不仅学会了如何使用它，还学习了一些关于如何用Java编写更好的代码和一般的面向对象编程的有用见解。

在本文中，我将分享我在学习Spring时遇到的一些最佳实践，主要是阅读Craig Walls 的经典Spring in Action书以及我对Spring的经验。

这本书对我有特别巨大的影响，因为克雷格的优秀写作风格和他在春季解释每一个概念的方式。如果你还没有阅读，我强烈建议 - 这是完全值得你的时间和金钱。

无论如何，在不浪费任何时间的情况下，我已经学习了三个最佳实践，并建议每个Java程序员都要注意并在Java中编写代码时应用它。

> Spring Data REST 也支持 [Spring Data Neo4j](https://spring.io/guides/gs/accessing-neo4j-data-rest), [Spring Data Gemfire](https://spring.io/guides/gs/accessing-gemfire-data-rest) 和 [Spring Data MongoDB](https://spring.io/guides/gs/accessing-mongodb-data-rest) 作为后端存储, 但这些并不是本指南的一部分。

> 运行时异常（即未经检查的异常）会自动强制执行整个逻辑工作单元的回滚。


## 面向接口编程

这是我在阅读Head First Design Patterns时首先学习的一个旧的OOP指南。这种OOP设计原则的主要目的是减少两类之间的耦合，从而提高灵活性。

Spring严格遵循这一面向对象的准则，并经常公开接口以使用关键类，例如，创建JdbcOperation接口以利用JdbcTemplate。这种做法促进了不同层之间的松散耦合。

另一个很好的例子是一个Cache接口，它被用来提供缓存。所有其他缓存实现（例如EhCache，ConcurrentMapCache和NoOpCache）都实现此接口。

如果您的代码依赖于缓存接口而不是任何特定的实现，则可以切换缓存提供程序而不影响代码的其他部分。

下面是使用Collection框架编写Java接口的简单代码示例。如果仔细观察，在本例中，我使用了一个接口而不是实现来声明Java中的变量，参数和返回类型的方法。

导入 java。util。数组 ;
导入 java。util。列表 ;
导入 java。util。流。收藏家 ;
/ **
 *程序演示Java中的接口编码
 * @作者WINDOWS 8
 *
 * /
公开 课 你好 {
  public  static  void  main（String  args []）{
    //使用接口作为变量类型
    列表< String >  rawMessage  =  数组。asList（“one”，“two”，“three”）;
    List < String >  allcaps  =  toCapitalCase（rawMessage）;
    系统。出去。println（allcaps）;
  }
  / **
   *使用接口作为参数类型和返回类型
   * /
  public  static  List < String >  toCapitalCase（List < String >  messages）{
    返回 消息。stream（）
                    。map（String :: toUpperCase）
                    。收集（收藏家。toList（））;
  }
}


这种编码风格是灵活的，并且在未来更容易改变。


## 怎样完成指南？

像大多数 Spring [入门指南](https://spring.io/guides)一样, 你可以从头开始，完成每一步, 或者你也可以绕过你熟悉的基本步骤再开始。 不管通过哪种方式，你最后都会得到一份可执行的代码。

**如果从基础开始**，你可以往下查看[怎样使用 Gradle 构建项目](#scratch)。

**如果已经熟悉跳过一些基本步骤**，你可以：

* [下载](https://github.com/spring-guides/gs-accessing-data-rest/archive/master.zip)并解压源码库，或者通过 [Git](https://spring.io/understanding/Git)克隆：

 `git clone https://github.com/spring-guides/gs-accessing-data-rest.git`
* 进入 `gs-accessing-data-rest/initial`目录
* 跳过前面的部分[创建一个域对象](#initial) 

**当你完成之后**，你可以在`gs-accessing-data-rest/complete`根据代码检查下结果。

<h2 id="scratch"> 使用Gradle构建 </h2>

首先你需要编写基础构建脚本。在构建 Spring 应用的时候，你可以使用任何你喜欢的系统来构建， 这里提供一份你可能需要用 [Gradle](http://gradle.org/) 或者 [Maven](https://maven.apache.org/) 构建的代码。 如果你两者都不是很熟悉, 你可以先去参考[如何使用 Gradle 构建 Java 项目](https://spring.io/guides/gs/gradle)或者[如何使用 Maven 构建 Java 项目](https://spring.io/guides/gs/maven)。

创建以下目录结构

在你的项目根目录，创建如下的子目录结构; 例如，如果你使用的是*nix系统，你可以使用`mkdir -p src/main/java/hello`:

```
└── src
    └── main
        └── java
            └── hello
```

创建Gradle构建文件

下面是一份[初始化Gradle构建文件](https://github.com/spring-guides/gs-accessing-data-rest/blob/master/initial/build.gradle)

`build.gradle`

```
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.5.7.RELEASE")
    }
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'org.springframework.boot'

jar {
    baseName = 'gs-accessing-data-rest'
    version = '0.1.0'
}

repositories {
    mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile("org.springframework.boot:spring-boot-starter-data-rest")
    compile("org.springframework.boot:spring-boot-starter-data-jpa")
    compile("com.h2database:h2")
    testCompile("org.springframework.boot:spring-boot-starter-test")
}
```

[Spring Boot gradle 插件](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-tools/spring-boot-gradle-plugin) 提供了很多非常方便的功能：

* 将 classpath 里面所有用到的 jar 包构建成一个可执行的 JAR 文件，使得运行和发布你的服务变得更加便捷。
* 搜索public static void main()方法并且将它标记为可执行类。
* 提供了将内部依赖的版本都去匹配 Spring Boot 依赖的版本.你可以根据你的需要来重写版本，但是它默认提供给了 Spring Boot 依赖的版本。

## 使用Maven构建

首先，你需要设置一个基本的构建脚本。当使用Spring构建应用程序时，你可以使用任何你喜欢的构建系统，但是使用 [Maven](https://maven.apache.org/) 构建的代码如下所示。如果您不熟悉Maven，请参阅[使用Maven构建Java项目](https://spring.io/guides/gs/maven)。

### 创建目录结构

在你选择的项目目录中，创建以下子目录结构;例如, 在Linux/Unix系统中使用如下命令: `mkdir -p src/main/java/hello`

```
└── src
    └── main
        └── java
            └── hello
```

`pom.xml`

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.springframework</groupId>
    <artifactId>gs-accessing-data-rest</artifactId>
    <version>0.1.0</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.7.RELEASE</version>
    </parent>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-rest</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

    <repositories>
        <repository>
            <id>spring-releases</id>
            <url>https://repo.spring.io/libs-release</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-releases</id>
            <url>https://repo.spring.io/libs-release</url>
        </pluginRepository>
    </pluginRepositories>
</project>
```

[Spring Boot Maven 插件](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-tools/spring-boot-maven-plugin) 提供了很多便捷的特性:

- 它收集类路径上的所有jar包，并构建一个可运行的jar包，这样可以更方便地执行和发布你的服务。
- 它寻找`public static void main()` 方法来将其标记为一个可执行的类。
- 它提供了一个内置的依赖解析器将应用与Spring Boot依赖的版本号进行匹配。你可以修改成任意的版本，但它将默认为Boot所选择了一组版本。

## 使用你的IDE构建

- 阅读如何将本指南直接导入 [Spring Tool Suite](https://spring.io/guides/gs/sts/)。
- 阅读如何使用 [IntelliJ IDEA](https://spring.io/guides/gs/intellij-idea) 来构建。

<h2 id="initial">创建一个域对象</h2>

创建一个新的`Person`域对象。

`src/main/java/hello/Person.java`

```
package hello;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Person {

	@Id
	@GeneratedValue(strategy = GenerationType.AUTO)
	private long id;

	private String firstName;
	private String lastName;

	public String getFirstName() {
		return firstName;
	}

	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}

	public String getLastName() {
		return lastName;
	}

	public void setLastName(String lastName) {
		this.lastName = lastName;
	}
}
```

这个 `Person` 类有一个名和姓属性.还有一个id对象配置为自动生成,所以你不必处理。

## 创建一个 Person 仓库

接下来你需要创建一个简单的仓库。

`src/main/java/hello/PersonRepository.java`

```
package hello;

import java.util.List;

import org.springframework.data.repository.PagingAndSortingRepository;
import org.springframework.data.repository.query.Param;
import org.springframework.data.rest.core.annotation.RepositoryRestResource;

@RepositoryRestResource(collectionResourceRel = "people", path = "people")
public interface PersonRepository extends PagingAndSortingRepository<Person, Long> {

	List<Person> findByLastName(@Param("name") String name);

}
```

这个存储库是一个接口,允许你对`Person`对象执行各种操作。它在 Spring Data Commons中的[PagingAndSortingRepository](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html)扩展这些操作数据共享。

在运行时,Spring Data REST自动创建该接口的一个实现。然后它会使用Spring MVC [@RepositoryRestResource](https://docs.spring.io/spring-data/rest/docs/current/api/org/springframework/data/rest/core/annotation/RepositoryRestResource.html)注释直接创建RESTful端点`/people`。

> @RepositoryRestResource不是存储仓库必需导出的。它仅用于改变导出的细节,例如使用 `/people`而不是默认的 `/people`值。

在这里你也定义了一个定制的查询检索一个‘Person’的对象列表基于lastName。您将进一步在本指南看到如何调用它。

## 使应用可运行

尽管可以将本服务打包为传统的 [WAR](https://spring.io/understanding/WAR) 文件，然后部署在外部的应用程序服务器上，下面展示一种更简便的方法，即创建独立的应用程序。这种方法将本服务打包为单独的、可直接运行的JAR文件，这个jar文件由传统的`main()`函数方法驱动。使用这种打包方法，可以使用Spring提供的嵌入式 [Tomcat](https://spring.io/understanding/Tomcat)  servlet容器作为运行时(HTTP runtime)， 而不是直接部署外部实例中。

`src/main/java/hello/Application.java`

```
package hello;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
}
```

`@SpringBootApplication`作为一个方便使用的注解，提供了如下的功能：

- `@Configuration`表明使用该注解的类是应用程序上下文(Applicaiton Context)中Bean定义的来源。
- `@EnableAutoConfiguration`注解根据classpath的配置、其他bean的定义或者不同的属性设置(property settings)等条件，使Spring Boot自动加入所需的bean。
- 对于Spring MVC应用，通常需要加入`@EnableWebMvc`注解，但是当**spring-webmvc** 存在于classpath中时，Spring Boot自动加入该注解。该注解将当前应用标记为web应用，并激活web应用的关键行为，例如开启`DispatcherServlet`。
- `@ComponentScan`注解使Spring在`hello`包(package)中搜索其他的组件、配置(configurations)和服务(service),在本例中，spring会搜索到控制器(controllers)。

`main()`方法使用Spring Boot的`SpringApplication.run()`方法来加载应用。你有没有注意到本例子中一行XML代码都没有吗？也没有web.xml文件。此web应用100%使纯java代码，因此不需花精力处理任何像基础设施或者下水管道一般的配置工作。

Spring Boot自动加上Spring Data JPA创建`PersonRepository`的具体实现和使用JPA配置它跟后端内存数据库。

Spring Data REST构建于Spring MVC之上。这里是Spring MVC控制器集合，JSON转换器,和其他bean需要提供一个RESTful的前端。这些组件链接到Spring Data JPA的后端。使用Spring Boot将自动配置；如果你想研究这是如何工作的,你可以在Spring Data REST中通过查看`RepositoryRestMvcConfiguration`了解。

### 构建可执行的JAR

您可以在命令行使用Gradle或Maven运行应用程序。或者您可以构建一个可执行的JAR文件,其中包含所有必需的依赖关系,类,和资源,并运行。这使得在整个开发生命周期中非常容易，跨不同的环境，版本等传输和部署服务成为一个应用程序。等等。

如果您使用的是 Gradle，则可以使用该应用程序 `./gradlew bootRun`。或者您可以使用JAR文件构建 `./gradlew build`。然后可以运行 JAR 文件：

```
java -jar build/libs/gs-accessing-data-rest-0.1.0.jar
```

如果您使用 Maven，则可以使用该命令 `./mvnw spring-boot:run`。或者您可以使用 JAR 文件来构建 `./mvnw clean package`。然后可以运行 JAR 文件：:

```
java -jar target/gs-accessing-data-rest-0.1.0.jar
```

> 上面的过程将创建一个可运行的JAR。您也可以选择 [构建一个WAR文件](https://spring.io/guides/gs/convert-jar-to-war/)。

显示记录输出。该服务应该在几秒钟内启动并运行。

## 测试应用程序

现在应用程序正在运行，您可以测试它。你可以使用任何你喜欢的REST客户端。下面使用*nix系统工具`curl`进行测试。

首先你想看到顶级服务。

```
$ curl http://localhost:8080
{
  "_links" : {
    "people" : {
      "href" : "http://localhost:8080/people{?page,size,sort}",
      "templated" : true
    }
  }
}
```

在这里，您可以首先了解此服务器提供的内容。有一个**people**链接位于<http://localhost:8080/people>。它包含了一些比如`?page`, `?size`, 和 `?sort`的选项。

> Spring Data REST 使用 [HAL format](http://stateless.co/hal_specification.html) 提供 JSON 输出。它是灵活的，并提供了一种方便的方式来提供与所提供数据相邻的联系。

```
$ curl http://localhost:8080/people
{
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/people{?page,size,sort}",
      "templated" : true
    },
    "search" : {
      "href" : "http://localhost:8080/people/search"
    }
  },
  "page" : {
    "size" : 20,
    "totalElements" : 0,
    "totalPages" : 0,
    "number" : 0
  }
}
```

目前没有元素，因此没有页面。创建一个新`Person`!

```
$ curl -i -X POST -H "Content-Type:application/json" -d "{  \"firstName\" : \"Frodo\",  \"lastName\" : \"Baggins\" }" http://localhost:8080/people
HTTP/1.1 201 Created
Server: Apache-Coyote/1.1
Location: http://localhost:8080/people/1
Content-Length: 0
Date: Wed, 26 Feb 2014 20:26:55 GMT
```

- `-i` 确保你可以看到响应消息头。这个 URI 指向显示新创建的`Person` 。
- `-X POST` 发信号通知用于创建新条目的POST
- `-H "Content-Type:application/json"` 设置内容类型，以便应用程序知道有效载荷包含一个JSON对象
- `-d "{ \"firstName\" : \"Frodo\", \"lastName\" : \"Baggins\" }"`
  是正在发送的数据。数据中的双引号需要转义为`\“`。

> 注意上一个`POST`操作如何包含一个`Location`头。这包含新创建的资源的URI。 Spring Data REST还有`RepositoryRestConfiguration.setReturnBodyOnCreate（...）`和`setReturnBodyOnUpdate（...）`两个方法，您可以使用它们来配置框架，以立即返回刚创建的资源的表示形式。 `RepositoryRestConfiguration.setReturnBodyForPutAndPost（...）`是一种用于创建和更新表示响应的快捷方法。

从这里您可以查询所有人：

```
$ curl http://localhost:8080/people
{
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/people{?page,size,sort}",
      "templated" : true
    },
    "search" : {
      "href" : "http://localhost:8080/people/search"
    }
  },
  "_embedded" : {
    "persons" : [ {
      "firstName" : "Frodo",
      "lastName" : "Baggins",
      "_links" : {
        "self" : {
          "href" : "http://localhost:8080/people/1"
        }
      }
    } ]
  },
  "page" : {
    "size" : 20,
    "totalElements" : 1,
    "totalPages" : 1,
    "number" : 0
  }
}
```


**persons**对象包含一个包含Frodo的列表。注意它如何包括一个**self**链接。 Spring Data REST还使用[Evo Inflector]（http://www.atteo.org/2011/12/12/Evo-Inflector.html）将分组的实体名称复数化。

您可以直接查询单个记录：

```
$ curl http://localhost:8080/people/1
{
  "firstName" : "Frodo",
  "lastName" : "Baggins",
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/people/1"
    }
  }
}
```

> 这可能看起来纯粹是基于网络的，但在幕后，有一个H2关系数据库。在生产中，您可能会使用一个真正的数据库，像PostgreSQL。

在本指南中，只有一个域对象。使用更复杂的系统，其中域对象彼此相关，Spring Data REST将呈现其他链接，以帮助导航到连接的记录。

查找所有自定义查询

```
$ curl http://localhost:8080/people/search
{
  "_links" : {
    "findByLastName" : {
      "href" : "http://localhost:8080/people/search/findByLastName{?name}",
      "templated" : true
    }
  }
}
```

您可以查看查询的URL，包括HTTP查询参数`name`。如果你注意到，这匹配嵌入在界面中的`@Param（“name”）`注解。

要使用`findByLastName`查询，请执行以下操作：

```
$ curl http://localhost:8080/people/search/findByLastName?name=Baggins
{
  "_embedded" : {
    "persons" : [ {
      "firstName" : "Frodo",
      "lastName" : "Baggins",
      "_links" : {
        "self" : {
          "href" : "http://localhost:8080/people/1"
        }
      }
    } ]
  }
}
```

因为你定义它在代码中返回`List <Person>`，它会返回所有的结果。如果你已经定义了它，只返回`Person`，它会选择一个Person对象返回。由于这可能是不可预测的，您可能不想为返回多个条目的查询执行此操作。

您也可以发出`PUT`，`PATCH`和`DELETE`REST调用来替换，更新或删除现有记录。

```
$ curl -X PUT -H "Content-Type:application/json" -d "{ \"firstName\": \"Bilbo\", \"lastName\": \"Baggins\" }" http://localhost:8080/people/1
$ curl http://localhost:8080/people/1
{
  "firstName" : "Bilbo",
  "lastName" : "Baggins",
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/people/1"
    }
  }
}
```

```
$ curl -X PATCH -H "Content-Type:application/json" -d "{ \"firstName\": \"Bilbo Jr.\" }" http://localhost:8080/people/1
$ curl http://localhost:8080/people/1
{
  "firstName" : "Bilbo Jr.",
  "lastName" : "Baggins",
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/people/1"
    }
  }
}
```

> PUT替换整个记录。未提供的字段将被替换为null。 PATCH可用于更新某一项的子集。

您可以删除记录：

```
$ curl -X DELETE http://localhost:8080/people/1
$ curl http://localhost:8080/people
{
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/people{?page,size,sort}",
      "templated" : true
    },
    "search" : {
      "href" : "http://localhost:8080/people/search"
    }
  },
  "page" : {
    "size" : 20,
    "totalElements" : 0,
    "totalPages" : 0,
    "number" : 0
  }
}
```


这个[接口驱动的hypermedia](https://spring.io/understanding/HATEOAS)一个非常方便的一面是如何使用curl（或您正在使用的任何REST客户端）发现所有RESTful端点。没有必要与客户交换正式的合同或接口文件。

## 总结

恭喜你!您刚刚开发了一个使用[基于hypermedia](https://spring.io/guides/gs/rest-hateoas) 的[RESTful](https://spring.io/understanding/REST)前端和基于JPA的后端应用。


> 本文由spring4all.com翻译小分队创作，采用[知识共享-署名-非商业性使用-相同方式共享 4.0 国际 许可](http://creativecommons.org/licenses/by-nc-sa/4.0/) 协议进行许可。
