第四章 **领域特定语言**

*Domain Specific Languages*

# 1. **DSL**

Camel使用Java 领域特定语言或DSL来创建[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)或各种领域特定语言（DSL）的路由，如下所列。

l [Java DSL** **-](https://camel.apache.org/manual/latest/java-dsl.html) 基于Java的DSL，流畅的构建器风格。

l [Spring XML](https://camel.apache.org/components/latest/spring.html) - Spring XML文件中基于XML的DSL

l Blueprint XML - OSGi Blueprint XML文件中基于XML的DSL

l Rest DSL - 一种使用Java或XML的REST样式定义REST服务的DSL。

l [DSL注解** **-](https://camel.apache.org/manual/latest/bean-integration.html) 在Java bean中使用注解。

l [Kotlin** **DSL](https://github.com/koolio/kool/tree/master/kool-camel) - **进展中的工作** - 目前开发外部ASF中，但在CamelKotlin和DSL准备就绪时我们将稍晚时将其包含在Camel。

DSL的主入口点是

l [CamelContext](https://camel.apache.org/manual/latest/camelcontext.html)，创建Camel路由规则库。

l RouteBuilder，使用路由DSL创建路由集合。

# 2. **Java** **DSL**

Apache Camel使用流畅的构建器风格提供了基于Java的DSL。通过扩展RouteBuilder类并实现configure方法，就可以使用Java DSL 。

通过一个例子来说明。在下面的代码中，我们创建一个MyRouteBuilder类，它扩展了Camel的org.apache.camel.builder.RouteBuilder。

在configure方法中，我们就可以使用Java DSL。

import org.apache.camel.builder.RouteBuilder;

*/** * A Camel Java DSL Router */*

public class MyRouteBuilder extends RouteBuilder {

*/** * Let's configure the Camel routing rules using Java code... */*

public void configure() {

*// here is a sample which processes the input files*

*// (leaving them in place - see the 'noop' flag)*

    *// then performs content based routing on the message using XPath* from("file:src/data?noop=true") 
.choice() .when(xpath("/person/city = 'London'"))

.to("file:target/messages/uk")

.otherwise()

.to("file:target/messages/others");

}

}

在configure方法中，我们可以定义Camel路由。在上面的示例中，我们只有一条路由，即获取文件（例如，from）。

from("file:src/data?noop=true")

然后，我们使用基于内容的路由（例如，choice）来路由消息，具体取决于某人是否来自伦敦。

.choice() .when(xpath("/person/city = 'London'"))

.to("file:target/messages/uk")

.otherwise()

.to("file:target/messages/others");

## 2.1. **ROUTE**

Camel支持使用Java DSL（领域特定语言）定义路由规则，从而避免了使用RouteBuilder来处理繁琐的XML。

例如，可以如下创建一条简单的路由。

RouteBuilder builder = new RouteBuilder() {

public void configure() {

errorHandler(deadLetterChannel("mock:error"));

from("direct:a").to("direct:b");

}

};

从上面可以看到，Camel使用URI将端点和路由连接在一起。

## 2.2. **URI字符串格式**

**自Camel 2.0起可用**

如果您的端点URI能够接受选项，并且希望能够替换该值，例如通过将字符串连接在一起来构建URI，则可以使用java.lang.String.format方法。但在Camel2.0我们在Java DSL新增了两个便捷的方法，所以你可以通过fromF和toF以格式化字符串来构建URI。

from("direct:start").toF("file://%s?fileName=%s", path, name); fromF("file://%s?include=%s", path, pattern).toF("mock:%s", result);

## 2.3. **FILTER**

您可以将简单的路由与过滤器结合使用，这些过滤器可以是任意断言实现。

RouteBuilder builder = new RouteBuilder() {

public void configure() {

errorHandler(deadLetterChannel("mock:error"));

from("direct:a")

.filter(header("foo").isEqualTo("bar"))

.to("direct:b");

}

};

## 2.4. **CHOICE**

通过选择，您可以提供断言和结果的列表以及可选的默认else子句，如果不满足任何条件，则将调用该子句。

RouteBuilder builder = new RouteBuilder() {

public void configure() {

errorHandler(deadLetterChannel("mock:error"));

from("direct:a")

.choice()

.when(header("foo").isEqualTo("bar"))

.to("direct:b")

.when(header("foo").isEqualTo("cheese"))

.to("direct:c")

.otherwise()

.to("direct:d");

}

};

### 2.4.1. **使用自定义****Processor**

这是使用自定义Processor的示例

myProcessor = new** **Processor() {

**    **public void process(Exchange exchange) {

**        **log.debug("Called with exchange: "+ exchange);

**    **}

};

RouteBuilder builder = new** **RouteBuilder() {

**    **public void configure() {

**        **errorHandler(deadLetterChannel("mock:error"));

**        **from("direct:a")

**            **.process(myProcessor);

**    **}

};

您可以将自定义Processor与过滤器filter和选择choice混合并匹配。

RouteBuilder builder = new RouteBuilder() {

public void configure() {

errorHandler(deadLetterChannel("mock:error"));

from("direct:a")

.filter(header("foo").isEqualTo("bar"))

.process(myProcessor);

}

};

# 3. **Spring****支持**

Apache Camel旨在通过多种方式与Spring Framework完美配合。

l Camel使用Spring Transactions作为JMS和JPA等组件中的默认事务处理

l Camel通过XML配置与Spring 2 XML处理一起工作

l Camel Spring XML Schema在Xml引用定义

l Camel支持Spring Remoting的强大版本，它可以在客户端和服务器端之间使用强大的路由，并使用所有可用的组件进行传输

l Camel提供了与Spring ApplicationContext中定义的任何Bean的强大Bean集成。

l Camel与各种Spring助手类集成在一起；例如为Spring Resources提供Type Converter支持等

l 允许Spring依赖注入Component实例或[CamelContext](https://camel.apache.org/manual/latest/camelcontext.html)实例本身，并自动将Spring bean作为组件和端点公开。

l 允许您重用Spring Testing框架，以使用Enterprise Integration Patterns和Camel强大的Mock and Test端点简化单元和集成测试。

l 从Camel 2.15开始:Camel使用camel-spring-boot组件支持Spring Boot。

l 从Camel 2.17.1开始:Camel支持基于Spring Cache的幂等存储库

## 3.1. **使用****Spring****配置****CamelContext**

您可以使用CamelContextFactoryBean在任何spring.xml中配置CamelContext。这将自动启动CamelContext以及所有引用的路由以及所有引用的Component和Endpoint实例。

l 添加Camel schema

l 通过两种方式配置路由:

○ 使用Java代码

○ 使用Spring XML

## 3.2. **添加** **Camel****Schema**

对于Camel 1.x，您需要使用以下名称空间:

http://activemq.apache.org/camel/schema/spring

具有以下schema location:

http://activemq.apache.org/camel/schema/spring/camel-spring.xsd

您需要将Camel添加到schema Location声明中

http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd

因此，XML文件如下所示:

<beans xmlns="http://www.springframework.org/schema/beans"

   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

   xsi:schemaLocation="

   http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd

   http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
## 3.3. **使用****Camel****:命名空间**

或者，您可以在XML声明中引用CamelXSD:

Xmlns:camel ="http://camel.apache.org/schema/spring"

i. 所以声明是:

xsi:schemaLocation ="

http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd

<beans xmlns="http://www.springframework.org/schema/beans"

    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

    xmlns:camel="http://camel.apache.org/schema/spring"

    xsi:schemaLocation="

       http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd

       http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
ii. 然后使用camel:名称空间前缀，您可以省略内联名称空间声明:

<camel:camelContext id ="camel5">

[camel:package](camel:package) org.apache.camel.spring.example </ camel:package>

</ camel:camelContext>

## 3.4. **使用****Spring****进行高级配置**

在使用Spring的CamelContext的高级配置中查看更多详细信息

## 3.5. **使用****Java****代码**

您可以使用Java代码来定义[RouteBuilder](https://camel.apache.org/manual/latest/route-builder.html)实现。可以在Spring定义为Bean类，然后在您的Camel上下文中引用，例如

<camelContext id="camel5" xmlns="http://camel.apache.org/schema/spring">

**  **<routeBuilder ref="myBuilder"/>

</camelContext>

<bean id="myBuilder"class="org.apache.camel.spring.example.test1.MyRouteBuilder"/>

## 3.6. **使用<****package****>**

Camel还提供了强大的功能，可以自动发现和初始化给定程序包中的路由。这是通过在Spring上下文定义中的Camel上下文中添加标签，并指定要递归搜索RouteBuilder实现的软件包来配置的。要在1.X中使用此功能，需要<package> </ package>标记，该标记指定以逗号分隔应搜索软件包列表，例如

<camel:camelContext id="camel5">

**  **[camel:package](camel:package)org.apache.camel.spring.example[/camel:package](/camel:package)

[/camel:camelContext](/camel:camelContext)

在将软件包名称指定为org.apache.camel或该软件包的子软件包时请注意。这会使Camel在其自己的包中搜索可能会导致问题的路由。

**忽略已经实例化的类**

**<package>**和**<packageScan>**会跳过已经被Spring等创建的任何类，因此，如果你定义路由Builder作为一个Spring bean标签则该类将被跳过。您可以使用**<routeBuilder ref="theBeanId"/>**或**<contextScan>**功能包括那些bean 。

## 3.7. **使用 <****packageScan****>**

在Camel 2.0中，已对此进行了扩展，允许使用类似于Ant的路径匹配来选择性地包含和排除已发现的路由类。在Spring，通过添加**<packageScan/>**标签来指定。该标签必须包含一个或多个**package**元素（类似于**1.x**），并可选地包含一个或多个**includes**或**excludes**元素，用来指定类名称的匹配规则。例如，

<camelContext xmlns="http://camel.apache.org/schema/spring">

**  **<packageScan>

**    **<package>org.example.routes</package>

**    **<excludes>**.*Excluded*</excludes>

**    **<includes>**.*</includes>

**  **</packageScan>

</camelContext>

在包含模式之前应用排除模式。如果未定义包含或排除模式，则将返回在包中发现的所有Route类。

在上面的示例中，Camel将扫描所有**org.example.routes**程序包和所有子包中的**RouteBuilder**类。比方说扫描发现两个**RouteBuilders**，包**org.example.routes**下的**MyRoute**被调用，另一个包含**excluded**规则的**MyExcludedRoute**被排除。提取每个类的完全限定名称（如，**org.example.routes.MyRoute**，**org.example.routes.excluded.MyExcludedRoute**），并应用包含和排除模式。

排除模式 *.**Excluded*** 将匹配FQCN **org.example.routes.excluded.MyExcludedRoute**并禁止Camel对其初始化。

在[后](http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/util/AntPathMatcher.html)台，这操作是通过Spring的[AntPatternMatcher](http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/util/AntPathMatcher.html)实现的，其规则为 ？匹配一个字符，* 匹配零个或多个字符，** 匹配零个或多个全限定名称的段

例如:

l *.**Excluded*** 将匹配**org.simple.Excluded**，**org.apache.camel.SomeExcludedRoute**或**org.example.RouteWhichIsExcluded**。

l *.??cluded** 将匹配**org.simple.IncludedRoute**，**org.simple.Excluded**但不匹配**org.simple.PrecludedRoute**。

## 3.8. **使用 ** **c****ontextScan**

**从Camel 2.4开始可用**

您可以允许Camel扫描容器上下文，例如实例化路由构建器的Spring ApplicationContext。这使您可以使用Spring **<component-scan>**功能，并让Camel获取任何由Spring在其扫描过程中创建的**RouteBuilder**实例。

*<!-- enable Spring @Component scan -->*

<context:component-scan base-package="org.apache.camel.spring.issues.contextscan"/>

<camelContext xmlns="http://camel.apache.org/schema/spring">

**    ***<!-- and then let Camel use those @Component scanned route builders -->*

<contextScan/>

</camelContext>

这样，您就可以使用Spring **@Component**注解路由，并让Camel包含这些路由:

@Component

public** **class MyRoute extends SpringRouteBuilder {

** **@Override** **public void configure() throws Exception {

**    **from("direct:start") .to("mock:result");

** **}

}

您还可以使用ANT样式进行包含和排除，如**<packageScan>**文档中上文所述。

如何从其他xml文件导入路由

## 3.9. **测试****期间****排除。**

在测试时，通常希望能够从初始化中选择性地排除不适用于测试场景或不适合测试场景的匹配路由。例如，在Spring上下文文件**routes-context.xml**和**org.example.routes**包中的三个路由构建器**RouteA****，****RouteB**和**RouteC**。**packageScan**定义将发现所有这三个路由并将其初始化。

比方说**RouteC**不适用于我们的测试方案，并且在测试过程中会产生很多噪音。能够从此特定测试中排除此路由将是很好的。在**SpringTestSupport**类已做修改，以允许此场景。它提供了两个方法（**excludedRoute**和**excludedRoutes**），可以重写它们以排除单个类或类的数组。

public** **class RouteAandRouteBOnlyTest extends SpringTestSupport {

**  **@Override

**  **protected Class excludeRoute() {

**    **return** **RouteC.class;

**  **}

}

为了通过spring来钩入**camelContext**初始化来排除**MyExcludedRouteBuilder.class**，我们需要拦截spring上下文的创建。当覆盖的**createApplicationContext**创建spring上下文时，我们调用**getRouteExcludingApplicationContext()**方法来提供一个负责排除工作的特殊父spring上下文。

@Override

protected AbstractXmlApplicationContext createApplicationContext() {

**  **return** **new** **ClassPathXmlApplicationContext(

**    **new** **String[] {"routes-context.xml"}, getRouteExcludingApplicationContext());

}

**RouteC**现在将从初始化中排除。同样，在另一个仅测试**RouteC**的测试中，我们可以通过覆盖排除**RouteB**和**RouteA**:

@Override

protected** **Class[] excludeRoutes() {

** **return** **new** **Class[]{RouteA.class, RouteB.class};

}

## 3.10. **使用****Spring** **XML**

您可以使用Spring 2.0 XML配置方法为[路由](https://camel.apache.org/manual/latest/routes.html)指定XML配置，例如以下[示例](http://svn.apache.org/repos/asf/camel/trunk/components/camel-spring/src/test/resources/org/apache/camel/spring/routingUsingCamelContextFactory.xml)。

<camelContext id="camel-A" xmlns="http://camel.apache.org/schema/spring">

**  **<route>

**    **<from uri="seda:start"/>

**    **<to uri="mock:result"/>

**  **</route>

</camelContext>

配置组件和端点

在Spring XML您可以配置您的组件或[端点](https://camel.apache.org/manual/latest/endpoint.html)实例，如下所示。

<camelContext id="camel"xmlns="http://camel.apache.org/schema/spring">

<jmxAgent id="agent"disabled="true"/>

</camelContext>

<bean id="activemq" class="org.apache.activemq.camel.component.ActiveMQComponent">

**  **<property name="connectionFactory">

**    **<bean class="org.apache.activemq.ActiveMQConnectionFactory">

**      **<property name="brokerURL"value="vm://localhost?broker.persistent=false&broker.useJmx=false"/>

**    **</bean>

**  **</property>

</bean>

它允许您使用某些名称（在上面的示例中的**activemq**）配置组件，然后可以使用**activemq:[queue:|topic:]destinationName**引用该组件。SpringCamelContext可以从Spring上下文中懒惰地获取用于Endpoint URI的方案名称的组件。

有关更多详细信息，请参阅配置端点和组件。

## 3.11. **Spring****缓存幂等存储库**

自**Camel****2.17.1起**可用

<bean id="repo"class="org.apache.camel.spring.processor.idempotent.SpringCacheIdempotentRepository">

**  **<constructor-arg>

**    **<bean class="org.springframework.cache.guava.GuavaCacheManager"/>

**  **</constructor-arg>

** **<constructor-arg value="idempotent"/>

</bean>

<camelContext xmlns="http://camel.apache.org/schema/spring">

** **<route id="idempotent-cache">

**    **<from uri="direct:start"/>

**    **<idempotentConsumer messageIdRepositoryRef="repo"skipDuplicate="true">

**        **<header>MessageId</header>

**        **<to uri="log:org.apache.camel.spring.processor.idempotent?level=INFO&showAll=true&multiline=true"/>** **

**        **<to uri="mock:result"/>

**    **</idempotentConsumer>

** **</route>

</camelContext>

CamelContextAware，如果想在POJO中注入[CamelContext](https://camel.apache.org/manual/latest/camelcontext.html)，只需实现[CamelContextAware接口即可](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/CamelContextAware.html)。然后当Spring创建您的POJO时，CamelContext将被注入到您的POJO中。另请参阅Bean集成以进行进一步的注入。

## 3.12. **集成****测试**

为了避免在使用Spring事务进行测试时出现路由阻塞的情况，请参阅有关Transactional Client下的Spring Integration Testing的注释
