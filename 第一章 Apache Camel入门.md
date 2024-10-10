# **Apache Camel****入门**

# 1. **入门介绍**

首先，您需要下载Camel发布版; 或者您可以用源代码自己构建发布版。

然后回到这里，您可能希望在继续之前阅读以下文档:

l 了解更多的入门指南。

l 了解[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)以及如何用Camel实现它们。

l 查看Architecture架构指南，了解如何使用Java DSL或基于Spring的[Xml配置](https://camel.apache.org/manual/latest/xml-configuration.html)构建路由（route）。

## 1.1. **使用****CamelContext****和****RouteBuilder**

开始使用Camel的大致步骤:

1. 创建CamelContext。
2. [配置组件（component）或](https://camel.apache.org/manual/latest/configuring-camel.html)端点（endpoint），二选一即可。
3. 使用DSL和RouteBuilder或XML配置添加你希望的任意route规则。
4. 启动上下文。

当您的应用程序关闭时，您可能希望停止上下文。

当你准备好以后，为什么不[执行一个例子](https://camel.apache.org/manual/latest/walk-through-an-example.html)呢？（本文档附录1也同时提供）。

然后继续下一步执行[另一个例子](https://camel.apache.org/manual/latest/walk-through-another-example.html)，（本文档附录3也同时提供）。

然后开始去看教程。

## 1.2. **使用****Spring**

如果您使用Spring作为依赖注入容器，请参阅Camel Spring文档。

## 1.3. **其他资源**

我们强烈建议您冲一杯咖啡或茶，花30分钟阅读以下资源:

l 《Camel in Action》[第1章（相关链接）](http://manning.com/ibsen/chapter1sample.pdf)免费，。强烈建议阅读以了解Camel是做什么的以及Camel基本的概念。这是一个免费章节，您可以直接下载为pdf（约20页）。经验告诉我们Camel最终用户，在他们开始学习Camel时非常需要阅读这一章。

l Jonathan Anstey编写的《[Fuse IDE如何帮助](http://java.dzone.com/articles/open-source-integration-apache)[Apache Camel的开源集成](http://java.dzone.com/articles/open-source-integration-apache)》 。更新了关于Apache Camel[:Integration Nirvana](http://architects.dzone.com/articles/apache-camel-integration)的文章。了解Camel很好的文章，，并有一个很好的示例。

l Camel产品页面上的一些商业供应商也提供各种教程，网络研讨会，示例等。这可能有用。

l 本文章是一个链接集合，包含文章，博客，播客，演示文稿以及来自社区的人们对Camel的热文。

# 2. **Apache Camel入门**

## 2.1. **企业集成模式（EIP）的书**

设计模式方面的书的编写目的不是提倡作者发明新的技术，而是要记录特定领域内现有的最佳实践。通过这样做，设计模式书的作者希望传播最佳实践的知识并促进讨论架构设计的词汇。

最著名的模式书籍之一是Erich Gamma，Richard Helm，Ralph Johnson和John Vlissides的《[设计模式:可重复使用的面向对象软件](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)的[元素](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612)》，俗称["四人帮"（GoF）](http://en.wikipedia.org/wiki/Design_Patterns)一书。自设计模式出版以来，已经编写了许多其他质量不同的模式书籍。一本著名的模式书被称为《企业集成模式[:](http://www.amazon.com/Enterprise-Integration-Patterns-Designing-Deploying/dp/0321200683)[设计，构建和部署消息传递解决方案](http://www.amazon.com/Enterprise-Integration-Patterns-Designing-Deploying/dp/0321200683)》（《[Enterprise Integration Patterns: Designing, Building, and Deploying Messaging Solutions](http://www.amazon.com/Enterprise-Integration-Patterns-Designing-Deploying/dp/0321200683)》） 由Gregor Hohpe和Bobby Woolf编写。常见的，人们通过其首字母 EIP来称呼这本书。正如EIP的副标题所暗示的那样，本书侧重于异步消息传递系统的设计模式。这本书讨论了65种模式。每个模式都有一个书面名称，大多数也有一个图形符号，用于架构图中。

## 2.2. **Camel****项目**

Camel（[http://camel.apache.org](http://camel.apache.org/)）是一个基于Java的开源项目，可帮助用户实现EIP手册中的许多设计模式。由于Camel实现了许多在EIP书中的设计模式，因此对于使用Camel的人来说，将EIP书作为参考是一个好主意。

## 2.3. **Camel****的在线文档**

该文档全部位于Camel网站右侧菜单的Documentation类别下（也以[PDF格式提供](http://camel.apache.org/manual.html)）。还提供与Camel相关的书籍，特别是《[Camel in Action](http://manning.com/ibsen)》，目前作为Camel圣经 - 它有一个[免费的第一章（pdf）](http://www.manning.com/ibsen/chapter1sample.pdf)，强烈建议阅读以更熟悉Camel。

### 2.3.1. **浏览在线文档的有用提示**

Camel在线文档顶部的面包屑可以帮助您在父和子目录之间导航。

例如，如果您在"Languages"文档页面上，则淡红色条的左侧包含以下链接。

Apache Camel > Documentation > Architecture > Languages

正如您所料，单击"Apache Camel"会将您带回Apache Camel的主页，然后单击"Documentation"将您带到文档页主面。您可以将"Architecture"和"Languages"按钮理解为表示您位于"Architecture"一章的"Languages"部分。将页面添加到浏览器书签也可以节省时间。

## 2.4. **在线****Javadoc****文档**

Apache Camel网站提供了 [Javadoc documentation](http://camel.apache.org/maven/current/camel-core/apidocs/index.html)。值得注意的是，Javadoc文档分布在几个独立的 Javadoc层次结构中，而不是全部包含在单个Javadoc层次结构中。特别是，Camel 的核心 API 有一个Javadoc层次结构，Camel支持的每个组件技术都有一个单独的Javadoc层次结构。例如，如果您将Camel与ActiveMQ和FTP一起使用，那么您需要查看[core API](http://camel.apache.org/maven/current/camel-core/apidocs/index.html) 和[Spring API](http://camel.apache.org/maven/current/camel-spring/apidocs/index.html)的Javadoc层次结构。

## 2.5. **Camel****的基本概念和术语**

在本节中，将解释一些对Camel至关重要的概念和术语。本节并不是一个完整的Camel教程，而是作为第一步大致介绍Camel的关键部位。

### 2.5.1. **Endpoint****(端点)**

在谈论进程间通信时经常使用术语endpoint。例如，在客户端、服务器通信中，客户端是一个endpoint，服务器是另一个endpoint。根据上下文，endpoint可以引用地址，例如host:port用于TCP的通信，或者它可以指代在该地址可访问的软件实体。例如，如果某人使用www.example.com:80作为endpoint的示例，则他们可能是指该主机名的实际端口（即地址），或者他们可能是指Web服务器（即可在其上可访问的软件）地址。通常，在该地址可访问的地址和软件之间的区别并不重要。

一些中间件技术使的几个软件实体可以在同一物理地址被访问。例如，CORBA是面向对象的远程过程调用（RPC）中间件标准。如果CORBA服务器进程包含多个对象，则客户端可以在同一物理地址（host:port）与任何这些对象进行通信，但客户端需要通过该对象的逻辑地址与其进行通信（在CORBA术语中称为IOR），包括物理地址（host:port）加上一个唯一标识其服务器进程内对象的id。（IOR包含一些与本讨论无关的其他信息。）在谈论CORBA时，有些人可能会使用术语"endpoint"来指代CORBA服务器的物理地址，而其他人可能会使用该术语来指代单个CORBA对象的逻辑地址，另外的人仍然可以使用该术语来引用以下任何内容:

l host:port:CORBA服务器进程的物理地址。

l host:port加id:CORBA对象的逻辑地址。

l 相对重量级的软件实体:CORBA服务器进程。

l 轻量级软件实体:CORBA对象。

因此，您可以看到术语**端点**（Endpoint）至少有两种方式不明确。首先，它是模棱两可的，因为它可能指的是地址或在该地址可访问软件实体。其次，它所指的粒度是模糊的:重量级或轻量级软件实体，或物理地址、逻辑地址。理解不同的人使用术语端点（Endpoint）的方式略有不同（因而模棱两可）是很有用的，Camel对这个术语的使用可能与之前的任何含义又不相同。

Camel为许多不同通信技术实现的端点（Endpoint）提供开箱即用的支持。以下是Camel支持的端点（Endpoint）技术的一些示例。

l JMS队列。

l Webservice。

l File，File可能听起来像一种不太可能的端点类型，直到您意识到在某些系统中，一个应用程序可能会将信息写入File，之后，另一个应用程序可能会读取该File。

l FTP服务器。

l 电子邮件。客户端可以向电子邮件地址发送消息，服务器可以从邮件服务器读取传入消息。

l POJO（普通的旧Java对象）。

在基于Camel的应用程序中，您创建（Camel包装的）一些端点并将这些端点与路由连接，我将在后面的[2.5.8节（"路由，RouteBuilders和Java DSL"）中讨论](https://camel.apache.org/manual/latest/book-getting-started.html)。Camel定义了一个名为Endpoint的Java接口。每个Camel支持的端点都有一个实现此Endpoint接口的类。正如我在2.4节[（"在线Javadoc文档"）中](https://camel.apache.org/manual/latest/book-getting-started.html)讨论的那样，Camel为Camel支持的每种通信技术提供了一个单独的Javadoc层次结构。因此，您将在[JMS Javadoc层次结构中](http://camel.apache.org/maven/current/camel-jms/apidocs/)找到有关JmsEndpoint 类的文档，而FtpEndpoint 该类的文档位于[FTP Javadoc层次结构中](http://camel.apache.org/maven/current/camel-ftp/apidocs/)。

### 2.5.2. **CamelContext**

CamelContext对象表示Camel的运行时系统。通常在应用程序中有一个CamelContext对象。典型的应用程序执行以下步骤:

1. 创建一个CamelContext对象。
2. 将端点及其对应的组件（在第2.5.5节（"组件"）中讨论）添加到CamelContext对象（Component是用于创建Endpoint实例的工厂）。
3. 添加路由（route）到CamelContext对象用以连接endpoint。
4. 调用CamelContext对象的start()方法。这将启动Camel内部线程，用于处理endpoint中消息的发送，接收和处理。
5. 最终调用CamelContext对象上的操作stop()。执行此操作会优雅地停止所有endpoint和Camel内部线程。

请注意，CamelContext.start()操作不会无限期地阻塞。更准确地说，它启动线程内部每个Component和Endpoint，然后start()返回。相反，CamelContext.stop()等待每个内部的所有线程Endpoint和Component终止然后stop()返回。

如果忽略调用CamelContext.start()，则应用程序不会处理消息，因为不会创建内部线程。

如果您忘记在终止应用程序之前调用CamelContext.stop()，则该应用程序可能会以不一致的状态终止。如果在JUnit测试中因忽略导致调用CamelContext.stop()，那么测试可能会失败，因为消息没有机会被完全处理。

### 2.5.3. **CamelTemplate**

Camel曾经有一个被调用的类CamelClient，但是它被重命名为CamelTemplate类似于一些其他开源项目中使用的命名约定，例如[Spring中](http://www.springframework.org/)的TransactionTemplate和JmsTemplate类。

这个CamelTemplate类很好的包装了CamelContext类。它有Message或Exchange** **发送方法 - 在两篇段落中分别讲到:第2.5.1节（"Endpoint"）至[第2.5.6节（"Message和Exchange"](https://camel.apache.org/manual/latest/book-getting-started.html)）。这提供了一种将消息输入源端点的方法，以便消息沿着路由（route）移动到目标端点（在[第2.5.8节（"路由，RouteBuilders和Java DSL"）中讨论](https://camel.apache.org/manual/latest/book-getting-started.html)）。

### 2.5.4. **URL，URI，URN和IRI的含义**

一些Camel方法采用的是URI字符串参数。很多人都知道URI是"像URL一样"，但是没有正确理解URI和URL之间的关系，或者它与其他缩略词（如IRI和URN）之间的关系。

大多数人都熟悉的URL（统一资源定位器），如http://…，ftp://…，\mailto:…:。简而言之，URL指定资源的位置。

一个URI（统一资源标识符）是一个URL 或一个URN。因此，要完全理解URI的含义，首先需要了解什么是URN。

**URN****:**是统一资源名称的首字母缩写。存在很多"唯一标识符"方案，例如，ISBN（全球唯一的书籍），社会安全号码（在一个国家内是唯一的），客户号码（在公司的客户数据库中是唯一的）和电话号码。每个"唯一标识符"方案都有自己的表示法。URN是不同"唯一标识符"方案的包装器。URN的语法是urn:<scheme-name>:<unique-identifier>。URN唯一地标识资源，例如书籍，人或设备。URN本身并未指定资源的位置。相反，假设注册表提供从资源的URN到其位置的映射。URN规范没有说明注册表采用什么形式，但它可能是数据库，服务器应用程序，报表或任何其他方面的。URN的一些假设的例子如urn:employee:08765245，urn:customer:uk:3458:hul8和urn:foo:0000-0000-9E59-0000-5E-2。<scheme-name>（在这些示例中，员工，客户和foo）的一部分隐式地定义如何解析和解释它后面的唯一标识结点<unique-identifier>。任意URN都是没有意义的，除非:（1）您知道<scheme-name>隐含的语义，以及（2）您可以访问适用于<scheme-name>的注册表。注册表不必是公共的或全局可访问的。例如，urn:employee:08765245 可能仅在特定公司内有意义。

到目前为止，URN还没有像URL一样受欢迎。因此，URI被广泛滥用为URL的同义词。

**IRI****:**是国际化资源标识符的首字母缩写（internationalized resource identifier）。IRI只是URI的国际化版本。特别是，URI可以包含字母和数字以及US-ASCII字符集，而IRI除了包含这些相同的字母和数字外，而且还包含欧洲重音字符，希腊字母，中国汉字等。

### 2.5.5. **Components（****组件）**

Component是个令人困惑的术语; EndpointFactory会更合适，因为一个Component是用于创建Endpoint实例的工厂。例如，如果基于Camel的应用程序使用多个JMS队列，则应用程序将创建JmsComponent类的一个实例（实现Component接口），然后应用程序多次调用JmsComponent对象上的操作createEndpoint()。每次调用JmsComponent.createEndpoint()都会创建一个JmsEndpoint类的实例（实现Endpoint接口）。实际上，应用程序级代码不会直接调用Component.createEndpoint()。相反，应用程序级代码通常会调用CamelContext.getEndpoint(); 在内部，CamelContext对象找到所需的Component对象（我将在稍后讨论）然后调用createEndpoint()。

请考虑以下代码:

myCamelContext.getEndpoint("pop3://john.smith@mailserv.example.com?password=myPa

getEndpoint()方法的参数是一个URI。URI 前缀（即 **:** 前面的部分）指定组件的名称。在内部，CamelContext对象维护从组件名称到Component对象的映射。对于上例中给出的URI，CamelContext对象可能会将pop3前缀映射到MailComponent类的实例。然后CamelContext对象调用MailComponent.createEndpoint("pop3://john.smith@mailserv.example.com?password=myPassword")。createEndpoint()操作将URI拆分为其组成部分，并使用这些部分来创建和配置Endpoint对象。

在上一段中，我提到了一个CamelContext对象维护了从组件名称到Component对象的映射。这引发了如何使用命名填充Component对象映射的问题。填充有两种方法。第一种方法是调用应用程序级代码CamelContext.addComponent(String componentName, Component component)。下面的示例显示了MailComponent在3个不同名称下在映射中注册的单个对象。

Component mailComponent = new org.apache.camel.component.mail.MailComponent();

myCamelContext.addComponent("pop3", mailComponent);

myCamelContext.addComponent("imap", mailComponent);

myCamelContext.addComponent("smtp", mailComponent);

填充Component对象中命名对象映射的第二种（也是首选）方法CamelContext是让CamelContext对象执行延迟初始化。这种方法依赖于开发人员在编写实现Component接口的类时遵循约定。我通过一个例子说明了这个惯例。让我们假设您编写了一个名为com.example.myproject.FooComponent的类，并且您希望Camel通过名称foo自动识别它。为此，您必须编写一个名为META-INF/services/org/apache/camel/component/foo（没有.properties文件扩展名）的属性文件，其中包含一个名为class的条目，其值是您的类的完全路径名称。如下所示:

**META-INF/services/org/apache/camel/component/foo**

class=com.example.myproject.FooComponent

如果您希望Camel也通过名称bar识别该类，那么您在同一目录中编写另一个bar属性文件。编写属性文件后，创建包含com.example.myproject.FooComponent类和属性文件的JAR文件，并将此jar文件添加到CLASSPATH。然后，当应用程序级的代码调用一个CamelContext上对象的createEndpoint("foo:…")，Camel会发现"foo"的属性在CLASSPATH文件，从属性文件获得属性class的value值，并使用反射API来创建指定类的一个实例。

正如我在2.5.1节（"Endpoint"）中所说，Camel为众多通信技术提供了开箱即用的支持。开箱即用的支持包括实现Component接口的类和属性文件，这些文件使CamelContext对象能够填充其命名和Component对象的映射。

在本节前面，我给出了以下调用示例CamelContext.getEndpoint():

myCamelContext.getEndpoint("pop3://john.smith@mailserv.example.com?password=myPassword");

当我最初给出那个例子时，我说getEndpoint()参数是一个URI。我说是因为在线Camel文档和Camel源代码都声称该参数是一个URI。实际上，该参数仅限于URL。这是因为当Camel从参数中提取组件名称时，它会查找第一个":"，这是一个简单的算法。要理解原因，请回忆[第2.5.4节（"URL，URI，URN和IRI的含义"）](https://camel.apache.org/manual/latest/book-getting-started.html)，URI可以是URL 或 URN。现在考虑以下getEndpoint调用:

myCamelContext.getEndpoint("pop3:...");

myCamelContext.getEndpoint("jms:...");

myCamelContext.getEndpoint("urn:foo:...");

myCamelContext.getEndpoint("urn:bar:...");

Camel标识在上述例子中作为components分pop3，jms，urn和urn。如果将后面两个的组件标识urn:foo和urn:bar替代地，直接简写为foo和bar（即，跳过urn:前缀）将更有用。因此，在实践中，您必须使用URL（<scheme>:…的字符串）而不是URN（urn:<scheme>:…的字符串）来标识端点。缺乏对URN的适当支持意味着您应该将getEndpoint()参数视为URL而不是（如声明的）URI。

### 2.5.6. **Message和Exchange**

Message接口为单个消息提供抽象，例如请求，回复或异常消息。

实现Message接口的类为每一种通信技术提供了Camel支持。例如，JmsMessage类提供了JMS的Message接口实现。Message接口的公共API 提供了get和set方法来访问消息的消息id，消息体body和消息头header。

Exchange接口提供消息交换的抽象，即请求消息及其相应的回复或异常消息。在Camel术语中，请求，回复和异常消息被称为in，out和fault消息。

实现Exchange接口的类为每一种通信技术提供了Camel支持。例如，JmsExchange类提供了JMS的Exchange接口实现。Exchange接口的公共API 非常有限。这是有意义的，并且期望实现此接口的每个类将提供其自己的技术特性操作。

应用程序级程序员很少直接访问Exchange接口（或实现它的类）。但是，Camel中的许多类都是泛型类型并且它们实例化（或实现）自Exchange。因此，Exchange接口在类和方法的参数中出现很多。

### 2.5.7. **Processor（****处理器）**

Processor接口表示处理消息的类。如下所示:

**Processor**

package org.apache.camel;

public interface Processor {

**    **void process(Exchange exchange) throws Exception;

}

请注意，process()方法的参数是Exchange而不是Message。这提供了灵活性。例如，此方法的实现最初可能会调用exchange.getIn()以获取输入消息并对其进行处理。如果在处理期间发生错误，则该方法可以调用exchange.setException()。

应用程序级开发人员可以实现Processor接口的业务逻辑的类。但是，Camel库中有许多类通过实现Processor接口为EIP书中的设计模式提供支持。例如，ChoiceProcessor实现消息路由器模式，也就是说，它使用级联if-then-else语句将消息从输入队列路由到多个输出队列之一。另一个例子是FilterProcessor丢弃不满足断言（即条件）的消息。

### 2.5.8. **Routes（路由）****，RouteBuilders和Java DSL**

Message进入队列后route会一步一步的移动它，通过任意类型的决策（如过滤器(filters)和路由器(routers)）到达目标队列（如果有的话）。Camel为应用程序开发人员提供了两种指定路由的方法。一种方法是在XML文件中指定路由信息。对该方法的讨论超出了本文档的范围。另一种方式是通过Camel调用Java DSL（domain-specific language，特殊领域语言）。

#### 2.5.8.1. **Java DSL简介**

术语"domain-specific language"意味有一个编译器或解释器，它用于处理特定领域的语法，可以外挂一个文件，文件内有自己特定的关键字和语法。 Camel没有采取这种术语叫法。Camel文档始终使用术语"Java DSL"而不是"DSL"，但这并不能完全避免潜在的混淆。Camel"Java DSL"是一个类库，除了Java包名它的用法很像DSL，。您可以在下面的示例中看到这一点。之后的注释解释了示例中使用的一些构造。

**Camel的"Java DSL"示例**

RouteBuilder builder = new RouteBuilder() {

**    **public void configure(){

**        **	from("queue:a").filter(header("foo").isEqualTo("bar")).to("queue:b"); **    **

**        **	from("queue:c").choice()

**                **	.when(header("foo").isEqualTo("bar")).to("queue:d")

**                **	.when(header("foo").isEqualTo("cheese")).to("queue:e")

**                **	.otherwise().to("queue:f");

**    **}

};

CamelContext myCamelContext = new DefaultCamelContext(); myCamelContext.addRoutes(builder);

上例中的第一行创建了一个对象，该对象是RouteBuilder类匿名实例，实现了configure()方法。

CamelContext.addRoutes(RouterBuilder builder)方法调用builder.setContext(this)，因此RouteBuilder对象知道与哪个CamelContext对象相关联，然后调用builder.configure()的方法体，configure()方法体内调用如from()，filter()，choice()，when()，isEqualTo()，otherwise()和to()。

RouteBuilder.from(String uri)方法在与RouteBuilder对象关联的CamelContext上调用getEndpoint(uri)，以获取指定的Endpoint，然后用FromBuilder 封装Endpoint。FromBuilder.filter(Predicate predicate)方法创建一个FilterProcessor对象，然后用表达式header("foo").isEqualTo("bar")作为过滤条件。通过这种方式，这些操作逐步构建一个Route对象（RouteBuilder为它提供包装器）并将其添加到与RouteBuilder对象关联的CamelContext中。

#### 2.5.8.2. **Java DSL的评价**

Camel在线文档将Java DSL与基于XML的Spring配置文件配置路由和端点的替代方案进行了比较。特别是，Java DSL比XML对应实现更简洁。此外，许多集成开发环境（IDE）在其编辑器中提供自动完成功能。这种功能适用于Java DSL，从而使开发人员更容易编写Java DSL。

但是，Camel文档忽略了另一种选择：编写一个可以处理存储在外部文件中的DSL的解析器。目前，Camel没有提供这样的DSL解析器，我不知道它是否在Camel维护者的"待办事项"列表中。我认为DSL解析器可以提供比当前Java DSL更大的优势。特别地，DSL将具有可以以相对短的BNF形式表达的句法定义。Camel用户通过阅读此BNF学习如何使用DSL所需的工作几乎肯定会远远低于研究RouterBuilder课程API所需的工作量。

## 2.6. **继续学习** **Camel**

返回主入门页面以获取其他介绍性参考信息。

# 附录1 **示例代码** **- 通过J****ava启动**

本小型指南将带您浏览一个*github上*[*简单示例*](https://github.com/apache/camel/blob/master/examples/camel-example-jms-file/src/main/java/org/apache/camel/example/jmstofile/CamelJmsToFileExample.java)的源代码。

可以通过使用[Spring](https://camel.apache.org/manual/latest/spring.html)或直接在Java中配置Camel（[*github上*](https://github.com/apache/camel/blob/master/examples/camel-example-jms-file/src/main/java/org/apache/camel/example/jmstofile/CamelJmsToFileExample.java)[*简单示例*](https://github.com/apache/camel/blob/master/examples/camel-example-jms-file/src/main/java/org/apache/camel/example/jmstofile/CamelJmsToFileExample.java)）。下面详细对其解释:

我们首先创建一个[CamelContext](https://camel.apache.org/manual/latest/camelcontext.html)，它是[Components](https://camel.apache.org/components/latest/index.html)，[Routes](https://camel.apache.org/manual/latest/routes.html)等的容器:

CamelContext context = new** **DefaultCamelContext();

有多种方法可以将组件添加到CamelContext。您可以隐式添加组件（在设置路由时），就如此处的[FileComponent](https://camel.apache.org/components/latest/file-component.html)（"file://test"中的file）:

context.addRoutes(new** **RouteBuilder() {

**    **public void configure() {

**        **from("test-jms:queue:test.queue").to("file://test");

**    **}

});

或显式 —** **如我们在此处添加JMS组件时所做的:

ConnectionFactory connectionFactory = new** **ActiveMQConnectionFactory("vm://localhost?broker.persistent=false");

*// Note we can explicit name the component*

context.addComponent("test-jms", JmsComponent.jmsComponentAutoAcknowledge(connectionFactory));

以上适用于任何JMS提供程序（provider）。如果我们在使用[ActiveMQ，](https://camel.apache.org/components/latest/activemq-component.html)则可以在指定连接到ActiveMQ 的[brokerURL的](http://activemq.apache.org/configuring-transports.html)同时，使用[activeMQComponent()方法](#activeMQComponent(java.lang.String))这样更简单的形式。

在正常使用中，外部系统将通过其[组件](https://camel.apache.org/components/latest/index.html)（如果它是组件之一）将消息或事件直接发射到Camel，但是我们将使用 [ProducerTemplate](https://camel.apache.org/manual/latest/producertemplate.html)，这是测试配置的一种非常简单的方法:

ProducerTemplate template = context.createProducerTemplate();

接下来，您**必须**启动CamelContext。如果您使用[Spring](https://camel.apache.org/manual/latest/spring.html)来配置Camel上下文，将自动为您完成；但是，如果您使用的是纯Java方法，则只需调用start()方法

camelContext.start();

这将启动所有已配置的路由规则。

因此，在启动[CamelContext之后](https://camel.apache.org/manual/latest/camelcontext.html)，我们可以将一些对象发射到Camel中:

for** **(int** **i = 0; i < 10; i++) {

**    **template.sendBody("test-jms:queue:test.queue", "Test Message: "** **+ i);

}

## 1. **发生了什么****？**

从[ProducerTemplate到组件*test-jms:queue:test.queue*](https://camel.apache.org/manual/latest/producertemplate.html)（我们将Object（在这种情况下为文本）发送到[CamelContext中](https://camel.apache.org/manual/latest/camelcontext.html)）。这些文本对象将[自动转换](https://camel.apache.org/manual/latest/type-converter.html)为JMS消息，并发布到名为test.queue的JMS队列中。设置[Route时](https://camel.apache.org/manual/latest/routes.html)，我们将[FileComponent](https://camel.apache.org/components/latest/file-component.html)配置为侦听test.queue。

[FileComponent](https://camel.apache.org/components/latest/file-component.html)将使消息弹出队列，并将其保存到名为test的目录中。每条消息将保存在与其目的地和消息ID相对应的文件中。

最后，我们在[Route中](https://camel.apache.org/manual/latest/routes.html)配置了自己的侦听器，接收来自[FileComponent的](https://camel.apache.org/components/latest/file-component.html)通知，并将其打印为文本。

**仅此****而已！**

如果您有时间，请再花5分钟来介绍[另一个示例](https://camel.apache.org/manual/latest/walk-through-another-example.html)，该[示例](https://camel.apache.org/manual/latest/walk-through-another-example.html)演示了Spring DSL（基于XML）路由。也就是附录2。

# 附录2 **示例代码** **- 通过****Spring****启动**

## 1．介绍

继续第一个[示例](https://camel.apache.org/manual/latest/walk-through-an-example.html)的Spring方案，我们仔细研究一下路由并解释一些要点，这样您就不会走进陷阱，而是可以在下班后步行到当地的酒吧喝一大杯啤酒。

首先，我们花一点时间看一下Enterprise Integration Patterns（简称EIP，[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)，集成方案的基本模式目录）。特别是，我们专注于Pipes and Filters（一个中心化模式，[管道和过滤器](http://www.enterpriseintegrationpatterns.com/PipesAndFilters.html)）。它用于通过一系列处理步骤路由消息，每个处理步骤执行特定的功能，与Java Servlet过滤器非常相似。

## 2．Pipes and Filters - 管道和过滤器

在此示例中，我们希望按照一系列步骤来处理消息，其中每个步骤都可以执行其特定功能。在我们的示例中，我们有一个[JMS](https://camel.apache.org/components/latest/jms-component.html)队列来接收新订单。收到订单后，我们需要分几个步骤进行处理:

l 验证订单

l 注册订单

l 发送确认电子邮件

可以在如下的路由中创建:

<route>

**   **<from uri="jms:queue:order"/>

**   **<pipeline>

**      **<bean ref="validateOrder"/>

**      **<bean ref="registerOrder"/>

**      **<bean ref="sendConfirmEmail"/>

**   **</pipeline>

</route>

**Pipeline****（****管道****）****使用了****默认的****构造方式**

在上述路由中，pipeline作为默认值可以省略掉，如下:

<route>

**   **<from uri="jms:queue:order"/>

**   **<bean ref="validateOrder"/>

**   **<bean ref="registerOrder"/>

**   **<bean ref="sendConfirmEmail"/>

</route>

通常不用声明管道pipeline。

需要使用pipeline的一个场景是广播，其中一个端点，发送到逻辑组时，是其他端点的管道，例如。

<route>

**   **<from uri="jms:queue:order"/>

**   **<multicast>

**     **<to uri="log:org.company.log.Category"/>

**     **<pipeline>

**       **<bean ref="validateOrder"/>

**       **<bean ref="registerOrder"/>

**       **<bean ref="sendConfirmEmail"/>

**     **</pipeline>

**   **</multicast>

</route>

上面的路由同时将订单（从jms:queue:order）发送到两个位置，即我们的日志组件，并发送到另一个的Bean的"管道"。如果您考虑相反的情况，没有<pipeline>结点

<route>

**   **<from uri="jms:queue:order"/>

**   **<multicast>

**     **<to uri="log:org.company.log.Category"/>

**     **<bean ref="validateOrder"/>

**     **<bean ref="registerOrder"/>

**     **<bean ref="sendConfirmEmail"/>

**   **</multicast>

</route>

您会看到多播不会将消息从一个bean"流"到另一个，而是将订单并行发送到所有4个端点（1个日志，3个 Bean），这不是我们想要的。我们需要消息流到validateOrder，然后流到registerOrder，然后是sendConfirmEmail，因此添加管道即可提供此功能。

其中的bean ref是Spring bean ID的引用，因此我们使用常规Spring XML将bean定义为:

<bean id="validateOrder" class="com.mycompany.MyOrderValidator"/>

我们的验证器bean是一个普通的POJO，它从未如此依赖于Camel。因此，您可以根据需要实现此POJO。Camel使用相当智能的[Bean绑定](https://camel.apache.org/manual/latest/bean-binding.html)来使用接收到的消息的有效负载来调用POJO。在此示例中，我们将**不**深入探讨这种情况。稍后，您将对Camel有所了解后，应该回到本主题，来了解如何使用POJO bean轻松绑定路由。

那么上面的路由发生了什么。好了，当从[JMS](https://camel.apache.org/components/latest/jms-component.html)队列接收到订单时，消息就像管道和过滤器一样被路由:

1. 来自[JMS的](https://camel.apache.org/components/latest/jms-component.html)有效负载作为输入发送到validateOrder bean
2. 来自validateOrder bean的输出作为输入发送到registerOrder bean
3. registerOrder bean的输出作为输入发送到sendConfirmEmail bean

## 3．使用Camel组件

在路由中，让我们想象订单的注册必须通过将数据发送到可能是大型机的TCP套接字来完成。由于Camel有许多[组件，](https://camel.apache.org/components/latest/index.html)我们将使用支持[TCP](https://camel.apache.org/components/latest/mina-component.html)连接的camel-mina组件。因此，我们将路由更改为:

<route>

**   **<from uri="jms:queue:order"/>

**   **<bean ref="validateOrder"/>

**   **<to uri="mina:tcp://mainframeip:4444?textline=true"/>

**   **<bean ref="sendConfirmEmail"/>

</route>

路由中现在具有的to类型可以用作Bean类型的直接替代。现在的步骤是:

1. 将来自[JMS的](https://camel.apache.org/components/latest/jms-component.html)有效负载作为输入发送到validateOrder bean
2. 使用TCP将来自validateOrder bean的输出作为文本发送到大型机
3. 将来自大型机的输出作为输入发送回sendConfirmEmai bean

这里要注意的是to在示例中它不是路径的终点（世界），而是在[Pipes和filter](https://camel.apache.org/manual/latest/pipeline-eip.html)的中间使用的。实际上，我们也可以将bean类型更改to为:

<route>

**   **<from uri="jms:queue:order"/>

**   **<to uri="bean:validateOrder"/>

**   **<to uri="mina:tcp://mainframeip:4444?textline=true"/>

**   **<to uri="bean:sendConfirmEmail"/>

</route>

由于to属于通用类型，因此我们必须在uri方案中说明它是哪个组件。因此，我们必须为正在使用的[Bean](https://camel.apache.org/components/latest/bean-component.html)组件写上[**bean****:**前缀。](https://camel.apache.org/components/latest/bean-component.html)

## 4．结论

提供此示例是为了演示Spring DSL（基于XML），而不是[第一个示例中](https://camel.apache.org/manual/latest/walk-through-an-example.html)的纯Java DSL 。并且要指出的是，to不一定是路由图中的最后一个节点。

此示例也基于**in-only**消息交换模式。您还必须了解的是调用者期望获取响应**的in-out**消息交换模式。我们将在另一个示例中对此进行研究。
