# 第三章 **A****rchitecture****(架构)**

Camel使用基于Java的[ ](https://camel.apache.org/manual/latest/dsl.html)[Routing Domain Specific Language](https://camel.apache.org/manual/latest/dsl.html)(简称DSL)或XML Configuration来配置路由和中介规则，这些规则被添加到[CamelContext](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/CamelContext.html)以实现各种[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)。

抽象来讲，Camel由一个[CamelContext](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/CamelContext.html)构成，这个CamelContext包含一组Component实例。每个Component又包含若干个Endpoint实例。您可以在Java代码或Spring或Guice等IoC容器中显式配置组件实例，也可以使用URI自动发现它们。

Endpoint的行为非常类似于Web应用程序中的URI或URL或JMS系统中的Destination; 你可以与Endpoint通信; 向其发送消息或接收其消息。具体是在Endpoint上创建[Producer(生产者)](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Producer.html)或[Consumer](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Consumer.html)([消费者](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Consumer.html))以与其交换消息。

DSL规范大量使用可插拔式语言来创建Expression(表达式)或Predicate(断言)，并且DSL真正强大之处，允许你根据自己的需要扩展为最合适的语言。而且许多语言也支持[基于注解的表达语言](https://camel.apache.org/manual/latest/parameter-binding-annotations.html)。

## **C****amel****架构****图**

![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps1.jpg)

## **C****amel****主要部件介绍**

Camel架构上主要分为三部分:component、Endpoint、Processor。component负责各种客户端连接，并生成统一格式的Endpoint；在服务端再由Processor连接Endpoint，然后在Processor内提供可插拔式编程。

1. **Camel component**

l 为各种Camel客户端提供统一的endpoint接口。

l 充当所有其他客户端系统的连接器。

2. **Camel Endpoint**

Camel能够通过Processor发送或者接收消息给各种Endpoint。

3. **Camel Processor**

3.1. **Camel Processor分类:Filter**和**Router**两种。

3.2. **Camel Processor作用**

l 将Camel Processor和Endpoint连接起来。

l 用来路由。

l 用来做转换。

l 用来做断言。

l 用来做拦截。

l 用来做内容增强。

l 用来做验证。

l 用来做追踪。

l 用来做日志记录。

# 1. **异步****(****A****sync****)**

**从Camel 2.0开始提供**

Camel中的异步API自Camel 2.0重写，以下信息适用于Camel 2.0及更高版本。

Camel中的Async API主要分为两个区域:

1. 客户端，启动Async消息传递。
2. 服务端，Camel Processor使用**多****线程**DSL将route转换为Async。

在解释以上两点之前，我们先了解一点背景信息，然后用图表从可视角度了解其含义。

在介绍第一点客户端如何启动异步消息交换时，我们也会混合介绍同步消息交换，以便我们可以比较和了解两者的差异。

最后，我们将注意力转向第二点，**线程** DSL 以及它可以用于什么。

## 1.1. **背景**

Camel 2.0中新的Async API更充分地利用了Java Concurrency API及其对异步执行任务的支持。

因此，具有Java Concurrency API知识的用户应该熟悉Camel Async API。

## 1.2. **主要****概念**

在进行消息传递时，需要记住几个方面。

首先，消息交换(message exchange)类型按调用者角度分类如下:

l Request only，请求/不回复。

l Request Reply，请求/回复。

Request only表示调用者发送消息后但**不**期望任何回复。这也称为fire(发射)和forget(遗忘)或event message(事件消息)。

Request Reply是指调用者发送消息然后**等待回复**。这就像我们每天上网时使用的[HTTP](https://camel.apache.org/components/latest/http-component.html)协议。我们发送请求以获取网页并等待回复消息随Web内容一起提供。

在Camel中，消息标有消息交换模式标记，该标记表明其是Request only还是Request Reply消息。Camel使用**JBI**术语**InOnly**表示Request only和**InOut**表示Request Reply。

其次，消息交换(message exchange)类型按执行方式分类如下:

l 同步，synchronous。

l 异步，asynchronous。

### 一.1.1. **同步****的****请求****/****回复** **-** **S****ynchronous****R****equest** **R****eply**

同步交换定义为调用者发送消息并等待其完成后再继续。如下图所示:

![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps2.jpg)

1) 客户端通过[HTTP](https://camel.apache.org/components/latest/http-component.html)向Camel 发送同步请求回复消息。客户端应用程序将等待Camel routes 和 processes响应。
2) 该消息使用同步请求应答调用外部[TCP](https://camel.apache.org/components/latest/mina-component.html)服务。客户端应用程序仍在等待响应。
3) 响应将发送回客户端。

### 一.1.2. **异步****的****请求****/****回复** **-** **A****ynchronous****R****equest** **R****eply**

另一方面，异步版本是调用者向Endpoint发送消息然后立即返回给调用者。而后，该消息在另一个线程(异步线程)中处理。然后调用者可以继续执行其他工作，同时异步线程正在处理该消息。如下图所示:

![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps3.jpg)

1) 客户端通过HTTP向Camel发送异步请求应答消息。不等待响应消息，可以在Camel路由message时继续执行其他工作。
2) Camel 使用同步请求调用外部[TCP](https://camel.apache.org/components/latest/mina-component.html)服务。客户端应用程序可以同时执行其他工作。
3) 客户端肯定希望得到回复，因此在第1步时使用haddller的异步代码等待接收响应数据，直到响应到达为止。

### 一.1.3. **同步的****请求****/不****回复** **-** **Synchronous Request Only**

也可以使用Camel执行同步的请求/不回复。客户端向Camel发送消息，不需要回复。但是，客户端仍然等待消息完全处理。如下图所示:

![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps4.jpg)

1) 客户端发送单次请求，我们仍然可以使用[HTTP，](https://camel.apache.org/components/latest/http-component.html)尽管http本质上是请求回复。
2) Camel 使用同步请求/回复调用外部[TCP](https://camel.apache.org/components/latest/mina-component.html)服务。客户端应用程序仍在等待。
3) 完全处理消息，并将控制返回给客户端。

那么为什么要使用同步[请求](https://camel.apache.org/manual/latest/event-message.html)/不回复？因为，您在继续前想要知道消息是否处理成功。使用同步，它允许您在处理消息时等待。如果处理成功，则控制权将返还给客户端，而不会出现错误。如果失败，客户端可以在抛出异常时检测到此情况。(exchange.isFailed()返回true)。

### 一.1.4. **异步的****请求****/不****回复** **-** **Asynchronous Request Only**

与同步请求/不回复相反，异步请求/不回复**不会**等待消息的处理完成。在这种情况下，客户端可以在Camel中路由和处理消息时立即继续执行其他工作。如下图所示:

![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps5.jpg)

1) 客户端仅发送请求，我们仍然可以使用[HTTP，](https://camel.apache.org/components/latest/http-component.html)尽管http本质上是请求回复。控制权立即返还到客户端应用程序，可以在Camel路由消息时继续执行其他工作。
2) Camel 使用同步请求/回复调用外部[TCP](https://camel.apache.org/components/latest/mina-component.html)服务。客户端应用程序可以同时执行其他工作。
3) 消息完成但没有结果返回给客户端。

**注意****:**Camel始终向客户端返回Async消息传递的Future句柄。客户端可以使用此句柄来获取处理结果，无论任务是成功完成还是处理期间发生异常。请注意，客户端并不一定要这样做，也是完全有效的，只是忽略Future句柄。

如果您想知道Async Request Only是否失败，那么您可以使用Future句柄并调用get()，如果它抛出ExecutionException则处理失败。包含由其引起的其他异常。您可以先调用isDone()以测试任务是否已完成或仍在进行中。否则调用get()将等待任务完成。

考虑到以上几点，我们可以留意Async API以及如何将它与Camel一起使用。

## 1.3. **C****lient**** API**

### 1.3.1. **异步客户端****API**

Camel在[ProducerTemplate](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/ProducerTemplate.html)中提供了Async Client API ，我们在Camel 2.0中添加了大约10个新方法。我们列出了下表中最重要的内容:


| **方法**           | **返回**         | **描述**                                                                                                                                                   |
| ------------------ | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| setExecutorService | void             | 用于设置Java ExecutorService。默认情况下，Camel将在池中提供带有5个线程的ScheduledExecutorService。                                                         |
| asyncSend          | Future<Exchange> | 用于向Camel Endpoint发送异步交换。在将任务提交给执行程序后，Camel将立即将控制权返回给调用程序线程。这允许您在Camel处理其他异步线程中的交换时执行其他工作。 |
| asyncSendBody      | Future<Object>   | 同上，但仅用于发送消息体。这是一种单向请求消息传递的样式，因此不需要回复。使用InOnly交换模式。                                                             |
| asyncRequestBody   | Future<Object>   | 同上，但仅用于发送消息体。这是一个请求/回复消息样式，因此需要回复。使用InOut交换模式。                                                                     |
| extractFutureBody  | T                | 用于使用Java Concurrency Future句柄从异步线程获取结果。                                                                                                    |

asyncSend和asyncRequest方法返回一个Future的对象。此对象是调用者稍后必须使用的，用来检查异步响应结果。可以使用extractFutureBody方法执行此操作，或者只使用普通Java方法在Future上调用get()。

### 1.3.2. **带有****callback****的****异步客户端****API**

除了上面的客户端API之外，Camel还提供了一个在消息交换完成时使用回调的变体。


| **方法**                 | **返回**         | **描述**                                                                                          |
| ------------------------ | ---------------- | ------------------------------------------------------------------------------------------------- |
| asyncCallback            | Future<Exchange> | 该方法将org.apache.camel.spi.Synchronization 作为回调参数传入。消息交换完成后将被调用。          |
| asyncCallbackSendBody    | Future<Object>   | 同上，但仅用于发送消息体。这是一种请求/不回复消息传递的模式，因此不需要回复。使用InOnly交换模式。 |
| asyncCallbackRequestBody | Future<Object>   | 如上所述，但仅用于发送消息体。这是一个请求/回复消息模式，因此需要回复。使用InOut交换模式。        |

这些方法还会返回Future句柄，以供您需要时调用。不同之处在于，当Exchange完成服务端路由时，它们也会调用回调。

### 1.3.3. **F****uture****的API**

java.util.concurrent.Future** **API具有以下方法:


| **方法** | **返回** | **描述**                                                                        |
| -------- | -------- | ------------------------------------------------------------------------------- |
| isDone() | boolean  | 无论任务是否完成都会返回一个布尔值。另外即使抛出异常导致任务失败也返回true。    |
| get()    | Object   | 获取任务的响应结果。如果抛出异常则抛出java.util.concurrent.ExecutionException。 |

### 1.3.4. **示例****:****异步****的****请求****/****回复**

假设我们想要调用[HTTP](https://camel.apache.org/components/latest/http-component.html)服务，但它通常很慢，因此我们不想阻塞并等待响应，因为我们要做其他重要的计算。因此，我们可以启动一个异步HTTP Endpoint，然后在[HTTP](https://camel.apache.org/components/latest/http-component.html)服务处理我们的请求时执行其他操作。稍后我们可以使用Future句柄来获取[HTTP](https://camel.apache.org/components/latest/http-component.html)服务的响应。所以我们做了如下的例子:

首先我们在Camel中定义两个路由route。一个模拟[HTTP](https://camel.apache.org/components/latest/http-component.html)响应缓慢的服务，它至少需要1秒才能回复。然后我们想要在[HTTP](https://camel.apache.org/components/latest/http-component.html)服务路由时调用的其他路由。我们在Camel启动两个路由route:

*//* *模拟**同步调用**，**一个**返回名称的服务。*

from("direct:name")

**  **.transform(constant("Claus"))

**  **.to("mock:result");

*//* *模拟**异步调用**，**延迟1秒**响应**，**模拟我们想要的**缓慢**http服务*

from("jetty:http://0.0.0.0:%s/myservice", getPort())

**  **.delay(1000)

**  **.transform(constant("Bye World"))

**  **.to("mock:result");

然后我们使用client API调用这两个路由，从两个路由获得响应。代码是基于单元测试，还有一些准备工作要做:

*// 连接至endpoint，名字为mock:result*

MockEndpoint mock = getMockEndpoint("mock:result");

*//* *返回name的服务**比异步**服务**更快。*

*//* *启动*

mock.expectedBodiesReceived("Claus", "Bye World");

*//* *先**向**HTTP* *Endpoint**发送****异步请求/回复****消息*

Future<Object> future = template.asyncRequestBody("http://0.0.0.0:"** **+ getPort() + "/myservice", "Hello World");

*// 在**等待**期间，**Camel允许随时获取Future，可以去处理其他**事情*

*// 因此，我们调用另一个****请求/回复****路由，但这一次是同步的。*

String name = template.requestBody("direct:name", "Give me a name", String.class);

assertEquals("Claus", name);

*//**好的，我们得到了一个名称，并且在异步路由运行的同时还做了一些其他工作，但是现*

*//* *在是等待并从异步任务获得响应的时候了。*

*//**我们使用提取**的**Future**body**从**Future**获取响应**(**如果需要，请等待**)**，然后返回字符*

*//**串响应体。我们在一行代码中**就可以**完成这项工作，而不是使用JDK**Future**的API来*

*//* *获取它，但是如果您想添加**(**字符串**)**以使CS满意，也可以使用它。*

String response = template.extractFutureBody(future, String.class);

assertEquals("Bye World", response);

assertMockEndpointsSatisfied();

以上，应该为您介绍如何使用Async API以及它操作方法的基本知识。

### 1.3.5. **示例****:****同步请求****/****回复**

此示例只是上面基于异步的示例的纯同步版本。

路由是相同的，所以它只是客户端如何启动和发送不同的消息:

MockEndpoint mock = getMockEndpoint("mock:result");

*//* *同步阻塞意味着响应比较慢的服务返回结果后才能继续执行*

mock.expectedBodiesReceived("Bye World", "Claus");

*// 向http Endpoint发送同步请求/响应消息*

String response = template.requestBody("http://0.0.0.0:"** **+ getPort() + "/myservice", "Hello World", String.class);

assertEquals("Bye World", response);

*// 向**direct endpoint**发送同步请求/响应消息*

String name = template.requestBody("direct:name", "Give me a name", String.class);

assertEquals("Claus", name);

assertMockEndpointsSatisfied();

### 1.3.6. **示例:****将****异步****API与回调一起使用**

假设我们想要调用[HTTP](https://camel.apache.org/components/latest/http-component.html)服务，但它通常很慢，因此我们不想阻塞并等待响应，而是让回调收集响应。这允许我们在发送下一个请求之前无需等待回复。

首先，我们在Camel中为[HTTP](https://camel.apache.org/components/latest/http-component.html)服务定义一个路由，我们模拟一个慢速服务器，因为它需要至少1秒的时间来回复。

*// 模拟程序在这里进行单元测试。*

*// 模拟我们想要调用异步的慢http服务(延迟一点)*

from("jetty:http://0.0.0.0:" + getPort() + "/myservice")

.delay(1000)

.transform(body().prepend("Hello "))

.to("mock:result");

然后我们定义回调来收集响应结果。由于这是基于单元测试，只是简单在List中收集响应。List是我们发送的所有请求的共用回调处，但您可以使用自定义的方式或使用匿名回调实现。回调支持很多种方法，在这个例子无论Exchange是成功还是失败，我们都会调用onDone。同时org.apache.camel.spi.Synchronization** **API提供了用于以上两种情况的onCompletion和onFailure方法。

*/***

* * Our own callback that will gather all the responses.*
* * We extend the SynchronizationAdapter class as we then only need to override the onComplete method.*
* */*

private** **static** **class MyCallback extends SynchronizationAdapter {

**  ***// below the String elements are added in the context of different threads so that we should make*

**  ***// sure that this's done in a thread-safe manner, that's no two threads should call the data.add()*

**  ***// method below concurrently, so why we use Vector here and not e.g. ArrayList*

**  **private** **final** **List<String> data = new** **Vector<>();

**  **@Override

**  **public void onComplete(Exchange exchange) {

**    ***// this method is invoked when the exchange was a success and we can get the response*

**    **String body = exchange.getOut().getBody(String.class);

**    **data.add(body);

**    ***// the latch is used for testing purposes*

**    **LATCH.countDown();

**  **}

**  **public List<String> getData() {

**    **return** **data;

**  **}

}

然后我们通过client API的异步回调，使用不同的输入调用3次[HTTP](https://camel.apache.org/components/latest/http-component.html)服务。由于调用是Async，客户端将各自发送3个请求，因此我们有3个并发交换将进行中。我们的回调收集了响应结果，因此我们不必关心响应如何获得。

MyCallback callback = new** **MyCallback();

*// Send 3 async request/reply message to the http endpoint*

*// where we let the callback handle gathering the responses*

String url = "http://localhost:"** **+ getPort() + "/myservice";

template.asyncCallbackRequestBody(url, "Claus", callback);

template.asyncCallbackRequestBody(url, "Hadrian", callback);

template.asyncCallbackRequestBody(url, "Willem", callback);

### 1.3.7. **示例:****将****异步****API与****Camel****典型****API一起使用**

使用Camel API创建生产者并发送Exchange时，我们这样做:

Endpoint endpoint = context.getEndpoint("http://slowserver.org/myservice");

Exchange exchange = endpoint.createExchange();

exchange.getIn().setBody("Order ABC");

*// create a regular producer*

Producer producer = endpoint.createProducer();

*// send the exchange and wait for the reply as this is synchronous*

producer.process(exchange);

在异步调用更常见的是，我们需要帮助类的一些帮助，所以代码如下:

Endpoint endpoint = context.getEndpoint("http://slowserver.org/myservice");

Exchange exchange = endpoint.createExchange();

exchange.getIn().setBody("Order ABC");

*// create a regular producer*

Producer producer = endpoint.createProducer();

*// normally you will use a shared executor service with pools*

ExecutorService executor = Executors.newSingleThreadExecutor();

*// send it async with the help of this helper*

Future<Exchange> future = AsyncProcessorHelper.asyncProcess(executor, producer, exchange);

*// here we got the future handle and we can do other stuff while the exchange is being routed in the other asynchronous thread*

...

*// and to get the response we use regular Java Concurrency API*

Exchange response = future.get();

## 1.4. **多线程****DSL**

在Camel 2.0中，多线程DSL取代了旧的线程DSL。

### 1.4.1. **Camel****2****.0到2.3的行为**

多线程DSL利用了JDK多线程并发框架。它可用于将同步路由转换为异步。发生的事情是，从线程开始，消息在新线程中异步路由。如果需要回复，调用者将等待回复，例如当我们使用请求/回复消息时调用者就要等待。或者例如使用不期望得到回复的请求/不回复消息，调用者也将完成这次请求。

### 1.4.2. **Camel** **2****.4以后的行为**

多线程DSL利用多线程的JDK并发框架。它可用于将同步路由转换为异步。发生的事情是，从线程开始，消息在新线程中异步路由。Camel利用[异步路由引擎](https://camel.apache.org/manual/latest/asynchronous-routing-engine.html)(在Camel 2.4中重新引入，在“2异步路由引擎”详细介绍)继续异步路由Exchange。

多线程DSL支持以下选项:


| **选项**               | **描述**                                                                                                                                                                                                                                                   |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| poolSize               | 表示底层Java ExecutorService的线程池大小，实际上也是由它完成处理异步任务和关联回复的所有繁重工作。默认情况下，池大小为10。                                                                                                                                 |
| maxPoolSize            | 表示底层Java ExecutorService的最大线程池大小                                                                                                                                                                                                               |
| KeepAliveTime          | 表示保持非活动线程保持活动状态的时间                                                                                                                                                                                                                       |
| TIMEUNIT               | keepAliveTime选项的时间单位                                                                                                                                                                                                                                |
| maxQueueSize           | 指示要在底层Java ExecutorService的工作队列中保留的最大任务数                                                                                                                                                                                               |
| threadName             | 使用自定义线程名称模式。有关详细信息，请参阅线程模型。                                                                                                                                                                                                     |
| rejectedPolicy         | 如何处理被拒绝的任务。可以是Abort，CallerRuns，Discard，或DiscardOldest。请参阅下面的更多细节。                                                                                                                                                            |
| callerRunsWhenRejected | 一个布尔值，可以更容易地在最常见的拒绝策略之间进行配置。此选项默认启用。true相当于rejectedPolicy=CallerRuns，false相当于rejectedPolicy=Abort。                                                                                                             |
| ExecutorService        | 您可以自定义ExecutorService，例如在托管环境中，J2EE容器可以提供此服务，因此所有线程池都由J2EE容器控制。                                                                                                                                                    |
| executorServiceRef     | 您可以从Camel Registry提供的别名引用自定义的ExecutorService。请记住，自定义ExecutorService的引用不能配置相关的选项(如poolSize或maxQueueSize)，因为自定义ExecutorService已经配置好了。                                                                      |
| waitForTaskToComplete  | **@deprecated****(****在Camel 2.4中删除****):**用于指定调用者是否应该在继续之前等待异步任务完成。支持以下3个选项:**Always**，**Never**或**IfReplyExpected**。前两个选项是强制选项。最后一个只会等待消息回复是基于请求回复。默认选项为**IfReplyExpected**。 |

### 1.4.3. **关于任务的拒绝**

threads** **DSL使用的队列线程池，当其工作队列满时，其他任务将被拒绝。您可以使用rejectedPolicy和callerRunsWhenRejected选项自定义如何对此作出反应。后者用于在两种最常见和推荐的设置之间轻松切换。要么让当前调用方线程执行任务(例如它将成为同步的)，要么给线程池处理当前任务的时间，而不添加更多的任务——类似于自限流。这是默认配置。如果设置callerRunsWhenRejected使用了Abort策略，意味着任务被拒绝，并且在Exchange上要设置RejectedExecutionException ，Exchange将停止继续路由，它的UnitOfWork将被视为失败。

其他选项Discard和DiscardOldest工作有点像Abort，但是他们没有在Exchange上设置任何异常，这意味着Exchange不会被视为失败，但Exchange将会成功。使用Discard，DiscardOldest时Exchange将不会继续路由。**注意****:** Camel 2.9或更低版本中的这两个选项存在问题导致UnitOfWork不被触发，因此我们不鼓励您在这些Camel版本中使用这些选项。这已在Camel 2.10修复。

### 1.4.4. **示例****:****多****线程DSL**

假设我们在JMS队列上接收订单。一些订单期望回复，而其他订单则不用回复(无论JMSReplyTo是否存在)。并且让我们想象这个处理顺序，我们需要做一些繁重的CPU计算。那么在处理整个消息之前，我们如何避免不希望回复的消息产生阻塞呢？我们使用threads** **DSL在繁重的CPU任务开始之前将路由转换为多线程异步路由。然后，不期望回复的消息可以预先返回。那些期待回复的消息，是的，他们无论如何都要等待。所以这可以像下面的route一样完成:

*// just a unit test but imagine using your own data format that does complex*

*// and CPU heavy processing for decrypting the message*

DataFormat mySecureDataFormat = new** **StringDataFormat("iso-8859-1");

*// list on the JMS queue for new orders*

from("jms:queue:order")

**  ***// do some sanity check validation*

**  **.to("bean:validateOrder")

**  **.to("mock:validate")

** ** *//**使用池大小为20的多线程*

*//**将路由异步化，因为其他一些人不希望收到回复*

*//**然后我们可以使用线程DSL作为转折点*

*//**如果设置了JMS ReplyTo，那么我们希望得到答复，否则不会*

*//**使用20个线程池作为转发点*

**  **.threads(20)

**  ***// do some CPU heavy processing of the message (we simulate and delay just 500 ms)*

**  **.unmarshal(mySecureDataFormat)

**  **.delay(500)

**  **.to("bean:handleOrder")

**  **.to("mock:order")

;


|  | **事务和多线程DSL请**注意，在使用事务时，它通常要求Exchange完全在同一个线程中处理，因为事务管理器通常用ThreadLocal存储中间事务状态。例如，Spring Transaction就是这样做的。因此，在使用threads DSL 时，在异步线程中处理的Exchange不能与调用者线程参与相同的事务。**注意:**这不适用于ProducerTemplate异步API，因为客户端通常不参与事务。因此，您仍然可以使用Camel Client Async API并执行异步消息传递，其中Exchange的处理仍在事务中处理。它只提交了不参与同一事务的Exchange的客户端。 |
| - | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

# 2. **异步路由引擎**

**自Camel 2.4起可用**

从Camel 2.4开始，异步路由引擎又回来了。

支持所有[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)以及选定数量的组件:

1. [AHC](https://camel.apache.org/components/latest/ahc-component.html) **Camel 2.8:** (only producer)
2. AWS **Camel 2.11:** (only consumer) for S3 and SNS.
3. [Avro](https://camel.apache.org/components/latest/avro-component.html) **Camel 2.10:** (only producer)
4. [CXF](https://camel.apache.org/components/latest/cxf-component.html) **Camel 2.5:** (both consumer and producer)
5. [CXFRS](https://camel.apache.org/components/latest/cxfrs-component.html) **Camel 2.5:** (only consumer)
6. [Direct-VM](https://camel.apache.org/components/latest/direct-vm-component.html) **Camel 2.10.5/2.11.0:** (both consumer and producer)
7. [File](https://camel.apache.org/components/latest/file-component.html) - (only consumer)
8. [FTP](https://camel.apache.org/components/latest/ftp-component.html) - (only consumer)
9. [Guava EventBus](https://camel.apache.org/components/latest/guava-eventbus-component.html) **Camel 2.10:** (only consumer)
10. JBI (both consumer and producer)
11. [Jetty](https://camel.apache.org/components/latest/jetty-component.html) (both consumer and producer)
12. [JGroups](https://camel.apache.org/components/latest/jgroups-component.html) **Camel 2.10:** (only consumer)
13. [JMS](https://camel.apache.org/components/latest/jms-component.html) **Camel 2.5:** (only producer for Request Reply messaging over JMS). **Camel 2.9:** (consumer, if option asyncConsumer=true is used).
14. [JMS](https://camel.apache.org/components/latest/jms-component.html) **Camel 2.9:** (also consumer)
15. [MQTT](https://camel.apache.org/components/latest/mqtt-component.html) **Camel 2.10.2:** (only producer)
16. NMR (both consumer and producer)
17. [Netty](https://camel.apache.org/components/latest/netty-component.html) only producer (**Camel 2.10:** also consumer)
18. [Restlet](https://camel.apache.org/components/latest/restlet-component.html) **Camel 2.8:** (only producer)
19. [SEDA](https://camel.apache.org/components/latest/seda-component.html) (both consumer and producer) SEDA was mistakenly in this list until November 3rd 2012. As of Camel 2.10.x, it still does not leverage the Async Routing Engine, but support is planned for [Camel 3.0](#Camel3.0-Roadmap-SEDA/VMcomponentstoleverageasyncroutingengine).
20. [Timer](https://camel.apache.org/components/latest/timer-component.html) **Camel 2.12:** (only consumer)

当我们说支持一个组件时，这意味着该组件正在利用异步模型。例如，[Jetty](https://camel.apache.org/components/latest/jetty-component.html)使用continuation和async http客户端完全异步和非阻塞。这意味着在等待回复时不会阻止任何线程。

将来，在适用的情况下，还将支持其他组件。

## 2.1. **强制使用同步处理**

您可以设置synchronous=true选项强制配置Endpoint同步处理。例如，使用[CXF](https://camel.apache.org/components/latest/cxf-component.html)发送Webservice时，如果已配置synchronous=true则调用方将等待回复。目前，所有生产者都支持此选项。如果您不想让[CXF](https://camel.apache.org/components/latest/cxf-component.html)消费者等待响应请使用异步处理，您也可以使用此选项synchronous=true来禁用它。JBI和NMR组件始终是异步的，不支持此选项。

## 2.2. **背景资料**

有关其他信息和异步模型背后的概念，请参阅异步模型。

# 3. **Backlog****调试器**

**自Camel 2.12起可用**

Camel支持backlog调试器，用于实时调试在Camel中路由的消息。与调试器相比，backlog调试器具有其他功能，可以更容易地针对工具进行调试。backlog调试器在JMX中以BacklogDebugger的名称暴露在跟踪器节点中。JMX API在org.apache.camel.api.management.mbean.ManagedBacklogDebuggerMBean接口中定义。

您可以通过调用enableDebugger或disableDebugger方法动态启用或禁用BacklogDebugger 。

## 3.1. **选项**


| **选项**           | **默认** | **描述**                                                                                     |
| ------------------ | -------- | -------------------------------------------------------------------------------------------- |
| enabled            | false    | 是否启用调试器。                                                                             |
| singleStepMode     | false    | 当前是否处于单步交换模式。                                                                   |
| bodyMaxChars       | 128kb    | 将跟踪消息中的消息体限制为最大大小。使用0或负值来设置为无限大小。                            |
| bodyIncludeStreams | false    | 是否包括基于流的消息体。如果启用，则要注意以后可能无法重新读取流。了解有关流缓存的更多信息。 |
| bodyIncludeFiles   | true     | 是否包含基于文件的消息的消息体。开销是必须从文件中读取文件内容。                             |

## 3.2. **操作**


| **选项**                                              | **类型**    | **描述**                                                                       |
| ----------------------------------------------------- | ----------- | ------------------------------------------------------------------------------ |
| enableDebugger                                        | void        | 启用调试器                                                                     |
| disableDebugger                                       | void        | 禁用调试器                                                                     |
| getDebuggerCounter                                    | long        | 获取已调试消息的总数。                                                         |
| resetDebuggerCounter                                  | void        | 重置调试器计数器。                                                             |
| dumpTracedMessagesAsXml(nodeId)                       | String      | 以XML格式转储来自给定节点id的调试消息。                                        |
| addBreakpoint(nodeId)                                 | void        | 在给定节点处添加断点。                                                         |
| addConditionalBreakpoint(nodeId, language, predicate) | void        | 在给定节点处添加条件断点。断言是从language参数创建的。                         |
| removeBreakpoint(nodeId)                              | void        | 从给定节点id中删除断点。                                                       |
| resumeBreakpoint(nodeId)                              | void        | 恢复暂停断点，然后继续路由Exchange。                                           |
| resumeAll                                             | void        | 恢复所有暂停的断点。                                                           |
| getSuspendedBreakpointNodeIds                         | Set<String> | 获取已挂起断点的所有节点的集合(如挂起断点处的交换)。                           |
| stepBreakpoint(nodeId)                                | void        | 从给定node上的挂起断点启动单步模式。然后调用step to step到路由中的下一个node。 |
| step                                                  | void        | 在单步模式下转到下一个node。                                                   |
| getBreakpoints                                        | Set<String> | 获取添加断点的所有node的集合。                                                 |
| enableBreakpoint(nodeId)                              | void        | 激活已暂时禁用的断点。                                                         |
| disableBreakpoint(nodeId)                             | void        | 暂时禁用断点。                                                                 |
| setMessageBodyOnBreakpoint(nodeId,body)               | void        | 在node上更新挂起的Exchange上的消息体。                                         |
| setMessageHeaderOnBreakpoint(nodeId,headerName,value) | void        | 在node上挂起的Exchange上更新/添加消息头。                                      |

## 3.3. **启用**

您需要使用JMX API启用它。

# 4. **业务活动监控**

Camel BAM模块提供了一个BAM(Business Activity Monitoring)框架，用于跨不同Endpoint实例上的多个消息交换测试业务流程

例如，在一个简单的系统中，您将购买订单提交到系统a，然后从系统B接收发票。

## 4.1. **Camel** **BAM****如何运作**

Camel BAM 在输入消息上使用[关联标识符](https://camel.apache.org/manual/latest/correlation-identifier.html)([Correlation Identifier](https://camel.apache.org/manual/latest/correlation-identifier.html))来确定它所属的流程实例。流程实例是一个实体bean，它可以维护每个活动的状态(活动通常映射到单个端点 - 例如提交采购订单或收到发票)。

return** **new** **ProcessBuilder(entityManagerFactory, transactionTemplate) {

**    **public void configure() throws Exception {

**        ***// let's define some activities, correlating on an XPath on the message bodies*

**        **ActivityBuilder a = activity("seda:a").name("a")

**                **.correlate(xpath("/hello/@id"));

**        **ActivityBuilder b = activity("seda:b").name("b")

**                **.correlate(xpath("/hello/@id"));

**        ***// now let's add some rules*

**        **b.starts().after(a.completes())

**                **.expectWithin(seconds(1))

**                **.errorIfOver(seconds(errorTimeout)).to("mock:overdue");

**    **}

};

然后，在任何活动收到消息时您可以添加要触发的规则 - 例如设置预期时间或跨活动执行值的实时一致性计算。

## 4.2. **简单的例子**

以上示例展示了如何基于一个简单的业务流程执行一些基于时间的规则，该流程包含两个活动——a和B——它们与上面示例中的采购订单和发票相对应。如果您想试验这个场景，您可以编辑这个[Test Case](http://svn.apache.org/repos/asf/camel/trunk/components/camel-bam/src/test/java/org/apache/camel/bam/BamRouteTest.java)，它定义了activity和规则，然后测试它们是否正常工作。

正如您在上面的示例中所看到的，我们首先定义了两个活动，然后定义了规则来指定流程实例何时期望它们完成，以及何时应该提出错误条件。ProcessBuilder是一个RouteBuilder，可以添加到任何CamelContext中。

## 4.3. **完整的例子**

有关完整示例，请参阅[BAM示例](https://camel.apache.org/manual/latest/bam-example.html)，它是标准Camel示例的一部分

## 4.4. **用例**

在金融界，一个共同的要求是跟踪交易。通常，交易员会提交一个前台交易，然后通过中间办公室和后台办公室通过各种系统进行结算，以便进行货币交换。您可能希望测试前台和后台的交易是否在一定的时间内匹配;如果它们不匹配或后台交易没有在规定的时间内到达，您可能会发出警报。

# 5. **批量消费者(B****atch Consumer****)**

**从Camel 2.0开始提供**

批量消费者基本上是一个[轮询消费者](https://camel.apache.org/manual/latest/polling-consumer.html)，它能够轮询池中的多个Exchange。我们在Camel 2.0中所做的是将其标准化为org.apache.camel.BatchConsumer接口，一个消费者实现该接口表示它也支持批处理。

以下组件中其Consumer支持[Batch Consumer](https://camel.apache.org/manual/latest/batch-consumer.html):

l [Atom](https://camel.apache.org/components/latest/atom-component.html)

l File

l FTP

l [hbase](https://camel.apache.org/components/latest/hbase-component.html)

l [JPA](https://camel.apache.org/components/latest/jpa-component.html)

l [JCLOUDS](https://camel.apache.org/components/latest/jclouds-component.html)

l [Mail](https://camel.apache.org/components/latest/mail-component.html)

l [MyBatis](https://camel.apache.org/components/latest/mybatis-component.html)

l [SNMP](https://camel.apache.org/components/latest/snmp-component.html)

l [SQL](https://camel.apache.org/components/latest/sql-component.html)

l [SQS](https://camel.apache.org/components/latest/aws-sqs-component.html)

l [S3](https://camel.apache.org/components/latest/aws-s3-component.html)

## 5.1. **消费者****选项**

Batch Consumer支持以下选项:


| **选项**           | **描述**                                                                                                                                                  |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| maxMessagesPerPoll | 一个整数，用于定义每个轮询收集的最大消息数。默认情况下，不设置最大值。可用于设置例如1000的限制，以避免在启动服务器时有数千个文件。设置值0或负值以禁用它。 |

## 5.2. **E****xchange****选项**

对于在同一批次中轮询的每个Exchange，在Exchange上设置以下属性。


| **属性**           | **描述**                                                               |
| ------------------ | ---------------------------------------------------------------------- |
| CamelBatchSize     | 此批次中轮询的Exchange总数。                                           |
| CamelBatchIndex    | 批次的当前索引。从0开始。                                              |
| CamelBatchComplete | 一个布尔值，表示批处理中的最后一个Exchange。仅true适用于最后一个条目。 |

# 6. **B****rowsable****E****ndpoint**

BrowsableEndpoint是一个扩展接口，Endpoint可以实现该接口来支持在其上浏览pending或已经发送的消息交换

示例实现包括

l [JMS](https://camel.apache.org/components/latest/jms-component.html) for queues only (as of 1.3.0)

l List

l [Mock](https://camel.apache.org/components/latest/mock-component.html)

l [Seda](https://camel.apache.org/components/latest/seda-component.html)

l [VM](https://camel.apache.org/components/latest/vm-component.html)

# 7. **核心**


| 此页面正在进行中。分层可能还不正确 |
| ---------------------------------- |

Camel-core是Apache Camel的基础模块。它包含公共API和Java DSL以及小量实现包。

最重要的包是:


| **包名**  | **描述**                                                       |
| --------- | -------------------------------------------------------------- |
| builder   | 用于创建 Routes, Predicates, Expressions和Error Handlers      |
| model     | 包含形成java DSL的类(* Type)。中心类是RouteBuilder             |
| language  | Expressions和Predicates的语言API和插件                         |
| component | 一些简单的组件，如bean或log。您将在其他camel模块中找到大量组件 |
| impl      | Model和Camel的实现类                                           |
| processor | processor来实现企业集成模式EIP                                 |
| spi       | 服务提供者接口。用于实现并扩展Camel的策略api                   |
| camel     | Camel基础包。像Message和CamelContext这样的定义可以在这里找到   |

## 7.1. **包关系****图**

该图显示了camel-core中顶级包的松耦合分层。松耦合意味着一个层可以引用它下面的任何层。

![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps6.jpg)

## 7.2. **架构图****中包含的****违规**

向上的每个箭头显示分层中的违规。这意味着包中的一些类引用了它上面的一个包类。这些图表是使用称为structure 101的架构工具构建的。我们提供了制造商的标题软件，为我们提供所有感兴趣的Camel开发人员的许可证。如果您需要许可证，请联系我(Christian Schneider chris at die-schneider.net)。然后我会尝试为您组织许可证。

image:: architecture_incl_violations.png [image]

# 8. **上下文**

[CamelContext](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/CamelContext.html)表示Camel独立路由规则库。您可以类似于Spring [ApplicationContext的](http://static.springsource.org/spring/docs/3.0.x/javadoc-api/org/springframework/context/ApplicationContext.html)方式使用CamelContext 。

请参阅[生命周期](https://camel.apache.org/manual/latest/lifecycle.html)以了解CamelContext的整个生命周期

# 9. **端点（****Endpoint****）**

Camel使用[Endpoint](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Endpoint.html)接口支持Message Endpoint模式。Endpoint通常由Component创建，Endpoint通常通过其URI在DSL中引用。

对于Endpoint，您可以使用以下方法:

l [createProducer](#createProducer())()将创建一个[Producer，](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Producer.html)用于向Endpoint发送消息交换。

l [createConsumer(](#createConsumer(org.apache.camel.Processor)))实现了事件驱动的消费者模式，Endpoint通过创建Consumer时的 [Processor](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Processor.html)消费消息交换

l [createPollingConsumer(](#createPollingConsumer()))实现Polling Consumer模式，Endpoint通过[PollingConsumer](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/PollingConsumer.html)消费消息交换

# 10. **复杂事件处理**

## 10.1. **Camel** **CEP**

[复杂事件处理](http://en.wikipedia.org/wiki/Complex_event_processing)或[事件流处理](http://en.wikipedia.org/wiki/Event_stream_processing)([Complex Event Processing](http://en.wikipedia.org/wiki/Complex_event_processing) or [Event Stream Processing](http://en.wikipedia.org/wiki/Event_stream_processing))是[处理](http://en.wikipedia.org/wiki/Complex_event_processing)[事件流](http://en.wikipedia.org/wiki/Event_stream_processing)的方法，通常来自多个来源。

使用Camel进行CEP的另一种方法是使用Camel RX，它提供Java，Scala，Groovy中的类型安全DSL，以类似于自然集合的方式处理事件(同时具有高性能和异步性)。Camel RX使用[RxJava ](https://github.com/Netflix/RxJava/wiki)[API](http://netflix.github.com/RxJava/javadoc/)，它是[Reactive Extensions](https://rx.codeplex.com/)的JVM港口

## 10.2. **CEP与****Camel** **RX**

Camel RX提供了各种方法来获取[Observable<T>](http://netflix.github.com/RxJava/javadoc/rx/Observable.html)，它提供了用于处理单个流上的事件的类型安全的DSL。

一旦你有了[Observable<T>，](http://netflix.github.com/RxJava/javadoc/rx/Observable.html)你就可以:

l [filter events](https://github.com/Netflix/RxJava/wiki/Filtering-Operators) * [transform events](https://github.com/Netflix/RxJava/wiki/Transformative-Operators) - [过滤事件](https://github.com/Netflix/RxJava/wiki/Filtering-Operators) * [转换事件](https://github.com/Netflix/RxJava/wiki/Transformative-Operators)。

l [combine event streams](https://github.com/Netflix/RxJava/wiki/Combinatorial-Operators) - [组合事件流](https://github.com/Netflix/RxJava/wiki/Combinatorial-Operators)。

l [other utility methods](https://github.com/Netflix/RxJava/wiki/Utility-Operators) - [其他实用方法](https://github.com/Netflix/RxJava/wiki/Utility-Operators)。

# 11. **组件（C****omponent****）**

Component本质上是[Endpoint](https://camel.apache.org/manual/latest/endpoint.html)实例的工厂。

您可以显式配置Component实例并将它们添加到IoC容器(如Spring或Guice)中的[CamelContext](https://camel.apache.org/manual/latest/camelcontext.html)，也可以使用[URI](https://camel.apache.org/manual/latest/uris.html)自动发现它们。

## 11.1. **包含的组件**

Camel通过[URI](https://camel.apache.org/manual/latest/uris.html)包含以下Component实现。


|  | 请务必阅读[如何配置端点？](https://camel.apache.org/manual/latest/faq/how-do-i-configure-endpoints.html)了解有关配置端点的更多信息。例如，如何在[注册表中](https://camel.apache.org/manual/latest/registry.html)引用bean 或如何使用原始值作为密码选项，以及如何使用[属性占位符](https://camel.apache.org/manual/latest/using-propertyplaceholder.html)等。 |
| - | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

# 12. **调试器（D****ebugger****）**

**自Camel 2.6起可用**

Camel Debugger与Tracer有很大关系，事实上他们是姊妹关系。Debugger是一个带有调试器框架的增强型Tracer，因此可以通过开发工具轻松监视Camel routes，跟踪消息并在路由中设置断点等。

**提示**:还有一个BacklogDebugger允许从JMX和第三方工具进行调试。

## 12.1. **关于****D****ebugger**

调试器允许工具或类似工具附加在断点，断点在交换被路由时被调用。

## 12.2. **默认****实现**

Camel提供了一个默认实现org.apache.camel.impl.DefaultDebugger，您可以在CamelContext上使用setDebugger方法进行设置。

同样，您可以在CamelContext上使用getDebugger方法来获取调试器Debugger。org.apache.camel.spi.Debugger内可以通过方法附加或者删除断点。并且还可以暂停/恢复所有断点等。

您还可以将条件附加到断点，以便它只在条件匹配时作出反应。

## 12.3. **从****Camel-Test****轻松调试****Camel路由 **

如果您正在使用camel-test组件开发单元测试，则调试器开箱即用。

从**Camel 2.9**开始，您需要通过重写isUseDebugger()方法使其返true回来显式启用Debugger。

## 12.4. **示例**

在这个单元测试中

public** **class DebugTest extends CamelTestSupport

我们想调试以下路由

@Override

protected RouteBuilder createRouteBuilder() throws Exception {

**    **return** **new** **RouteBuilder() {

**        **@Override

**        **public void configure() throws Exception {

**            ***// this is the route we want to debug*

**            **from("direct:start")

**                **.to("mock:a")

**                **.transform(body().prepend("Hello "))

**                **.to("mock:b");

**        **}

**    **};

}

通过覆盖debugBefore所示方法可以轻松完成

@Override

public boolean isUseDebugger() {

**    ***// must enable debugger*

**    **return** **true;

}

@Override

protected void debugBefore(Exchange exchange, Processor processor,

                       ProcessorDefinition<?> definition, String id, String shortName) {
**    ***// 在我们要进入给定**processor**之前，将调用此方法*

* //**从Java编辑器中，您只需在下面的代码行中添加一个断点*

**    **log.info("Before "** **+ definition + " with body "** **+ exchange.getIn().getBody());

}

然后从Java编辑器中添加一个断点到debugBefore方法里。然后启动单元测试并等待Java编辑器激发断点。然后，您可以在调试期间检查信息交换Exchange，也可同时在路由期间进行。ProcessorDefinition、id和shortName三个参数几乎包含所有信息，它们告诉你在router中断点被激发的具体位置。

**提示**:在调用处理器之后还有一个方法debugAfter可以调用。这使您可以在调用路由中的处理器后立即查看 Exchange发生的情况。

下面的屏幕截图显示了Debugger的运行情况。IDE(IDEA)已达到断点，我们可以检查参数。

注意我们如何看到消息将被发送到"mock:a"端点。

![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps7.jpg)

# 13. **延迟拦截器（D****elay** **I****nterceptor****）**

**可在Camel 1.5中使用**

Delay interceptor是一种路由拦截器，用于减慢消息处理速度。启用此拦截器允许您对路由内的消息传递的每个步骤之间设置固定时间段的延迟，以方便显式比较各步骤是否正常和处理是否缓慢，并且你不会收到大量输出日志轰炸，方便排查。

Delay interceptor可以配置如下:

l 在spring中设置CamelContext的delay属性。

l 在Java代码中将延迟拦截器添加到CamelContext中。

## 13.1. **使用S****pring****配置**

只需设置CamelContext标签的delay属性，如下所示:

**    **<camelContext id="camel" delayer="500" xmlns="http://activemq.apache.org/camel/schema/spring">

**        **<route>

**            **<from uri="direct:start"/>

**            **<to uri="mock:result"/>

**        **</route>

**    **</camelContext>

## 13.2. **使用****Java****配置**

您可以在RouteBulder中添加delayer拦截器:

getContext().setDelayer(200);

## 13.3. **粒度**

在**Camel 2.0中，**您可以根据需要在CamelContext和route上配置它。路由route将覆盖CamelContext上下文设置。

例如，下面是具有200毫秒延迟的route。

<camelContext ...>

**   **<route delayer="200">

**     **...

**   **</route>

**   **<route>

**     **...

**   **</route>

</camelContext>

# 14. **依赖注入**

依赖注入或控制反转是一种模式，其中对象的依赖关系被注入到对象中，而对象不太了解注入的执行方式。在撰写本文时，几个最受欢迎的依赖注入库是

l Spring

l Guice

l CDI

Camel的开发使得任何依赖注入框架都可以轻松使用 - 然而我们还在努力为Spring，CDI和Guice优化Camel。

# 15. **D****ozer****类型转换**

[Dozer](https://github.com/DozerMapper/dozer/blob/master/docs/asciidoc/about/about.adoc)是一个快速灵活的框架，用于在Java Bean之间映射。再加上Camel的自动类型转换，用于处理企业集成项目中出现的对象映射难题，它是一个强大的工具。

为了解释如何在Camel中使用Dozer，我们将使用以下简单客户支持服务示例。该服务的初始版本定义了一个结构非常扁平的"Customer"对象。

**传统****Customer****服务类**

public** **class Customer {

**    **private** **String firstName;

**    **private** **String lastName;

**    **private** **String street;

**    **private** **String zip;

**    **public Customer() {}

**    **public Customer(String firstName, String lastName, String zip, String street) {

**        **this.firstName = firstName;

**        **this.lastName = lastName;

**        **this.zip = zip;

**        **this.street = street;

**    **}

**    **public String getFirstName() {

**        **return** **firstName;

**    **}

**    **public void setFirstName(String firstName) {

**        **this.firstName = firstName;

**    **}

**    **... getters and setters for** **each field

在接下来的版本中，我们决定通过将Addess封装成Class来更好地构建数据模型，领域对象最终看起来如下所示。

**新版Customer****对象**

public** **class Customer {

**    **private** **String firstName;

**    **private** **String lastName;

**    **private** **Address address;

**    **public Customer() {}

**    **public Customer(String firstName, String lastName, Address address) {

**        **this.firstName = firstName;

**        **this.lastName = lastName;

**        **this.address = address;

**    **}

....

public** **class Address {

**    **private** **String zipCode;

**    **private** **String streetName;

**    **public Address() {}

**    **public Address(String zipCode, String streetName) {

**        **this.zipCode = zipCode;

**        **this.streetName = streetName;

**    **}

好多了！但正如经常发生的那样，先前版本使用老式"Customer"对象的服务与客户端一起生成，并且项目必须支持遗留接口。要支持这两个版本，我们必须添加一种机制，以便在旧的Customer服务类型和新的Customer域类型之间进行转换，然后再返回。比较简单的做法是编写自定义转换类在它们之间进行映射，但这样做可能并不只是类型的不一致，这些自定义映射可能很快就会累积起来，冗长且容易出错的。

在很大程度上，这两个对象共享相同的结构，只有Addess不同。如果有一种实用的方法来自动化这种映射，那么类似的属性可以自动映射，只有不一致的需要做自定义映射。

这就是引进Dozer的地方; 它使用反射来使用一组简单的映射规则在两种bean类型之间映射数据。如果没有指定规则，Dozer将尝试使用两个bean的匹配属性在它们之间进行映射。通过这种方式，可以关注bean之间的不一致性，即Addess属性，Dozer将自动匹配同名属性。

## 15.1. **配置D****ozer**

Dozer的配置非常灵活，[这里](https://github.com/DozerMapper/dozer/blob/master/docs/asciidoc/documentation/mappings.adoc)介绍[了](https://github.com/DozerMapper/dozer/blob/master/docs/asciidoc/documentation/mappings.adoc)许多映射方案。对于我们的简单示例，配置如下所示。

**mapping.xml**

<mappings xmlns="http://dozermapper.github.io/schema/bean-mapping"

      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

      xsi:schemaLocation="http://dozermapper.github.io/schema/bean-mapping http://dozermapper.github.io/schema/bean-mapping.xsd">
**  **<mapping>

**    **<class-a>org.apache.camel.converter.dozer.service.Customer</class-a>

**    **<class-b>org.apache.camel.converter.dozer.model.Customer</class-b>

**    **<field>

**      **<a>street</a>

**      **<b>address.streetName</b>

**    **</field>

**    **<field>

**      **<a>zip</a>

**      **<b>address.zipCode</b>

**    **</field>

**  **</mapping>

</mappings>

## 15.2. **在****Camel****中支持Dozer**

Camel提供了一种简单的机制，可以将Dozer Mappers与其强大的[Type Conversion](http://camel.apache.org/type-converter.html)框架集成在一起。通过创建一个DozerTypeConverterLoader实例来配置，这个实例提供CamelContext和可选的Dozer Mapper。如果没有提供Dozer Mapper，将搜索Camel的注册表registry以查找合适的实例。加载程序将向Dozer Mapper查询其转换的类型，并将其注册到Camel的类型转换框架中，以按该Mapper处理。


|  | **局限性**Camel Dozer类型转换器不支持映射ID不同(例如map-id)但相同类型的转换。 |
| - | ----------------------------------------------------------------------------- |

在Java中，它可以配置如下:

Mapper mapper = DozerBeanMapperBuilder.create()

**                **.withMappingFiles("mapping.xml")

**                **.build();

new** **DozerTypeConverterLoader(camelContext, mapper);

或者在spring:

<bean id="dozerConverterLoader" class="org.apache.camel.converter.dozer.DozerTypeConverterLoader">

**  **<argument index="0" ref="myCamel"/>

**  **<argument index="1" ref="mapperConfiguration"/>

</bean>

<bean id="mapperConfiguration" class="org.apache.camel.converter.dozer.DozerBeanMapperConfiguration">

**  **<property name="mappingFiles">

**    **<list>

**      **<value>mapping.xml</value>

**    **</list>

**  **</property>

</bean>

<camelContext id="myCamel" xmlns="http://camel.apache.org/schema/spring">

**  **...

</camelContext>

或者在OSGi Blueprints中:

<bean id="dozerConverterLoader" class="org.apache.camel.converter.dozer.DozerTypeConverterLoader">

**  **<argument index="0" ref="myCamel"/>

**  **<argument index="1" ref="mapperConfiguration"/>

</bean>

<bean id="mapperConfiguration" class="org.apache.camel.converter.dozer.DozerBeanMapperConfiguration">

**  **<property name="mappingFiles">

**    **<list>

**      **<value>mapping.xml</value>

**    **</list>

**  **</property>

</bean>

<camelContext id="myCamel" xmlns="http://camel.apache.org/schema/blueprint">

**  **...

</camelContext>

您应该注意到Spring或OSGi Blueprints的配置是相同的，除了'camelContext'的'xmlns'。

现在，在需要时，Camel将使用Dozer进行转换; 在我们的案例中是指新域和旧的Customer类型之间，例如:

*// given the following route*

from("direct:legacy-service-in").bean(new** **CustomerProcessor());

*// and a processor*

public** **class CustomerProcessor {

**    **public Customer processCustomer(org.apache.camel.converter.dozer.model.Customer customer) {

**       **...

**    **}

}

*// service objects can be sent to the processor and automagically converted by Camel & Dozer*

template.sendBody("direct:legacy-service-in", new org.apache.camel.converter.dozer.service.Customer("Bob", "Roberts", "12345", "1 Main st."));

# 16. **B****ean****集成**

Camel以多种方式支持bean和POJO的集成

## 16.1. **注解**

在spring XML中定义的Bean或Spring组件扫描到的bean，凡是xml结点名为**<camelContext>**或类型为CamelBeanPostProcessor的，我们都可以通过Camel注解注入如resources、producing、consuming或routing messages。

以下注解由Camel的CamelBeanPostProcessor支持并注入 


| **注解**        | **描述**                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| @EndpointInject | 要注入端点，请在[POJO Producing中](https://camel.apache.org/manual/latest/pojo-producing.html)查看更多详细信息。                |
| @BeanInject     | **Camel 2.13****:**注入从Registry获得的bean。参见[Bean Injection](https://camel.apache.org/manual/latest/bean-injection.html)。 |
| @PropertyInject | **Camel 2.12****:**使用属性占位符注入值。                                                                                       |
| @Produce        | 注入生产者以向端点发送消息。请参阅POJO Producing。                                                                              |
| @Consume        | 为方法注入消费者。见[POJO消费](https://camel.apache.org/manual/latest/pojo-consuming.html)。                                    |

查看更多细节:

l POJO消费，从Camel消费或路由消息

l POJO生产，用POJO可以轻松地生产Camel消息

l DynamicRouter注解，用于从POJO方法创建动态路由

l RecipientList注解，用于从POJO方法创建接收者列表

l RoutingSlip注解，用于为POJO方法创建RoutingSlip注解

l Bean注入，将Camel相关资源注入您的POJO

l [使用Exchange模式注](https://camel.apache.org/manual/latest/using-exchange-pattern-annotations.html)解，描述了该模式注解如何通过Spring Remoting或POJO生产来更改方法调用的行为（见24使用Exchange模式注解）。

**示例**

有关如何使用注解进行路由和消息传递，请参阅POJO消息传递示例。

## 16.2. **B****ean** **C****omponent**

Bean Component允许调用一种特定的方法。 Bean Component还支持通过ProxyHelper为Java接口创建代理，然后向Camel端点发送包含[BeanInvocation](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/component/bean/BeanInvocation.html)的消息。

## 16.3. **S****pring** **R****emoting**

我们支持使用Camel作为底层传输机制的Spring Remoting提供程序。这种方法的好处是我们可以使用任何Camel传输组件在bean之间进行通信。这也意味着我们可以在bean之间使用基于内容的路由器和其他[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html) ; 特别是我们可以使用Message Translator处理各种线上的消息，比如添加消息头等等。

**Bean绑定**

每当Camel通过上述方法之一(POJO Consuming，[Bean](https://camel.apache.org/components/latest/bean-component.html)组件或[Spring Remoting](https://camel.apache.org/manual/latest/spring-remoting.html))调用bean方法时，**Bean绑定**机制用于确定具体使用什么方法(如果它不显式)，Message对应什么参数，并且通过参数绑定注解或通过方法名定位对应的参数。

# 17. **Bean****绑定**

Camel中的Bean绑定定义了调用哪些方法以及在调用[Message时](https://camel.apache.org/manual/latest/message.html)如何将[Message](https://camel.apache.org/manual/latest/message.html)转换为方法的参数。

## 17.1. **选择要调用的方法**

Camel [消息](https://camel.apache.org/manual/latest/message.html)绑定的bean，调用的方法按以下重要性顺序进行:

1) 如果消息头包含**CamelBeanMethodName**，则调用该方法，将消息体转换为方法的参数类型。

l 从**Camel 2.8**开始，您可以指定参数类型，以准确选择在具有相同名称的重载中使用哪个方法(有关详细信息，请参见下文)。

l 从**Camel 2.9**开始，您可以直接在方法选项中指定参数值(有关详细信息，请参见下文)。

2) 您可以在[DSL中](https://camel.apache.org/manual/latest/dsl.html)或使用[POJO Consuming](https://camel.apache.org/manual/latest/pojo-consuming.html)或[POJO Producing](https://camel.apache.org/manual/latest/pojo-producing.html)时明确指定方法名称。
3) 如果bean标记有@Handler注解的方法，则选择该方法。
4) 如果bean可以使用[Type Converter](https://camel.apache.org/manual/latest/type-converter.html)机制转换为[Processor](https://camel.apache.org/manual/latest/processor.html)，那么它将用于处理消息。[ActiveMQ](https://camel.apache.org/components/latest/activemq-component.html)组件使用此机制，以允许任何JMS MessageListener通过Camel直连，无需编写任何集成代码。您可以使用相同的机制将Camel集成到任何其他**消息传递/远程处理**框架中。
5) 如果消息体可以转换为org.apache.camel.component.bean.BeanInvocation(org.apache.camel.component.bean.ProxyHelper默认的有效载荷)组件 - 那么它用来调用方法并传递其参数。
6) 消息体的类型用于找到匹配的方法; 如果无法明确单个方法名，则会引发错误。
7) 您也可以使用Exchange作为参数本身，但返回类型必须为void。
8) 如果bean类是私有的(或者是包私有的)，那么接口方法将是首选的(从**Camel 2.9**开始)，因为Camel不能在这样的bean类上调用方法

如果Camel无法选择要调用的方法，则抛出AmbiguousMethodCallException类型的异常。

默认情况下，返回值在输出消息消息体中设置。

## 17.2. **异步处理**

从**Camel 2.18**开始，您可以返回CompletionStage实现(例如CompletableFuture)以实现异步处理。

请务必使CompletionStage结果或异常正确完成，包括任何timeout处理。Exchange进程将一直处于等待，不会自动强行处理任何timeout。监视org.apache.camel.spi.InflightRepository是否有任何挂起的消息，这非常有用。

请注意，使用"null"完成不会将outbody消息正文设置为null，但会保持消息完整。这对于支持不修改交换并返回CompletableFuture<Void>的方法很有用。要将body设置为null，只需添加Exchange方法参数并直接修改交换消息。

例子:

简单的异步processor，修改消息体。

public CompletableFuture<String> doSomethingAsync(String body)

不修改交换的组合processor

** **public CompletableFuture<Void> doSomethingAsync(String body) {

**     **return CompletableFuture.allOf(doA(body), doB(body), doC());

** **}

## 17.3. **参数绑定**

当选择一个方法进行调用时，Camel将绑定到该方法的参数。

以下特定的Camel类型会自动绑定:

l org.apache.camel.Exchange

l org.apache.camel.Message

l org.apache.camel.CamelContext

l org.apache.camel.TypeConverter

l org.apache.camel.spi.Registry

l java.lang.Exception

因此，如果您声明以上任何类型，它们都将由Camel提供绑定。**请注意，****Exception****将绑定到**[**Exchange**](https://camel.apache.org/manual/latest/exchange.html)**的****Exception** - 因此，在使用[Pojo](https://camel.apache.org/components/latest/bean-component.html)来处理(例如onException路由)，它通常是可用的。

最有趣的是，Camel还会尝试将[Exchange](https://camel.apache.org/manual/latest/exchange.html)的消息体绑定到方法的第一个参数(尽管不是上述任何类型)。因此例如，如果我们将参数声明为String body，则Camel会将IN body绑定到此类型。Camel也会自动转换为方法中声明的类型。

我们来看一些例子:

下面是一个带有body绑定的简单方法。Camel将IN body绑定到body参数并将其转换为String。

public String doSomething(String body)

在下面的示例中，我们也获得了一个自动绑定类型 - 例如，我们可以用Registry来查找bean。

public String doSomething(String body, Registry registry)

我们也可以使用[Exchange](https://camel.apache.org/manual/latest/exchange.html):

public String doSomething(String body, Exchange exchange)

您还可以有多种类型:

public String doSomething(String body, Exchange exchange, TypeConverter converter)

并且假设您使用[Pojo](https://camel.apache.org/components/latest/bean-component.html)来处理给定的自定义异常InvalidOrderException** **- 我们也可以将其绑定:

public String badOrder(String body, InvalidOrderException invalid)

请注意，即使我们使用java.lang.Exception子类，我们也可以绑定它，因为Camel仍然知道它是一个异常并且可以绑定(如果存在)。

那么heads和其他stuff呢？那么现在它有点棘手 - 所以我们可以使用注解来帮助我们，或者在方法名称选项中指定绑定。

有关详细信息，请参阅以下部分。

### 17.3.1. **绑定注****解**

您可以使用[参数绑定注](https://camel.apache.org/manual/latest/parameter-binding-annotations.html)解来自定义参数值如何从[Message](https://camel.apache.org/manual/latest/message.html)创建

### 17.3.2. **例子**

例如，[Bean](https://camel.apache.org/manual/latest/bean-eip.html):

public class Bar {

**    **public String doSomething(String body) {

**    **// process the in body and return whatever you want

**    **return "Bye World";

}

或Exchange示例。请注意，当只有一个类型为org.apache.camel.Exchange的参数时，返回类型必须为**void**:

** **public class Bar {

**     **public void doSomething(Exchange exchange) {

**         **// process the exchange

**         **exchange.getIn().setBody("Bye World");

** **}

[[BeanBinding- @Handler]] === @Handler

您可以使用@Handler注解在bean中标记一个方法，以表示此方法应该用于[Bean绑定](https://camel.apache.org/manual/latest/bean-binding.html)。这样做的好处是，您无需在Camel路由中指定方法名称，因此在IDE中重命名方法后不会出现无法找到其引用的问题。

public class Bar {

**    **@Handler

**    **public String doSomething(String body) {

**        **// process the in body and return whatever you want

**        **return "Bye World";

**    **}

}

### 17.3.3. **使用方法选项进行参数绑定**

**自Camel 2.9起可用**

Camel使用以下规则来确定它是否是方法选项中的参数值

l 值为true或者false表示布尔值。

l 该值是一个数值，如123或7。

l 值是一个用单引号或双引号括起来的String。

l 值为null表示null值。

l 它可以使用[简单](https://camel.apache.org/manual/latest/simple-language.html)语言进行求值，这意味着您可以使用例如body，header.foo和其他[简单](https://camel.apache.org/manual/latest/simple-language.html)标记。请注意，标记必须用${}括起来。

任何其他值都被认为是类型声明 - 请参阅下一节有关为重载方法指定类型的内容。

调用[Bean时，](https://camel.apache.org/manual/latest/bean-eip.html)您可以通过提供方法名称来指示Camel调用的特定方法:

.bean(OrderService.class, "doSomething")

在这里，我们告诉Camel调用doSomething方法 - Camel处理参数的绑定。现在假设该方法有2个参数，第二个参数是一个布尔值，我们想要传入一个true:

public void doSomething(String payload, boolean highPriority) {

**    **...

}

现在可以在**Camel 2.9**开始如下实现:

.bean(OrderService.class, "doSomething(*, true)")

在上面的示例中，我们使用通配符*定义了第一个参数，它告诉Camel将此参数绑定到任何类型，并让Camel去弄清楚。第二个参数的固定值为true。我们可以指定Camel使用消息体，而不是通配符，如下所示:

.bean(OrderService.class, "doSomething(${body}, true)")

参数的语法使用[简单](https://camel.apache.org/manual/latest/simple-language.html)表达式语言([Simple](https://camel.apache.org/manual/latest/simple-language.html) expression language)，因此我们必须在正文中使用${ }占位符来引用消息体。

如果要传入null值，则可以在method选项中明确定义，如下所示:

.to("bean:orderService?method=doSomething(null, true)")

指定null为参数值指示Camel强制传递null值。

除了消息体之外，您还可以将消息头传递为java.util.Map:

.bean(OrderService.class, "doSomethingWithHeaders(${body}, ${headers})")

您还可以传递除布尔值之外的其他固定值。例如，您可以传入String和整数:

.bean(MyBean.class, "echo('World', 5)")

在上面的例子中，我们使用两个参数调用echo方法。第一个包含内容'World'(被单引号引用)，第二个包含值5。Camel会自动将这些值转换为参数类型。

[Simple](https://camel.apache.org/manual/latest/simple-language.html)语言的强大功能允许我们绑定到消息头和消息头其他值，例如:

.bean(OrderService.class, "doSomething(${body}, ${header.high})")

您还可以使用[Simple](https://camel.apache.org/manual/latest/simple-language.html)表达式语言的OGNL支持。现在假设消息体是一个具有名为asXml方法的对象。要调用asXml方法，我们可以执行以下操作:

.bean(OrderService.class, "doSomething(${body.asXml}, ${header.high})")

另外，不使用上例所示.bean，还可以用.to，如图所示:

.to("bean:orderService?method=doSomething(${body.asXml}, ${header.high})")

### 17.3.4. **使用类型限定符在重载方法中进行选择**

**自Camel 2.8起可用**

如果您有一个带有重载方法的[Bean](https://camel.apache.org/manual/latest/bean-eip.html)，您现在可以在方法名称中指定参数类型，以便Camel可以匹配您要使用的方法。

给出以下bean:

** **from("direct:start")

**    **.bean(MyBean.class, "hello(String)")

**    **.to("mock:result");

然后MyBean有2个名称为hello和times的重载方法。因此，如果我们想要使用具有2个参数的方法，我们可以在Camel路由中执行以下操作:

from("direct:start")

**    **.bean(MyBean.class, "hello(String,String)")

**    **.to("mock:result");

我们也可以使用通配符 *，所以我们可以如下去调用2个参数的方法

** **from("direct:start")

**    **.bean(MyBean.class, "hello(*,*)")

**    **.to("mock:result");

默认情况下，Camel将使用简单名称匹配类型名称，例如，将忽略任何前导包名称。但是，如果要使用FQN进行匹配，请指定FQN类型，Camel将使用该类型。因此，如果你有一个com.foo.MyOrder并且想要与FQN匹配，而**不是**简单的名称"MyOrder"，那么请遵循以下示例:

.bean(OrderService.class, "doSomething(com.foo.MyOrder)")

Camel当前仅支持使用**方法选项**或**类型限定符**两种参数绑定方式。您**不能同时**使用两者，例如

** **doSomething(com.foo.MyOrder ${body}, boolean ${header.high})

这可能在将来会在新版中提供改进。

# 18. **参数绑定注解**

**camel-core**

下面的注解是**camel-core****的**一部分，因此不需要**camel-spring**或spring。这些注解可以与[Bean](https://camel.apache.org/components/latest/bean-component.html) component一起使用，也可以在[DSL中](https://camel.apache.org/manual/latest/dsl.html)调用bean时使用。

Annotations可用于定义[表达式](https://camel.apache.org/manual/latest/expression.html)或在调用bean方法时从[Message中](https://camel.apache.org/manual/latest/message.html)提取各种header、属性、有效负载(有关如何调用bean方法的更多详细信息，请参阅[Bean集成](https://camel.apache.org/manual/latest/bean-integration.html))，同时有助于消除调用哪个方法的歧义。

如果没有使用注解，则Camel假定单个参数是消息体。然后，Camel将使用[Type Converter](https://camel.apache.org/manual/latest/type-converter.html)机制将表达式值转换为实际的参数类型。

核心注解如下


| **注解**                           | **含义**                                                                                                                                                                  | **参数**         |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| org.apache.camel.Body              | 绑定到inbound message body                                                                                                                                                |                  |
| org.apache.camel.ExchangeException | 绑定到Exchange上的Exception                                                                                                                                               |                  |
| org.apache.camel.Header            | 绑定到inbound message header                                                                                                                                              | Header字符串名称 |
| org.apache.camel.Headers           | 绑定到inbound message headers的Map                                                                                                                                        |                  |
| org.apache.camel.OutHeaders        | 绑定到 outbound message headers的Map                                                                                                                                     |                  |
| org.apache.camel.Property          | 绑定到exchange上命名的属性                                                                                                                                                | 属性的字符串名称 |
| org.apache.camel.Properties        | 绑定到exchange上的属性map                                                                                                                                                 |                  |
| org.apache.camel.Handler           | 不是作为类型参数的一部分，放在这里，只是着重说明在Camel中有这个注解。详细请查阅[Bean Binding中](https://camel.apache.org/manual/latest/bean-binding.html)以了解更多信息。 |                  |

使用注解@Header，@Headers，@OutHeaders和@Properties可以绑定到后台java.util.Map，以便直接更改Map的内容，例如使用put方法添加新entity实体。有关此类示例，请参见OrderService类 [Exception](https://camel.apache.org/manual/latest/exception-clause.html)部分，您可以使用@Header("myHeader")或@Property("myProperty")获取java.util.Map的内对应的value值。

## 18.1. **例**

在下面的这个例子中，我们有一个@Consume注解的consumer，(像消息驱动里一样)它消费来自activemq队列的JMS消息。我们使用@Header和@Body参数绑定注解将JMSMessage绑定到方法参数上。

public class Foo {

**    **@Consume(uri = "activemq:my.queue")

**    **public void doSomething(@Header("JMSCorrelationID") String correlationID, @Body String body) {

**        **// process the inbound message here

**    **}

}

在上面，Camel将提取Message.getJMSCorrelationID()的值，然后使用[Type Converter](https://camel.apache.org/manual/latest/type-converter.html)将值调整为参数的类型(如果需要) - 它将为**correlationID**参数注入参数值。然后，消息的有效负载将转换为String并注入**body**参数。

如果您不想使用@Consume注解，则不一定需要使用@Consume注解，因为您也可以使用Camel [DSL](https://camel.apache.org/manual/latest/dsl.html)来路由到bean的方法。

## 18.2. **使用DSL调用****Bean****方法**

这是另一个不使用[POJO](https://camel.apache.org/manual/latest/pojo-consuming.html) consume注解但是使用[DSL](https://camel.apache.org/manual/latest/dsl.html)将消息路由到bean方法的示例

public class Foo {

**    **public void doSomething(@Header("JMSCorrelationID") String correlationID, @Body String body) {

**        **// process the inbound message here

**    **}

}

然后路由DSL看起来像这样

from("activemq:someQueue").

**  **to("bean:myBean");

这里将在[](https://camel.apache.org/manual/latest/registry.html)[Registry](https://camel.apache.org/manual/latest/registry.html)中查找**myBean**(例如JNDI或Spring ApplicationContext)，然后将使用消息体来确定要调用的方法。

如果你想显式调用，可以用如下方法

from("activemq:someQueue").

**  **to("bean:myBean?methodName=doSomething");

在这里，我们有一个漂亮的例子，向你展示一些Camel的强大力量。您可以将注解与正常参数混合匹配，因此我们可以将此示例与注解和Exchange一起使用:

**    **public void doSomething(@Header("user") String user, @Body String body, Exchange exchange) {

**        **exchange.getIn().setBody(body + "MyBean");

**    **}

## 18.3. **基于注****解****的表达语言**

使用[Bean Integration](https://camel.apache.org/manual/latest/bean-integration.html)时，您还可以使用Camel支持的任何[语言](https://camel.apache.org/manual/latest/languages.html)将表达式绑定到方法参数。例如，您可以使用以下任何注解:


| **注解**                                 | **描述**                                                                            |
| ---------------------------------------- | ----------------------------------------------------------------------------------- |
| org.apache.camel.language.Bean           | 注入[Bean](https://camel.apache.org/components/latest/bean-language.html)表达式     |
| org.apache.camel.language.Constant       | 注入[常量](https://camel.apache.org/manual/latest/constant-language.html)表达式     |
| org.apache.camel.builder.script.Groovy   | 注入[Groovy](https://camel.apache.org/components/latest/groovy-language.html)表达式 |
| org.apache.camel.Header                  | 注入header表达式                                                                    |
| org.apache.camel.language.mvel.MVEL      | 注入[MVEL](https://camel.apache.org/components/latest/mvel-language.html)表达式     |
| org.apache.camel.language.ognl.OGNL      | 注入[OGNL](https://camel.apache.org/components/latest/ognl-language.html)表达式     |
| org.apache.camel.language.Simple         | 注入一个Simple表达式                                                                |
| org.apache.camel.language.XPath          | 注入[XPath](https://camel.apache.org/components/latest/xpath-language.html)表达式   |
| org.apache.camel.component.xquery.XQuery | 注入[XQuery](https://camel.apache.org/components/latest/xquery-language.html)表达式 |

### 18.3.1. **例**

public class Foo {

**    **@MessageDriven(uri = "activemq:my.queue")

**    **public void doSomething(@XPath("/foo/bar/text()") String correlationID, @Body String body) {

**        **// process the inbound message here

**    **}

}

**[[ParameterBindingAnnotations-Advancedexampleusing @ Bean]] ====使用@Bean的高级示例**

使用org.apache.camel.language/Bean.adoc[@Bean]绑定注解的示例，您可以在其中使用[POJO](https://camel.apache.org/components/latest/bean-component.html)，而且您可以在其中执行任何您喜欢的Java代码:

public class Foo {

**    **@MessageDriven(uri = "activemq:my.queue")

**    **public void doSomething(@Bean("myCorrelationIdGenerator") String correlationID, @Body String body) {

**        **// process the inbound message here

**    **}

}

然后我们可以使用id为**myCorrelationIdGenerator**的spring bean 来对id编程。

public class MyIdGenerator {

**    **private UserManager userManager;

**    **public String generate(@Header(name = "user") String user, @Body String payload) throws Exception {

**       **User user = userManager.lookupUser(user);

**       **String userId = user.getPrimaryId();

**       **String id = userId + generateHashCodeForPayload(payload);

**       **return id;

**   **}

}

这个[POJO](https://camel.apache.org/components/latest/bean-component.html) MyIdGenerator有一个public方法，该方法有两个参数，分别使用了@Header和@Body注解，以帮助Camel从正在处理的Exchange消息中知道要绑定的内容。

当然，如果你只是想实例化个简单的id生成器，就不需要这么复杂。这里只是想说明可以在任何地方使用[Bean Binding](https://camel.apache.org/manual/latest/bean-binding.html)注解。

public class MySimpleIdGenerator {

**    **public static int generate()  {

**       **// generate a unique id

**       **return 123;

**   **}

}

最后我们只需要记住在Spring [注册表中](https://camel.apache.org/manual/latest/registry.html)注册我们的bean :

<bean id="myCorrelationIdGenerator" class="com.mycompany.MySimpleIdGenerator"/>

### 18.3.2. **使用**[**G****roovy****的**](https://camel.apache.org/components/latest/groovy-language.html)**示例**

在此示例中，我们有一个Exchange，其中包含存储在header中的User对象。此User对象具有获取某些用户信息的方法。我们希望使用[Groovy](https://camel.apache.org/components/latest/groovy-language.html)注入一个表达式，该表达式将用户的全名提取并拼接到fullName参数中。

**    **public void doSomething(@Groovy("$request.header['user'].firstName $request.header['user'].familyName) String fullName, @Body String body) {

**        **// process the inbound message here

**    **}

Groovy支持GStrings，它就像一个模板，我们可以插入$占位符，之后将由Groovy编译运行。

# 19. **Pojo****生产**

有两种不同的方法可以从POJO 向任何Camel Endpoint发送消息。

[[POJOProducing- @EndpointInject]] = Via @EndpointInject

要允许从POJO发送消息，您可以使用org.apache.camel.EndpointInject注解。这将注入一个org.apache.camel.ProducerTemplate的bean，以便bean可以参与消息交换。

示例:向ActiveMQ队列**foo.bar**发送消息:

public class Foo {

**  **@EndpointInject(uri="activemq:foo.bar")

**  **ProducerTemplate producer;

**  **public void doSomething() {

**    **if (whatever) {

**      **producer.sendBody("<hello>world!</hello>");

**    **}

**  **}

}

这样做的缺点是你的代码现在依赖于Camel API **ProducerTemplate**。下一节将介绍如何删除此依赖项。


|  | 请参阅[POJO Consuming](https://camel.apache.org/manual/latest/pojo-consuming.html)，了解如何使用Endpoint注解bean的成员变量，例如，注解为 **@Produce**，**@EndpointInject**的bean如何使用其**property**。 |
| - | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

[[POJOProducing-HidingtheCamelAPIsFromYourCodeUsing @ Produce]] ==隐藏代码中的Camel API @Produce

接下来我们介绍从应用程序代码中[隐藏中间件](https://camel.apache.org/manual/latest/hiding-middleware.html) API的方法。可以使用**@Produce**设置注入点(位置在成员变量或其setter方法)，在注入点上可以使用**ProducerTemplate****或**业务逻辑中由你定义的某个interface。例:

public interface MyListener {

**    **String sayHello(String name);

}

public class MyBean {

**    **@Produce(uri = "activemq:foo")

**    **protected MyListener producer;

**    **public void doSomething() {

**        **// lets send a message

**        **String response = producer.sayHello("James");

**    **}

}

在这里，Camel将自动通过**@Produce**注入智能客户端代理，同时它也是一个**MyListener**实例。当我们在这个interface上调用方法时，方法调用被转换为一个对象，并使用Camel [Spring Remoting](https://camel.apache.org/manual/latest/spring-remoting.html)机制将它发送到Endpoint - 在这种情况下，[ActiveMQ](https://camel.apache.org/components/latest/activemq-component.html) Endpoint指向队列**foo**; 然后调用者阻塞等待响应。

如果要进行异步消息发送，则[在注入点上](https://camel.apache.org/manual/latest/using-exchange-pattern-annotations.html)使用[@InOnly注](https://camel.apache.org/manual/latest/using-exchange-pattern-annotations.html)解。

# 20. **Pojo****消费**

要消费消息，请使用org.apache.camel.Consume注解将bean的某方法标记为consumer方法。注解的uri定义要使用的Camel Endpoint。

例如，我们调用onCheese()方法，使用[ActiveMQ](https://camel.apache.org/components/latest/activemq-component.html)的inbound JMS的String消息体，在cheese队列上调用该方法，这将使用[Type Converter](https://camel.apache.org/manual/latest/type-converter.html)将JMS ObjectMessage或BytesMessage转换为String - 或者只使用JMS中的TextMessage

public class Foo {

**  **@Consume(uri="activemq:cheese")

**  **public void onCheese(String name) {

**    **...

**  **}

}

然后通过[bean绑定](https://camel.apache.org/manual/latest/bean-binding.html)，将inbound[消息](https://camel.apache.org/manual/latest/message.html)转换到方法的参数列表。

这样做基本上创建了一个看起来像这样的router

from(uri).bean(theBean, "methodName");

**使用多个CamelContext时**

当你使用超过1个[CamelContext时，](https://camel.apache.org/manual/latest/camelcontext.html)你最终可能会创建一个[POJO** **Consuming](https://camel.apache.org/manual/latest/pojo-consuming.html) ; 因此，使用**@Consume**的context选项，允许你通过ID/名称指定使用哪个[CamelContext](https://camel.apache.org/manual/latest/camelcontext.html)。

## 20.1. **使用C****ontext****选项****选择****某个C****amelContext**

请参阅上面的警告。

您可以使用context选项指定consumer应该只应用到哪个[CamelContext](https://camel.apache.org/manual/latest/camelcontext.html)。例如:

**  **@Consume(uri="activemq:cheese", context="camel-1")

**  **public void onCheese(String name) {

上面的consumer只能为具有id =camel-1 的[CamelContext](https://camel.apache.org/manual/latest/camelcontext.html)创建。您在XML结点中设置如下:

<camelContext id="camel-1" ...>

## 20.2. **使用显式路由**

在数量众多的Endpoint或者在许多不同环境下的复杂router中，如果要调用bean方法，可以使用普通的router [DSL](https://camel.apache.org/manual/latest/dsl.html)或[Spring](https://camel.apache.org/manual/latest/spring.html) XML配置文件。

例如

from(uri).beanRef("myBean", "methodName");

然后，它将在[Registry中](https://camel.apache.org/manual/latest/registry.html)查找并找到bean并调用给定的bean名称。(您可以省略方法名称，Camel根据方法注解和body类型找出正确的调用方法)。

## 20.3. **使用B****ean** **E****ndpoint**

您始终可以使用bean Endpoint

from(uri).to("bean:myBean?method=methodName");

## 20.4. **使用属性定义****E****ndpoint**

**自Camel 2.11起可用**

注解@Consume、@Produce、@EndpointInject现在提供了一个property属性，您可以使用该属性将Endpoint定义为bean的属性。然后Camel将使用getter方法访问该属性。

**适用于****以上三个注解**

下面的解释适用于所有三个注解，例如@Consume、@Produce和@EndpointInject

例如

public class MyService {

**  **private String serviceEndpoint;

**  **public void setServiceEndpoint(String uri) {

**     **this.serviceEndpoint = uri;

**  **}

**  **public String getServiceEndpoint() {

**     **return serviceEndpoint

**  **}

**  **@Consume(property = "serviceEndpoint")

**  **public void onService(String input) {

**     **...

**  **}

}

MyService bean具有一个名为serviceEndpoint的属性，该属性具有getter/setter。现在我们想要将bean用于[POJO Consuming](https://camel.apache.org/manual/latest/pojo-consuming.html)，因此我们在onService方法中使用@Consume。请注意我们如何使用property = "serviceEndpoint来配置具有端点url的属性。

如果在Spring XML或Blueprint中定义bean，则可以按如下方式配置属性:

<bean id="myService" class="com.foo.MyService">

**  **<property name="serviceEndpoint" value="activemq:queue:foo"/>

</bean>

这允许您使用任何标准IoC风格配置bean。

Camel提供了一个命名约定，允许您不必明确命名该属性，隐式指定。

Camel使用以下算法来查找getter方法。该方法必须是getXXX方法。

1. 如果显式给定，请使用给定属性名称。
2. 如果未配置属性名称，则使用方法名称。
3. 尝试获取名称为 *Endpoint* 的属性(例如，使用Endpoint作为后缀)。
4. 尝试使用名称获取属性(例如，没有后缀)。
5. 如果属性名称以**on**开头，则忽略掉on**，**然后再次尝试步骤3和4。

所以在上面的例子中，我们可以将@Consume注解定义为

@Consume(property = "service")

public void onService(String input) {

现在，该属性被命名为"service"，然后匹配算法中的第3步，并让Camel调用getServiceEndpoint方法。

我们也可以省略属性，使其隐式

@Consume

public void onService(String input) {

现在Camel匹配第5个规则，忽略方法名的前缀**on**，并查到"service"的属性。因为有一个getServiceEndpoint方法，Camel将使用它。

**[[POJOConsuming-Whichapproachtouse？]] ==使用哪种方法？**

当使用单个定义明确的输入URI创建简单路由时，使用@Consume注解会更简单。

但是，如果您需要更复杂的路由或者需要从许多地方调用相同的bean方法，请参阅如上所示的路由[DSL](https://camel.apache.org/manual/latest/dsl.html)。

# 21. **错误处理器（****ErrorHandler****）**

Camel支持可插拔式[ErrorHandler](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/processor/ErrorHandler.html)方式来处理事件驱动Consumer的错误。同时可以配合在DSL中使用Exception子句直接定位错误进行处理。

有关介绍和背景材料，请参阅Camel中的错误处理。

**Exception子句**

使用错误处理器Error handler结合Exception子句是一个非常强大的组合。我们鼓励最终用户在您的错误处理策略中使用此组合。请参阅示例和Exception子句。

**最后使用try ... catch ...**

与错误处理相关的是[Try Catch Finally](https://camel.apache.org/manual/latest/try-catch-finally.html)，他们作为DSL的一部分您可以在route中直接使用。它基本上是对Java语言中常见try catch的模仿，但功能更强大。

Camel提供的开箱即用的实现是:

## 21.1. **在****非事务场景**

l DefaultErrorHandler是Camel中的默认错误处理器。此错误处理器不支持死信队列，它会将Exception传回给调用方，对调用方是透明的。它拥有一组有限的功能。

l 死信通道(Dead Letter Channel)支持将消息发送到死信Endpoint之前多次重发消息。

l NoErrorHandler禁用错误处理。

## 21.2. **在****事务场景**

l TransactionErrorHandler是Camel中用于事务路由的默认错误处理器。请参阅Transactional Client EIP模式。

l 错误处理器可以在DSL中，应用于整个规则集或特定的路由规则，如下一个示例所示。错误处理规则会在单个RouteBuilder中的每个路由规则上继承。

## 21.3. **错误处理****器简介**

### 21.3.1. **默认错误处理器-****D****efault****E****rror****H****andler**

DefaultErrorHandler是Camel中的默认错误处理器。与[死信通道](https://camel.apache.org/manual/latest/dead-letter-channel.html)不同，它没有任何	死信队列，并且默认情况下**不**处理异常。

### 21.3.2. **死信****通****道**

死信通道将使用1秒延迟重新发送6次，如果交换失败则将记录日志设为ERROR级别。

您可以配置要使用的默认死信Endpoint:

在Spring DSL中配置如下

<bean id="deadLetterErrorHandler" class="org.apache.camel.builder.DeadLetterChannelBuilder">

**  **<property name="deadLetterUri" value="log:dead"/>

</bean>

<camelContext errorHandlerRef="deadLetterErrorHandler" xmlns="http://camel.apache.org/schema/spring">

**  **...

</camelContext>

或者从**Camel 2.3.0开始**

<camel:errorHandler id="deadLetterErrorHandler" type="DeadLetterChannel" deadLetterUri="log:dead">

<camel:camelContext errorHandlerRef="deadLetterErrorHandler">

**  **...

[/camel:camelContext](/camel:camelContext)

### 21.3.3. **禁用****错误处理****器**

不需要错误处理器可以设置禁用，如下。

errorHandler(noErrorHandler());

或者在Spring DSL中

<bean id="noErrorHandler" class="org.apache.camel.builder.NoErrorHandlerBuilder"/>

<camelContext errorHandlerRef="noErrorHandler" xmlns="http://camel.apache.org/schema/spring">

**  **...

</camelContext>

或者从**Camel 2.3.0开始**

<camel:errorHandler id="noErrorHandler" type="NoErrorHandler"/>

<camel:camelContext errorHandlerRef="noErrorHandler">

**  **...

[/camel:camelContext](/camel:camelContext)

### 21.3.4. **T****ransaction****E****rror****H****andler**

TransactionErrorHandler是Camel中用于事务路由的默认错误处理器。

**提示**:如果您使用**transacted** DSL将路由标记为事务**，**则Camel将自动使用TransactionErrorHandler。它将查找全局/每个route配置的错误处理器，并在其为TransactionErrorHandlerBuilder实例时使用它。否则，Camel将自动创建一个临时的TransactionErrorHandler，它会取代默认的错误处理器，这是约定的配置。

## 21.4. **错误处理****器的特性**

以下是错误处理器支持的特性细分:


| **特性**               | **支持的错误处理器**                                              |
| ---------------------- | ----------------------------------------------------------------- |
| 适用所有作用域         | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| onException            | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| onWhen                 | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| continued              | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| handled                | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| 自定义ExceptionPolicy  | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| useOriginalBody        | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| retryWhile             | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| onRedelivery           | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| RedeliveryPolicy       | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| asyncDelayedRedelivery | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| redeliverWhileStopping | DefaultErrorHandler，TransactionErrorHandler，Dead Letter Channel |
| 死信队列               | Dead Letter Channel                                               |
| onPrepareFailure       | DefaultErrorHandler，Dead Letter Channel                          |

有关上述某些功能的文档，请参阅Exception Clause文档。

## 21.5. **作用域**

错误处理器的作用域为

l 全局(在RouteBuilder内部)。

l 每条route。

以下示例显示了如何注册全局错误处理器:

RouteBuilder builder = new** **RouteBuilder() {

**    **public void configure() {

**        **errorHandler(deadLetterChannel("seda:error"));

**        ***// here is our regular route*

**        **from("seda:a").to("seda:b");

**    **}

};

以下示例显示如何注册特定于route范围内的错误处理器

RouteBuilder builder = new** **RouteBuilder() {

**    **public void configure() {

**        ***// this route is using a nested error handler*

**        **from("seda:a")

**            ***// here we configure the error handler*

**            **.errorHandler(deadLetterChannel("seda:error"))

**            ***// and we continue with the routing here*

**            **.to("seda:b");

**        ***// this route will use the default error handler*

**        **from("seda:b").to("seda:c");

**    **}

};

## 21.6. **基于S****pring****的配置**

**Java DSL与Spring DSL**错误处理器配置上略有不同。Spring DSL更依赖于标准的Spring bean配置，而Java DSL则使用fluent构建。

错误处理器可以配置为spring bean其作用域如下:

l global(camelContext标签)

l 每条route(route标签)

l 或每个policy(policy/事务标签)

错误处理器需要配置errorHandlerRef属性。

**提示****:*****Error Handler层次结构***错误处理器是继承的，因此如果您只设置了一个全局错误处理器，那么它在任何地方都可以使用。但是您可以在route中用另一个错误处理器覆盖它。

### 21.6.1. **基于S****pring****的配置示例**

在此示例中，我们在路由route上配置一个[死信通道](https://camel.apache.org/manual/latest/dead-letter-channel.html)，该[通道](https://camel.apache.org/manual/latest/dead-letter-channel.html)最多应重新发送3次，并在重试之前稍微延迟一下。首先，我们在errorHandlerRefroute标签上使用errorHandlerRef 属性引用**myDeadLetterErrorHandler**。

然后我们配置**myDeadLetterErrorHandler**，这是我们的死信通道。这个配置是使用标准Spring的bean元素。

最后，我们还有另一个spring bean用于重新发送策略，我们可以配置重新发送多少次、延迟等选项。

从Camel 2.3.0开始，camel为Error Handler提供了一个客户化bean配置，你可以在这里找到这些例子。

## 21.7. **使用事务错误处理****器**

事务错误处理器基于spring事务。这需要使用camel-spring component。

请参阅Transactional Client，其中包含许多有关如何使用的示例以及使用此错误处理器的事务行为和配置。

# 22. **消息交换**

为了支持各种消息交换模式，例如单向事件消息和请求/回复消息，Camel使用具有**pattern** 成员变量的[Exchange](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Exchange.html)接口，该成员变量可以设置为**InOnly，**用于具有单向入站消息的事件消息，或者**InOut**用于请求/回复消息，请求/回复消息是具有入站和出站的消息。

# 23. **Exchange****模式**

有很多不同的消息交换模式可以在消息传递中使用。这个概念也在WSDL和JBI的MEP中得到了验证。

[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)(EIP)的常见例子是

l Request Reply，请求回复。

l Event Message (or one way)，事件消息(或单向)。

在Camel中，我们有一个[ExchangePattern](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/ExchangePattern.html)枚举常量，可以在Message Exchange 上的**exchangePattern**属性上配置，指定消息交换是单向事件消息(InOnly)还是请求应答消息交换(InOut)。

例如，要覆盖[JMS](https://camel.apache.org/components/latest/jms-component.html) Endpoint上的默认模式，您可以使用以下URI

jms:MyQueue?exchangePattern=InOut

# 24. **使用E****xchange****模式注解**

使用[POJO Producing](https://camel.apache.org/manual/latest/pojo-producing.html)或[Spring Remoting时，](https://camel.apache.org/manual/latest/spring-remoting.html)您可以调用通常默认为InOut for [Request Reply的方法](https://camel.apache.org/manual/latest/requestReply-eip.html)。那就是结果中有In和Out消息。通常，此调用操作是同步的，调用方将阻塞，直到服务器返回结果。

Camel具有扩展灵活的[Exchange模式](https://camel.apache.org/manual/latest/exchange-pattern.html)支持 - 因此您还可以支持[事件消息](https://camel.apache.org/manual/latest/event-message.html)模式以使用InOnly进行异步单向操作。这通常被称为"fire and forget"，例如发送JMS消息但不等待任何响应。

从1.5开始，Camel支持在常规Java方法、类或接口上指定消息交换模式的注解。

## 24.1. **指定I****n****o****nly****方法**

通常，默认的InOut是大多数情况下想要的，可以用InOnly注解启用。

public interface Foo {

**  **Object someInOutMethod(String input);

**  **String anotherInOutMethod(Cheese input);

**  **@InOnly

**  **void someInOnlyMethod(Document input);

}

上面的代码显示了一个接口上的三种方法; 前两个使用默认的InOut机制，但**someInOnlyMethod**使用InOnly注解将其指定为单向发送。

## 24.2. **类级别注****解**

您还可以使用类级别注解将接口中的所有方法默认为某种模式，例如

@InOnly

public interface Foo {

**  **void someInOnlyMethod(Document input);

**  **void anotherInOnlyMethod(String input);

}

注解将在父类或接口上被检测。例如，如果您为其创建了子类

public class MyFoo implements Foo {

**  **...

}

从Foo继承的方法将是InOnly。

## 24.3. **类级别注****解的****重载**

您可以在特定方法上重载类级别注解。一个常见的用例是，如果您有一个具有许多InOnly方法的类或接口，但您想要将其中一个或两个方法作为InOut

@InOnly

public interface Foo {

**  **void someInOnlyMethod(Document input);

**  **void anotherInOnlyMethod(String input);

**  **@InOut

**  **String someInOutMethod(String input);

}

在上面的Foo接口中，**someInOutMethod**将是InOut

## 24.4. **使用您自己的注****解**

您可能希望创建自己的注解来表示一组不同的元数据; 例如组合同步、并发和事务行为。

因此，您可以使用@Pattern注解，以默认您要使用的交换模式。

例如，假设我们要创建自己的注解@MyAsyncService

@Retention(RetentionPolicy.RUNTIME)

@Target({ElementType.TYPE, ElementType.METHOD})

// lets add the message exchange pattern to it

@Pattern(ExchangePattern.InOnly)

// lets add some other annotations - maybe transaction behaviour?

public @interface MyAsyncService {

}

现在我们可以使用这个注解，Camel将找出正确的交换模式......

public interface Foo {

**  **void someInOnlyMethod(Document input);

**  **void anotherInOnlyMethod(String input);

**  **@MyAsyncService

**  **String someInOutMethod(String input);

}

# 25. **表达式（****Expression****）**

然后，可以使用表达式和断言在DSL或XML配置中创建各种[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)，如接收者列表Recipient List。

为了支持动态规则，Camel支持使用各种不同语言的可插入[表达式](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Expression.html)策略。

## 25.1. **API**

如果在DSL之外想要创建自己的表达式，可以通过实现[Expression接口](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Expression.html)，或者复用其他构建器或者使用[ExpressionBuilder类](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/builder/ExpressionBuilder.html)。

### 25.1.1. **表达****式**

Camel Expression的API在org.apache.camel.Expression接口中定义，如下所示:

public** **interface Expression {

**    ***/***

* * Returns the value of the expression on the given exchange*
---

*     * **@param** exchange the message exchange on which to evaluate the expression*

*     * **@param** type the expected type of the evaluation result*

*     * **@return** the value of the expression** */*
**    **<T> T evaluate(Exchange exchange, Class<T> type);

}

### 25.1.2. **断言**

Camel的断言API在org.apache.camel.Predicate接口中定义，如下所示:

public** **interface Predicate {

**    ***/**** * Evaluates the predicate on the message exchange and returns true if this*
  * * exchange matches the predicate*
  ---

  *     * **@param** exchange the message exchange*
  *     * **@return** true if the predicate matches*
  * */*
  **    **boolean matches(Exchange exchange);

  }

  ## 25.2. **表达****式****语言**

  **Camel**开箱即用支持以下语言

  l [Bean Language](https://camel.apache.org/components/latest/bean-language.html) for using Java for expressions

  l [Constant](https://camel.apache.org/manual/latest/constant-language.html)

  l [Header](https://camel.apache.org/manual/latest/header-language.html)

  l [JSonPath](https://camel.apache.org/components/latest/jsonpath-language.html)

  l [Mvel](https://camel.apache.org/components/latest/mvel-component.html)

  l [OGNL](https://camel.apache.org/components/latest/ognl-language.html)

  l [Ref Language](https://camel.apache.org/manual/latest/ref-language.html)

  l ExchangeProperty / Property

  l Scripting Languages such as

  ○ BeanShell

  ○ JavaScript

  ○ [Groovy](https://camel.apache.org/components/latest/groovy-language.html)

  l [Simple](https://camel.apache.org/manual/latest/simple-language.html)

  ○ [File Language](https://camel.apache.org/manual/latest/file-language.html)

  l [Spring Expression Language](https://camel.apache.org/components/latest/spel-language.html)

  l [SQL](https://camel.apache.org/components/latest/sql-component.html)

  l Tokenizer

  l [XPath](https://camel.apache.org/components/latest/xpath-language.html)

  l [XQuery](https://camel.apache.org/components/latest/xquery-component.html)

  l [VTD-XML](https://github.com/camel-extra/camel-extra/blob/master/components/camel-vtdxml/src/main/docs/vtdxml-component.adoc)

  这些语言大多数也支持[基于注解的表达式语言](https://camel.apache.org/manual/latest/parameter-binding-annotations.html)( [Annotation Based Expression Language](https://camel.apache.org/manual/latest/parameter-binding-annotations.html))。

  ## 25.3. **在IDE中使用表达式**


  | **语言(S)**                                                                                                  | **要导入的Builder类**                                                                                                                                                                 |
  | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | 脚本语言，如BeanShell，JavaScript，[Groovy](https://camel.apache.org/components/latest/groovy-language.html) |                                                                                                                                                                                       |
  | [SQL](https://camel.apache.org/components/latest/sql-component.html)                                         |                                                                                                                                                                                       |
  | [XPath](https://camel.apache.org/components/latest/xpath-language.html)                                      | [org.apache.camel.builder.xml.XPathBuilder](https://github.com/apache/camel/blob/master/components/camel-xpath/src/main/java/org/apache/camel/language/xpath/XPathBuilder.java)       |
  | [XQuery](https://camel.apache.org/components/latest/xquery-component.html)                                   | [org.apache.camel.builder.saxon.XQueryBuilder](https://github.com/apache/camel/blob/master/components/camel-saxon/src/main/java/org/apache/camel/component/xquery/XQueryBuilder.java) |

  要在IDE中使用表达式和断言，您需要为要使用的语言导入静态的构建器类。

  # 26. **内容增强器（C****ontent** **E****nricher****）**

  Camel支持对消息内容的增强或丰富([Content Enricher](http://www.enterpriseintegrationpatterns.com/DataEnricher.html)) ，实现上采用了[消息转换器](https://camel.apache.org/manual/latest/message-translator.html)([Message Translator](https://camel.apache.org/manual/latest/message-translator.html))的[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)，通过使用route中支持这种模式的[Processor](https://camel.apache.org/manual/latest/processor.html)来对消息内容实现增强或丰富；或者另一种方式可以通过使用[enrich](https://camel.apache.org/manual/latest/content-enricher.html)  DSL(增强DSL)元素来对消息内容实现增强或丰富。

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps8.png)

  ## 26.1. **使用M****essage** **T****ranslator****或P****rocessor****进行内容****增强**

  **使用**[**Fluent Builders**](https://camel.apache.org/manual/latest/fluent-builders.html)

  您可以使用[模板](https://camel.apache.org/manual/latest/templating.html)（[Templating](https://camel.apache.org/manual/latest/templating.html)）组件从一个destination消费消息，期间可以使用[Velocity](https://camel.apache.org/components/latest/velocity-component.html)或[XQuery](https://camel.apache.org/components/latest/xquery-component.html)等对其内容进行转换，然后将结果发送到另一个目标destination。例如使用InOnly(单向消息传递)

  from("activemq:My.Queue")

  **    **.to("velocity:com/acme/MyResponse.vm")

  **    **.to("activemq:Another.Queue");

  如果您想使用InOut(请求 - 回复)来处理[ActiveMQ](https://camel.apache.org/components/latest/activemq-component.html)上**My.Queue**队列的请求，并使用模板生成的响应结果，那么将响应发送回JMSReplyTo目的地，您可以使用:

  from("activemq:My.Queue")

  **    **.to("velocity:com/acme/MyResponse.vm");

  这是一个使用[DSL](https://camel.apache.org/manual/latest/dsl.html)直接转换消息的简单示例

  from("direct:start").setBody(body().append(" World!")).to("mock:result");

  在下面这个例子中，我们使用显式Java 添加自己的[处理器](https://camel.apache.org/manual/latest/processor.html)([Processor](https://camel.apache.org/manual/latest/processor.html))

  **                **from("direct:start").process(new** **Processor() {

  **                    **public void process(Exchange exchange) {

  **                        **Message in = exchange.getIn();

  **                        **in.setBody(in.getBody(String.class) + " World!");

  **                    **}

  **                **}).to("mock:result");

  我们可以使用[Bean Integration](https://camel.apache.org/manual/latest/bean-integration.html)在任何bean上使用任何Java方法来充当转换器

  from("activemq:My.Queue")

  **    **.beanRef("myBeanName", "myMethodName")

  **    **.to("activemq:Another.Queue");

  有关此模式的其他示例，您可以查看以下其中一个JUnit测试

  l [TransformTest](https://github.com/apache/camel/blob/master/core/camel-core/src/test/java/org/apache/camel/processor/TransformTest.java)

  l [TransformViaDSLTest](https://github.com/apache/camel/blob/master/core/camel-core/src/test/java/org/apache/camel/processor/TransformViaDSLTest.java)

  **使用Spring XML**

  <route>

  **    **<from uri="activemq:Input"/>

  **    **<bean ref="myBeanName" method="doTransform"/>

  <to uri="activemq:Output"/>

  </route>

  ## 26.2. **使用****enrich****DSL元素进行内容****增强**

  Camel DSL内有两种风格的内容增强器(content enricher)

  l enrich

  l pollEnrich

  enrich，使用一个Producer来获取附加数据，它通常用于[请求/回复](https://camel.apache.org/manual/latest/requestReply-eip.html)消息传递，例如用于调用外部Web service。

  pollEnrich，使用[轮询消费者](https://camel.apache.org/manual/latest/polling-consumer.html)([Polling Consumer](https://camel.apache.org/manual/latest/polling-consumer.html)) 来获取附加数据。它通常用于[事件消息消息](https://camel.apache.org/manual/latest/event-message.html)传递，例如读取文件或下载[FTP](https://camel.apache.org/components/latest/ftp-component.html)文件。

  **对****Camel 2.15或更早版本 -** **当前****Exchange数据****不可用**

  pollEnrich或者enrich不支持对当前Exchange的任何数据访问，也就是说当轮询Exchange时你不能获取到任何消息头。例如，你无法获取到消息头Exchange.FILE_NAME的文件名，而我们假设的场景下pollEnrich仅能消费该文件，因此，你**必须**得在endpoint的URI中显式设置文件名。

  您可以使用[](https://camel.apache.org/manual/latest/recipientList-eip.html)[Recipient List](https://camel.apache.org/manual/latest/recipientList-eip.html)和动态端点，并在收件人列表上定义AggregationStrategy，而不是使用enrich，这样就可以像enrich一样工作。

  pollEnrich只接受一条消息作为响应。就是说如果增强原始消息，这条原始消息是通过增强器从seda(stage event driver architecture，分阶段的事件驱动架构)系统收集来的。那么将只有一条响应消息与原始消息聚合在一起。

  从**Camel 2.16**开始，rich和pollEnrich都支持动态端点，它使用[Expression](https://camel.apache.org/manual/latest/expression.html)来计算uri，允许使用来自当前最新版本[Exchange的](https://camel.apache.org/manual/latest/exchange.html)数据。换句话说，上面说的所述内容不再推荐使用，它只是能够正常运行。

  ### 26.2.1. **Enrich****选项**


  | **名称**                | **默认值** | **描述**                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
  | ----------------------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | uri                     |            | 增强内容的外部服务对应的endpoint uri。必须使用uri或ref。**重要提示****:**从Camel 2.16开始，此选项将被删除，您可以使用[Expression](https://camel.apache.org/manual/latest/expression.html)来配置uri，例如[Simple](https://camel.apache.org/manual/latest/simple-language.html)或[Constant](https://camel.apache.org/manual/latest/constant-language.html)或任何其他可以使用当前[Exchange中的](https://camel.apache.org/manual/latest/exchange.html)值动态计算uri的动态语言。  |
  | ref                     |            | 增强内容的外部服务对应的endpoint。必须使用uri或ref。**重要提示****:**从Camel 2.16开始，此选项将被删除，您可以使用[Expression](https://camel.apache.org/manual/latest/expression.html)来配置uri，例如[Simple](https://camel.apache.org/manual/latest/simple-language.html)或[Constant](https://camel.apache.org/manual/latest/constant-language.html)或任何其他可以使用当前[Exchange中的](https://camel.apache.org/manual/latest/exchange.html)值动态计算uri的动态语言。      |
  | expression              |            | **Camel** **2.16****:**强制必填。用于配置uri 的[Expression](https://camel.apache.org/manual/latest/expression.html)，例如[Simple](https://camel.apache.org/manual/latest/simple-language.html)或[Constant](https://camel.apache.org/manual/latest/constant-language.html)或可以使用当前[Exchange中的](https://camel.apache.org/manual/latest/exchange.html)值动态计算uri的任何其他动态语言。                                                                                |
  | strategyRef             |            | 指用于将来自外部服务的回复合并到单个传出消息中的[AggregationStrategy](https://github.com/apache/camel/blob/master/core/camel-api/src/main/java/org/apache/camel/AggregationStrategy.java)。默认情况下，Camel将使用外部服务的回复作为传出消息。从**Camel 2.12**开始，您还可以使用POJO AggregationStrategy，有关详细信息，请参阅" [Aggregate](https://camel.apache.org/manual/latest/aggregate-eip.html)["](https://camel.apache.org/manual/latest/aggregate-eip.html)页面。 |
  | strategyMethodName      |            | **Camel 2.12****:**当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。有关更多详细信息，请参阅" [](https://camel.apache.org/manual/latest/aggregate-eip.html)[Aggregate](https://camel.apache.org/manual/latest/aggregate-eip.html)"页面。                                                                                                                                                                                                          |
  | strategyMethodAllowNull | false      | **Camel 2.12****:**如果此选项是false，则在没有增强数据的情况下不调用聚合方法。如果此选项是true，则使用null值作为oldExchange(当没有增强数据时)，使用POJO作为AggregationStrategy有关更多详细信息，请参阅" [](https://camel.apache.org/manual/latest/aggregate-eip.html)[Aggregate](https://camel.apache.org/manual/latest/aggregate-eip.html)"页面。                                                                                                                          |
  | aggregateOnException    | false      | **Camel 2.14****:**如果此选项是false，则在检索增强数据的过程中抛出异常时，**不**使用聚合方法。设置此选项true允许最终用户在aggregate方法中对异常执行操作。例如，抑制异常或设置自定义消息体等。                                                                                                                                                                                                                                                                                |
  | shareUnitOfWork         | false      | **Camel 2.16****:**Shares the unit of work with the parent and the resource exchange。默认情况下，Enrich不会共享父交换和资源交换之间的工作单元。这意味着资源交换有自己独立的工作单元。有关更多信息和示例，请参阅[Splitter](https://camel.apache.org/manual/latest/split-eip.html)。                                                                                                                                                                                          |
  | cacheSize               |            | **Camel 2.16****:**允许为ProducerCache缓存生产者配置缓存大小，以便在rich中重用。默认情况下，将使用默认缓存大小为1000。将值设置为-1可以同时关闭所有缓存。                                                                                                                                                                                                                                                                                                                     |
  | ignoreInvalidEndpoint   | false      | **Camel 2.16****:**是否忽略无法解析的端点URI。如果禁用，Camel将抛出无效endpoint URI的异常。                                                                                                                                                                                                                                                                                                                                                                                  |

  confluenceTableSmall

  **使用** [**Fluent Builders**](https://camel.apache.org/manual/latest/fluent-builders.html)

  AggregationStrategy aggregationStrategy = ...

  from("direct:start")

  **    **.enrich("direct:resource", aggregationStrategy)

  **    **.to("direct:result");

  from("direct:resource") ...

  内容增强器(enrich)从资源endpoint查找要附加的数据，用以增强传入的消息(包含在原始交换中)。聚合策略用于组合原始交换和资源交换。AggregationStrategy.aggregate(Exchange, Exchange)方法的第一个参数对应于原始交换，第二个参数对应资源交换。资源endpoint的结果存储在资源交换的out消息中。下面是用于实现聚合策略的示例模板:

  public** **class ExampleAggregationStrategy implements AggregationStrategy {

  **    **public Exchange aggregate(Exchange original, Exchange resource) {

  **        **Object originalBody = original.getIn().getBody();

  **        **Object resourceResponse = resource.getIn().getBody();

  **        **Object mergeResult = ... *//* *组合原始消息体和资源响应消息体*

  **        **if** **(original.getPattern().isOutCapable()) {

  **            **original.getOut().setBody(mergeResult);

  **        **} else** **{

  **            **original.getIn().setBody(mergeResult);

  **        **}

  **        **return** **original;

  **    **}

  }

  使用此模板，原始交换可以是任何模式。由增强器创建的资源交换始终是in-out的交换，也就是请求/回复类型的交换。

  **使用Spring XML**

  Spring DSL中的相同示例

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:start"/>

  **        **<enrich strategyRef="aggregationStrategy">

  **            **<constant>direct:resource</constant>

  **        **</enrich>

  **        **<to uri="direct:result"/>

  **    **</route>

  **    **<route>

  **        **<from uri="direct:resource"/>

  **        **...

  </route>

  </camelContext>

  <bean id="aggregationStrategy" class="..." />

  ### 26.2.2. **聚合策略是可选的**

  聚合策略是可选的。如果你不提供它，Camel默认只使用从资源获得的消息体。

  from("direct:start")

  **    **.enrich("direct:resource")

  **    **.to("direct:result");

  在上面的路由中，发送到direct:result端点的消息将包含来自direct:resource的输出，我们没有做任何自定义聚合。

  而对于Spring DSL:

  <route>

  **    **<from uri="direct:start"/>

  **    **<enrich>

  **        **<constant>direct:resource</constant>

  **    **</enrich>

  <to uri="direct:result"/>

  </route>

  ### 26.2.3. **使用动态URIS**

  **自Camel 2.16起可用**

  从Camel 2.16开始，rich和pollEnrich支持最新版本[Exchange](https://camel.apache.org/manual/latest/exchange.html)的动态uris计算 。例如，要从[HTTP](https://camel.apache.org/components/latest/http-component.html) endpoint进行增强，其消息头的orderId作为HTTP URL的的一部分:

  from("direct:start")

  **    **.enrich().simple("http:myserver/$\{header.orderId}/order")

  **    **.to("direct:result");

  在XML DSL中

  <route>

  **    **<from uri="direct:start"/>

  **    **<enrich>

  **        **<simple>http:myserver/$\{header.orderId}/order</simple>

  **    **</enrich>

  <to uri="direct:result"/>

  </route>

  ## 26.3. **使用 ** **pollEnrich****内容****增强**

  pollEnrich工作方式和enrich一样，然而它在[轮询消费](https://camel.apache.org/manual/latest/polling-consumer.html)时采用的是如下3种方法的

  l receive

  l receiveNoWait

  l receive(timeout)

  ### 26.3.1. **pollEnrich****选项**


  | **名称**                | **默认值** | **描述**                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
  | ----------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | uri                     |            | 增强内容的外部服务对应的endpoint uri。你必须使用uri或ref。**重要提示****:**从Camel 2.16开始，此选项将被删除，您可以使用[Expression](https://camel.apache.org/manual/latest/expression.html)来配置uri，例如[Simple](https://camel.apache.org/manual/latest/simple-language.html)或[Constant](https://camel.apache.org/manual/latest/constant-language.html)或任何其他可以使用当前版本[Exchange中的](https://camel.apache.org/manual/latest/exchange.html)值动态计算uri的动态语言。 |
  | ref                     |            | 增强内容的外部服务对应的endpoint uri。你必须使用uri或ref。**重要提示****:**从Camel 2.16开始，此选项将被删除，您可以使用[Expression](https://camel.apache.org/manual/latest/expression.html)来配置uri，例如[Simple](https://camel.apache.org/manual/latest/simple-language.html)或[Constant](https://camel.apache.org/manual/latest/constant-language.html)或任何其他可以使用当前[Exchange中的](https://camel.apache.org/manual/latest/exchange.html)值动态计算uri的动态语言。     |
  | expression              |            | **Camel** **2.16****:**强制性。用于配置uri 的[Expression](https://camel.apache.org/manual/latest/expression.html)，例如[Simple](https://camel.apache.org/manual/latest/simple-language.html)或[Constant](https://camel.apache.org/manual/latest/constant-language.html)或可以使用当前[Exchange中的](https://camel.apache.org/manual/latest/exchange.html)值动态计算uri的任何其他动态语言。                                                                                       |
  | strategyRef             |            | 指用于将来自外部服务的回复合并到单个传出消息中的[AggregationStrategy](https://github.com/apache/camel/blob/master/core/camel-api/src/main/java/org/apache/camel/AggregationStrategy.java)。默认情况下，Camel将使用外部服务的回复作为传出消息。从**Camel 2.12**开始，您还可以使用POJO AggregationStrategy，有关详细信息，请参阅" [](https://camel.apache.org/manual/latest/aggregate-eip.html)[Aggregate](https://camel.apache.org/manual/latest/aggregate-eip.html)"页面。      |
  | strategyMethodName      |            | **Camel 2.12****:**当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。有关更多详细信息，请参阅" [](https://camel.apache.org/manual/latest/aggregate-eip.html)[Aggregate](https://camel.apache.org/manual/latest/aggregate-eip.html)"页面。                                                                                                                                                                                                               |
  | strategyMethodAllowNull | false      | **Camel 2.12****:**当使用POJO作为AggregationStrategy时，如果此选项是false，则在没有增强数据的情况下不使用聚合方法。如果此选项是true，则使用null值作为oldExchange(当没有增强数据时)。有关更多详细信息，请参阅" [聚合"](https://camel.apache.org/manual/latest/aggregate-eip.html)页面。                                                                                                                                                                                           |
  | timeout                 | -1         | 从外部服务轮询时的超时时间。有关超时的重要详细信息，请参阅下文。                                                                                                                                                                                                                                                                                                                                                                                                                  |
  | aggregateOnException    | false      | **Camel 2.14****:**如果此选项是false，则从丰富资源检索数据抛出异常时，**不**使用聚合方法。设置此选项true存在异常时允许最终用户在aggregate方法中控制要执行的操作。例如，抑制异常或设置自定义消息体等。                                                                                                                                                                                                                                                                             |
  | cacheSize               |            | **Camel 2.16****:**允许配置ConsumerCache缓存大小，缓存consumer以便在pollEnrich中重用。默认情况下，将使用默认缓存大小1000。将值设置为-1可以同时关闭缓存。                                                                                                                                                                                                                                                                                                                          |
  | ignoreInvalidEndpoint   | false      | **Camel 2.16****:**是否忽略无法解析的端点URI。如果禁用，Camel将抛出无效端点URI的异常。                                                                                                                                                                                                                                                                                                                                                                                            |

  **使用超时值****是个****好习惯**

  默认情况下Camel会使用receive。在有可用消息之前可能会阻塞。因此，建议始终提供超时值，以明确我们可能会等待消息，直到达到超时。

  如果没有数据，那么newExchange聚合策略就是null。

  您可以传入确定要使用方法的超时值:

  l 如果超时为-1或其他负数，则选择receive(**重要****:**receive如果没有消息，方法可能会阻塞)。

  l 如果超时为0则选择receiveNoWait。

  l 否则receive(timeout)被选中

  超时值以毫秒为单位。

  Camel 2.15或更早版本 - 禁止使用当前Exchange的数据

  pollEnrich不支持对当前最新的Exchange的任何数据访问，也就是说当轮询Exchange时你不能获取到任何消息头。例如，你无法获取到消息头Exchange.FILE_NAME的文件名，而我们假设的场景下pollEnrich仅能消费该文件，因此，你**必须**得在endpoint的URI中显式设置文件名。

  从**Camel 2.16**开始，rich和pollEnrich都支持动态端点，它使用[Expression](https://camel.apache.org/manual/latest/expression.html)来计算uri，允许使用来自当前最新版本[Exchange的](https://camel.apache.org/manual/latest/exchange.html)数据。换句话说，上面说的所有内容都不再适用，它只是能正常运行而已。

  ### 26.3.2. **例**

  在此示例中，我们从名为inbox/data.txt的文件加载内容来丰富消息。

  from("direct:start")

  **    **.pollEnrich("file:inbox?fileName=data.txt")

  **    **.to("direct:result");

  在XML DSL中，您可以:

  <route>

  **    **<from uri="direct:start"/>

  **    **<pollEnrich>

  **        **<constant>file:inbox?fileName=data.txt</constant>

  **    **</pollEnrich>

  <to uri="direct:result"/>

  </route>

  如果没有文件，则消息为空。我们可以使用超时来等待(因为可能一直等待)直到文件存在，或使用超时等待一段时间。

  例如，要等待最多5秒钟，您可以执行以下操作:

  <route>

  **    **<from uri="direct:start"/>

  **    **<pollEnrich timeout="5000">

  **        **<constant>file:inbox?fileName=data.txt</constant>

  **    **</pollEnrich>

  <to uri="direct:result"/>

  </route>

  ### 26.3.3. **使用动态URIS**

  **自Camel 2.16起可用**

  从Camel 2.16开始，enrich和pollEnrich支持使用基于当前最新版本[Exchange](https://camel.apache.org/manual/latest/exchange.html)信息动态URI计算 。例如，使用消息头指定[SEDA](https://camel.apache.org/components/latest/seda-component.html)队列名称的endpoint，其pollEnrich如下 :

  from("direct:start")

  **    **.pollEnrich()

  **    **.simple("seda:$\{header.name}")

  **    **.to("direct:result");

  在XML DSL中

  <route>

  **    **<from uri="direct:start"/>

  **    **<pollEnrich>

  **        **<simple>seda:$\{header.name}</simple>

  **    **</pollEnrich>

  <to uri="direct:result"/>

  </route>

  # 27. **注入（****inject****）**

  [注入器](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/spi/Injector.html)是任何IoC容器(如Spring)的可插拔策略，能够创建和依赖注入特定类型的对象。

  例如，如果您使用" [智能默认值控制反转( ](https://camel.apache.org/manual/latest/inversion-of-control-with-smart-defaults.html)[Inversion Of Control With Smart Defaults](https://camel.apache.org/manual/latest/inversion-of-control-with-smart-defaults.html))"模式来最小化XML依赖; 当通过META-INF/services设置其URI，Camel将自动发现并用来新建端点。您可以在Spring XML文件中显式配置每个Component和Endpoint; 或者让Camel找到默认值，然后使用Injector创建并注入其依赖项。

  举个例子; 考虑[JMS](https://camel.apache.org/components/latest/jms-component.html)组件。不需要显式地在Spring XML中配置JMS组件，只需在Spring XML中提供ConnectionFactory，注入器将使用它在实例化JmsComponent时正确地配置它。

  # 28. **拦截（****intercept****）**

  Camel中的 拦截功能支持对路由上Exchange 的拦截。

  Camel支持三种拦截器interceptor:1. intercept ，在路由中路由Exchange时拦截其每个处理步骤。
  2. interceptFrom，拦截路由中传入的Exchange。
  3. interceptSendToEndpoint， 当Exchange即将被发送到给定endpoint时进行拦截。


  这些拦截器支持以下功能:

  1. when，用于仅在某些条件下触发拦截器。
  2. stop，强制停止继续路由Exchange并将其标记为已成功完成。Camel默认**不停止**。
  3. skip，与interceptSendToEndpoint一起使用时将**跳过**，将跳过Exchange发送到原来期望的endpoint。Camel默认**不跳过**。
  4. afterUrl，与interceptSendToEndpoint一起使用时，允许Exchange在绕行到一个端点URL后，再将Exchange发送到原始端点。
  5. interceptFrom与interceptSendToEndpoint支持endpoint URI的匹配规则：明确的uri、通配符、正则表达式。见高级部分。
  6. 拦截的endpoint uri被存储为消息头Exchange.INTERCEPTED_ENDPOINT。

  stop通常都可以使用，它不需要与拦截器一起使用，您也可以在常规路由中使用它。

  在Exchange上，如果将Exchange.ROUTE_STOP属性设置为 "true"或Boolean.TRUE，您还可以指示Camel 继续路由消息。例如，您可以从POJO或Processor中的常规Java代码执行此操作。

  ## 28.1. **拦截**

  Intercept就像一个常见的拦截器，应用于Exchange在路由时经历的每个处理步骤。您在路由中定义的每个DSL关键字，都可以将其视为AOP。

  经典的Hello World示例如下:

  intercept().to("log:hello");

  from("jms:queue:order").to("bean:validateOrder").to("bean:processOrder");

  发生的事情是Exchange在每个处理步骤之前被拦截，也就是说以下步骤在执行前先被拦截

  l .to("bean:validateOrder")

  l .to("bean:processOrder")

  因此，在此示例中，我们的Exchange拦截两次。

  when谓词上也支持intercept，所以我们可以附加一个谓语只触发特定条件下的拦截。

  例如，在下面的示例中，我们只拦截消息体包含字符串字**Hello**:

  在下面的route中，我们希望当消息包含单词"Hello"时停止:

  ### 28.1.1. **使用****Spring** **DSL**

  Spring DSL中的同一个hello world示例将是:

  <camelContext ...>

  **    **<intercept>

  **        **<to uri="log:hello"/>

  **    **</intercept>

  **    **<route>

  **        **<from uri="jms:queue:order"/>

  **        **<to uri="bean:validateOrder"/>

  **        **<to uri="bean:handleOrder"/>

  </route>

  </camelContext>

  使用**when**谓词的示例将是:

  使用**when**和**stop**的示例将是:

  ## 28.2. **InterceptFrom**

  InterceptFrom用于在路由中拦截传入的Exchange(它拦截所有的from** **DSL)。这允许您为收到的Exchange执行一些自定义行为。您可以为给定的端点提供特定的URI，然后它仅适用于该特定路由。

  所以让我们从日志示例开始。我们想记录所有**传入的**请求，以便我们使用interceptFrom路由到[Log](https://camel.apache.org/components/latest/log-component.html)组件。由于proceed是默认的，则Exchange将继续它的路由，因此它将继续mock:first。

  您还可以附加谓词以仅在满足某些条件时触发。例如，在下面的路由中，我们会在向我们发送测试消息时进行拦截，因此我们可以在继续路由之前进行一些自定义处理:

  如果我们想要过滤掉某些消息，我们可以使用stop()来指示Camel停止继续路由Exchange:

  如果想要仅应用于特定端点，如下面示例中的**seda****:****bar**端点，我们可以这样做:

  ### 28.2.1. **使用****Spring** **DSL**

  拦截当然也可以使用Spring DSL，如下面的示例所示:

  **注意：**interceptFrom也支持stop，因此您可以从某些端点进行拦截，并停止原始路由，然后在其他地方进行路由。

  ## 28.3. **端点的拦截发送**

  当交换发送到被拦截的端点时，将触发端点的拦截发送。这允许您在将Exchange发送到原始目的地之前将Exchange路由绕行或执行某些自定义处理。您也可以跳过预定目标destination。默认情况下，Camel将在拦截的路由完成后发送到原始目标。并且作为常规拦截，您还可以定义when谓词，因此我们在when值为**true时**进行拦截。这允许您进行一些过滤，仅在满足某些条件时进行拦截。最后，您可以将Exchange发送到使用afterUrl选项的端点。您可以使用它来处理来自原始端点的响应。

  让我们从一个简单的例子开始，我们想要在Exchange发送到mock:foo时拦截:

  而这一次我们添加了谓词，所以只有当消息体是Hello World时我们才会拦截。

  要跳过发送到mock:foo端点，我们在路由的末尾中使用* skip() DSL来指定让Camel跳过发送到原始目标端点。

  **有条件的跳过**

  skipSendToEndpoint与when谓词的组合仅在when谓词匹配时才会发生，从而更自然的逻辑。

  interceptSendToEndpoint("mock:foo").skipSendToOriginalEndpoint()

  **    **.when(simple("${body} == 'Hello World'")

  **    **.to("log:intercepted");

  ### 28.3.1. **使用S****pring**** DSL**

  拦截端点当然也可以使用Spring DSL。

  第1个例子，我们从Spring DSL中的第1个例子开始:

  第2个例子，请注意我们如何利用[Simple](https://camel.apache.org/manual/latest/simple-language.html)语言做断言:

  第3个例子，使用skip，请注意skip和**interceptSendToEndpoint**标签上的属性skipSendToOriginalEndpoint一起设置:

  <camelContext ...>

  **    **<interceptSendToEndpoint uri="mock:foo" skipSendToOriginalEndpoint="true">

  **        **<when><simple>${body} == 'Hello World'</simple></when>

  **        **<to uri="log:intercepted"/>

  **    **</intercept>

  **    **<route>

  **        **<from uri="jms:queue:order"/>

  **        **<to uri="bean:validateOrder"/>

  **        **<to uri="bean:handleOrder"/>

  </route>

  </camelContext>

  [[Intercept-InterceptSendToEndpoint with afterUrl]] == InterceptSendToEndpoint with afterUrl

  拦截的消息发送到原始端点后，拦截器允许调用一个端点，这允许您处理来自原始端点的响应。例如，要记录从发送到所有JMS端点的request/response，可以执行以下操作：

  interceptSendToEndpoint("jms*").afterUrl("log:jms-reply")

  **    **.to("log:jms-request");

  在XML DSL中:

  <camelContext ...>

  **    **<interceptSendToEndpoint uri="jms*" afterUrl="log:jms-reply">

  **        **<to uri="log:jms-request"/>

  </intercept>

  </camelContext>

  ## 28.4. **Intercpt****的高级用法**

  interceptFrom和interceptSendToEndpoint支持以下给定的规则匹配顺序，用以匹配端点URI:

  l 匹配精确的URI名称。这是我们上面看到的例子。

  l 通过通配符匹配。

  l 通过正则表达式匹配。

  被拦截的真实端点的URI存储在消息头中，其key为Exchange.INTERCEPTED_ENDPOINT。

  这允许您在通过通配符匹配时获取此信息。然后你知道被拦截的真实端点并且可以做出相应的反应。

  ### 28.4.1. **通过通配符匹配**

  通过通配符匹配允许您匹配一系列端点或所有给定类型。例如，使用uri="file:*"将匹配所有基于file的端点。

  intercept("jms:*").to("log:fromjms");

  通配符*对给定端点进行匹配，给定文本与之匹配时，匹配所有字符。例如，您可以这样做:

  intercept("file://order/inbox/*").to("log:newfileorders");

  拦截从order/inbox收到的任何文件。

  ### 28.4.2. **通过正则表达式匹配**

  正则表达式匹配就像通配符匹配，只是用正则表达式作为替换。因此，如果我们想拦截来自JMS队列的传入黄金和白银消息，我们可以这样做:

  intercept("jms:queue:(gold|silver)").to("seda:handleFast");

  **关于interceptFrom和interceptSendToEndpoint的动态和静态行为**

  interceptSendToEndpoint是动态的，因此，如果构造了Camel在启动时不知道的动态URI，它也会触发。

  interceptFrom不是动态的，因为它只拦截在CamelContext中注册的路由的输入。 因此，如果您使用Camel API动态构造一个Consumer并消费一个Endpoint，则不会触发interceptFrom 。

  # 29. **控制反转智能默认值**

  控制反转是一种配置bean的强大工具，bean被简单管理并通过IoC容器注入其各种依赖。使用像Spring这样的IoC容器的缺点之一是，您通常需要配置大量的XML。

  控制反转使用智能默认值模式，尝试通过向系统提供内置的智能默认值来解决xml配置问题，这样您只需配置非默认值。

  例如，使用Camel配置CamelContext，通过使用一个XML元素创建灵活、可扩展的component和endpoint实例，并提供一个功能强大的类型转换器注册表

  <camelContext xmlns="http://activemq.apache.org/camel/schema/spring">

  </camelContext>

  如果明确要配置上下文; 可以用XML显式地表示component、endpoint或依赖对象; 但所有常见的默认设置都是为您配置在一起的。

  # 30. **JMX**

  ## 30.1. **使用JMX管理A****pache** **C****amel**

  Camel默认启用JMX仪表agent，Camel runtime通过VM中的MBeanServer实例创建和注册MBean的管理对象，这使得Camel用户能够立即获得单个processor级别的Camel route执行情况。

  支持的管理对象类型是[endpoint](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/management/mbean/ManagedEndpoint.html)，[rout](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/management/mbean/ManagedRoute.html)e，[service](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/management/mbean/ManagedService.html)和[processor](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/management/mbean/ManagedProcessor.html)。除了性能计数器属性外，其中一些管理对象还公开了生命周期操作。

  [DefaultManagementObjectNameStrategy](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/management/DefaultManagementObjectNameStrategy.html)是默认的命名策略，它用于构建MBean注册对象的名称。默认情况下，CamelNamingStrategy创建的对象名称使用org.apache.camel作为域名。可以通过Java VM系统属性配置MBean对象的自定义域名:

  -Dorg.apache.camel.jmx.mbeanObjectDomainName=your.domain.name

  或者，通过在Spring配置中的camelContext元素中添加一个jmxAgent元素:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<jmxAgent id="agent" mbeanObjectDomainName="your.domain.name"/>

  ...

  </camelContext>

  当它们同时出现时，Spring配置总是优先于系统属性。所有与JMX相关的配置都是如此。

  ## 30.2. **在C****amel****中禁用JMX****仪表****Agent**

  您可以通过设置Java VM系统属性来禁用JMX仪表代理，如下所示:

  -Dorg.apache.camel.jmx.disabled=true

  属性值类型视为boolean。

  或者，通过在Spring配置中的camelContext元素内添加元素jmxAgent:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<jmxAgent id="agent" disabled="true"/>

  ...

  </camelContext>

  或者在**Camel 2.1**中，如果使用纯Java，则更容易(不必使用JVM系统属性)，可以按如下方式禁用它:

  CamelContext camel = new** **DefaultCamelContext();

  camel.disableJMX();

  ## 30.3. **在****Java** **VM中查找MB****ean****S****erver**

  每个CamelContext都包含一个[InstrumentationAgent](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/spi/InstrumentationAgent.html)，被封装在[InstrumentationLifecycleStrategy](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/management/InstrumentationLifecycleStrategy.html)实例内。InstrumentationAgent是Camel MBean对象，可以通过register/unregister和[MBeanServer](http://java.sun.com/j2se/1.5.0/docs/api/javax/management/MBeanServer.html)无缝集成。多个CamelContexts/InstrumentationAgent可以共享一个MBeanServer。默认情况下，Camel运行时选择[MBeanServerFactory.findMBeanServer方法](#findMBeanServer(java.lang.String))返回的第一个MBeanServer，该[方法](#findMBeanServer(java.lang.String))使用默认域名org.apache.camel进行匹配。

  您可能也希望更改默认域名，以匹配已在应用程序中使用的MBeanServer实例。特别是，如果MBeanServer连接到JMX connector server，则无需在Camel中创建连接器服务器。

  您可以通过系统属性配置默认的匹配域名。

  -Dorg.apache.camel.jmx.mbeanServerDefaultDomain=<your.domain.name>

  或者，通过jmxAgent在Spring配置中的camelContext元素中添加一个元素:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<jmxAgent id="agent" mbeanServerDefaultDomain="your.domain.name"/>

  ...

  </camelContext>

  如果匹配不到MBeanServer则会创建一个新的，并根据上面提到的默认和自定义配置设置新的MBeanServer默认域名。

  当需要通过设置系统属性来管理JVM MBean时，也可以使用[PlatformMBeanServer](#getPlatformMBeanServer())。MBeanServer默认域名配置将被忽略，因为它不适用。


  |  | 从下一版本(1.5)开始，默认值usePlatformMBeanServer将更改为true。您可以将属性设置false从而禁用PlatformMBeanServer。 |
  | - | ----------------------------------------------------------------------------------------------------------------- |

  -Dorg.apache.camel.jmx.usePlatformMBeanServer=True

  或者，通过在Spring配置中的camelContext元素内添加jmxAgent元素:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<jmxAgent id="agent" usePlatformMBeanServer="true"/>

  ...

  </camelContext>

  ## 30.4. **创建****JMX RMI****connector server**

  JMX connector server允许JMX客户端(如JConsole)远程管理MBean;可以通过设置系统属性选择性地打开Camel JMX RMI connector server，并将Camel使用的MBeanServer附加到该connector server上。

  -Dorg.apache.camel.jmx.createRmiConnector=True

  或者，通过在Spring配置中的camelContext元素内添加jmxAgent元素:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<jmxAgent id="agent" createConnector="true"/>

  ...

  </camelContext>

  ## 30.5. **JMX****服务URL**

  默认的JMX服务URL具有以下格式:

  service:jmx:rmi:*///jndi/rmi://localhost:<registryPort>/<serviceUrlPath>*

  registryPort是RMI注册表端口，默认值为1099。

  您可以用系统属性设置RMI注册表端口。

  -Dorg.apache.camel.jmx.rmiConnector.registryPort=<port number>

  或者，通过在Spring配置中的camelContext元素内添加jmxAgent元素:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<jmxAgent id="agent" createConnector="true" registryPort="port number"/>

  ...

  </camelContext>

  serviceUrlPath是URL中的路径名，默认值是/jmxrmi/camel。

  您可以用系统属性设置服务URL路径。

  -Dorg.apache.camel.jmx.serviceUrlPath=<path>


  |  | **在Java中****的****ManagementAgent设置**在**Camel 2.4**以后，您还可以在ManagementAgent设置以下各种选项:context.getManagementStrategy().getManagementAgent().setServiceUrlPath("/foo/bar");context.getManagementStrategy().getManagementAgent().setRegistryPort(2113);context.getManagementStrategy().getManagementAgent().setCreateConnector(true); |
  | - | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

  或者，通过在Spring配置中的camelContext元素中添加一个jmxAgent元素:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<jmxAgent id="agent" createConnector="true" serviceUrlPath="path"/>

  ...

  </camelContext>

  默认情况下，RMI服务器对象侦听动态生成的端口，这可能是通过防火墙建立的连接的问题。在这种情况下，RMI连接端口可以由系统属性显式设置。

  -Dorg.apache.camel.jmx.rmiConnector.connectorPort=<port number>

  或者，通过在Spring配置中的camelContext元素内添加jmxAgent元素:

  <camelContext id="camel" xmlns="http://activemq.apache.org/camel/schema/spring">

  **  **<jmxAgent id="agent" createConnector="true" connectorPort="port number"/>

  ...

  </camelContext>

  设置连接器端口选项后，JMX服务URL将变为:

  service:jmx:rmi:*//localhost:<connectorPort>/jndi/rmi://localhost:<registryPort>/<serviceUrlPath>*

  ## 30.6. **Camel** **JMX支持的系统属性**


  | **属性名称**         | **值**          | **描述**                             |
  | -------------------- | --------------- | ------------------------------------ |
  | org.apache.camel.jmx | true 或 false | 如果是true，它将启用Camel中的jmx功能 |

  请参阅以下部分中的更多系统属性:jmxAgent Properties Reference。

  ## 30.7. **如何使用JMX进行身份验证**

  JDK中的JMX具有用于身份验证以及通过SSL使用安全连接的功能。您必须参考SUN文档了解如何使用它:

  l [http://java.sun.com/j2se/1.5.0/docs/guide/management/agent.html](http://java.sun.com/j2se/1.5.0/docs/guide/management/agent.html)

  l [http://java.sun.com/javase/6/docs/technotes/guides/management/agent.html](http://java.sun.com/javase/6/docs/technotes/guides/management/agent.html)

  ## 30.8. **应用程序服务器中的JMX**

  ### 30.8.1. **T****omcat****6**

  有关在Tomcat中启用JMX的详细信息，请参阅[此页面](http://tomcat.apache.org/tomcat-6.0-doc/monitoring.html)。

  简而言之，修改catalina.sh(或Windows中的catalina.bat)文件以设置以下选项...

  ** **set CATALINA_OPTS=-Dcom.sun.management.jmxremote** **\

  **    **-Dcom.sun.management.jmxremote.port=1099** **\

  **    **-Dcom.sun.management.jmxremote.ssl=false** **\

  **    **-Dcom.sun.management.jmxremote.authenticate=false

  ### 30.8.2. **JB****oss**** AS 4**

  默认情况下，JBoss创建自己的MBeanServer。要允许Camel暴露到同一服务器，请按照下列步骤操作:

  1. 告诉Camel使用PlatformMBeanServer(在Camel 1.5中默认为true)

  <camel:camelContext id="camelContext">

  **  **<camel:jmxAgent id="jmxAgent" mbeanObjectDomainName="org.yourname" usePlatformMBeanServer="true"  />

  [/camel:camelContext](/camel:camelContext)

  2. 改变你的JBoss实例以使用PlatformMBeanServer。通过编辑或添加以下属性。请参阅[http://wiki.jboss.org/wiki/JBossMBeansInJConsole](http://wiki.jboss.org/wiki/JBossMBeansInJConsole)JAVA_OPTSrun.shrun.conf -Djboss.platform.mbeanserver

  ### 30.8.3. **Websphere**

  修改mbeanServerDefaultDomain为WebSphere:

  <camel:jmxAgent id="agent" createConnector="true" mbeanObjectDomainName="org.yourname" usePlatformMBeanServer="false" mbeanServerDefaultDomain="WebSphere"/>

  ### 30.8.4. **ORACLE OC4J**

  Oracle OC4J J2EE应用程序服务器不允许Camel通过PlatformMBeanServer访问。在日志中Camel被记录为WARNING。

  xxx xx, xxxx xx:xx:xx xx org.apache.camel.management.InstrumentationLifecycleStrategy onContextStartWARNING: Could not register CamelContext MBean

  java.lang.SecurityException: Unauthorized access from application: xx to MBean: java.lang:type=ClassLoading        at oracle.oc4j.admin.jmx.shared.UserMBeanServer.checkRegisterAccess(UserMBeanServer.java:873)

  要解决此问题，您应该在Camel中禁用JMX代理，请参阅在Camel中禁用JMX仪表代理。

  ## 30.9. **高级JMX配置**

  Spring配置文件允许您配置Camel如何向JMX公开以进行管理。在某些情况下，您可以在此处指定更多信息，例如连接器的端口或路径名称。

  ## 30.10. **例****:**

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<jmxAgent id="agent" createConnector="true" registryPort="2000" mbeanServerDefaultDomain="org.apache.camel.test"/>

  **    **<route>

  **      **<from uri="seda:start"/>

  **      **<to uri="mock:result"/>

  </route>

  </camelContext>

  如果希望更改Java 5 JMX设置，可以使用各种[JMX系统属性](#properties)

  例如，可以通过设置以下环境变量(根据平台使用**set**或**export**)启用到Sun JMX连接器的远程JMX连接。这些设置只在Java 1.5+中配置Sun JMX连接器，而不是Camel默认创建的JMX连接器。

  SUNJMX=-Dcom.sun.management.jmxremote=true** **-Dcom.sun.management.jmxremote.port=1616** **\-Dcom.sun.management.jmxremote.authenticate=false** **-Dcom.sun.management.jmxremote.ssl=false

  (SUNJMX环境变量很容易被Camel的启动脚本用作JVM的附加启动参数。 如果直接启动Camel，则必须自己传递这些参数。)

  ## 30.11. **JmxAgent**** 属性参考**


  | **Spring property**               | **System property**                                    | **Default Value**                    | **Description**                                                                                                                                                                                                                                                                                                                                                       |
  | --------------------------------- | ------------------------------------------------------ | ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | id                                |                                                        |                                      | The JMX agent name, and it is not optional                                                                                                                                                                                                                                                                                                                            |
  | usePlatformMBeanServer            | org.apache.camel.jmx.usePlatformMBeanServer            | false, true - Release 1.5 or later | If true, it will use the MBeanServerfrom the JVM                                                                                                                                                                                                                                                                                                                    |
  | mbeanServerDefaultDomain          | org.apache.camel.jmx.mbeanServerDefaultDomain          | org.apache.camel                     | The default JMX domain of the MBeanServer                                                                                                                                                                                                                                                                                                                            |
  | mbeanObjectDomainName             | org.apache.camel.jmx.mbeanObjectDomainName             | org.apache.camel                     | The JMX domain that all object names will use                                                                                                                                                                                                                                                                                                                         |
  | createConnector                   | org.apache.camel.jmx.createRmiConnect                  | false                                | If we should create a JMX connector (to allow remote management) for the MBeanServer                                                                                                                                                                                                                                                                                 |
  | registryPort                      | org.apache.camel.jmx.rmiConnector.registryPort         | 1099                                 | The port that the JMX RMI registry will use                                                                                                                                                                                                                                                                                                                           |
  | connectorPort                     | org.apache.camel.jmx.rmiConnector.connectorPort        | -1 (dynamic)                         | The port that the JMX RMI server will use                                                                                                                                                                                                                                                                                                                             |
  | serviceUrlPath                    | org.apache.camel.jmx.serviceUrlPath                    | /jmxrmi/camel                        | The path that JMX connector will be registered under                                                                                                                                                                                                                                                                                                                  |
  | onlyRegisterProcessorWithCustomId | org.apache.camel.jmx.onlyRegisterProcessorWithCustomId | false                                | **Camel 2.0:** If this option is enabled then only processors with a custom id set will be registered. This allows you to filer out unwanted processors in the JMX console.                                                                                                                                                                                          |
  | statisticsLevel                   |                                                        | All / Default                        | **Camel 2.1:**Configures the level for whether performance statistics is enabled for the MBean. See section *Configuring level of granularity for performance statistics* for more details. From **Camel 2.16** onwards the All option is renamed to Default, and a new Extended option has been introduced which allows gathered additional runtime JMX metrics. |
  | includeHostName                   | org.apache.camel.jmx.includeHostName                   |                                      | **Camel 2.13:**Whether to include the hostname in the MBean naming. From Camel 2.13 onwards this is default false, where as in older releases its default true. You can use this option to restore old behavior if really needed.                                                                                                                                   |
  | useHostIPAddress                  | org.apache.camel.jmx.useHostIPAddress                  | false                                | **Camel 2.16:**Whether to use hostname or IP Address in the service url when creating the remote connector. By default the hostname will be used.                                                                                                                                                                                                                     |
  | loadStatisticsEnabled             | org.apache.camel.jmx.loadStatisticsEnabled             | false                                | **Camel 2.16:**Whether load statistics is enabled (gathers load statistics using a background thread per CamelContext).                                                                                                                                                                                                                                               |
  | endpointRuntimeStatisticsEnabled  | org.apache.camel.jmx.endpointRuntimeStatisticsEnabled  | true                                 | **Camel 2.16:**Whether endpoint runtime statistics is enabled (gathers runtime usage of each incoming and outgoing endpoints).                                                                                                                                                                                                                                        |

  ## 30.12. **为新路由配置是否总是注册mb****ean****，或者只是默认情况下注册mb****ean**

  **自Camel 2.7起可用**

  Camel现在提供2个设置来控制是否注册MBean


  | **选项**          | **默认** | **描述**                                                  |
  | ----------------- | -------- | --------------------------------------------------------- |
  | registerAlways    | false    | 如果启用，则始终注册MBean。                               |
  | registerNewRoutes | true     | 如果启用，则在CamelContext启动后添加新路由也将注册MBean。 |

  默认情况下，Camel启动时为配置的所有路由注册MBean。如果添加新路由之后，registerNewRoutes选项控制是否还应注册MBean。如果在不需要则可以禁用此功能。

  当使用动态EIP模式(例如具有唯一端点的接收者列表)时，请谨慎使用registerAlways选项。如果是这种情况的，则每个唯一端点及其相关services/producers也将被注册。由于注册表中MBeans数量的增加，这可能导致系统降级。MBean不是轻量级对象，因此消耗内存。

  ## 30.13. **使用JMX监控****Camel**

  ## 30.14. **使用JC****onsole****监控****Camel**

  如果您在与Camel相同的主机上运行JConsole，则CamelContext应该出现在本地连接列表中。

  要连接到远程Camel实例，或者本地进程未显示，请使用"远程进程"选项，然后输入URL。下面是一个localhost 示例

  URL:service:jmx:rmi:///jndi/rmi://localhost:1099/jmxrmi/camel。

  将Apache Camel与JConsole一起使用:

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps9.jpg)

  ## 30.15. **注册了哪些****e****ndpoint**

  在**Camel 2.1**以后，**只有** singleton端点被注册，因为在使用数千或数百万个端点的情况下，非单例的开销很大。使用接收者列表EIP或ProducerTemplate发送大量消息时就会发生这种情况。

  ## 30.16. **注册了哪些****Processor**

  Apache Camel在路由中开箱即用的所有Processor都已注册(EIP，消费者和生产者)。

  ## 30.17. **如何使用****JMX NotificationListener****监听****Camel****事件？**

  Camel通知事件给出了正在发生事情的粗略概述。您可以从上下文和端点查看生命周期事件，您可以看到正在接收和发送到端点的交换。

  从**Camel 2.4，**您可以使用自定义JMX NotificationListener来监听camel事件。

  首先，您需要在启动CamelContext之前设置JmxNotificationEventNotifier:

  *// Set up the JmxNotificationEventNotifier*

  notifier = new** **JmxNotificationEventNotifier();

  notifier.setSource("MyCamel");

  notifier.setIgnoreCamelContextEvents(true);

  notifier.setIgnoreRouteEvents(true);

  notifier.setIgnoreServiceEvents(true);

  CamelContext context = new** **DefaultCamelContext(createRegistry());

  context.getManagementStrategy().addEventNotifier(notifier);

  其次，您可以注册您的监听器以监听事件:

  *// register the NotificationListener*

  ObjectName on = ObjectName.getInstance("org.apache.camel:context=camel-1,type=eventnotifiers,name=JmxEventNotifier");

  MyNotificationListener listener = new** **MyNotificationListener();

  context.getManagementStrategy().getManagementAgent().getMBeanServer().addNotificationListener(on,

  **    **listener,

  **    **new** **NotificationFilter() {

  **        **private** **static** **final** **long** **serialVersionUID = 1L;

  **        **public boolean isNotificationEnabled(Notification notification) {

  **            **return** **notification.getSource().equals("MyCamel");

  **        **}

  **    **}, null);

  ## 30.18. **使用****Tracer** **MB****ean****进行细粒度跟踪**

  除了上面的粗粒度通知，**Camel 2.9.0还**支持JMX Notification用于细粒度跟踪事件。

  这些可以在Tracer MBean中找到。 要激活细粒度跟踪，首先需要在上下文或路由上激活跟踪。

  这可以在配置上下文时或在上下文/路由MBean上完成。

  第二步，您必须在跟踪器上设置jmxTraceNotifications属性为true。这同样可以在配置上下文时或在Tracer MBean运行时上完成。

  现在，您可以使用JConsole在Tracer MBean上注册TraceEvent Notifications。路由上的每一步都会有一个通知，包含所有交换和消息详细信息:

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps10.jpg)

  ## 30.19. **将JMX用于您自己的****Camel****代码**

  ## 30.20. **注册您自己的托管****E****ndpoint**

  **从Camel 2.0开始提供**
  您可以使用Spring托管注解@ManagedResource装饰自己的Endpoint，以允许在Camel MBeanServer中注册它们，从而使JMX访问您的自定义MBean。


  |  | 在**Camel 2.1中，**我们已将此更改为仅应用于Endpoint，您还需要实现org.apache.camel.spi.ManagementAware接口。稍后会详细介绍。 |
  | - | --------------------------------------------------------------------------------------------------------------------------- |

  例如，我们有以下自定义Endpoint，我们定义了一些要管理的选项:

  @ManagedResource(description = "Our custom managed endpoint")

  public** **class CustomEndpoint extends MockEndpoint implements ManagementAware<CustomEndpoint> {

  **    **public CustomEndpoint(final String endpointUri, final Component component) {

  **        **super(endpointUri, component);

  **    **}

  **    **public Object getManagedObject(CustomEndpoint object) {

  **        **return** **this;

  **    **}

  **    **public boolean isSingleton() {

  **        **return** **true;

  **    **}

  **    **protected String createEndpointUri() {

  **        **return** **"custom";

  **    **}

  **    **@ManagedAttribute

  **    **public String getFoo() {

  **        **return** **"bar";

  **    **}

  **    **@ManagedAttribute

  **    **public String getEndpointUri() {

  **        **return** **super.getEndpointUri();

  **    **}

  }

  **注意:**从**Camel** **2.9**起，鼓励使用org.apache.camel.api.management包的@ManagedResource，@ManagedAttribute以及@ManagedOperation。这允许您的自定义代码不依赖于Spring JAR。

  ## 30.21. **编写自己的托管服务**

  **自Camel 2.1起可用**

  Camel现在提供在注册管理服务时使用自己的MBean。这意味着你可以开发一个自定义的Camel组件，让它以MBean公开暴露给Endpoint、消费者、生产者等。你需要做的就是实现接口org.apache.camel.spi.ManagementAware并返回Camel应该使用的托管对象。

  在你认为JMX API非常痛苦和糟糕之前，你是对的。幸运的是我们Spring创建了一系列注解，您可以用它们来导出现有bean的管理。这意味着，你经常使用ManagementAware接口的getManagedObject方法以返回this。有关示例，请参阅上面的代码示例CustomEndpoint。

  现在在**Camel 2.1中，**你可以为Camel注册管理的所有对象执行此操作，这些对象相当多，但并不是全部。

  对于未实现ManagementAware接口的服务，Camel将回退到使用下表中定义的默认包装器:


  | **类型**     | **MBean wrapper**   |
  | ------------ | ------------------- |
  | CamelContext | ManagedCamelContext |
  | Component    | ManagedComponent    |
  | Endpoint     | ManagedEndpoint     |
  | Consumer     | ManagedConsumer     |
  | Producer     | ManagedProducer     |
  | Route        | ManagedRoute        |
  | Processor    | ManagedProcessor    |
  | Tracer       | ManagedTracer       |
  | Service      | ManagedService      |

  除此之外，还有一些针对特殊类型的扩展包装，例如:


  | **类型**              | **MBean wrapper**            |
  | --------------------- | ---------------------------- |
  | ScheduledPollConsumer | ManagedScheduledPollConsumer |
  | BrowsableEndpoint     | ManagedBrowseableEndpoint    |
  | Throttler             | ManagedThrottler             |
  | Delayer               | ManagedDelayer               |
  | SendProcessor         | ManagedSendProcessor         |

  在未来，我们将为更多EIP模式添加额外的包装器。

  ## 30.22. **M****anagement****O****bject****N****ame****S****trategy**

  **自Camel 2.1起可用**

  Camel为命名策略提供了一个可插拔的API org.apache.camel.spi.ManagementObjectNameStrategy。默认实现用于计算所有MBean注册的MBean名称。

  ## 30.23. **管理命名模式**

  **自Camel 2.10起可用**

  从**Camel 2.10**开始，我们简化了为MBean配置命名模式的过程。该模式用作ObjectName的一部分，在域名后键入。

  默认情况下，Camel将为ManagedCamelContextMBean使用MBean名称，如下所示:

  org.apache.camel:context=localhost/camel-1,type=context,name=camel-1

  从**Camel 2.13**开始，主机名不包含在MBean名称中，因此上面的示例如下:

  org.apache.camel:context=camel-1,type=context,name=camel-1

  如果您在CamelContext上配置名称，则CamelContext名称也是ObjectName的一部分。例如，如果我们有

  <camelContext id="myCamel" ...>

  然后MBean名称如下:

  org.apache.camel:context=localhost/myCamel,type=context,name=myCamel

  现在，如果JVM中存在命名冲突，例如已存在上面名称的MBean，则Camel默认会使用计数器在JMXMBeanServer中找到一个新的自由名称来自动纠正这个错误。如下所示，现在附加了计数器，因此我们将myCamel-1作为ObjectName的一部分:

  org.apache.camel:context=localhost/myCamel-1,type=context,name=myCamel

  这是可能的，因为Camel默认使用支持以下标记的命名模式:

  l camelId = CamelContext id(例如名称)

  l name - 与camelId一样 

  l counter- 递增计数器 * bundleId** **- OSGi包ID(仅适用于OSGi环境)

  l symbolicName - OSGi符号名称(仅适用于OSGi环境)

  l version - OSGi捆绑版本(仅适用于OSGi环境)

  默认命名模式在OSGi和非OSGi之间进行区分，如下所示:

  l 非OSGI: name

  l OSGi的: bundleId-name

  l OSGi **Camel 2.13****:** symbolicName

  但是，如果在JMXMBeanServer中存在命名冲突，Camel将自动回退并使用模式中的计数器来解决这个问题。因此将使用以下模式:

  l 非OSGI: name-counter

  l OSGi的: bundleId-name-counter

  l OSGi **Camel 2.13****:** symbolicName-counter

  如果设置显式命名模式，则始终使用该模式，并且**不**使用上面的默认模式。

  这使我们能够非常容易地完全控制注册表中的CamelContext id和JMXMBeanRegistry中的JMX MBean的命名。

  从**Camel 2.15**开始，您可以使用JVM系统属性配置缺省管理名称模式，以便为JVM全局配置该模式。请注意，您可以通过显式配置来覆盖此模式，如下面的示例所示。

  将JVM系统属性设置为使用默认管理名称模式，该模式将名称前缀设置为cool。

  System.setProperty(JmxSystemPropertyKeys.MANAGEMENT_NAME_PATTERN, "cool-#name#");

  因此，如果我们想显式地命名CamelContext并使用固定的MBean名称(例如没有计数器)，则可以使用新的managementNamePattern属性:

  <camelContext id="myCamel" managementNamePattern="#name#">

  然后MBean名称将始终如下:

  org.apache.camel:context=localhost/myCamel,type=context,name=myCamel

  在Java中，您可以按照以下方式配置managementNamePattern:

  context.getManagementNameStrategy().setNamePattern("#name#");

  您还可以在managementNamePattern中使用与id不同的名称，例如，我们可以这样做:

  <camelContext id="myCamel" managementNamePattern="coolCamel">

  如果不希望OSGi bundle id作为MBean名称的一部分，您可能希望在OSGi环境中这样做。因为如果重启服务器，或者卸载并安装相同的应用程序，OSGi bundle id可能会发生变化。然后，您可以按照以下步骤来避免将OSGi bundle id用作名称的一部分:

  <camelContext id="myCamel" managementNamePattern="#name#">

  注意，这要求myCamel在整个JVM中是惟一的。如果您安装了第二个具有相同CamelContext id和managementNamePattern的Camel应用程序，那么启动时Camel将失败，并抛出一个MBean已经存在异常。

  ## 30.24. **M****anagement****S****trategy**

  **自Camel 2.1起可用**

  Camel现在提供了一个完全可插拔的管理策略，允许您100%控制管理。它是一个包含许多管理方法的丰富接口。不仅用于从MBeanServer中添加和删除托管对象，还使用org.apache.camel.spi.EventNotifier API提供事件通知。例如，为其他管理产品提供适配器变得更容易。此外，它还允许您提供更多详细信息和Apache提供的开箱即用特性。

  ## 30.25. **配置性能统计信息的粒度级别**

  **自Camel 2.1起可用**

  现在，您可以在Camel启动时设置是否启用性能统计信息，和预设置级别。级别如下

  l Extended - 默认值，但在运行时会收集额外的统计信息，如endpoint的细粒度使用级别等。这个选项需要Camel 2.16。

  l All** **/ Default** **- Camel将启用route和processor的统计信息(细粒度)。从**Camel 2.16**开始，All选项被重命名为Default。

  l RoutesOnly - Camel只会启用路由统计(粗粒度)

  l Off - Camel不会启用任何统计信息。

  从**Camel 2.9**开始，性能统计信息还包括每个CamelContext和Route MBean的平均负荷统计信息。统计数据是基于线上交换次数的平均负荷，每1、5和15分钟的速率。类似于Unix系统上的负荷统计信息。**Camel 2.11**起，您可以明确禁用负荷的性能统计信息，禁用设置通过在<jmxAgent>设置loadStatisticsEnabled=false。请注意，如果将统计级别配置为关闭，它也将关闭。从**Camel 2.13**开始，默认情况下禁用负荷性能统计信息。您可以通过设置<jmxAgent>上loadStatisticsEnabled=true使其启用。

  在运行时，您始终可以使用管理控制台(例如JConsole)在给定路由或处理器上更改其统计信息是否启用。


  |  | **统计启用意味着什么？**启用统计意味着Camel将为该特定MBean执行细粒度的性能统计信息。您可以看到的统计数据很多，例如:number of exchanges completed/failed, last/total/mina/max/mean processing time, first/last failed time, etc |
  | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

  使用Java DSL可以通过以下方式设置此级别:

  *// only enable routes when Camel starts*

  context.getManagementStrategy().setStatisticsLevel(ManagementStatisticsLevel.RoutesOnly);

  从Spring DSL你可以:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **    **<jmxAgent id="agent" statisticsLevel="RoutesOnly"/>

  ** **...

  </camelContext>

  ## 30.26. **脱敏-****隐藏敏感信息**

  **自Camel 2.12起可用**

  默认情况下，Camel在JMX中使用MBean，例如使用URI配置的端点。在此配置中，可能存在密码等敏感信息。

  启用mask选项可以隐藏此信息，如下所示:

  使用Java DSL可以通过以下方式启用它:

  **  ***// only enable routes when Camel starts*

  **  **context.getManagementStrategy().getManagementAgent().setMask(true);

  Spring DSL你可以:

  **    **<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **        **<jmxAgent id="agent" mask="true"/>

  **     **...

  **    **</camelContext>

  这将屏蔽具有密码和密码短语等选项的URI，并用xxxxxx作替换值。

  ## 30.27. **声明要屏蔽的JMX属性和操作**

  在org.apache.camel.api.management.ManagedAttribute和org.apache.camel.api.management.ManagedOperation上，可以将属性mask设置为true，以指示应该屏蔽此JMX属性/操作的结果(如果在JMX代理上启用，请参见上文)。

  例如，在camel-core的默认托管端点上org.apache.camel.api.management.mbean.ManagedEndpointMBean，我们声明了EndpointUri** **JMX属性被屏蔽:

  @ManagedAttribute(description = "Endpoint URI", mask = true)

  String getEndpointUri();

  # 31. **Camel****生命周期**

  Camel使用一个名为[Service](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Service.html)的简单生命周期接口，它有一个start()和stop()方法。

  各种类都实现了CamelContext这样的Service，例如大量的组件和端点类。

  当您使用Camel时，您通常必须启动CamelContext，它将启动所有各种组件和端点并激活路由规则，直到停止上下文。

  如果您正在使用Spring，您可能希望阅读Camel Spring文档。

  ## 31.1. **CamelContext****生命周期**

  在CamelContext提供了一些方法来控制它的生命周期:

  l start

  l stop

  l suspend **Camel** **2.5**

  l resume **Camel** **2.5**

  操作配对:start/stop 和suspend/resume（挂起/恢复）。

  Stop执行优雅的关闭，这意味着清除它的所有内部状态、缓存等。而且路由正在以一种优雅的方式停止，以确保消息有时间完成。如果您在停止之后启动CamelContext，那么它将执行冷启动，重新创建所有状态和缓存等。

  相反，您可以使用挂起/恢复操作。它们将使用相同的优雅关闭功能保持CamelContext 为热状态且仅挂起/停止路由。这可确保消息有时间完成。

  如果您临时停止Camel应用程序，建议最终用户使用suspend/resume。

  所有这些操作也可以在JMX中使用，因此您可以从管理控制台控制Camel。

  如果您使用stop/start 编写单元测试并执行冷重启，则之前查找的任何端点等都已过时，因此您需要再次重新查找这些端点。

  而使用suspend/resume来保留这些端点，您仍然可以在恢复后使用它们。

  ## 31.2. **服务生命周期**

  Camel中的service(org.apache.camel.Service)遵循以下生命周期状态，如下图所示:

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml18764\wps11.jpg)

  **注意****:**service可以通过org.apache.camel.SuspendableService最佳地支持suspend/resume。这意味着并非Camel中的所有服务都支持suspend。鼓励消费者支持suspend，允许路由suspend/resume。

  org.apache.camel.support.service.ServiceSupport是一个很好的基类，可以对定制服务进行扩展，因为它提供了跟踪状态的基本功能。在doStart、doStop、doSuspend、doResume方法中实现自定义逻辑。

  ## 31.3. **路****由****生命周期**

  Camel中的路由具有以下操作来控制其生命周期

  l start

  l stop

  l suspend

  l resume

  l remove (以前叫做shutdown)

  remove操作将**删除**该路由，例如在JMX中，该路由将被取消注册并且消失。因此，如果您确实要删除路由，请仅使用remove。必须先停止路由才能删除。

  JMX中的start和resume操作事先检查状态。因此，如果路由停止并且您单击resume，它将知道要调用start。同样，如果一条路由被暂停，你点击start它就知道了要调用resume。这使管理更容易一些。

  如果路由被挂起，那么它会保留其资源及其所有JMX指标。作为停止路由的方法，优美的方法将在哪里停止路由，并清除它的资源以及它们的JMX度量。如果你想暂时“pause”一条路由，那么考虑使用suspend/resume而不是stop/start。

  如果路由消费者不支持暂停，它将回退并停止路由。

  ## 31.4. **相关信息**

  [看一下控制总线组件](https://camel.apache.org/components/latest/controlbus-component.html)([Control Bus Component](https://camel.apache.org/components/latest/controlbus-component.html))

  # 32. **on****C****ompletion**

  Camel有一个包含交换的工作单元的概念。工作单元支持在交换完成时调用同步回调。回调API在org.apache.camel.spi.Synchronization中定义。从**Camel 2.14**开始，我们有一个扩展的同步org.apache.camel.spi.SynchronizationRouteAware为路由事件提供回调。

  **获****取****UnitOfWork**

  您可以使用方法getUnitOfWork()从org.apache.camel.Exchange获取org.apache.camel.spi.UnitOfWork。

  在Camel 2.0中，我们为这些回调添加了新的**onCompletion** DSL名称。

  **onCompletion**支持以下功能:

  l scope:global and/or per route (route scope override all global scope)。

  l multiple global scope。

  l 始终触发，只有在成功完成或仅在失败时触发。

  l onWhen 谓词，仅在某些情况下触发。

  l **Camel 2.14****:** mode:定义在路由消费者将响应写回被调用方之前或之后运行(如果是InOut)。

  l * Camel 2.14:*是否运行同步或异步(是否使用线程池)。

  从**Camel 2.14**开始，onCompletion已被修改为支持以同步或异步模式(使用线程池)运行completion任务，也支持在路由consumer完成之前或之后运行，以提供更多的灵活性。例如，指定在路由consumer完成之前同步运行，这允许consumer将响应回写至调用者之前修改交换。您可以使用它来添加客户报头，或发送到日志以记录响应消息等。

  **从Camel 2.14开始****的变化**，**Camel 2.14以后**onCompletion已经改变了的默认值和行为。它现在运行 * 同步运行，没有任何线程池。而Camel 2.13中默认情况下 * 使用线程池异步运行。

  **Camel 2.13或更早版本 - onCompletion在独****立****线程中运行**

  **onCompletion**与原始路由并行运行在独立的线程中。因此，它不打算影响原路由的结果。onCompletion的想法是派生出一个新的线程，如发送日志到一个中央日志数据库，发送电子邮件，发送更改到监控系统，存储结果消息的副本等。

  因此，如果你想做一些工作影响原来的路由，那么就**不能**使用**onCompletion**了。注意:如果您使用本页顶部提到的UnitOfWork API，那么您可以在原始路由中运行的Exchange上注册一个Synchronization回调。这样可以让你在路由完成时做一些自定义代码; 这是自定义组件可以在他们需要的onCompletion服务上登记注册的方式，例如，File组件为移动/删除原始文件的工作执行此操作。

  ## 32.1. **路由范围的****onCompletion**

  当原始Exchange完成时**onCompletion** DSL允许你添加自定义的routes/processors。Camel衍生了Exchange的副本并将其路由到一个独立线程中，有点像消息监听。在**onCompletion**路由运行时，原始线程继续并行执行。我们决定使用这个模型，是因为我们不希望**onCompletion**路由干扰原始路由。

  **路由范围仅支持1个onCompletion**

  一条路由中只能有1个onCompletion。只有在上下文范围内，您才能拥有多个。请注意，当您使用作用于onCompletion的路由时，将禁用该路由的任何上下文作用域。

  from("direct:start")

  **    **.onCompletion()

  **        ***// this route is only invoked when the original route is complete as a kind*

  **        ***// of completion callback*

  **        **.to("log:sync")

  **        **.to("mock:sync")

  **    ***// must use end to denote the end of the onCompletion route*

  **    **.end()

  **    ***// here the original route contiues*

  **    **.process(new** **MyProcessor())

  **    **.to("mock:result");

  默认情况下，将在Exchange完成时触发**onCompletion**，无论Exchange是成功完成还是失败(例如抛出异常)。您可以将触发器限制为仅发生onCompleteOnly或onFailureOnly如下所示:

  from("direct:start")

  **    ***// here we qualify onCompletion to only invoke when the exchange failed (exception or FAULT body)*

  **    **.onCompletion().onFailureOnly()

  **        **.to("log:sync")

  **        **.to("mock:sync")

  **    ***// must use end to denote the end of the onCompletion route*

  **    **.end()

  **    ***// here the original route continues*

  **    **.process(new** **MyProcessor())

  **    **.to("mock:result");

  您可以识别Exchange是否为**onCompletion**Exchange，因为Camel将在关闭**onCompletion** Exchange时将属性Exchange.ON_COMPLETION添加为布尔值true。

  ### 32.1.1. **使用****Spring** **DSL的****onCompletion**

  使用Spring DSL将onCompletion定义为:

  <route>

  **    **<from uri="direct:start"/>

  **    ***<!-- this onCompletion block will only be executed when the exchange is done being routed -->*

  **    ***<!-- this callback is always triggered even if the exchange failed -->*

  **    **<onCompletion>

  **        ***<!-- so this is a kinda like an after completion callback -->*

  **        **<to uri="log:sync"/>

  **        **<to uri="mock:sync"/>

  **    **</onCompletion>

  **    **<process ref="myProcessor"/>

  <to uri="mock:result"/>

  </route>

  onCompleteOnly和onFailureOnly被定义为<onCompletion>标签上的布尔属性，所以失败的例子是

  <route>

  **    **<from uri="direct:start"/>

  **    ***<!-- this onCompletion block will only be executed when the exchange is done being routed -->*

  **    ***<!-- this callback is only triggered when the exchange failed, as we have onFailure=true -->*

  **    **<onCompletion onFailureOnly="true">

  **        **<to uri="log:sync"/>

  **        **<to uri="mock:sync"/>

  **    **</onCompletion>

  **    **<process ref="myProcessor"/>

  <to uri="mock:result"/>

  </route>

  ## 32.2. **全局****on****C****ompletion**

  就像route作用域一样，只是它们是全局定义的。下面一个例子

  *// define a global on completion that is invoked when the exchange is complete*

  onCompletion().to("log:global").to("mock:sync");

  from("direct:start")

  **    **.process(new** **MyProcessor())

  **    **.to("mock:result");

  ### 32.2.1. **使用S****pring** **DSL的O****n****C****ompletion**

  就像route作用域一样，只是它们是全局定义的。下面一个例子:

  *<!-- this is a global onCompletion route that is invoke when any exchange is complete*

  * as a kind of after callback -->*
  <onCompletion>

  **    **<to uri="log:global"/>

  <to uri="mock:sync"/>

  </onCompletion>

  <route>

  **    **<from uri="direct:start"/>

  **    **<process ref="myProcessor"/>

  <to uri="mock:result"/>

  </route>

  **路由范围覆盖全局范围****，**如果在路由中定义了**onCompletion**，它将覆盖**所有**全局范围，因此覆盖仅使用路由的作用域，不再使用全局范围。

  ## 32.3. **使用****on****C****ompletion****with****on****W****hen****断言**

  与Camel中的其他DSL一样，您可以将一个断言附加到**onCompletion，**这样它只会在断言匹配某些条件时触发。例如，在消息正文仅包含Hello单词时触发:

  from("direct:start")

  **    **.onCompletion().onWhen(body().contains("Hello"))

  **        ***// this route is only invoked when the original route is complete as a kind*

  **        ***// of completion callback. And also only if the onWhen predicate is true*

  **        **.to("log:sync")

  **        **.to("mock:sync")

  **    ***// must use end to denote the end of the onCompletion route*

  **    **.end()

  **    ***// here the original route contiues*

  **    **.to("log:original")

  **    **.to("mock:result");

  ## 32.4. **线程池下使用O****n****C****ompletion**

  **自Camel 2.14起可用**

  从Camel 2.14开始OnCompletion将默认不使用线程池。要使用线程池，请设置 executorService或parallelProcessing为true。

  例如在Java DSL中

  **                **onCompletion().parallelProcessing()

  **                    **.to("mock:before")

  **                    **.delay(1000)

  **                    **.setBody(simple("OnComplete:${body}"));

  在XML DSL中

  **      **<onCompletion parallelProcessing="true">

  **        **<to uri="before"/>

  **        **<delay><constant>1000</constant></delay>

  **        **<setBody><simple>OnComplete:${body}</simple></setBody>

  **      **</onCompletion>

  您还可以使用executorServiceRef选项引用要使用的特定线程池

  **      **<onCompletion executorServiceRef="myThreadPool">

  **        **<to uri="before"/>

  **        **<delay><constant>1000</constant></delay>

  **        **<setBody><simple>OnComplete:${body}</simple></setBody>

  **      **</onCompletion>

  ## 32.5. **在路由****消费者****将响应发送回调用者之前使用****on****C****ompletion****运行**

  **自Camel 2.14起可用**

  OnCompletion支持两种模式

  l AfterConsumer，在消费者完成后运行的默认模式。

  l BeforeConsumer，在消费者完成之前运行，并在消费者将响应写回调用者之前运行。

  AfterConsumer模式是默认模式，与旧版Camel版本的行为相同。

  新的BeforeConsumer模式用于在消费者将其响应写回调用方之前运行onCompletion(如果处于InOut模式)。这允许onCompletion修改Exchange，例如添加特殊报文头，或将Exchange记录为response日志等。

  例如，要添加"created by"报头您可以使用modeBeforeConsumer()，如下所示:

  **    **.onCompletion().modeBeforeConsumer()

  **        **.setHeader("createdBy", constant("Someone"))

  **    **.end()

  在XML DSL中，将mode属性设置为BeforeConsumer:

  **      **<onCompletion mode="BeforeConsumer">

  **        **<setHeader name="createdBy">

  **          **<constant>Someone</constant>

  **        **</setHeader>

  **      **</onCompletion>

  # 33. **断言**

  Camel支持名为[Predicate](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Predicate.html)的可插拔接口，可用于将动态断言[集成](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)到[企业集成模式中，](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)例如使用[消息过滤器](https://camel.apache.org/manual/latest/filter-eip.html)或[基于内容的路由器时](https://camel.apache.org/manual/latest/content-based-router-eip.html)。

  Predicate将被计算为布尔值，因此结果只能为true或false。在用于控制消息的路由去往何处，[Predicate](https://camel.apache.org/manual/latest/predicate.html)的功能是非常强大的。

  一个简单的示例是基于header路由[Exchange](https://camel.apache.org/manual/latest/exchange.html):

  from("jms:queue:order")

  **   **.choice()

  **      **.when(header("type").isEqualTo("widget")).to("bean:widgetOrder")

  **      **.when(header("type").isEqualTo("wombat")).to("bean:wombatOrder")

  **   **.otherwise()

  **      **.to("bean:miscOrder")

  **   **.end();

  在上面的路由中，[断言](https://camel.apache.org/manual/latest/predicate.html)是一个被构造为header("type").isEqualTo("widget")的[表达式](https://camel.apache.org/manual/latest/expression.html)以进行计算。有许多Builder类帮助我们构造简洁而优雅的语法。isEqualTo是一个构建器方法，它根据input返回[断言](https://camel.apache.org/manual/latest/predicate.html)。

  有时，Builder可能会变得冗长而且有点复杂，您可以在路由外定义断言，然后只需将断言引用至路由中:

  Predicate isWidget = header("type").isEqualTo("widget");

  然后你可以在路由中引用它:

  from("jms:queue:order")

  **   **.choice()

  **      **.when(isWidget).to("bean:widgetOrder")

  **      **.when(isWombat).to("bean:wombatOrder")

  **   **.otherwise()

  **      **.to("bean:miscOrder")

  **   **.end();

  ## 33.1. **否定****断言**

  您可以使用PredicateBuilder的**not**方法来否定断言。

  首先我们静态导入not，以使我们的路由易于阅读:

  import** **static** **org.apache.camel.builder.PredicateBuilder.not

  然后我们可以使用它来包围一个现有的断言，并如示例所示对其进行否定:

  from("direct:start")

  **    **.choice()

  **        **.when(not(header("username").regex("goofy|pluto"))).to("mock:people")

  **        **.otherwise().to("mock:animals")

  **    **.end();

  ## 33.2. **复合****断言**

  您还可以使用布尔运算符(如and, or, not等等其他运算符)创建复合断言。

  目前，此功能仅适用于基于Java DSL，但不适用于Spring DSL和Blueprint DSL。

  使用[PredicateBuilder](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/builder/PredicateBuilder.html)类，您可以基于逻辑运算符和比较运算符组合**来自不同Expression Languages**的断言:

  l not，and，or

  l isNull， isNotNull

  l isEqualTo，isGreaterThan，isLessThan

  l startsWith， endsWith

  l in ("任何X断言都是正确的")

  此外，使用PredicateBuilder您可以创建正则表达式并将它们用作断言，将它们应用于表达式的结果，例如PredicateBuilder.regex(header("foo"), "\d{4}")将正则表达式应用于header = foo。

  结合不同的表达语言也是可以的，例如:

  PredicateBuilder.and(XPathBuilder.xpath("/bookings/flights"), simple("${property.country = 'Spain'}"))

  下面的示例演示了更多用例:

  *// We define 3 predicates based on some user roles*

  *// we have static imported and/or from org.apache.camel.builder.PredicateBuilder*

  *// First we have a regular user that is just identified having a username header*

  Predicate user = header("username").isNotNull();

  *// The admin user must be a user AND have a admin header as true*

  Predicate admin = and(user, header("admin").isEqualTo("true"));

  *// And God must be an admin and (either have type god or a special message containing Camel Rider)*

  Predicate god = and(admin, or(body().contains("Camel Rider"), header("type").isEqualTo("god")));

  *// As you can see with the predicates above we can stack them to build compound predicates*

  *// In our route below we can create a nice content based router based on the predicates we*

  *// have defined. Then the route is easy to read and understand.*

  *// We encourage you to define complex predicates outside the fluent router builder as*

  *// it will just get a bit complex for humans to read*

  from("direct:start").choice()

  **    **.when(god).to("mock:god")

  **    **.when(admin).to("mock:admin")

  **    **.when(user).to("mock:user")

  **    **.otherwise().to("mock:guest")

  .end();

  ## 33.3. **可扩展的****断言**

  Camel支持使用多个可扩展的断言[语言](https://camel.apache.org/manual/latest/languages.html) ; 开箱即用支持以下语言

  l [Bean Language](https://camel.apache.org/components/latest/bean-language.html) for using Java for expressions

  l [Constant](https://camel.apache.org/manual/latest/constant-language.html)

  l [Header](https://camel.apache.org/manual/latest/header-language.html)

  l [JSonPath](https://camel.apache.org/components/latest/jsonpath-language.html)

  l [Mvel](https://camel.apache.org/components/latest/mvel-language.html)

  l [OGNL](https://camel.apache.org/components/latest/ognl-language.html)

  l [Ref Language](https://camel.apache.org/manual/latest/ref-language.html)

  l [ExchangeProperty](https://camel.apache.org/manual/latest/exchangeProperty-language.html)

  l [Scripting Languages](https://camel.apache.org/manual/latest/scripting-languages.html) such as

  ○ [Groovy](https://camel.apache.org/components/latest/groovy-language.html)

  l [Simple](https://camel.apache.org/manual/latest/simple-language.html)

  ○ [File Language](https://camel.apache.org/manual/latest/file-language.html)

  l [Spring Expression Language](https://camel.apache.org/components/latest/spel-language.html)

  l [Tokenizer](https://camel.apache.org/manual/latest/tokenize-language.html)

  l [XPath](https://camel.apache.org/components/latest/xpath-language.html)

  l [XQuery](https://camel.apache.org/components/latest/xquery-language.html)

  l [VTD-XML](https://github.com/camel-extra/camel-extra/blob/master/components/camel-vtdxml/src/main/docs/vtdxml-component.adoc)

  大多数这些语言也支持[基于注解的表达式语言](https://camel.apache.org/manual/latest/parameter-binding-annotations.html)。

  您可以通过实现[Predicate接口](https://github.com/apache/camel/blob/master/core/camel-api/src/main/java/org/apache/camel/Predicate.java)轻松编写自己的插件断言。

  还有许多辅助构建器可用，例如[PredicateBuilder类](https://github.com/apache/camel/blob/master/core/camel-core/src/main/java/org/apache/camel/builder/PredicateBuilder.java)。

  ## 33.4. **在IDE中使用****断言**

  要在IDE中使用不同的表达式和断言，您需要为使用的语言执行构建器类的静态导入。


  | **语言(S)**                                                                                                                                                                     | **要导入的Builder类**                                                     |
  | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
  | [脚本语言](https://camel.apache.org/manual/latest/scripting-languages.html)，如[Groovy](https://camel.apache.org/components/latest/groovy-language.html)                        | [XPath](https://camel.apache.org/components/latest/xpath-language.html)   |
  | [org.apache.camel.builder.xml.XPathBuilder](https://github.com/apache/camel/blob/master/components/camel-xpath/src/main/java/org/apache/camel/language/xpath/XPathBuilder.java) | [XQuery](https://camel.apache.org/components/latest/xquery-language.html) |

  # 34. **R****egistry**

  Camel支持可插拔的[Registry](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/spi/Registry.html)插件策略。允许Camel类似注册表轻松地使用。

  l [SimpleRegistry](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/impl/SimpleRegistry.html)，是一个基于java.util.Map的简单注册表。

  l [JndiRegistry](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/impl/JndiRegistry.html)，使用JNDI InitialContext作为注册表。

  l [ApplicationContextRegistry](http://camel.apache.org/maven/current/camel-spring/apidocs/org/apache/camel/spring/spi/ApplicationContextRegistry.html)，如果您使用的是Spring，它会使用ApplicationContext作为注册表。

  您还可以通过[camelContext.getRegistry()方法](#getRegistry())从CamelContext访问注册表。

  # 35. **R****oute****B****uilder**

  RouteBuilder是一个基类，使用DSL创建路由规则。然后将RouteBuilder的实例添加到CamelContext中。

  # 36. **R****outes**

  Camel支持使用Java DSL(特定领域语言)定义路由规则，这避免了使用RouteBuilder处理繁琐的XML。

  例如，可以如下创建简单路由。

  RouteBuilder builder = new** **RouteBuilder() {

  **    **public void configure() {

  **        **errorHandler(deadLetterChannel("mock:error"));

  **        **from("direct:a").to("direct:b");

  **    **}

  };

  正如您上面所看到的，Camel使用URI将端点连接在一起。

  ## 36.1. **URI字符串格式**

  **从Camel 2.0开始提供**

  如果您的端点URI有接受选项并且您希望能够替换该值，例如通过将字符串连接在一起来构建URI，那么您可以使用java.lang.String.format方法。但是在Camel 2.0中我们在Java DSL中添加了两个实用的方法，所以可以使用fromF和toF来使用字符串格式来构建URI。。

  from("direct:start").toF("file://%s?fileName=%s", path, name);

  fromF("file://%s?include=%s", path, pattern).toF("mock:%s", result);

  ## 36.2. **过滤器****-****filter**

  您可以将简单路由与过滤器结合使用，过滤器可以是任意断言逻辑。

  RouteBuilder builder = new** **RouteBuilder() {

  **    **public void configure() {

  **        **errorHandler(deadLetterChannel("mock:error"));

  **        **from("direct:a")

  **            **.filter(header("foo").isEqualTo("bar"))

  **                **.to("direct:b");

  **    **}

  };

  ## 36.3. **选择****-****choice**

  通过choice，您可以提供断言和结果列表以及可选的default otherwise子句，如果不满足任何条件，则调用该子句。

  RouteBuilder builder = new** **RouteBuilder() {

  **    **public void configure() {

  **        **errorHandler(deadLetterChannel("mock:error"));

  **        **from("direct:a")

  **            **.choice()

  **                **.when(header("foo").isEqualTo("bar"))

  **                    **.to("direct:b")

  **                **.when(header("foo").isEqualTo("cheese"))

  **                    **.to("direct:c")

  **                **.otherwise()

  **                    **.to("direct:d");

  **    **}

  };

  ## 36.4. **使用自定义处理器P****rocessor**

  以下是使用自定义处理器的示例

  myProcessor = new** **Processor() {

  **    **public void process(Exchange exchange) {

  **        **log.debug("Called with exchange: "** **+ exchange);

  **    **}

  };

  RouteBuilder builder = new** **RouteBuilder() {

  **    **public void configure() {

  **        **errorHandler(deadLetterChannel("mock:error"));

  **        **from("direct:a")

  **            **.process(myProcessor);

  **    **}

  };

  您可以将自定义处理器与过滤器和choice混合搭配。

  RouteBuilder builder = new** **RouteBuilder() {

  **    **public void configure() {

  **        **errorHandler(deadLetterChannel("mock:error"));

  **        **from("direct:a")

  **            **.filter(header("foo").isEqualTo("bar"))

  **                **.process(myProcessor);

  **    **}

  };

  # 37. **T****ransformer**

  **自Camel 2.19起可用**

  Transformer根据声明的路由定义Input Type和/或Output Type执行消息的声明性转换，该路由定义了预期的消息类型。默认的camel Message实现DataTypeAware，它允许保存由DataType表示的消息类型。如果输入类型和/或输出类型被路由定义为Input Type和/或Output Type，并且它与运行时的实际消息类型不同，则camel内部processor会查找从当前消息类型转换为预期消息类型的Transformer转换。一旦转换成功或消息已经处于预期类型，则更新消息数据类型。

  ## 37.1. **数据类型格式**

  scheme:name

  其中**scheme**是数据模型的种类，就像java，xml或者json，**name**是特定数据类型名称。如果您只指定**scheme，**那么它会命中具有该scheme的所有数据类型，就像通配符一样。

  ## 37.2. **支持的T****ransformer**


  | **Transformer**         | **描述**                                                                               |
  | ----------------------- | -------------------------------------------------------------------------------------- |
  | Data Format Transformer | 使用数据格式进行转换                                                                   |
  | Endpoint Transformer    | 使用Endpoint进行转换                                                                   |
  | Custom Transformer      | 使用自定义transformer类进行转换。Transformer必须是org.apache.camel.spi.Transformer子类 |

  ### 37.2.1. **常****用****选项**

  所有Transformer都有以下常用选项，用于指定Transformer支持的数据类型。scheme或fromType和toType两者之一必须指定。


  | **名称** | **描述**                                                                                                |
  | -------- | ------------------------------------------------------------------------------------------------------- |
  | scheme   | 数据模型的类型如xml或json。例如，如果指定为xml，则Transformer适用于所有java - > xml和xml - > java转换。 |
  | fromType | 要转换的原始[数据类型](https://camel.apache.org/manual/latest/transformer.html)。                       |
  | toType   | 要转换的目标[数据类型](https://camel.apache.org/manual/latest/transformer.html)。                       |

  ### 37.2.2. **DataFormat Transformer****选项**


  | **名称** | **描述**       |
  | -------- | -------------- |
  | type     | 数据格式类型   |
  | ref      | 引用数据格式ID |

  以下是指定为bindy数据类型的示例:

  Java DSL:

  BindyDataFormat bindy = new** **BindyDataFormat();

  bindy.setType(BindyType.Csv);

  bindy.setClassType(com.example.Order.class);

  transformer()

  **    **.fromType(com.example.Order.class)

  **    **.toType("csv:CSVOrder")

  **    **.withDataFormat(bindy);

  XML DSL:

  <dataFormatTransformer fromType="java:com.example.Order" toType="csv:CSVOrder">

  <bindy id="csvdf" type="Csv" classType="com.example.Order"/>

  </dataFormatTransformer>

  ### 37.2.3. **Endpoint Transformer****选项**


  | **名称** | **描述**   |
  | -------- | ---------- |
  | ref      | 引用端点ID |
  | uri      | 端点URI    |

  以下是在Java DSL中指定端点URI的示例:

  transformer()

  **    **.fromType("xml")

  **    **.toType("json")

  **    **.withUri("dozer:myDozer?mappingFile=myMapping.xml...");

  以下是XML DSL中指定端点引用的示例:

  <endpointTransformer ref="myDozerEndpoint" fromType="xml" toType="json"/>

  ### 37.2.4. **自定义****Transformer****选项**

  请注意，Transformer必须是org.apache.camel.spi.Transformer子类 


  | **名称**  | **描述**                          |
  | --------- | --------------------------------- |
  | ref       | 引用自定义Transformer bean ID     |
  | className | 自定义Transformer类的完全限定类名 |

  以下是指定自定义Transformer类的示例:

  Java DSL:

  transformer()

  **    **.fromType("xml")

  **    **.toType("json")

  **    **.withJava(com.example.MyCustomTransformer.class);

  XML DSL:

  <customTransformer className="com.example.MyCustomTransformer" fromType="xml" toType="json"/>

  ## 37.3. **例子**

  例如声明Endpoint Transformer，使用XSLT组件从xml:ABCOrder转换为xml:XYZOrder，我们可以如下做:

  Java DSL:

  transformer()

  **    **.fromType("xml:ABCOrder")

  **    **.toType("xml:XYZOrder")

  **    **.withUri("xslt:transform.xsl");

  XML DSL:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **    **<transformers>

  **        **<endpointTransformer uri="xslt:transform.xsl" fromType="xml:ABCOrder" toType="xml:XYZOrder"/>

  **    **</transformers>

  ....

  </camelContext>

  如果您有以下路由定义，则以上转换将支持从direct:abc端点将消息发送到端点direct:xyz:

  Java DSL:

  from("direct:abc")

  **    **.inputType("xml:ABCOrder")

  **    **.to("direct:xyz");

  from("direct:xyz")

  **    **.inputType("xml:XYZOrder")

  **    **.to("somewhere:else");

  XML DSL:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:abc"/>

  **        **<inputType urn="xml:ABCOrder"/>

  **        **<to uri="direct:xyz"/>

  **    **</route>

  **    **<route>

  **        **<from uri="direct:xyz"/>

  **        **<inputType urn="xml:XYZOrder"/>

  **        **<to uri="somewhere:else"/>

  </route>

  </camelContext>

  # 38. **V****alidator**

  **自Camel 2.19起可用**

  Validator根据路由声明的Input Type和/或Output Type执行消息的声明性验证，该声明按预期定义了消息类型。请注意，只有validate声明的类型属性为true 时才执行验证。如果validate在Input Type和/或Output Type声明中属性为true ，则camel内部处理器从注册表中查找相应的Validator并应用。

  ## 38.1. **数据类型格式**

  scheme:name

  其中**scheme**是数据模型的种类，就像java，xml或者json，**name**是特定数据类型名称。

  ## 38.2. **支持的验证器**


  | **验证器**         | **描述**                                                                            |
  | ------------------ | ----------------------------------------------------------------------------------- |
  | PredicateValidator | 使用Expression或Predicate进行验证                                                   |
  | EndpointValidator  | 通过转发到与验证组件(如验证组件或Bean验证组件)一起使用的endpoint进行验证。          |
  | CustomValidator    | 使用自定义验证程序类进行验证。Validator必须是org.apache.camel.spi.Validator的子类。 |

  ## 38.3. **常见选项**

  所有验证器都有以下常用选项，用于指定验证器支持的数据类型。type必须指定。


  | **名称** | **描述**                                        |
  | -------- | ----------------------------------------------- |
  | type     | 要验证的[数据类型](#Validator-DataTypeFormat)。 |

  ## 38.4. **PredicateValidator****选项**


  | **名称**   | **描述**               |
  | ---------- | ---------------------- |
  | expression | 用于验证的表达式或断言 |

  以下是断言验证的示例:

  Java DSL:

  validator()

  **    **.type("csv:CSVOrder")

  **    **.withExpression(bodyAs(String.class).contains("{name:XOrder}"));

  XML DSL:

  <predicateValidator Type="csv:CSVOrder">

  <simple>${body} contains '{name:XOrder}'</simple>

  </predicateValidator>

  ## 38.5. **EndpointValidator****选项**


  | **名称** | **描述**   |
  | -------- | ---------- |
  | ref      | 引用端点ID |
  | uri      | 端点URI    |

  以下是在Java DSL中指定端点URI的示例:

  validator()

  **    **.type("xml")

  **    **.withUri("validator:xsd/schema.xsd");

  在XML DSL中指定端点引用的示例:

  <endpointValidator uri="validator:xsd/schema.xsd" type="xml"/>

  请注意端点验证器只是将消息转发到指定的端点。在上面的例子中，camel将消息转发给validator: 端点，它实际上是一个[验证组件](https://camel.apache.org/components/latest/validator-component.html)。您还可以使用任何其他验证组件，比如Bean验证组件。

  ## 38.6. **自定义验证器选项**

  请注意，Validator必须是org.apache.camel.spi.Validator子类 


  | **名称**  | **描述**                        |
  | --------- | ------------------------------- |
  | ref       | 引用自定义Validator bean ID     |
  | className | 自定义Validator类的完全限定类名 |

  下面是一个指定自定义Validator类的Java DSL示例::

  validator()

  **    **.type("json")

  **    **.withJava(com.example.MyCustomValidator.class);

  XML DSL:

  <customTransformer className="com.example.MyCustomValidator" type="json"/>

  ## 38.7. **示例**

  例如，声明Endpoint Validator使用验证器组件进行验证 xml:ABCOrder，我们可以执行以下操作:

  Java DSL:

  validator()

  **    **.type("xml:ABCOrder")

  **    **.withUri("validator:xsd/schema.xsd");

  XML DSL:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **    **<validators>

  **        **<endpointValidator uri="validator:xsd/schema.xsd" type="xml:ABCOrder"/>

  </validators>

  </camelContext>

  如果您有以下路由定义，则在direct:abc端点收到消息时将应用上述验证器。请注意，在Java DSL中使用inputTypeWithValidate而不是inputType，并且XML DSL中inputType声明的属性validate设置为true:

  Java DSL:

  from("direct:abc")

  **    **.inputTypeWithValidate("xml:ABCOrder")

  **    **.log("${body}");

  XML DSL:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:abc"/>

  **        **<inputType urn="xml:ABCOrder" validate="true"/>

  **        **<log message="${body}"/>

  </route>

  </camelContext>

  # 39. **S****pring** **R****emoting**

  我们支持Camel中的Spring Remoting。Spring Remoting的实现使用Camel作为底层传输机制。这种方法的好处是我们可以使用任何Camel传输[组件](https://camel.apache.org/components/latest/index.html)在bean之间进行通信。

  这也意味着我们可以在bean之间使用[基于内容的路由器](https://camel.apache.org/manual/latest/content-based-router-eip.html)([Content Based Router](https://camel.apache.org/manual/latest/content-based-router-eip.html))和其他[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html) ; 特别是我们可以使用[Message Translator](https://camel.apache.org/manual/latest/message-translator.html)除了添加各种报文头之外，还能够转换线上消息的外观。

  ## 39.1. **使用C****amel** **S****pring** **R****emoting**

  在Spring XML中，只需使用org.apache.camel.spring.remoting.CamelProxyFactoryBean创建客户端代理实现某个接口，然后将消息发送到某些远程Camel [ endpoint](https://camel.apache.org/manual/latest/endpoint.html)，如[ActiveMQ](https://camel.apache.org/components/latest/activemq-component.html)，[JMS](https://camel.apache.org/components/latest/jms-component.html)，[File](https://camel.apache.org/components/latest/file-component.html)，[HTTP](https://camel.apache.org/components/latest/http-component.html)，[XMPP](https://camel.apache.org/components/latest/xmpp-component.html)等。

  然后使用org.apache.camel.spring.remoting.CamelServiceExporter实现您的服务。

  以下[示例](https://github.com/apache/camel/blob/master/components/camel-spring/src/test/resources/org/apache/camel/spring/remoting/spring-with-exporter.xml)显示如何创建一个代理，当使用fire调用**direct:say**端点的消息时

  *<**!-**- 创建direct**:**say端点的代理。 -**-**>*

  <bean id ="sayProxy" class ="org.apache.camel.spring.remoting.CamelProxyFactoryBean">

  <property name ="serviceUrl" value ="direct:say"/>

  <property name ="serviceInterface" value ="org.apache.camel.spring.remoting.ISay"/>

  <property name ="binding" value ="true"/>

  </bean>

  然后我们在端点上公开服务，以便将来自**direct****:****sayImpl**的消息分派给服务(请注意，我们在这两个端点之间有一条路由)。

  *<**!-**- 通过pojo暴露上面的bean**:**say endpoint  **--**>*

  <bean id ="say" class ="org.apache.camel.spring.remoting.CamelServiceExporter">

  <property name ="uri" value ="direct:sayImpl"/>

  <property name ="service">

  <bean class ="org.apache.camel.spring.remoting.SayService"/>
  </property>

  <property name ="method" value ="say"/>

  <property name ="serviceInterface" value ="org.apache.camel.spring.remoting.ISay"/>

  </bean>

  ## 39.2. **使用自定义命名空间**

  在[此示例中，](https://github.com/apache/camel/blob/master/components/camel-spring/src/test/resources/org/apache/camel/spring/remoting/spring-with-exporter-namespace.xml)我们使用Camel自定义命名空间使XML更加简洁。首先，通过代理元素创建代理

  *<**!-**- 创建direct**:**say端点的代理。 -**-**>*

  <camel:proxy id ="sayProxy" serviceUrl ="direct:say"

               serviceInterface= "org.apache.camel.spring.remoting.ISay"/>
  然后我们通过export元素公开服务

  <camel:export id ="say" uri ="direct:sayImpl" serviceRef ="sayService" method ="say" serviceInterface= "org.apache.camel.spring.remoting.ISay"/>

  *<!-- *

  *bean**被定义在**Camel**的一侧*

  <bean id ="sayService" class ="org.apache.camel.spring.remoting.SayService"/>

  *-->*

  它更简洁 - 使用您喜欢的任何方法，因为它们都是等效的。

  ## 39.3. **S****ervice****E****xporter****是可选的**

  请注意，该服务不是强制性的; 由于[Bean](https://camel.apache.org/manual/latest/bean-binding.html)组件和各种其他形式的[Bean Integration](https://camel.apache.org/manual/latest/bean-integration.html)可用于将任何消息交换路由到bean，因此如果您愿意，可以忽略serviceExporter。service exporter的主要价值是将URI绑定到bean的单个XML元素，它允许bean的完整API受到service Interface的限制。

  ## 39.4. **使用I****nOnly****方法调用**

  从1.5开始，Camel支持@InOnly和@Pattern注解，允许您指定哪些方法是InOut([请求回复](https://camel.apache.org/manual/latest/requestReply-eip.html))或是InOnly(oneway or fire and forget [Event Message](https://camel.apache.org/manual/latest/event-message.html))。

  有关更多详细信息，请参阅[使用Exchange模式注](https://camel.apache.org/manual/latest/using-exchange-pattern-annotations.html)解。

  ## 39.5. **B****ean****绑定**

  Camel中的Bean绑定定义了调用哪些方法以及在调用[Message时](https://camel.apache.org/manual/latest/message.html)如何将[Message](https://camel.apache.org/manual/latest/message.html)转换为方法的参数。

  ## 39.6. **选择要调用的方法**

  将Camel [消息](https://camel.apache.org/manual/latest/message.html)绑定到bean方法调用可以以不同的方式进行，其重要性顺序如下:

  l 如果消息包含头**CamelBeanMethodName**，则调用该方法，将body转换为方法参数的类型。

  ○ 从**Camel 2.8**开始，您可以限定参数类型，以准确选择在具有相同名称的重载中使用哪种方法(有关详细信息，请参见下文)。

  ○ 从**Camel 2.9**开始，您可以直接在方法选项中指定参数值(有关详细信息，请参见下文)。

  l 您可以在[DSL中](https://camel.apache.org/manual/latest/dsl.html)或使用[POJO Consuming](https://camel.apache.org/manual/latest/pojo-consuming.html)或[POJO Producing](https://camel.apache.org/manual/latest/pojo-producing.html)时明确指定方法名称。

  l 如果bean具有标记有@Handler注解的方法，则选择该方法。

  l 如果bean可以使用[Type Converter](https://camel.apache.org/manual/latest/type-converter.html)机制转换为[Processor](https://camel.apache.org/manual/latest/processor.html)，那么这将用于处理消息。[ActiveMQ](https://camel.apache.org/components/latest/activemq-component.html)组件使用此机制允许Camel直接调用任何JMS MessageListener，而无需编写任何集成代码。 您可以使用相同的机制将Camel集成到任何其他消息传递/远程处理框架中。

  l 如果消息的主体可以转换为org.apache.camel.component.bean.BeanInvocation(默认的有效负载使用org.apache.camel.component.bean.ProxyHelper)组件 - 那么它用于调用方法并传递其参数。

  l 否则，使用消息体的类型来找到匹配方法； 如果不能明确选择一个方法，则会引发错误。

  l 您也可以使用Exchange作为参数本身，但返回类型必须为void。

  l 如果bean类是私有的(或者是包私有的)，那么接口方法将是首选的(从**Camel 2.9**开始)，因为Camel不能在这样的bean类上调用方法。

  如果Camel无法选择要调用的方法，则抛出AmbiguousMethodCallException。

  默认情况下，返回值在出站（outbound）消息体中设置。

  ## 39.7. **异步处理**

  从**Camel 2.18**开始，您可以返回CompletionStage实现(例如CompletableFuture)以实现异步处理。

  请务必获取到结果或异常，使CompletionStage正确完成，包括任何超时处理。Exchange处理将阻塞等待完成，并且不会自动强制处理任何超时。监控org.apache.camel.spi.InflightRepository非常有用可以获得任何挂起的消息。

  **注意，**使用"null"不会完全将outbody消息体设置为null，但是会保持消息的完整性。这对于支持不修改exchange并返回CompletableFuture<Void>的方法非常有用。要将body设置为null，只需添加Exchange方法参数并直接修改Exchange消息。

  例子:

  简单的异步处理器，修改消息体。

  public CompletableFuture<String> doSomethingAsync(String body)

  不修改交换的复合处理器

  ** **public CompletableFuture<Void> doSomethingAsync(String body) {

  **     **return CompletableFuture.allOf(doA(body), doB(body), doC());

  ** **}

  ## 39.8. **参数绑定**

  当选择一个方法进行调用时，Camel将绑定到该方法的参数。

  以下Camel类型会自动绑定:

  l org.apache.camel.Exchange

  l org.apache.camel.Message

  l org.apache.camel.CamelContext

  l org.apache.camel.TypeConverter

  l org.apache.camel.spi.Registry

  l java.lang.Exception

  因此，如果您声明了以上这些类型，它们将由Camel提供自动绑定。**请注意，****Exception****将绑定到**[**Exchange**](https://camel.apache.org/manual/latest/exchange.html)**的捕获异常** - 因此，如果您使用[Bean](https://camel.apache.org/components/latest/bean-component.html)来处理例如路由的onException，这通常是有用的。

  最有趣的是，Camel还会尝试将[Exchange](https://camel.apache.org/manual/latest/exchange.html)的消息体绑定到方法的第一个参数(尽管不是上述任何类型)。因此，例如，如果我们将参数声明为String body，则Camel会将IN消息体绑定到此类型。Camel也会自动转换为方法中声明的类型。

  我们来看一些例子:

  下面是一个带有body绑定的简单方法。Camel将IN消息体绑定到body参数并将其转换为String。

  public String doSomething(String body)

  在下面的示例中，我们也获得了一个自动绑定类型 - 例如，我们可以用来查找bean的Registry。

  public String doSomething(String body, Registry registry)

  我们也可以使用[Exchange](https://camel.apache.org/manual/latest/exchange.html):

  public String doSomething(String body, Exchange exchange)

  您还可以有多种类型:

  public String doSomething(String body, Exchange exchange, TypeConverter converter)

  假设您使用[Pojo](https://camel.apache.org/components/latest/bean-component.html)来处理给定的自定义异常InvalidOrderException - 我们也可以将其绑定:

  public String badOrder(String body, InvalidOrderException invalid)

  请注意，即使我们使用java.lang.Exception子类，我们也可以绑定它，因为Camel仍然知道它是一个异常并且可以绑定(如果存在)。

  那么消息头和其他内容呢？有点棘手 - 所以我们可以使用注解来帮助我们，或者在方法名称选项中指定绑定。有关详细信息，请参阅以下部分。

  ## 39.9. **绑定注****解**

  您可以使用[参数绑定注](https://camel.apache.org/manual/latest/parameter-binding-annotations.html)解来自定义如何从[Message](https://camel.apache.org/manual/latest/message.html)创建参数值。

  ### 39.9.1. **例子**

  以[Bean](https://camel.apache.org/components/latest/bean-component.html)举例，如:

  public class Bar {

  **    **public String doSomething(String body) {

  **    ***// process the in body and return whatever you want*

  **    **return "Bye World";

  }

  或Exchange示例。请注意，当只有一个类型org.apache.camel.Exchange的参数时，返回类型必须为**void**:

  ** **public class Bar {

  **     **public void doSomething(Exchange exchange) {

  **        *** // process the exchange*

  **         **exchange.getIn().setBody("Bye World");

  ** **}

  [[SpringRemoting- @Handler]] === @Handler

  您可以使用@Handler注解在bean中标记一个方法，以指明此方法应该用于[Bean绑定](https://camel.apache.org/manual/latest/bean-binding.html)。这有一个好处，您不需要在Camel路由中指定方法名，因此在IDE中重命名方法后不会遇到问题。

  public class Bar {

  **    **@Handler

  **    **public String doSomething(String body) {

  **        ***// process the in body and return whatever you want*

  **        **return "Bye World";

  **    **}

  }

  ### 39.9.2. **使用方法选项进行参数绑定**

  **自Camel 2.9起可用**

  Camel使用以下规则来确定它是否是方法选项中的参数值

  l 值为true或者false表示布尔值。

  l 该值是一个数值，如123或7。

  l 该值是一个用单引号或双引号括起来的String。

  l 值为null表示null值。

  l 它可以使用[简单](https://camel.apache.org/manual/latest/simple-language.html)语言进行计算，这意味着您可以使用例如body，header.foo和其他[简单](https://camel.apache.org/manual/latest/simple-language.html)标记。请注意，语言符号必须用**${** **}**括起来。

  任何其他值都被认为是类型声明 - 请参阅下一节有关为重载方法指定类型的内容。

  调用[Bean时，](https://camel.apache.org/manual/latest/bean-eip.html)您可以通过提供方法名称来指示Camel调用特定方法:

  .bean(OrderService.class, "doSomething")

  在这里，我们告诉Camel调用doSomething方法 - Camel处理参数的绑定。现在假设该方法有两个参数，第二个参数是一个布尔值，我们想要传入一个true值:

  public void doSomething(String payload, boolean highPriority) {

  **    **...

  }

  现在可以在**Camel 2.9**实现:

  .bean(OrderService.class, "doSomething(*, true)")

  在上面的示例中，我们使用通配符*定义了第一个参数，它告诉Camel将此参数绑定到任何类型，并让Camel弄清楚这一点。第二个参数的固定值为true。我们可以指示Camel使用消息体，而不是通配符，如下所示:

  .bean(OrderService.class, "doSomething(${body}, true)")

  参数的语法使用[简单](https://camel.apache.org/manual/latest/simple-language.html)表达式语言，因此我们必须在正文中使用**${** **}**占位符来引用消息体。

  如果要传入null值，则可以在method选项中明确定义，如下所示:

  .to("bean:orderService?method=doSomething(null, true)")

  指定null为参数值指示Camel强制传递null值。

  除了消息体，您还可以将消息头传递为java.util.Map:

  .bean(OrderService.class, "doSomethingWithHeaders(${body}, ${headers})")

  您还可以传递除布尔值之外的其他固定值。例如，您可以传入String和整数:

  .bean(MyBean.class, "echo('World', 5)")

  在上面的例子中，我们使用两个参数调用echo方法。第一个包含内容'World'(没有引号)，第二个包含值5. 

  Camel会自动将这些值转换为参数类型。

  拥有[Simple](https://camel.apache.org/manual/latest/simple-language.html)语言的强大功能允许我们绑定到消息头和其他值，例如:

  .bean(OrderService.class, "doSomething(${body}, ${header.high})")

  您还可以使用[Simple](https://camel.apache.org/manual/latest/simple-language.html)表达式语言的OGNL支持。现在假设消息体是一个具有名为asXml的方法的对象。要调用asXml方法，我们可以执行以下操作:

  .bean(OrderService.class, "doSomething(${body.asXml}, ${header.high})")

  您可能需要使用.to，而不是使用在上面例子所示的.bean，如图所示:

  .to("bean:orderService?method=doSomething(${body.asXml}, ${header.high})")

  ### 39.9.3. **使用类型限定符在重载方法中进行选择**

  **自Camel 2.8起可用**

  如果您有一个带有重载方法的[Bean](https://camel.apache.org/manual/latest/bean-eip.html)，您现在可以在方法名称中指定参数类型，以便Camel可以匹配您要使用的方法。

  给出以下bean:

  ** **from("direct:start")

  **    **.bean(MyBean.class, "hello(String)")

  **    **.to("mock:result");

  然后MyBean有两个重载方法名称分别为hello和times。因此，如果我们想要使用具有两个参数的方法，我们可以在Camel路由中执行以下操作:

  from("direct:start")

  **    **.bean(MyBean.class, "hello(String,String)")

  **    **.to("mock:result");

  我们也可以使用 * 通配符，这是我们可以说我们想用我们做的两个参数来执行方法

  ** **from("direct:start")

  **    **.bean(MyBean.class, "hello(*,*)")

  **    **.to("mock:result");

  默认情况下，Camel将使用简单名称匹配类型名称，例如，将忽略任何前导包名称。但是，如果要使用FQN进行匹配，请指定FQN类型，Camel将利用该类型。因此，如果你有一个com.foo.MyOrder并且想要与FQN匹配，而**不是**简单的名称"MyOrder"，那么请遵循以下示例:

  .bean(OrderService.class, "doSomething(com.foo.MyOrder)")

  Camel当前仅支持在方法名称选项中指定参数绑定或键入每个参数。您**不能同时**指定两者，例如

  ** **doSomething(com.foo.MyOrder ${body}, boolean ${header.high})

  这可能在以后版本得到支持。

  # 40. **隐藏中间件**

  在编写软件时，尽可能尝试将中间件代码与业务逻辑分离是很重要的。

  这会提供许多好处......

  l 您可以随时为部署选择合适的中间件解决方案并进行切换。

  l 您不必花费大量时间来学习任何特定技术的细节，无论是[JMS](https://camel.apache.org/components/latest/jms-component.html)，[JPA](https://camel.apache.org/components/latest/jpa-component.html)还是[MyBatis](https://camel.apache.org/components/latest/mybatis-component.html)等等。

  例如，如果您想在应用程序中实现某种消息传递、远程处理、可靠的负载平衡或异步处理，我们建议您使用Camel注解将服务和业务逻辑绑定到Camel [组件](https://camel.apache.org/components/latest/index.html)，这意味着您可以轻松地在诸如

  l 在与[SEDA的](https://camel.apache.org/components/latest/seda-component.html) JVM消息传递中。

  l 通过[ActiveMQ](https://camel.apache.org/components/latest/activemq-component.html)或其他[JMS](https://camel.apache.org/components/latest/jms-component.html)提供程序使用JMS 进行可靠的负载平衡，网格或发布和订阅。

  l 由于您可能已经在使用可以使用的数据库，因此数量较少，但管理较轻松。

  l [JPA](https://camel.apache.org/components/latest/jpa-component.html)使用实体bean /表作为队列。

  l [MyBatis](https://camel.apache.org/components/latest/mybatis-component.html)使用SQL。

  l [MyBatis](https://camel.apache.org/components/latest/jdbc-component.html) [JDBC]用于原始SQL访问。

  ## 40.1. **如何与中间件API分离**

  使用远程处理时的最佳方法是使用[Spring Remoting](https://camel.apache.org/manual/latest/spring-remoting.html)，然后可以使用后台的任何消息传递或远程处理技术。使用Camel的实现时，您可以使用任何Camel [组件](https://camel.apache.org/components/latest/index.html)以及任何[企业集成模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)。

  另一种方法是通过[Bean Integration](https://camel.apache.org/manual/latest/bean-integration.html)将Java bean绑定到Camel端点。例如，使用[POJO Consuming](https://camel.apache.org/manual/latest/pojo-consuming.html)和[POJO Producing，](https://camel.apache.org/manual/latest/pojo-producing.html)您可以避免使用任何Camel API将您的代码与中间件API 和 Camel API分离！

  # 41. **健康检查**

  **自****Camel****2****.20起可用**

  Camel通过基于以下概念的可插拔运行状况检查策略提供支持以探查集成状态：

  l **HealthCheck****：**代表健康检查并定义其基本合同；

  l **HealthCheckResponse：**代表健康检查调用响应；

  l **HealthCheckConfiguration：**一个基本配置对象，其中包含一些基本设置，例如呼叫之间的最小延迟，在将检查标记为失败之前可以报告服务不正常的次数；除了这些简单的选项外，check实施还负责在需要时实施进一步的限制；

  l **HealthCheckRegistry：**用于健康检查的注册表；

  l **HealthCheckRepository：**一个简单的界面，用于定义健康检查提供程序。默认情况下，有一个可以捕获注册表中所有可用的检查，因此您可以添加自己的检查，即在spring / spring-boot中使bean处于活动状态；组件可以提供自己的存储库；

  l **HealthCheckService：**一种简单的服务，在后台运行，并根据计划调用检查；

  ## 41.1. **示例****：**

  l **Spring Boot**：

  *# Enable route checks*

  camel.health.check.routes.enabled** **= true

  *# Configure default thresholds*

  camel.health.check.routes.thresholds.exchanges-failed** **= 10

  *# Configure a different exchanges-failed  threshold for the route bar*

  camel.health.check.routes.threshold[bar].exchanges-failed** **= 20

  *# Configure different thresholds for the route slow without inherit global*

  *# thresholds*

  camel.health.check.routes.threshold[slow].inherit** **= false

  camel.health.check.routes.threshold[slow].last-processing-time.threshold** **= 1s

  camel.health.check.routes.threshold[slow].last-processing-time.failures** **= 5

  l **Spring XML DSL**：

  <beans xmlns="http://www.springframework.org/schema/beans"

     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

     xsi:schemaLocation="

       http://www.springframework.org/schema/beans

       http://www.springframework.org/schema/beans/spring-beans.xsd

       http://camel.apache.org/schema/spring

       http://camel.apache.org/schema/spring/camel-spring.xsd">
  **  ***<!--*

  * This repository will automatically be added to Camel's health check*
    * repository list.*

      * -->*
    **  **<bean id="hc-repo-routes" class="org.apache.camel.impl.health.RoutesHealthCheckRepository">
    **    **<property name="evaluators">
    **      **<list>
    **        ***<!--*
    * Set the checks that will be applied to every route if no per route*
      * configuration is defined, see below.*

        *    -->*
        **        **<bean class="org.apache.camel.impl.health.RoutePerformanceCounterEvaluators.ExchangesFailed">

        **          **<constructor-arg value="10"/>

        **        **</bean>

        **        **<bean class="org.apache.camel.impl.health.RoutePerformanceCounterEvaluators.LastProcessingTime">

        **          **<constructor-arg value="1000"/>

        **          **<constructor-arg value="1"/>

        **        **</bean>

        **      **</list>

        **    **</property>

        **    **<property name="routesEvaluators">

        **      **<map>

        **        ***<!--*

        * Set the checks to be associated with the route named route-1, note that*
          * default checks are not inherit so there will be only one check for this*

            * route.*

              *    -->*
              **        **<entry key="route-1">

              **          **<list>

              **            **<bean class="org.apache.camel.impl.health.RoutePerformanceCounterEvaluators.ExchangesInflight">

              **              **<constructor-arg value="10"/>

              **            **</bean>

              **          **</list>

              **        **</entry>

              **      **</map>

              **    **</property>

              **  **</bean>

              **  **<camelContext xmlns="http://camel.apache.org/schema/spring">

              **      **...

              **  **</camelContext></beans>

              ## 41.2. **编写自定义检查：**

              从2.20.0版本开始，Camel开箱即用提供的健康检查数量有限，因此您可能需要编写自己的检查，可以通过实现HealthCheck接口或扩展AbstractHealthCheck（提供一些有用的方法）来进行检查：

              public** **final** **class MyHealthCheck extends AbstractHealthCheck {

              **    **public ContextHealthCheck() {

              **        **super("camel", "my-check");

              **        ***// make this check enabled by default*

              **        **getConfiguration().setEnabled(true);

              **    **}

              **    **@Override

              **    **protected void doCall(HealthCheckResultBuilder builder, Map<String, Object> options) {

              **        ***// Default value*

              **        **builder.unknown();

              **        ***// Add some details to the check result*

              **        **builder.detail("my.detail", camelContext.getName());

              **        **if** **(unhealtyCondition) {

              **            **builder.down();

              **        **} else** **{

              **            **builder.up();

              **        **}

              **    **}

              }

              现在，您可以通过将实例添加到应用程序上下文（Spring，Blueprint）或直接添加到注册表中来使MyHealthCheck对骆驼可用。
