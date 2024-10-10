第七章 [**Enterprise Integration Patterns**](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)

**企业****集成****模式**

Camel支持Gregor Hohpe和Bobby Woolf著作中的大多数[企业集成模式](http://www.eaipatterns.com/toc.html)。

如果您不熟悉Camel，则需要先[使用](https://camel.apache.org/manual/latest/getting-started.html)用户指南中的[入门](https://camel.apache.org/manual/latest/getting-started.html)，然后再尝试实现这些模式。

1.1. **消息传递系统**


| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps1.jpg) | [Message Channel](https://camel.apache.org/manual/latest/message-channel.html "https://camel.apache.org/manual/latest/message-channel.html")          | 一个应用程序如何通过消息传递与另一应用程序通信？           |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps2.jpg) | [Message](https://camel.apache.org/manual/latest/message.html "https://camel.apache.org/manual/latest/message.html")                                  | 通过消息信道连接的两个应用程序如何交换一条信息？           |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps3.jpg) | [Pipes and Filters](https://camel.apache.org/manual/latest/pipeline-eip.html "https://camel.apache.org/manual/latest/pipeline-eip.html")              | 如何在具备独立性、灵活性的同时对消息执行复杂的处理？       |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps4.jpg) | [Message Router](https://camel.apache.org/manual/latest/message-router.html "https://camel.apache.org/manual/latest/message-router.html")             | 如何分离各处理步骤，根据一组条件将消息传递到不同的过滤器？ |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps5.jpg) | [Message Translator](https://camel.apache.org/manual/latest/message-translator.html "https://camel.apache.org/manual/latest/message-translator.html") | 使用不同数据格式的系统如何通过消息传递相互通信？           |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps6.jpg) | [Message Endpoint](https://camel.apache.org/manual/latest/message-endpoint.html "https://camel.apache.org/manual/latest/message-endpoint.html")       | 应用程序如何连接到消息传递信道以发送和接收消息？           |

1.2. **消息信道**


| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps7.png)  | [Point to Point Channel](https://camel.apache.org/manual/latest/point-to-point-channel.html "https://camel.apache.org/manual/latest/point-to-point-channel.html")          | 调用者如何才能确保恰好有一个接收者会收到文件或执行调用？                                                                       |
| ------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps8.png)  | [Publish Subscribe Channel](https://camel.apache.org/manual/latest/publish-subscribe-channel.html "https://camel.apache.org/manual/latest/publish-subscribe-channel.html") | 发送者如何向所有感兴趣的接收者广播事件？                                                                                       |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps9.png)  | [Dead Letter Channel](https://camel.apache.org/manual/latest/dead-letter-channel.html "https://camel.apache.org/manual/latest/dead-letter-channel.html")                   | 消息传递系统将如何处理无法传递的消息？                                                                                         |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps10.png) | [Guaranteed Delivery](https://camel.apache.org/manual/latest/guaranteed-delivery.html "https://camel.apache.org/manual/latest/guaranteed-delivery.html")                   | 即使消息系统发生故障，发送者如何确保消息将被传递？                                                                             |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps11.png) | [Channel Adapter](https://camel.apache.org/manual/latest/channel-adapter.html "https://camel.apache.org/manual/latest/channel-adapter.html")                               | 如何将应用程序连接到消息传递系统，以便它可以发送和接收消息？                                                                   |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps12.png) | [Messaging Bridge](https://camel.apache.org/manual/latest/messaging-bridge.html "https://camel.apache.org/manual/latest/messaging-bridge.html")                            | 如何连接多个消息传递系统，以便在一个消息传递系统上也可以在其他消息传递系统上。                                                 |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps13.png) | [Message Bus](https://camel.apache.org/manual/latest/message-bus.html "https://camel.apache.org/manual/latest/message-bus.html")                                           | 有什么体系结构可以使单独的应用程序协同工作，但又可以以分离的方式协同工作，从而可以轻松添加或删除应用程序而不影响其他应用程序？ |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps14.png) | [Change Data Capture](https://camel.apache.org/manual/latest/change-data-capture.html "https://camel.apache.org/manual/latest/change-data-capture.html")                   | 通过捕获对数据库所做的更改并将其应用于其他系统来实现数据同步。                                                                 |

1.3. **消息****结构**


| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps15.png) | [Event Message](https://camel.apache.org/manual/latest/event-message.html "https://camel.apache.org/manual/latest/event-message.html")                            | 如何使用消息传递将事件Event从一个应用程序传输到另一个应用程序？ |
| ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps16.png) | [Request Reply](https://camel.apache.org/manual/latest/request-reply.html "https://camel.apache.org/manual/latest/request-reply.html")                            | 当应用程序发送消息时，如何从接收方获得响应？                    |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps17.png) | [Return Address](https://camel.apache.org/manual/latest/return-address.html "https://camel.apache.org/manual/latest/return-address.html")                         | 回复者如何知道将回复发送到哪里？                                |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps18.png) | [Correlation Identifier](https://camel.apache.org/manual/latest/correlation-identifier.html "https://camel.apache.org/manual/latest/correlation-identifier.html") | 收到回复的请求者如何知道该回复是针对哪个请求的？                |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps19.png) | [Message Expiration](https://camel.apache.org/manual/latest/message-expiration.html "https://camel.apache.org/manual/latest/message-expiration.html")             | 发送者如何指示何时应将消息视为过时的消息，因此不应进行处理？    |

1.4. **消息****路由**


| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps20.png) | [Content Based Router](https://camel.apache.org/manual/latest/content-based-router-eip.html "https://camel.apache.org/manual/latest/content-based-router-eip.html")           | 我们如何处理单个逻辑功能（例如清单检查）的实现分布在多个物理系统上的情况？                                                           |
| ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps21.png) | [Message Filter](https://camel.apache.org/manual/latest/filter-eip.html "https://camel.apache.org/manual/latest/filter-eip.html")                                             | 组件如何避免收到不感兴趣的消息？                                                                                                     |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps22.png) | [Dynamic Router](https://camel.apache.org/manual/latest/dynamicRouter-eip.html "https://camel.apache.org/manual/latest/dynamicRouter-eip.html")                               | 如何在保持效率的情况下避免路由器对所有可能目标的依赖？                                                                               |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps23.png) | [Recipient List](https://camel.apache.org/manual/latest/recipientList-eip.html "https://camel.apache.org/manual/latest/recipientList-eip.html")                               | 我们如何将消息路由到（静态或动态）指定收件人列表？                                                                                   |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps24.png) | [Splitter](https://camel.apache.org/manual/latest/split-eip.html "https://camel.apache.org/manual/latest/split-eip.html")                                                     | 如果消息包含多个元素，而每个元素可能都必须以不同的方式进行处理，我们该如何处理？                                                     |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps25.png) | [Aggregator](https://camel.apache.org/manual/latest/aggregate-eip.html "https://camel.apache.org/manual/latest/aggregate-eip.html")                                           | 我们如何合并单个但相关的消息的结果，以便可以整体处理它们？                                                                           |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps26.png) | [Resequencer](https://camel.apache.org/manual/latest/resequence-eip.html "https://camel.apache.org/manual/latest/resequence-eip.html")                                        | 我们如何才能使相关但不按顺序排列的消息流返回正确的顺序？                                                                             |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps27.png) | [Composed Message Processor](https://camel.apache.org/manual/latest/composed-message-processor.html "https://camel.apache.org/manual/latest/composed-message-processor.html") | 处理包含多个元素（每个元素可能需要不同的处理）的消息时，如何维护整个消息流？                                                         |
|                                                                          | [Scatter-Gather](https://camel.apache.org/manual/latest/scatter-gather.html "https://camel.apache.org/manual/latest/scatter-gather.html")                                     | 当需要将一条消息发送给多个收件人（每个收件人都可以发送回复）时，如何维护整个消息流？                                                 |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps28.png) | [Routing Slip](https://camel.apache.org/manual/latest/routingSlip-eip.html "https://camel.apache.org/manual/latest/routingSlip-eip.html")                                     | 如果在设计时未知步骤的顺序，并且每条消息可能有所不同，我们如何通过一系列处理步骤连续地路由消息？                                     |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps29.png) | [Process Manager](https://camel.apache.org/manual/latest/process-manager.html "https://camel.apache.org/manual/latest/process-manager.html")                                  | 当所需的步骤在设计时可能不知道并且可能不是顺序的时，我们如何通过多个处理步骤路由消息？                                               |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps30.png) | [Message Broker](https://camel.apache.org/manual/latest/message-broker.html "https://camel.apache.org/manual/latest/message-broker.html")                                     | 如何将消息的目的地与发送者分离，并保持对消息流的集中控制？                                                                           |
|                                                                          | [Throttler](https://camel.apache.org/manual/latest/throttle-eip.html "https://camel.apache.org/manual/latest/throttle-eip.html")                                              | 如何限制消息以确保特定端点不会过载，或者我们不会超出某些外部服务的商定SLA？（SLA，Service-Level Agreement的缩写,意思是服务等级协议） |
|                                                                          | [Sampling](https://camel.apache.org/manual/latest/sample-eip.html "https://camel.apache.org/manual/latest/sample-eip.html")                                                   | 在给定时间段内从多条消息中采样一条消息，以避免下游路由不会过载？                                                                     |
|                                                                          | [Delayer](https://camel.apache.org/manual/latest/delay-eip.html "https://camel.apache.org/manual/latest/delay-eip.html")                                                      | 如何延迟发送消息？                                                                                                                   |
|                                                                          | [Load Balancer](https://camel.apache.org/manual/latest/loadBalance-eip.html "https://camel.apache.org/manual/latest/loadBalance-eip.html")                                    | 如何在多个端点之间平衡负载？                                                                                                         |
|                                                                          | [Circuit Breaker](https://camel.apache.org/manual/latest/circuitBreaker-eip.html "https://camel.apache.org/manual/latest/circuitBreaker-eip.html")                            | 如果服务中断，如何停止调用外部服务？                                                                                                 |
|                                                                          | [Service Call](https://camel.apache.org/manual/latest/serviceCall-eip.html "https://camel.apache.org/manual/latest/serviceCall-eip.html")                                     | 如何在分布式系统中调用远程服务，在分布式系统中可以从某种服务注册表中查找该服务？                                                     |
|                                                                          | [Saga](https://camel.apache.org/manual/latest/saga-eip.html "https://camel.apache.org/manual/latest/saga-eip.html")                                                           | 如何在Camel路由中定义一系列相关动作，这些动作要么应该成功完成（全部），要么不执行/没有补偿？                                         |
|                                                                          | [Multicast](https://camel.apache.org/manual/latest/multicast-eip.html "https://camel.apache.org/manual/latest/multicast-eip.html")                                            | 如何同时将消息路由到多个端点？                                                                                                       |
|                                                                          | [Loop](https://camel.apache.org/manual/latest/loop-eip.html "https://camel.apache.org/manual/latest/loop-eip.html")                                                           | 如何重复循环处理消息？                                                                                                               |

1.5. **消息****转换**


| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps31.png) | [Content Enricher](https://camel.apache.org/manual/latest/content-enricher.html "https://camel.apache.org/manual/latest/content-enricher.html")   | 如果消息始发者没有所有必需的数据项可用，我们如何与另一个系统通信？ |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps32.png) | [Content Filter](https://camel.apache.org/manual/latest/content-filter-eip.html "https://camel.apache.org/manual/latest/content-filter-eip.html") | 当您只对几个数据项感兴趣时，如何简化处理大消息的处理？             |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps33.png) | [Claim Check](https://camel.apache.org/manual/latest/claimCheck-eip.html "https://camel.apache.org/manual/latest/claimCheck-eip.html")            | 如何在不牺牲消息内容的情况下减少跨系统发送的消息的数据量？         |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps34.png) | [Normalizer](https://camel.apache.org/manual/latest/normalizer.html "https://camel.apache.org/manual/latest/normalizer.html")                     | 您如何处理语义上等效但以不同格式到达的消息？                       |
|                                                                          | [Sort](https://camel.apache.org/manual/latest/sort-eip.html "https://camel.apache.org/manual/latest/sort-eip.html")                               | 如何对消息体进行排序？                                             |
|                                                                          | [Script](https://camel.apache.org/manual/latest/script-eip.html "https://camel.apache.org/manual/latest/script-eip.html")                         | 如何执行可能不会更改消息的脚本？                                   |
|                                                                          | [Validate](https://camel.apache.org/manual/latest/validate-eip.html "https://camel.apache.org/manual/latest/validate-eip.html")                   | 如何验证消息？                                                     |

1.6. **消息端点**


|                                                                          | [Messaging Mapper](https://camel.apache.org/manual/latest/messaging-mapper.html "https://camel.apache.org/manual/latest/messaging-mapper.html")                    | 如何在域对象和消息传递基础结构之间移动数据，同时又使两者相互独立？ |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps35.png) | [Event Driven Consumer](https://camel.apache.org/manual/latest/eventDrivenConsumer-eip.html "https://camel.apache.org/manual/latest/eventDrivenConsumer-eip.html") | 当消息可用时，应用程序如何自动消费它们？                           |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps36.png) | [Polling Consumer](https://camel.apache.org/manual/latest/polling-consumer.html "https://camel.apache.org/manual/latest/polling-consumer.html")                    | 准备就绪后，应用程序如何消费消息？                                 |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps37.png) | [Competing Consumers](https://camel.apache.org/manual/latest/competing-consumers.html "https://camel.apache.org/manual/latest/competing-consumers.html")           | 消息传递客户端如何同时处理多个消息？                               |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps38.png) | [Message Dispatcher](https://camel.apache.org/manual/latest/message-dispatcher.html "https://camel.apache.org/manual/latest/message-dispatcher.html")              | 单个信道上的多个消费者如何协调他们的消息处理？                     |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps39.png) | [Selective Consumer](https://camel.apache.org/manual/latest/selective-consumer.html "https://camel.apache.org/manual/latest/selective-consumer.html")              | 消息消费者如何选择希望接收的消息？                                 |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps40.png) | [Durable Subscriber](https://camel.apache.org/manual/latest/durable-subscriber.html "https://camel.apache.org/manual/latest/durable-subscriber.html")              | 订阅者在不监听消息时如何避免丢失消息？                             |
|                                                                          | [Idempotent Consumer](https://camel.apache.org/manual/latest/idempotentConsumer-eip.html "https://camel.apache.org/manual/latest/idempotentConsumer-eip.html")     | 消息接收者如何处理重复的消息？                                     |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps41.png) | [Transactional Client](https://camel.apache.org/manual/latest/transactional-client.html "https://camel.apache.org/manual/latest/transactional-client.html")        | 客户端如何通过消息传递系统控制其事务？                             |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps42.png) | [Messaging Gateway](https://camel.apache.org/manual/latest/messaging-gateway.html "https://camel.apache.org/manual/latest/messaging-gateway.html")                 | 封装应用程序Rest接口如何对消息传递系统访问？                       |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps43.png) | [Service Activator](https://camel.apache.org/manual/latest/service-activator.html "https://camel.apache.org/manual/latest/service-activator.html")                 | 如何设计应用程序来调用通过消息、非消息传递技术的服务？             |

1.7. **系统管理**


| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps44.png) | [ControlBus](https://camel.apache.org/components/latest/controlbus-component.html "https://camel.apache.org/components/latest/controlbus-component.html") | 我们如何有效管理分布在多个平台和地理区域中的消息传递系统？      |
| ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps45.png) | [Detour](https://camel.apache.org/manual/latest/intercept.html "https://camel.apache.org/manual/latest/intercept.html")                                   | 如何通过中间步骤路由消息来执行验证、测试或调试功能？            |
| ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps46.png) | [Wire Tap](https://camel.apache.org/manual/latest/wireTap-eip.html "https://camel.apache.org/manual/latest/wireTap-eip.html")                             | 您如何检查在点对点信道上传播的消息？                            |
|                                                                          | [Message History](https://camel.apache.org/manual/latest/message-history.html "https://camel.apache.org/manual/latest/message-history.html")              | 我们如何在松散耦合的系统中有效地分析和调试消息流？              |
|                                                                          | [Log](https://camel.apache.org/manual/latest/log-eip.html "https://camel.apache.org/manual/latest/log-eip.html")                                          | 如何记录消息处理日志？                                          |
|                                                                          | [Step](https://camel.apache.org/manual/latest/step-eip.html "https://camel.apache.org/manual/latest/step-eip.html")                                       | Step将一组EIP组合在一起，形成一个用于度量和监视的复合逻辑单元。 |

1.7.1. **EIP图标**

EIP图标库以Visio模具文件的形式提供，适用于Camel颜色显示图标。[在此处](https://camel.apache.org/manual/latest/_attachments/Hohpe_EIP_camel_20150622.zip)下载它以获取演示文稿，功能和技术分析文档。

也可以在[OpenOffice 3.x Draw](https://camel.apache.org/manual/latest/_attachments/Hohpe_EIP_camel_OpenOffice.zip)，[Microsoft Visio](http://www.eaipatterns.com/download/EIP_Visio_stencil.zip)或[Omnigraffle中](http://www.graffletopia.com/stencils/137)使用原始的EIP模具。

# 1. [**Aggregate EIP**](https://camel.apache.org/manual/latest/aggregate-eip.html)

[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的[聚合器](http://www.enterpriseintegrationpatterns.com/Aggregator.html)允许将许多消息组合在一起成为一条消息。

![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps47.png)

关联[表达式](https://camel.apache.org/manual/latest/expression.html)用于确定应聚合在一起的消息。如果要将所有消息聚合到单个消息中，只需使用常量表达式。AggregationStrategy用于将单个关联key的所有消息exchange组合到单个消息exchange中。

## 1.1. **聚合器选项**

Aggregate EIP支持27个选项，如下所示:


| **名称**                             | **描述**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | **默认** | **类型**                             |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------------------------------ |
| **correlationExpression**            | **必需**用关联key计算聚合的的表达式。具有相同关联key的Exchange被聚合在一起。如果无法计算关联key，则抛出异常。您可以使用ignoreBadCorrelationKeys选项禁用此功能。                                                                                                                                                                                                                                                                                                                         |          | NamespaceAware Expression            |
| **completionPredicate**              | 用于指示汇总Exchange完成时间的断言。如果未指定，并且AggregationStrategy对象实现Predicate，则aggregationStrategy对象将用作completionPredicate。                                                                                                                                                                                                                                                                                                                                          |          | NamespaceAware Expression            |
| **completionTimeoutExpression**      | 以毫秒计的时间，聚合交换在完成（超时）之前应处于非活动状态。此选项可以设置为固定值，也可以使用动态计算超时的表达式 - 使用Long作为结果。如果两者都设置，并且表达式结果为null或0，Camel将回退使用固定值。您不能将此选项与completionInterval一起使用，只能使用其中一个。默认情况下，超时检查程序每秒运行一次，您可以使用completionTimeoutCheckerInterval选项来配置运行检查程序的频率。超时是近似值，并且无法保证在超时值之后准确触发超时。建议不要使用非常低的超时值或检查间隔。           |          | NamespaceAware Expression            |
| **completionSizeExpression**         | 聚合完成之前聚合的消息数。此选项可以设置为固定值或使用动态计算大小的表达式 - 将使用整数作为结果。如果两者都设置，如果表达式结果为null或0，则Camel将回退以使用固定值。                                                                                                                                                                                                                                                                                                                   |          | NamespaceAware Expression            |
| **optimisticLockRetryPolicy**        | 允许在使用乐观锁定时配置重试设置。                                                                                                                                                                                                                                                                                                                                                                                                                                                      |          | OptimisticLockRetry PolicyDefinition |
| **parallelProcessing**               | 聚合完成后，它们将从聚合器发送出去。此选项指示Camel是否应使用具有多个线程的线程池进行并发。如果未指定自定义线程池，则Camel将创建一个包含10个并发线程的默认池。                                                                                                                                                                                                                                                                                                                          | FALSE    | Boolean                              |
| **optimisticLocking**                | 开启乐观锁，这需要使用aggregationRepository，通过实现org.apache.camel.spi.OptimisticLockingAggregationRepository来支持。                                                                                                                                                                                                                                                                                                                                                                | FALSE    | Boolean                              |
| **executorServiceRef**               | 如果使用parallelProcessing，则可以指定要使用的自定义线程池。实际上，如果您不使用parallelProcessing，则此自定义线程池也用于发送聚合交换。                                                                                                                                                                                                                                                                                                                                                |          | String                               |
| **timeoutCheckerExecutorServiceRef** | 如果使用completionTimeout，completionTimeoutExpression或completionInterval选项之一，则会创建后台线程以检查每个聚合器的完成情况。设置此选项提供自定义线程池，而不是为每个聚合器创建新线程。                                                                                                                                                                                                                                                                                              |          | String                               |
| **aggregationRepositoryRef**         | 将自定义聚合存储库设置为使用默认情况下使用org.apache.camel.processor.aggregate.MemoryAggregationRepository                                                                                                                                                                                                                                                                                                                                                                              |          | String                               |
| **strategyRef**                      | 在Registry中查找AggregationStrategy的引用。必需配置AggregationStrategy，用于将传入的Exchange与现有已合并的Exchange合并。首先调用oldExchange参数为null。在后续调用中，oldExchange包含合并的交换，newExchange当然是新的传入Exchange。                                                                                                                                                                                                                                                     |          | String                               |
| **strategyMethodName**               | 当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。                                                                                                                                                                                                                                                                                                                                                                                                             |          | String                               |
| **strategyMethodAllowNull**          | 如果此选项为false，则聚合方法不会用于第一个聚合。如果此选项为true，则在将POJO用作AggregationStrategy时，将使用null值作为oldExchange（在第一个聚合处）。                                                                                                                                                                                                                                                                                                                                 | FALSE    | Boolean                              |
| **completionSize**                   | 聚合完成之前聚合的消息数。此选项可以设置为固定值或使用允许您动态计算大小的表达式 - 将使用整数作为结果。如果两者都设置，如果表达式结果为null或0，则Camel将回退以使用固定值。                                                                                                                                                                                                                                                                                                             |          | Integer                              |
| **completionInterval**               | 以毫秒为单位的重复周期，聚合器将通过该周期完成所有当前聚合交换。Camel有一个后台任务，每个时段都会触发。您不能将此选项与completionTimeout一起使用，只能使用其中一个。                                                                                                                                                                                                                                                                                                                    |          | Long                                 |
| **completionTimeout**                | 以毫秒计的时间，聚合交换在完成（超时）之前应处于非活动状态。此选项可以设置为固定值，也可以使用允许您动态计算超时的表达式 - 将使用Long作为结果。如果两者都设置，如果表达式结果为null或0，Camel将回退使用固定值。您不能将此选项与completionInterval一起使用，只能使用其中一个。默认情况下，超时检查程序每秒运行一次，您可以使用completionTimeoutCheckerInterval选项来配置运行检查程序的频率。超时是近似值，并且无法保证在超时值之后准确触发超时。建议不要使用非常低的超时值或检查器间隔。 |          | Long                                 |
| **completionTimeoutCheckerInterval** | 检查超时的后台任务使用的millis间隔（org.apache.camel.TimeoutMap）。默认情况下，超时检查程序每秒运行一次。超时是近似值，并且无法保证在超时值之后准确触发超时。建议不要使用非常低的超时值或检查器间隔。                                                                                                                                                                                                                                                                                   | 1000     | Long                                 |
| **completionFromBatchConsumer**      | 启用批处理完成模式，我们从org.apache.camel.BatchConsumer聚合，并通过检查交换属性org.apache.camel.Exchange＃BATCH_COMPLETE来汇总org.apache.camel.BatchConsumer报告的总交换总数。此选项不能与discardOnAggregationFailure一起使用。                                                                                                                                                                                                                                                        | FALSE    | Boolean                              |
| **completionOnNewCorrelationGroup**  | 在新传入关联group时，在先前所有组上开启完成。例如，在连续顺序时完成具有相同关联key的组。请注意，如果启用此选项，则只有1个关联组可以正在进行，就像新的关联组启动时一样，然后强制完成先前的组。                                                                                                                                                                                                                                                                                           | FALSE    | Boolean                              |
| **eagerCheckCompletion**             | 使用急切完成检查，这意味着completionPredicate将使用incoming的Exchange。否则，completionPredicate将使用聚合的Exchange。                                                                                                                                                                                                                                                                                                                                                                  | FALSE    | Boolean                              |
| **ignoreInvalidCorrelationKeys**     | 如果无法成功计算关联key，则通过记录DEBUG将忽略该关联key，然后忽略传入的Exchange。                                                                                                                                                                                                                                                                                                                                                                                                       | FALSE    | Boolean                              |
| **closeCorrelationKeyOnCompletion**  | 完成时关闭相关key。任何迟到的交换都有一个已关闭的关联key，它将被定义并抛出ClosedCorrelationKeyException。                                                                                                                                                                                                                                                                                                                                                                               |          | Integer                              |
| **discardOnCompletionTimeout**       | 在完成超时时丢弃聚合消息。这意味着在超时时，聚合消息将被丢弃，而不会从聚合器发送出去。                                                                                                                                                                                                                                                                                                                                                                                                  | FALSE    | Boolean                              |
| **discardOnAggregationFailure**      | 聚合失败时丢弃聚合消息（从AggregationStrategy抛出异常。这意味着部分聚合的消息被丢弃而不是从聚合器发出。此选项不能与completionFromBatchConsumer一起使用。                                                                                                                                                                                                                                                                                                                                | FALSE    | Boolean                              |
| **forceCompletionOnStop**            | 表示在上下文停止时完成所有当前聚合的交换                                                                                                                                                                                                                                                                                                                                                                                                                                                | FALSE    | Boolean                              |
| **completeAllOnStop**                | 表示在上下文停止时等待完成所有当前和部分（挂起）聚合交换。这也意味着我们将等待存储在聚合存储库中的所有挂起的交换完成，因此存储库在我们停止之前是空的。您可能希望在使用基于内存的聚合存储库时启用此功能，并且不要将数据存储在磁盘上。启用此选项后，聚合器将在停止CamelContext或使用它的路由之前等待其停止之前完成所有这些交换。                                                                                                                                                          | FALSE    | Boolean                              |
| **aggregateControllerRef**           | 使用org.apache.camel.processor.aggregate.AggregateController允许外部源控制此聚合器。                                                                                                                                                                                                                                                                                                                                                                                                    |          | String                               |

## 1.2. **关于AggregationStrategy**

AggregationStrategy用于聚合（通过其关联ID查找）两个exchange到单个的exchange。可能的实现包括执行某种组合或增强处理，例如将订单项一起添加到发票中或只使用其中一个删除而另一个exchange，例如跟踪状态或市场数据价格; 比较早的值很少使用。

请注意，聚合策略是强制选项，必须提供给聚合器。

以下是一些AggregationStrategy示例实现，可帮助您创建自己的自定义策略。

*//simply combines Exchange String body values using '+' as a delimiter*

class StringAggregationStrategy implements AggregationStrategy {

**    **public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

**        **if** **(oldExchange == null) {

**            **return** **newExchange;

**        **}

**        **String oldBody = oldExchange.getIn().getBody(String.class);

**        **String newBody = newExchange.getIn().getBody(String.class);

**        **oldExchange.getIn().setBody(oldBody + "+"** **+ newBody);

**        **return** **oldExchange;

**    **}

}

*//simply combines Exchange body values into an ArrayList<Object>*

class ArrayListAggregationStrategy implements AggregationStrategy {

**    **public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

**        **Object newBody = newExchange.getIn().getBody();

**        **ArrayList<Object> list = null;

**        **if** **(oldExchange == null) {

**            **list = new** **ArrayList<Object>();

**            **list.add(newBody);

**            **newExchange.getIn().setBody(list);

**            **return** **newExchange;

**        **} else** **{

**            **list = oldExchange.getIn().getBody(ArrayList.class);

**            **list.add(newBody);

**            **return** **oldExchange;

**        **}

**    **}

}

## 1.3. **关于Completion****（****完成****）**

在某个时刻进行汇总[Exchange](https://camel.apache.org/manual/latest/exchange.html)时，您需要指出汇总[Exchange](https://camel.apache.org/manual/latest/exchange.html)已完成，以便可以将其发送到聚合器之外，Camel允许您以以下各种方式指示完成情况:

l completionTimeout	——如果在该时间段内没有为该关联键聚合新的交换，则触发不活动超时。

l completionInterval	——每个X周期结束所有当前聚合交换。

l completionSize		——是一个数字，表示在X次聚合交换后，它完成了。

l completionPredicate	——在聚合新交换时运行[断言](https://camel.apache.org/manual/latest/predicate.html)，以确定是否完成。配置的aggregationStrategy可以实现Predicate接口，如果没有配置，completionPredicate将被用作completionPredicate。配置的aggregationStrategy可以实现PreCompletionAwareAggregationStrategy并将在每个完成检查模式中作为completionPredicate。有关详细信息，请参见下文。

l completionFromBatchConsumer	——[批处理消费者的](https://camel.apache.org/manual/latest/batch-consumer.html)特殊选项，允许您在聚合来自批处理的所有消息时完成。

l forceCompletionOnStop			——表示在上下文停止时完成所有当前聚合的交换。

l 使用AggregateController**	**	——允许使用外部源来完成组或所有组。这可以使用Java或JMX API完成。

请注意，所有完成方式都是每个关联键的（per correlation key）。您可以以任何您喜欢的方式组合它们。它基本上是第一个触发的。因此，您可以使用完成大小和完成超时。只有completionTimeout和completionInterval不能同时使用。

请注意，完成是强制选项，必须提供给聚合器。如果没有提供，Camel将在启动时抛出异常。

## 1.4. **预完成模式**

**从Camel 2.16开始提供**

可能存在这样的用例：您希望新传入的[Exchange](https://camel.apache.org/manual/latest/exchange.html)确定关联组是否应该预先完成，然后新传入的[Exchange](https://camel.apache.org/manual/latest/exchange.html)从头开始创建新组。要确定这个，AggregationStrategy可以实现PreCompletionAwareAggregationStrategy的preComplete方法:

**    ***/***

* * Determines if the aggregation should complete the current group, and start a new group, or the aggregation*
  * * should continue using the current group.*
  ---

  *     * **@param** oldExchange the oldest exchange (is <tt>null</tt> on first aggregation as we only have the new exchange)*
  *     * **@param** newExchange the newest exchange (can be <tt>null</tt> if there was no data possible to acquire)*
  *     * **@return** <tt>true</tt> to complete current group and start a new group, or <tt>false</tt> to keep using current*
  * */*
  **    **boolean preComplete(Exchange oldExchange, Exchange newExchange);

  如果preComplete方法返回true，则完成目前的组（不聚合新传入交换（newExchange）。然后使用newExchange从头开始关联组，这样组只包含新传入交换。这是已知的作为预完成模式。当聚合处于预完成模式时，则仅使用以下完成

  l aggregationStrategy必须实现PreCompletionAwareAggregationStrategy** **xxx。

  l completionTimeout或completionInterval也可用作回退完成。

  l 不使用任何其他完成（例如按大小，批量消费者等）。

  l eagerCheckCompletion隐含为true，但该选项无效。

  ## 1.5. **持久聚合存储库**

  聚合器提供可插拔的存储库，您可以实现自己的存储库org.apache.camel.spi.AggregationRepository。

  如果您需要持久化存储库，则可以使用Camel [LevelDB](https://camel.apache.org/components/latest/leveldb.html)或[SQL Component](https://camel.apache.org/components/latest/sql-component.html)组件。

  ## 1.6. **使用TimeoutAwareAggregationStrategy**

  **从Camel 2.9.2开始提供**

  如果您的聚合策略实现TimeoutAwareAggregationStrategy，那么Camel将在超时发生时调用timeout方法。请注意，index和total参数的值将为-1，并且仅当配置为固定值时才会提供timeout参数。您**不得**抛出timeout方法的任何异常。

  ## 1.7. **使用CompletionAwareAggregationStrategy**

  **自Camel 2.9.3起可用**

  如果您的聚合策略实现CompletionAwareAggregationStrategy，那么Camel将在聚合Exchange完成时调用onComplete方法。这允许您执行任何最后一分钟的自定义逻辑，例如清理某些资源，或者现在已完成的交换上的其他工作。

  您**不得**抛出该onCompletion方法的任何异常。

  ## 1.8. **完成当前组由AggregationStrategy决定**

  **自Camel 2.15起可用**

  现在AggregationStrategy可以包含一个返回Exchange的属性，该属性包含一个布尔值，用于指示是否应该完成当前组。这允许否决任何现有的完成断言/大小/超时等，并完成组。

  例如，如果消息体大小大于5，则以下逻辑（来自单元测试）将完成该组。这可以通过将属性Exchange.AGGREGATION_COMPLETE_CURRENT_GROUP设置为true来完成。

  **    **public** **final** **class MyCompletionStrategy implements AggregationStrategy {

  **        **@Override

  **        **public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

  **            **if** **(oldExchange == null) {

  **                **return** **newExchange;

  **            **}

  **            **String body = oldExchange.getIn().getBody(String.class) + "+"

  **                **+ newExchange.getIn().getBody(String.class);

  **            **oldExchange.getIn().setBody(body);

  **            **if** **(body.length() >= 5) {

  **                **oldExchange.setProperty(Exchange.AGGREGATION_COMPLETE_CURRENT_GROUP, true);

  **            **}

  **            **return** **oldExchange;

  **        **}

  **    **}

  ## 1.9. **完成所有先前组****由****AggregationStrategy决定**

  **自Camel 2.21起可用**

  现在AggregationStrategy可以包含一个返回的Exchange属性，该属性包含一个布尔值，用于指示是否应该完成所有以前的组。这允许否决任何现有的完成断言/大小/超时等，并完成所有现有的先前组。

  例如，以下逻辑（来自单元测试）将在启动新聚合组时完成所有先前组。这是通过将属性Exchange.AGGREGATION_COMPLETE_ALL_GROUPS设置为true来完成的。

  **    **public** **final** **class MyCompletionStrategy implements AggregationStrategy {

  **        **@Override

  **        **public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

  **            **if** **(oldExchange == null) {

  **                ***// we start a new correlation group, so complete all previous groups*

  **                **newExchange.setProperty(Exchange.AGGREGATION_COMPLETE_ALL_GROUPS, true);

  **                **return** **newExchange;

  **            **}

  **            **String body1 = oldExchange.getIn().getBody(String.class);

  **            **String body2 = newExchange.getIn().getBody(String.class);

  **            **oldExchange.getIn().setBody(body1 + body2);

  **            **return** **oldExchange;

  **        **}

  **    **}

  ## 1.10. **手动强制立即完成所有聚合交换**

  **自Camel 2.9起可用**

  您可以通过发送包含头Exchange.AGGREGATION_COMPLETE_ALL_GROUPS，并设置为true的消息来手动触发所有当前聚合交换的完成。该消息仅被视为信号消息，否则将不处理消息头/内容。

  可以可选地设置消息头Exchange.AGGREGATION_COMPLETE_ALL_GROUPS_INCLUSIVE为true以触发当前消息处理后，触发所有组的完成。

  ## 1.11. **在AggregationStrategy中使用List<V>**

  **自Camel 2.11起可用**

  如果你想将消息中的某些<V>值聚合到List<V>那么我们添加了一个抽象类org.apache.camel.processor.aggregate.AbstractListAggregationStrategy。从聚合器发出的已完成Exchange将包含在消息体中的List<V>。

  例如，要聚合List<Integer>您可以扩展此类并实现getValue方法，如下所示:

  ## 1.12. **使用AggregateController**

  **自Camel 2.16起可用**

  在运行时org.apache.camel.processor.aggregate.AggregateController允许您使用Java或JMX API控制聚合。可用于强制完成交换组，或查询其当前运行时统计信息。

  如果没有自定义配置，提供默认实现聚合器，可以使用getAggregateController()方法访问。通过aggregateController在路由中配置控制器可能更容易，如下所示:

  private** **AggregateController controller = new** **DefaultAggregateController();

  from("direct:start")

  **   **.aggregate(header("id"), new** **MyAggregationStrategy())

  **      **.completionSize(10).id("myAggregator")

  **      **.aggregateController(controller)

  **      **.to("mock:aggregated");

  然后在AggregateController上有API来强制完成。例如，用键foo完成一个组

  int** **groups = controller.forceCompletionOfGroup("foo");

  返回的数字是完成的组数。在这种情况下，如果foo组存在并且已经完成，则为1。如果foo不存在则返回0。

  还有一个api来完成所有组

  int** **groups = controller.forceCompletionOfAllGroups();

  从XML DSL配置它

  <bean id="myController" class="org.apache.camel.processor.aggregate.DefaultAggregateController"/>

  **  **<camelContext xmlns="http://camel.apache.org/schema/spring">

  **        **<route>

  **            **<from uri="direct:start"/>

  **            **<aggregate strategyRef="myAppender" completionSize="10"

                     aggregateControllerRef="myController">
  **                **<correlationExpression>

  **                    **<header>id</header>

  **                **</correlationExpression>

  **                **<to uri="mock:result"/>

  **            **</aggregate>

  **        **</route>

  **    **</camelContext>

  聚合器上还有JMX API，可在Camel JMX树的处理器节点下使用。

  ## 1.13. **使用G****r****oupedExchanges**

  在下面的路由中，我们使用groupExchanges()将所有Exchange组合在一起:

  from("direct:start")

  **    ***// aggregate all using same expression*

  **    **.aggregate(constant(true))

  **    ***// wait for 0.5 seconds to aggregate*

  **    **.completionTimeout(500L)

  **    ***// group the exchanges so we get one single exchange containing all the others*

  **    **.groupExchanges()

  **    **.to("mock:result");

  结果，我们传出一个Exchange路由到"mock:result"端点。Exchange是包含所有入站的Exchange。

  然后，聚合器的输出将包含在列表中组合在一起的交换，如下所示:

  List<Exchange> grouped = exchange.getIn().getBody(List.class);

  ## 1.14. **使用POJO作为AggregationStrategy**

  **自Camel 2.12起可用**

  要使用AggregationStrategy你必须实现org.apache.camel.AggregationStrategy接口，这意味着你的逻辑将绑定到Camel API。您可以使用POJO作为逻辑，让Camel适应您的POJO。要使用POJO，必须遵守惯例:

  l 必须有一个public方法来使用。

  l 该方法不可以使用void。

  l 该方法可以是静态的或非静态的。

  l 该方法必须具有2个或更多参数。

  l 参数配对，前50％应用于oldExchange而另50％用于newExchange。

  l 上一条意味着必须有相同数量的参数，例如2,4,6等。

  l 方法配对预计按如下方式排序:

  ○ 第一个参数是消息体

  ○ 第二个参数是消息头的Map

  ○ 第3个参数是Exchange属性的Map

  最好用一些例子解释这个约定。

  在下面的方法中，我们只有2个参数，所以第一个参数是oldExchange消息体，第二个参数是newExchange消息体:

  public String append(String existing, String next) {

  **  **return** **existing + next;

  }

  在下面的方法中，我们只有4个参数，所以第一个参数是oldExchange消息体，第二个是oldExchange消息头的Map，第三个是与newExchange配对消息体，第四个参数是newExchange消息头的Map:

  public String append(String existing, Map existingHeaders, String next, Map nextHeaders) {

  **  **return** **existing + next;

  }

  最后，如果我们有6个参数，我们也有Exchange的属性:

  public String append(String existing, Map existingHeaders, Map existingProperties,

                   String next, Map nextHeaders, Map nextProperties) {
  **  **return** **existing + next;

  }

  要将此与Aggregate EIP一起使用，我们可以使用具有聚合逻辑的POJO，如下所示:

  public** **class MyBodyAppender {

  **    **public String append(String existing, String next) {

  **        **return** **next + existing;

  **    **}

  }

  然后在Camel路由中我们创建bean的一个实例，然后引用路由中org.apache.camel.builder.AggregationStrategies的bean方法bean，如下所示 :

  private** **MyBodyAppender appender = new** **MyBodyAppender();

  public void configure() throws Exception {

  **    **from("direct:start")

  **        **.aggregate(constant(true), AggregationStrategies.bean(appender, "append"))

  **            **.completionSize(3)

  **            **.to("mock:result");

  }

  我们也可以直接提供bean class:

  public void configure() throws Exception {

  **    **from("direct:start")

  **        **.aggregate(constant(true), AggregationStrategies.bean(MyBodyAppender.class, "append"))

  **            **.completionSize(3)

  **            **.to("mock:result");

  }

  如果bean只有一个方法，我们不需要指定方法的名称:

  public void configure() throws Exception {

  **    **from("direct:start")

  **        **.aggregate(constant(true), AggregationStrategies.bean(MyBodyAppender.class))

  **            **.completionSize(3)

  **            **.to("mock:result");

  }

  并且append方法可以是静态的:

  public** **class MyBodyAppender {

  **    **public static String append(String existing, String next) {

  **        **return** **next + existing;

  **    **}

  }

  如果您使用的是XML DSL，那么我们需要使用POJO声明一个<bean>:

  <bean id="myAppender" class="com.foo.MyBodyAppender"/>

  在Camel路由中，我们使用strategyRef通过其id来引用bean，并且strategyMethodName可以用来定义要调用的方法名称:

  <camelContext xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:start"/>

  **        **<aggregate strategyRef="myAppender" strategyMethodName="append" completionSize="3">

  **            **<correlationExpression>

  **                **<constant>true</constant>

  **            **</correlationExpression>

  **            **<to uri="mock:result"/>

  **        **</aggregate>

  </route>

  </camelContext>

  使用XML DSL时，必须将POJO定义为<bean>。

  ## 1.15. **没有数据时聚合**

  默认情况下，当使用POJO作为AggregationStrategy时，**只有**在聚合数据时**才会**调用其方法（默认情况下）。您可以使用strategyMethodAllowNull选项进行配置。

  在不使用POJO的情况下，您可以使用null** **作为oldExchange或newExchange参数。例如，对于传入聚合器的第一个Exchange，Aggregate EIP将调用AggregationStrategy并使用null参数的oldExchange** **。然后进行后续[Exchange](https://camel.apache.org/manual/latest/exchange.html)时oldExchange和newExchange参数都不能为null。

  **Content Enricher EIP示例，没有数据****时**

  尽管使用POJO作为AggregationStrategy我们使此过程更简单，并且只在oldExchange和newExchange不为null时才调用方法，因为这是最常见的用例。

  如果您需要允许oldExchange或newExchange为null，则可以使用AggregationStrategyBeanAdapter的POJO进行配置。在bean适配器上，我们调用setAllowNullNewExchange允许新的交换为null，如下所示。

  public void configure() throws Exception {

  **    **AggregationStrategyBeanAdapter myStrategy = new** **AggregationStrategyBeanAdapter(appender, "append");

  **    **myStrategy.setAllowNullOldExchange(true);

  **    **myStrategy.setAllowNullNewExchange(true);

  **    **from("direct:start")

  **        **.pollEnrich("seda:foo", 1000, myStrategy)

  **            **.to("mock:result");

  }

  使用AggregationStrategies的beanAllowNull方法可以更容易地配置它，如下所示:

  public void configure() throws Exception {

  **    **from("direct:start")

  **        **.pollEnrich("seda:foo", 1000, AggregationStrategies.beanAllowNull(appender, "append"))

  **            **.to("mock:result");

  }

  然后POJO中的append方法需要处理newExchange可以为null 的情况:

  public** **class MyBodyAppender {

  **    **public String append(String existing, String next) {

  **        **if** **(next == null) {

  **            **return** **"NewWasNull"** **+ existing;

  **        **} else** **{

  **            **return** **existing + next;

  **        **}

  **    **}

  }

  在上面的示例中，我们使用了[Content Enricher](https://camel.apache.org/manual/latest/content-enricher.html) EIP的pollEnrich。newExchange在无法从"seda:foo"端点获取到数据的情况下将为null，1秒后超时命中。因此，如果我们需要设置一些特殊的merge逻辑，我们需要设置setAllowNullNewExchange=true，因此append将调用该方法。如果我们不这样做，那么当超时被命中时，通常不会调用append方法，这意味着[Content Enricher](https://camel.apache.org/manual/latest/content-enricher.html)没有合并/更改消息。

  在XML DSL中，您可以配置该strategyMethodAllowNull选项并将其设置为true，如下所示:

  <camelContext xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:start"/>

  **        **<aggregate strategyRef="myAppender"

                 strategyMethodName="append"

                 strategyMethodAllowNull="true"

                 completionSize="3">
  **            **<correlationExpression>

  **                **<constant>true</constant>

  **            **</correlationExpression>

  **            **<to uri="mock:result"/>

  **        **</aggregate>

  </route>

  </camelContext>

  ## 1.16. **不一样****的****消息体类型**

  例如，当strategyMethodAllowNull设置为true时，消息体的参数类型不必相同。例如，假设我们想要从com.foo.User类型聚合到包含用户名的List<String>类型。我们可以按如下方式编写POJO代码:

  public** **static** **final** **class MyUserAppender {

  **    **public List addUsers(List names, User user) {

  **        **if** **(names == null) {

  **            **names = new** **ArrayList();

  **        **}

  **        **names.add(user.getName());

  **        **return** **names;

  **    **}

  }

  请注意，返回类型是我们要包含用户名的List。第一个参数是名称List，然后注意第二个参数是传入com.foo.User类型。

  # 2. [**Batch-Config EIP**](https://camel.apache.org/manual/latest/batch-config-eip.html)

  批处理重新排序EIP

  Batch-config EIP支持5个选项，如下所示:


  | **名称**                   | **描述**                                             | **默认** | **类型** |
  | -------------------------- | ---------------------------------------------------- | -------- | -------- |
  | **batchSize**              | 设置批次的要重新排序的大小。默认大小为100。          | 100      | Integer  |
  | **batchTimeout**           | 设置收集元素的要重新排序的超时。默认超时为1000毫秒。 | 1000     | Long     |
  | **allowDuplicates**        | 是否允许重复。                                       | FALSE    | Boolean  |
  | **reverse**                | 是否逆序。                                           | FALSE    | Boolean  |
  | **ignoreInvalidExchanges** | 是否忽略无效的交换Exchange                           | FALSE    | Boolean  |

  # 3. [**Bean EIP**](https://camel.apache.org/manual/latest/bean-eip.html)

  Bean EIP将bean绑定到Camel消息交换。

  ## 3.1. **URI格式**

  bean:beanID[?options]

  其中**beanID**是在[Registry中](https://camel.apache.org/manual/latest/registry.html)查找bean的任何字符串。

  ## 3.2. **EIP选项**

  Bean EIP支持4个选项，如下所示


  | **名称**     | **描述**                                   | **默认** | **类型** |
  | ------------ | ------------------------------------------ | -------- | -------- |
  | **ref**      | 设置bean的引用                             |          | String   |
  | **method**   | 设置要使用的bean的方法名称                 |          | String   |
  | **beanType** | 设置bean的Class                            |          | String   |
  | **cache**    | 缓存bean查找，以避免在每次使用时查找bean。 | TRUE     | Boolean  |

  :

  ## 3.3. **Bean作为端点**

  Camel还支持调用[Bean](https://camel.apache.org/components/latest/bean-component.html)作为端点。在以下路由中:

  发生的事情是，当交换路由到myBean时，Camel将使用[Bean Binding](https://camel.apache.org/manual/latest/bean-binding.html)来调用bean。

  bean的来源只是一个简单的POJO:

  Camel将使用[Bean Binding](https://camel.apache.org/manual/latest/bean-binding.html)来调用sayHello方法，方法是将Exchange的In body转换为String类型并将方法的输出存储在Exchange Out体上。

  ## 3.4. **Java DSL Bean语法**

  Java DSL附带了[Bean](https://camel.apache.org/components/latest/bean-component.html)组件的语法。您可以使用以下语法，而不是将bean明确指定为端点（即to("bean:beanName")）。

  *// Send message to the bean endpoint*

  *// and invoke method resolved using Bean Binding.*

  from("direct:start").beanRef("beanName");

  *// Send message to the bean endpoint*

  *// and invoke given method.*

  from("direct:start").beanRef("beanName", "methodName");

  您可以指定bean自身，而不是将引用的名称传递给bean（以便Camel将在注册表中查找它）:

  *// Send message to the given bean instance.*

  from("direct:start").bean(new** **ExampleBean());

  *// Explicit selection of bean method to be invoked.*

  from("direct:start").bean(new** **ExampleBean(), "methodName");

  *// Camel will create the instance of bean and cache it for you.*

  from("direct:start").bean(ExampleBean.class);

  ## 3.5. **Bean绑定**

  如何选择要调用的bean方法（如果未通过**method**参数显式指定它们）以及如何从[Message](https://camel.apache.org/manual/latest/message.html)构造参数值都是由[Bean绑定](https://camel.apache.org/manual/latest/bean-binding.html)机制定义的，该机制在Camel的所有各种[Bean集成](https://camel.apache.org/manual/latest/bean-integration.html)机制中使用。

  # 4. [**Choice EIP**](https://camel.apache.org/manual/latest/choice-eip.html)

  [EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)中[基于内容的路由器](http://www.enterpriseintegrationpatterns.com/ContentBasedRouter.html)可以让你将消息基于交换的内容路由到正确的目的地。

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps48.png)

  ## 4.1. **Choice选项**

  Choice EIP支持以下列出的2个选项:


  | **名称**        | **描述**     | **默认** | **类型**            |
  | --------------- | ------------ | -------- | ------------------- |
  | **whenClauses** | 设置when子句 |          | List                |
  | **otherwise**   | 设置其他节点 |          | OtherwiseDefinition |

  ## 4.2. **例子**

  以下示例显示如何将请求从输入端点**seda****:****a**路由到**seda****:****b****、****seda****:****c**或**seda****:****d，**具体取决于各种[Predicate](https://camel.apache.org/manual/latest/predicate.html)表达式的计算结果

  RouteBuilder builder = new** **RouteBuilder() {

  **    **public void configure() {

  **        **from("direct:a")

  **            **.choice()

  **                **.when(simple("${header.foo} == 'bar'"))

  **                    **.to("direct:b")

  **                **.when(simple("${header.foo} == 'cheese'"))

  **                    **.to("direct:c")

  **                **.otherwise()

  **                    **.to("direct:d");

  **    **}

  };


  |  | 如果您使用when或otherwise遇到Java DSL问题，请参阅[为什么我不能在Java Camel路由中使用when或otherwise](https://camel.apache.org/manual/latest/faq/why-can-i-not-use-when-or-otherwise-in-a-java-camel-route.html)。 |
  | - | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

  使用Xml的相同示例:

  <camelContext xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:a"/>

  **        **<choice>

  **            **<when>

  **                **<simple>${header.foo} == 'bar'</simple>

  **                **<to uri="direct:b"/>

  **            **</when>

  **            **<when>

  **                **<simple>${header.foo} == 'cheese'</simple>

  **                **<to uri="direct:c"/>

  **            **</when>

  **            **<otherwise>

  **                **<to uri="direct:d"/>

  **            **</otherwise>

  **        **</choice>

  </route>

  </camelContext>

  # 5.  [**CircuitBreaker****EIP**](https://camel.apache.org/manual/latest/circuitBreaker-eip.html)

  断路器模式的灵感来自于现实世界中的断路器，该断路器用于检测过多的电流消耗并快速失效以保护电气设备。基于软件的断路器通过封装操作并监视其故障来遵循相同的概念。断路器模式在三种状态下运行，如下图所示：

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps49.jpg)

  状态如下：

  l **Closed** 				——成功运行时。

  l **open**  				——当检测到故障，断路器断开短路和快速失败。在这种状态下，断路器避免了调用受保护的操作，并且避免了在满负荷的服务上增加额外的负载。

  l **Half Open**（**半开）** 	——在打开状态中短暂运行后，将尝试查看某个操作是否可以成功完成，并且根据结果，该操作将转换为打开或关闭状态。

  ## 5.1. **例**

  以下是显示路由终端端点的示例路由，该端点通过回退到内联的回退路由来防止运行缓慢。默认情况下，超时请求仅为**1000ms，**因此HTTP端点必须相当快才能成功。

  from("direct:start")

  **    **.circuitBreaker()

  **        **.to("http://fooservice.com/slow")

  **    **.onFallback()

  **        **.transform().constant("Fallback message")

  **    **.end()

  **    **.to("mock:result");

  在XML DSL中：

  <camelContext xmlns="http://camel.apache.org/schema/spring">

  **  **<route>

  **    **<from uri="direct:start"/>

  **    **<circuitBreaker>

  **      **<to uri="http://fooservice.com/slow"/>

  **      **<onFallback>

  **        **<transform>

  **          **<constant>Fallback message</constant>

  **        **</transform>

  **      **</onFallback>

  **    **</circuitBreaker>

  **    **<to uri="mock:result"/>

  **  **</route>

  </camelContext>

  ## 5.2. **CircuitBreaker****实现**

  Camel提供了这种模式的两种实现：

  l [Hystrix**	**	——](https://camel.apache.org/manual/latest/hystrix-eip.html)使用Netflix Hystrix实现。

  l [Resilience4j**	**——](https://camel.apache.org/manual/latest/resilience4j-eip.html)使用Resilience4j实现。

  # 6. [**Claim Check EIP**](https://camel.apache.org/manual/latest/claimCheck-eip.html)

  **自Camel 2.21起可用**

  来自[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的[Claim Check](http://www.enterpriseintegrationpatterns.com/patterns/messaging/StoreInLibrary.html)允许您使用声明检查（唯一键）替换消息内容，该声明检查可用于稍后检索消息内容。

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps50.png)

  在您不信任外部系统信息的情况下，它也很有用; 在这种情况下，您可以使用声明检查来隐藏数据的敏感部分。


  |  | 此EIP模式的Camel实现将消息内容临时存储在内部存储器中。 |
  | - | ------------------------------------------------------ |

  Claim Check EIP支持5个选项，如下所示:


  | **名称**               | **描述**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | **默认** | **类型**            |
  | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | ------------------- |
  | **operation**          | **必****选项，要**使用的声明检查操作。支持以下操作:Get - 获取（不删除）给定键的声明检查。GetAndRemove - 获取并删除给定键的声明检查。Set - 使用给定key设置新的（将覆盖密钥已存在）声明检查。Push - 在堆栈上设置新的声明检查（不使用key）。Pop - 从堆栈中获取最新的索赔检查（不使用key）。                                                                                                                                                                                                                                                                                                                                                                     |          | ClaimCheckOperation |
  | **key**                | 使用给定key进行申明检查的id（对于动态key，使用简单语言语法作为key）。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |          | String              |
  | **filter**             | 指定一个过滤器来控制哪些数据从声明检查存储库中合并数据。支持以下语法:body - 聚合消息体attachments - 聚合所有消息附件headers - 聚合所有消息头header:pattern - 聚合与模式匹配的所有消息头。该模式使用以下规则并按顺序应用:精确匹配，通配符匹配(模式以*号结束，名称以pattern开始)返回true，否则返回false。您可以用逗号分隔指定多个规则。例如，同时处理消息体包含foo body,和所有以header:foo开头的消息头。该语法支持以下前缀，可用于指定include、exclude，或remove-include(是默认模式)-exclude(exclude优先于include)-remove(remove优先)，例如排除消息头foo，删除所有以bar开头的消息头-header:foo,--headers:bar注意不能同时使用include和exclude的header:pattern。 |          | String              |
  | **strategyRef**        | 使用自定义AggregationStrategy而不是默认实现。请注意，您不能同时使用自定义聚合策略和配置数据。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |          | String              |
  | **strategyMethodName** | 当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |          | String              |

  ## 6.1. **Claim Check****操作**

  使用此EIP时，您必须指定要使用的操作，该操作可以是以下内容:

  l Get - 获取（不删除）给定键的声明检查。

  l GetAndRemove - 获取并删除给定键的声明检查。

  l Set - 使用给定设置新的key（将覆盖已存在key）声明检查。

  l Push - 在堆栈上设置新的声明检查（不使用key）。

  l Pop - 从堆栈中获取最新的声明检查（不使用key）。

  当使用Get，GetAndRemove或Set操作你必须指定一个key。然后，这些操作将使用此key存储和检索数据。您可以使用它来在不同的key中存储多个数据。

  在Push和Pop操作都**没有**使用key，但数据存储了堆栈的结构。

  ## 6.2. **过滤要合并的数据**

  filter选项用于定义在使用Get或Pop操作时要合并的数据。然后使用AggregationStrategy合并数据。默认策略使用该filter选项轻松指定要合并的数据。

  该filter选项String使用以下语法获取值:

  l body 			=聚合消息体

  l attachments 	=聚合所有消息附件

  l headers 		=聚合所有消息头

  l header:pattern 	=聚合与模式匹配的所有消息头

  模式规则支持通配符和正则表达式:

  l 通配符匹配（模式以 *** **结尾，名称以pattern开头）

  l 正则表达式匹配

  您可以指定以逗号分隔的多个规则。

  ### 6.2.1. **基于过滤器示例**

  例如，要包含消息体和以foo开头的所有报文头:

  body,header:foo*

  只合并消息体:

  body

  只合并消息附件:

  attachments

  只合并返回报文头:

  header

  只合并名叫foo的报文头:

  header:foo

  如果将过滤规则指定为空或通配符，则会合并所有内容。

  请注意，合并数据时，将覆盖任何现有数据，并保留任何其他现有数据。

  ### 6.2.2. **包含和排除模式的细粒度过滤**

  该语法还支持以下前缀，可用于指定包含，排除或删除

  l + 	= 包括（这是默认模式）

  l - 	= 排除（排除优先于包含）

  l -- 	= 删除（删除优先）

  例如，跳过消息体，并合并其他所有内容

  -body

  或者跳过消息头foo，并合并其他所有内容

  -header:foo

  您还可以在合并数据时指示删除报文头，例如删除以bar开头的所有报文头:

  --headers:bar*

  请注意，header:pattern您不能同时包含include（+）和exclude（-）。

  ## 6.3. **动态键**

  声明检查键是静态的，但您可以使用simple语言语法来定义动态键，例如使用名为myKey的消息中的报文头:

  from("direct:start")

  **    **.to("mock:a")

  **    **.claimCheck(ClaimCheckOperation.Set, "${header.myKey}")

  **    **.transform().constant("Bye World")

  **    **.to("mock:b")

  **    **.claimCheck(ClaimCheckOperation.Get, "${header.myKey}")

  **    **.to("mock:c")

  **    **.transform().constant("Hi World")

  **    **.to("mock:d")

  **    **.claimCheck(ClaimCheckOperation.Get, "${header.myKey}")

  **    **.to("mock:e");

  ## 6.4. **Java示例**

  以下示例显示了操作Push和Pop操作;

  from("direct:start")

  **    **.to("mock:a")

  **    **.claimCheck(ClaimCheckOperation.Push)

  **    **.transform().constant("Bye World")

  **    **.to("mock:b")

  **    **.claimCheck(ClaimCheckOperation.Pop)

  **    **.to("mock:c");

  例如，如果从一开始的消息体是Hello World那么数据被推送到Claim Check EIP的堆栈上。然后将消息体转换为Bye World，即mock:b端点接收的内容。当我们从Claim Check EIP中Pop检索原始消息体并将其合并回来时mock:c将检索消息体Hello World。

  以下是使用Get和Set操作的示例，它使用键foo:

  from("direct:start")

  **    **.to("mock:a")

  **    **.claimCheck(ClaimCheckOperation.Set, "foo")

  **    **.transform().constant("Bye World")

  **    **.to("mock:b")

  **    **.claimCheck(ClaimCheckOperation.Get, "foo")

  **    **.to("mock:c")

  **    **.transform().constant("Hi World")

  **    **.to("mock:d")

  **    **.claimCheck(ClaimCheckOperation.Get, "foo")

  **    **.to("mock:e");

  请注意我们如何使用Get操作将相同的数据Get两次，因为它不会删除数据。如果您只想获取一次数据，则可以使用GetAndRemove。

  最后一个示例显示了如何使用filter选项我们只想返回foo或bar报文头:

  from("direct:start")

  **    **.to("mock:a")

  **    **.claimCheck(ClaimCheckOperation.Push)

  **    **.transform().constant("Bye World")

  **    **.setHeader("foo", constant(456))

  **    **.removeHeader("bar")

  **    **.to("mock:b")

  **    ***// only merge in the message headers foo or bar*

  **    **.claimCheck(ClaimCheckOperation.Pop, null, "header:(foo|bar)")

  **    **.to("mock:c");

  ## 6.5. **Xml示例**

  以下示例显示了Push和Pop操作;

  <route>

  **  **<from uri="direct:start"/>

  **  **<to uri="mock:a"/>

  **  **<claimCheck operation="Push"/>

  **  **<transform>

  **    **<constant>Bye World</constant>

  **  **</transform>

  **  **<to uri="mock:b"/>

  **  **<claimCheck operation="Pop"/>

  **  **<to uri="mock:c"/>

  </route>

  例如，如果从一开始的消息体是Hello World那么数据被推送到Claim Check EIP的堆栈上。然后将消息体转换为Bye World，即mock:b端点接收的内容。当我们从Claim Check EIP中Pop检索原始消息体并将其合并回来时mock:c将检索消息体Hello World。

  以下是使用Get和Set操作的示例，它使用键foo:

  <route>

  **  **<from uri="direct:start"/>

  **  **<to uri="mock:a"/>

  **  **<claimCheck operation="Set" key="foo"/>

  **  **<transform>

  **    **<constant>Bye World</constant>

  **  **</transform>

  **  **<to uri="mock:b"/>

  **  **<claimCheck operation="Get" key="foo"/>

  **  **<to uri="mock:c"/>

  **  **<transform>

  **    **<constant>Hi World</constant>

  **  **</transform>

  **  **<to uri="mock:d"/>

  **  **<claimCheck operation="Get" key="foo"/>

  **  **<to uri="mock:e"/>

  </route>

  请注意我们如何使用Get操作将相同的数据Get两次，因为它不会删除数据。如果您只想获取一次数据，则可以使用GetAndRemove。

  最后一个示例显示了如何使用filter选项我们只想返回名叫foo或bar的报文头:

  <route>

  **  **<from uri="direct:start"/>

  **  **<to uri="mock:a"/>

  **  **<claimCheck operation="Push"/>

  **  **<transform>

  **    **<constant>Bye World</constant>

  **  **</transform>

  **  **<setHeader name="foo">

  **    **<constant>456</constant>

  **  **</setHeader>

  **  **<removeHeader headerName="bar"/>

  **  **<to uri="mock:b"/>

  **  ***<!-- only merge in the message headers foo or bar -->*

  **  **<claimCheck operation="Pop" filter="header:(foo|bar)"/>

  **  **<to uri="mock:c"/>

  </route>

  # 7. [**Content Based Router**](https://camel.apache.org/manual/latest/content-based-router-eip.html)

  [EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)中[基于内容的路由器](http://www.enterpriseintegrationpatterns.com/ContentBasedRouter.html)可以让你将消息基于消息交换的内容路由到正确的目的地。

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps51.png)

  以下示例显示如何将请求从输入**seda****:**端点路由到**seda****:****b****、****seda****:****c**或**seda****:****d，**具体取决于各种[Predicate](https://camel.apache.org/manual/latest/predicate.html)表达式的计算结果

  ## 7.1. **使用**[**流利的建设者**](https://camel.apache.org/manual/latest/fluent-builders.html)

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


  |  | 如果您遇到Java DSL关于when和otherwise的问题，请参阅[为什么我不能在Java Camel路由中使用when或otherwise](https://camel.apache.org/manual/latest/faq/why-can-i-not-use-when-or-otherwise-in-a-java-camel-route.html)。 |
  | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

  ## 7.2. **使用**[**Spring Xml Extensions**](https://camel.apache.org/manual/latest/spring-xml-extensions.html)

  <camelContext errorHandlerRef="errorHandler"** **xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:a"/>

  **        **<choice>

  **            **<when>

  **                **<xpath>$foo = 'bar'</xpath>

  **                **<to uri="direct:b"/>

  **            **</when>

  **            **<when>

  **                **<xpath>$foo = 'cheese'</xpath>

  **                **<to uri="direct:c"/>

  **            **</when>

  **            **<otherwise>

  **                **<to uri="direct:d"/>

  **            **</otherwise>

  **        **</choice>

  **    **</route>

  </camelContext>

  有关此模式的更多示例，您可以查看[junit测试用例](https://github.com/apache/camel/blob/master/camel-core/src/test/java/org/apache/camel/processor/ChoiceTest.java)。

  ## 7.3. **使用此模式**

  如果您想使用此EIP模式，请阅读[入门指南](https://camel.apache.org/manual/latest/getting-started.html)。您可能还会发现该[架构](https://camel.apache.org/manual/latest/architecture.html)特别适用于[端点](https://camel.apache.org/manual/latest/endpoint.html)和[URI](https://camel.apache.org/manual/latest/uris.html)的描述。然后，在尝试使用此模式之前，您可以先尝试一些[示例](https://camel.apache.org/manual/latest/examples.html)。

  # 8. [**Content Filter**](https://camel.apache.org/manual/latest/content-filter-eip.html)

  Camel 使用路由逻辑中的以下机制之一让[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)支持[内容过滤器](http://www.enterpriseintegrationpatterns.com/ContentFilter.html)，以转换入站消息中的内容。

  l [消息翻译](https://camel.apache.org/manual/latest/message-translator.html)

  l 调用[Java bean](https://camel.apache.org/manual/latest/bean-integration.html)

  l [Processor](https://camel.apache.org/manual/latest/processor.html)对象

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps52.png)

  过滤消息的常用方法是在[DSL中](https://camel.apache.org/manual/latest/dsl.html)使用[Expression](https://camel.apache.org/manual/latest/expression.html)，如[XQuery](https://camel.apache.org/components/latest/xquery-language.html)或其中一种受支持的[脚本语言](https://camel.apache.org/manual/latest/scripting-languages.html)。

  ## 8.1. **使用**[**流利的建设者**](https://camel.apache.org/manual/latest/fluent-builders.html)

  这是一个直接使用[DSL](https://camel.apache.org/manual/latest/dsl.html)的简单示例

  在此示例中，我们添加了自己的[处理器](https://camel.apache.org/manual/latest/processor.html)

  有关此模式的其他示例，您可以查看其中一个JUnit测试

  l [TransformTest](https://github.com/apache/camel/blob/master/core/camel-core/src/test/java/org/apache/camel/processor/TransformTest.java)

  l [TransformViaDSLTest](https://github.com/apache/camel/blob/master/core/camel-core/src/test/java/org/apache/camel/processor/TransformViaDSLTest.java)

  ## 8.2. **使用Spring Xml**

  <route>

  **  **<from uri="activemq:Input"/>

  **  **<bean ref="myBeanName" method="doTransform"/>

  **  **<to uri="activemq:Output"/>

  </route>

  您还可以使用XPath过滤掉您感兴趣的部分消息:

  <route>

  **  **<from uri="activemq:Input"/>

  **  **<setBody>

  **    **<xpath resultType="org.w3c.dom.Document">//foo:bar</xpath>

  **  **</setBody>

  **  **<to uri="activemq:Output"/>

  </route>

  ## 8.3. **使用此模式**

  如果您想使用此EIP模式，请阅读" [入门"](https://camel.apache.org/manual/latest/getting-started.html)，您可能还会发现该[体系结构](https://camel.apache.org/manual/latest/architecture.html)特别适用于[端点](https://camel.apache.org/manual/latest/endpoint.html)和[URI](https://camel.apache.org/manual/latest/uris.html)的描述。然后，在尝试使用此模式之前，您可以先尝试一些[示例](https://camel.apache.org/manual/latest/examples.html)。

  # 9. [**Convert Body To EIP**](https://camel.apache.org/manual/latest/convertBodyTo-eip.html)

  ConvertBodyTo EIP允许您将body转换为其他类型。

  Convert Body To EIP支持2个选项，如下所示:


  | **名称**    | **描述**                       | **默认** | **类型** |
  | ----------- | ------------------------------ | -------- | -------- |
  | **Type**    | **必****选项要**转换的java类型 |          | String   |
  | **charset** | 转换时使用特定的字符集         |          | String   |

  # 10. [**Custom Load Balancer EIP**](https://camel.apache.org/manual/latest/customLoadBalancer-eip.html)

  此EIP允许您使用自己的Load Balancer实现。

  自定义负载均衡器EIP支持下面列出的1个选项:


  | **名称** | **描述**                                   | **默认** | **类型** |
  | -------- | ------------------------------------------ | -------- | -------- |
  | **ref**  | **必需**指从注册表中查找的自定义负载均衡器 |          | String   |

  使用Java DSL的示例:

  from("direct:start")

  **    ***// using our custom load balancer*

  **    **.loadBalance(new** **MyLoadBalancer())

  **    **.to("mock:x", "mock:y", "mock:z");

  使用XML DSL的相同示例:

  *<!-- this is the implementation of our custom load balancer -->*

  <bean id="myBalancer" class="org.apache.camel.processor.CustomLoadBalanceTest$MyLoadBalancer"/><camelContext xmlns="http://camel.apache.org/schema/spring">

  **  **<route>

  **    **<from uri="direct:start"/>

  **    **<loadBalance>

  **      ***<!-- refer to my custom load balancer -->*

  **      **<custom ref="myBalancer"/>

  **      ***<!-- these are the endpoints to balancer -->*

  **      **<to uri="mock:x"/>

  **      **<to uri="mock:y"/>

  **      **<to uri="mock:z"/>

  **    **</loadBalance>

  **  **</route>

  </camelContext>

  请注意，在上面的XML DSL中，我们使用<custom>的仅在**Camel 2.8及**更高版本中可用。在旧版本中，您必须执行以下操作:

  <loadBalance ref="myBalancer">

  **  ***<!-- these are the endpoints to balancer -->*

  **  **<to uri="mock:x"/>

  **  **<to uri="mock:y"/>

  **  **<to uri="mock:z"/>

  </loadBalance>

  要实现自定义负载均衡器，您可以扩展一些支持类，如LoadBalancerSupport和SimpleLoadBalancerSupport。前者支持异步路由引擎，后者则不支持。以下是自定义负载均衡器实现的示例:

  public** **static** **class MyLoadBalancer extends LoadBalancerSupport {

  **    **public boolean process(Exchange exchange, AsyncCallback callback) {

  **        **String body = exchange.getIn().getBody(String.class);

  **        **try** **{

  **            **if** **("x".equals(body)) {

  **                **getProcessors().get(0).process(exchange);

  **            **} else** **if** **("y".equals(body)) {

  **                **getProcessors().get(1).process(exchange);

  **            **} else** **{

  **                **getProcessors().get(2).process(exchange);

  **            **}

  **        **} catch** **(Throwable e) {

  **            **exchange.setException(e);

  **        **}

  **        **callback.done(true);

  **        **return** **true;

  **    **}

  }

  # 11. [**Delay EIP**](https://camel.apache.org/manual/latest/delay-eip.html)

  ## 11.1. **选项**

  Delay EIP支持3个选项，如下所示:


  | **名称**                   | **描述**                                                     | **默认** | **类型** |
  | -------------------------- | ------------------------------------------------------------ | -------- | -------- |
  | **executorServiceRef**     | 如果已启用asyncDelay，则引用自定义线程池。                   |          | String   |
  | **asyncDelayed**           | 启用异步延迟，这意味着线程在延迟时不会阻塞。                 | true     | boolean  |
  | **callerRunsWhenRejected** | 调用者是否应该在线程池拒绝任务时运行该任务。默认情况下是true | true     | boolean  |


  |  | 表达式是从当前时间等待的毫秒值，因此表达式应该只是3000。但是，您可以使用固定值的long值来指示毫秒的延迟。请参阅Delayer的Spring DSL示例。                                                                |
  | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
  |  | ***在Java DSL中使用Delayer***===查看此处:[https](https://issues.apache.org/jira/browse/CAMEL-2654):[//issues.apache.org/jira/browse/CAMEL-2654](https://issues.apache.org/jira/browse/CAMEL-2654) === |

  ## 11.2. **示例**

  下面的示例将延迟在**seda****:****b上**收到的所有消息 1秒，然后将它们发送到**mock****:****result**。

  from("seda:b")

  **  **.delay(1000)

  **  **.to("mock:result");

  您可以从延迟器接收消息的时间点开始延迟一段时间。例如延迟2秒

  delayer(2000)

  以上假设保持交货订单并且消息以延迟顺序交付。如果要根据传递时间对消息重新排序，可以将Resequencer与此模式一起使用。例如

  from("activemq:someQueue")

  **  **.resequencer(header("MyDeliveryTime"))

  **  **.delay("MyRedeliveryTime")

  **  **.to("activemq:aDelayedQueue");

  您当然可以使用各种表达式语言，例如XPath，XQuery，SQL或各种脚本语言。例如，要将报文头中指定消息延迟，请使用以下语法:

  from("activemq:someQueue")

  **  **.delay(header("delayValue"))

  **  **.to("activemq:aDelayedQueue");

  要使用简单语言延迟处理，您可以使用以下DSL:

  from("activemq:someQueue")

  **  **.delay(simple("${body.delayProperty}"))

  **  **.to("activemq:aDelayedQueue");

  ### 11.2.1. **Spring DSL**

  下面的示例演示了Spring DSL的延迟:

  <bean id="myDelayBean" class="org.apache.camel.processor.MyDelayCalcBean"/>

  <bean id="exchangeAwareBean" class="org.apache.camel.processor.ExchangeAwareDelayCalcBean"/>

  <camelContext xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="seda:a"/>

  **        **<delay>

  **            **<header>MyDelay</header>

  **        **</delay>

  **        **<to uri="mock:result"/>

  **    **</route>

  **    **<route>

  **        **<from uri="seda:b"/>

  **        **<delay>

  **            **<constant>1000</constant>

  **        **</delay>

  **        **<to uri="mock:result"/>

  **    **</route>

  **    **<route>

  **        **<from uri="seda:c"/>

  **        **<delay>

  **            **<method ref="myDelayBean" method="delayMe"/>

  **        **</delay>

  **        **<to uri="mock:result"/>

  **    **</route>

  **    **<route>

  **        **<from uri="seda:d"/>

  **        **<delay>

  **            **<method ref="exchangeAwareBean" method="delayMe"/>

  **        **</delay>

  **        **<to uri="mock:result"/>

  </route>

  </camelContext>

  ## 11.3. **异步延迟**

  **自Camel 2.4起可用**

  您可以让Delayer使用非阻塞异步延迟，这意味着Camel将使用调度程序来安排将来要执行的任务。然后该任务将继续路由。这允许调用者线程不阻塞并能够服务其他消息等。

  ### 11.3.1. **Java DSL**

  您可以使用asyncDelayed()来启用异步行为。

  from("activemq:queue:foo")

  **  **.delay(1000).asyncDelayed()

  **  **.to("activemq:aDelayedQueue");

  ### 11.3.2. **Spring Xml**

  您可以使用asyncDelayed="true"属性启用异步行为。

  <route>

  **   **<from uri="activemq:queue:foo"/>

  **   **<delay asyncDelayed="true">

  **       **<constant>1000</constant>

  **   **</delay>

  **   **<to uri="activemq:aDealyedQueue"/>

  </route>

  ## 11.4. **创建自定义延迟**

  您可以使用表达式（例如调用bean上的方法）来确定何时使用类似的方式发送消息

  from("activemq:foo").

  **  **delay().method("someBean", "computeDelay").

  **  **to("activemq:bar");

  然后bean看起来像这样......

  public** **class SomeBean {

  **  **public long computeDelay() {

  **     **long** **delay = 0;

  **     ***// use java code to compute a delay value in millis*

  **     **return** **delay;

  ** **}

  }

  # 12. [**Dynamic Router**](https://camel.apache.org/manual/latest/dynamic-router.html)

  来自EIP模式的[动态路由器](http://www.enterpriseintegrationpatterns.com/DynamicRouter.html)允许您路由消息，同时避免路由器对所有可能目的地的依赖性，同时保持其效率。

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps53.png)

  DSL中的dynamicRouter类似于动态路由滑片（dynamic Routing Slip），它动态计算滑片slip。


  |  | **注意**你必须确保用于dynamicRouter如bean 的表达式，将返回null以指示结束。否则，dynamicRouter将不断重复。 |
  | - | ---------------------------------------------------------------------------------------------------------- |

  ## 12.1. **选项**


  | **名称**               | **默认值** | **描述**                                                                                                                                        |
  | ---------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
  | uriDelimiter           | ,          | 如果Expression返回多个端点，则使用分隔符。                                                                                                      |
  | ignoreInvalidEndpoints | false      | 如果无法解析端点uri，则应忽略它。否则Camel会抛出一个异常，说明端点uri无效。                                                                     |
  | cacheSize              | 1000       | 允许为高速ProducerCache缓存生成器配置高速缓存大小，以便在路由滑片slip中复用。默认情况下，将使用默认缓存大小1000。将值设置为-1可以同时关闭缓存。 |

  ## 12.2. **Camel 2.5中的动态路由器**

  动态路由器将在Exchange上设置一个属性（Exchange.SLIP_ENDPOINT），该属性包含当前端点（通过滑行前进）。 这使您可以知道我们在单据中处理了多远。 （这是一个清单，因为动态路由器的实现是基于路由清单的）。

  ## 12.3. **Java DSL**

  在Java DSL中，您可以使用dynamicRouter如下所示:

  from("direct:start")

  **    ***// use a bean as the dynamic router*

  **    **.dynamicRouter(method(DynamicRouterTest.class, "slip"));

  这将充分利用bean计算slip，这可以实现如下:

  */***

  * * Use this method to compute dynamic where we should route next.*

  ---

  * * **@param** body the message body*

  * * **@return** endpoints to go, or <tt>null</tt> to indicate the end*

  * */*

  public String slip(String body) {

  **    **bodies.add(body);

  **    **invoked++;

  **    **if** **(invoked == 1) {

  **        **return** **"mock:a";

  **    **} else** **if** **(invoked == 2) {

  **        **return** **"mock:b,mock:c";

  **    **} else** **if** **(invoked == 3) {

  **        **return** **"direct:foo";

  **    **} else** **if** **(invoked == 4) {

  **        **return** **"mock:result";

  **    **}

  **    ***// no more so return null*

  **    **return** **null;

  }

  请注意，此示例仅用于显示和说明。当前的实现不是线程安全的。您必须将状态存储在Exchange上，以确保线程安全，如下所示:

  */***

  * * Use this method to compute dynamic where we should route next.*

  ---

  * * **@param** body the message body*

  * * **@param** properties the exchange properties where we can store state between invocations*

  * * **@return** endpoints to go, or <tt>null</tt> to indicate the end*

  * */*

  public String slip(String body, @Properties Map<String, Object> properties) {

  **    **bodies.add(body);

  **    ***// get the state from the exchange properties and keep track how many times*

  **    ***// we have been invoked*

  **    **int** **invoked = 0;

  **    **Object current = properties.get("invoked");

  **    **if** **(current != null) {

  **        **invoked = Integer.valueOf(current.toString());

  **    **}

  **    **invoked++;

  **    ***// and store the state back on the properties*

  **    **properties.put("invoked", invoked);

  **    **if** **(invoked == 1) {

  **        **return** **"mock:a";

  **    **} else** **if** **(invoked == 2) {

  **        **return** **"mock:b,mock:c";

  **    **} else** **if** **(invoked == 3) {

  **        **return** **"direct:foo";

  **    **} else** **if** **(invoked == 4) {

  **        **return** **"mock:result";

  **    **}

  **    ***// no more so return null*

  **    **return** **null;

  }

  您还可以将状态存储为消息头，但不保证在路由期间保留它们，而Exchange上的属性也是如此。虽然方法调用表达式中存在错误，但请参阅下面的警告。

  ## 12.4. **Spring Xml**

  Spring XML中的相同示例是:

  <bean id="mySlip" class="org.apache.camel.processor.DynamicRouterTest"/>

  <camelContext xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:start"/>

  **        **<dynamicRouter>

  **            ***<!-- use a method call on a bean as dynamic router -->*

  **            **<method ref="mySlip" method="slip"/>

  **        **</dynamicRouter>

  **    **</route>

  **    **<route>

  **        **<from uri="direct:foo"/>

  **        **<transform><constant>Bye World</constant></transform>

  </route>

  </camelContext>

  ## 12.5. **@DynamicRouter注解**

  您也可以使用@DynamicRouter注解route。然后，当动态处理消息时，将重复调用该方法。我们的想法是返回下一个端点uri指明去哪里。返回null表示结束。如果您愿意，可以返回多个端点，就像路由滑动一样，每个端点用分隔符分隔。

  public** **class MyDynamicRouter {

  **    **@Consume(uri = "activemq:foo")

  **    **@DynamicRouter

  **    **public String route(@XPath("/customer/id") String customerId, @Header("Location") String location, Document body) {

  **        ***// query a database to find the best match of the endpoint based on the input parameteres*

  **        ***// return the next endpoint uri, where to go. Return null to indicate the end.*

  **    **}

  }

  在上面我们可以使用参数绑定注解将Message的不同部分绑定到方法参数或使用表达式，例如使用[XPath](https://camel.apache.org/components/latest/xpath-language.html)或[XQuery](https://camel.apache.org/components/latest/xpath-language.html)。

  可以通过Bean Integration中描述的多种方式调用该方法，例如

  l POJO生产者

  l Spring Remoting

  l [Bean](https://camel.apache.org/components/latest/bean-component.html)组件

  # 13. [**Dynamic Router EIP**](https://camel.apache.org/manual/latest/dynamicRouter-eip.html)

  来自[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的[动态路由器](http://www.enterpriseintegrationpatterns.com/DynamicRouter.html)允许您路由消息，同时避免路由器对所有可能目的地的依赖性，同时保持其效率。

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps54.png)

  DSL中的dynamicRouter类似于动态路由滑片（dynamic Routing Slip），它动态计算滑片slip。


  |  | ***避免无限循环***===你必须确保用于dynamicRouter诸如bean 之类的表达式将返回null以指示结束。否则，dynamicRouter将不断重复。=== |
  | - | ------------------------------------------------------------------------------------------------------------------------------ |

  ## 13.1. **选项**

  动态路由器EIP支持3个选项，如下所示:


  | **名称**                   | **描述**                                                                                                             | **默认** | **类型** |
  | -------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
  | **uriDelimiter**           | 设置要使用的uri分隔符                                                                                                | ，       | String   |
  | **ignoreInvalidEndpoints** | 尝试使用该端点创建生产者时忽略invalidate端点异常                                                                     | False    | Boolean  |
  | **cacheSize**              | 设置org.apache.camel.spi.ProducerCache使用的最大大小，当重用uris时，该大小用于在使用此动态路由器时缓存和复用生产者。 |          | Integer  |

  动态路由器将在Exchange上设置Exchange.SLIP_ENDPOINT属性，该属性包含当前端点，因为它通过滑动提前。这可以让您知道我们在单据中处理了多远。（这是一个漏洞，因为动态路由器实现基于路由滑动的顶部）。

  ## 13.2. **示例**

  在Java DSL中，您可以使用dynamicRouter如下所示:

  from("direct:start")

  **    ***// use a bean as the dynamic router*

  **    **.dynamicRouter(method(DynamicRouterTest.class, "slip"));

  这将充分利用Bean来计算转差上即时，这可以实现如下:

  */***

  * * Use this method to compute dynamic where we should route next.*

  ---

  * * **@param** body the message body*

  * * **@return** endpoints to go, or <tt>null</tt> to indicate the end*

  * */*

  public String slip(String body) {

  **    **bodies.add(body);

  **    **invoked++;

  **    **if** **(invoked == 1) {

  **        **return** **"mock:a";

  **    **} else** **if** **(invoked == 2) {

  **        **return** **"mock:b,mock:c";

  **    **} else** **if** **(invoked == 3) {

  **        **return** **"direct:foo";

  **    **} else** **if** **(invoked == 4) {

  **        **return** **"mock:result";

  **    **}

  **    ***// no more so return null*

  **    **return** **null;

  }

  请注意，此示例仅用于显示和说明。当前的实现不是线程安全的。您必须将状态存储在Exchange上，以确保线程安全，如下所示:

  */***

  * * Use this method to compute dynamic where we should route next.*

  ---

  * * **@param** body the message body*

  * * **@param** properties the exchange properties where we can store state between invocations*

  * * **@return** endpoints to go, or <tt>null</tt> to indicate the end*

  * */*

  public String slip(String body, @Properties Map<String, Object> properties) {

  **    **bodies.add(body);

  **    ***// get the state from the exchange properties and keep track how many times*

  **    ***// we have been invoked*

  **    **int** **invoked = 0;

  **    **Object current = properties.get("invoked");

  **    **if** **(current != null) {

  **        **invoked = Integer.valueOf(current.toString());

  **    **}

  **    **invoked++;

  **    ***// and store the state back on the properties*

  **    **properties.put("invoked", invoked);

  **    **if** **(invoked == 1) {

  **        **return** **"mock:a";

  **    **} else** **if** **(invoked == 2) {

  **        **return** **"mock:b,mock:c";

  **    **} else** **if** **(invoked == 3) {

  **        **return** **"direct:foo";

  **    **} else** **if** **(invoked == 4) {

  **        **return** **"mock:result";

  **    **}

  **    ***// no more so return null*

  **    **return** **null;

  }

  您还可以将状态存储为消息头，但不保证在路由期间保留它们，而Exchange上的属性也是如此。虽然方法调用表达式中存在错误，但请参阅下面的警告。

  ### 13.2.1. **Spring Xml**

  Spring XML中的相同示例是:

  <bean id="mySlip" class="org.apache.camel.processor.DynamicRouterTest"/><camelContext xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:start"/>

  **        **<dynamicRouter>

  **            ***<!-- use a method call on a bean as dynamic router -->*

  **            **<method ref="mySlip" method="slip"/>

  **        **</dynamicRouter>

  **    **</route>

  **    **<route>

  **        **<from uri="direct:foo"/>

  **        **<transform><constant>Bye World</constant></transform>

  </route>

  </camelContext>

  ## 13.3. **@DynamicRouter注解**

  您也可以使用@DynamicRouter注释route。然后，当动态处理消息时，将重复调用该方法。我们的想法是返回下一个端点uri以指示去哪里。返回null表示结束。如果您愿意，可以返回多个端点，就像路由滑动一样，每个端点用分隔符分隔。

  public** **class MyDynamicRouter {

  **    **@Consume(uri = "activemq:foo")

  **    **@DynamicRouter

  **    **public String route(@XPath("/customer/id") String customerId, @Header("Location") String location, Document body) {

  **        ***// query a database to find the best match of the endpoint based on the input parameteres*

  **        ***// return the next endpoint uri, where to go. Return null to indicate the end.*

  **    **}

  }

  # 14. [**Enrich EIP**](https://camel.apache.org/manual/latest/enrich-eip.html)

  EIP模式支持Content Enricher（内容增强），Camel使用消息转换器，路由逻辑中的任意处理器或使用增强DSL元素来丰富消息。

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps55.png)

  Enrich EIP支持7种选项，如下所示:


  | **名称**                    | **描述**                                                                                                                                                                                    | **默认** | **类型** |
  | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
  | **strategyRef**             | 指用于将来自外部服务的回复合并到单个传出消息中的AggregationStrategy。默认情况下，Camel将使用外部服务的回复作为传出消息。                                                                    |          | String   |
  | **strategyMethodName**      | 当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。                                                                                                                 |          | String   |
  | **strategyMethodAllowNull** | 如果此选项为false，则在没有要丰富的数据时不使用聚合方法。如果此选项为true，则在将POJO用作AggregationStrategy时，将使用null值作为oldExchange（当没有数据可以充实时）。                       | False    | Boolean  |
  | **aggregateOnException**    | 如果此选项为false，则在尝试检索要从资源中丰富的数据时抛出异常时，不使用聚合方法。将此选项设置为true允许最终用户控制在聚合方法中存在异常时要执行的操作。例如，抑制异常或设置自定义消息体等。 | False    | Boolean  |
  | **shareUnitOfWork**         | 与父级和资源交换共享org.apache.camel.spi.UnitOfWork。默认情况下，Enrich不会共享父交换和资源交换之间的工作单元。这意味着资源交换有自己独立的工作单元。                                       | False    | Boolean  |
  | **cacheSize**               | 设置org.apache.camel.spi.ProducerCache使用的最大大小，用于在重用uris时缓存和重用生产者。                                                                                                    |          | Integer  |
  | **ignoreInvalidEndpoint**   | 尝试使用该端点创建生产者时忽略invalidate端点异常                                                                                                                                            | False    | Boolean  |

  ## 14.1. **使用消息转换器或处理器进行内容丰富**

  您可以使用Templating从一个目标消费消息，使用Velocity或XQuery等方法对其进行转换，然后将其发送到另一个目标。例如使用InOnly（单向消息传递）

  ## 14.2. **示例**

  from("activemq:My.Queue").

  **  **to("velocity:com/acme/MyResponse.vm").

  **  **to("activemq:Another.Queue");

  如果您想使用InOut（请求 - 回复）语义来处理ActiveMQ 上的**My.Queue**队列上的请求，并使用模板生成的响应，那么将响应发送回JMSReplyTo目的地，您可以使用:

  from("activemq:My.Queue").

  **  **to("velocity:com/acme/MyResponse.vm");

  这是一个使用DSL直接转换消息体的简单示例

  from("direct:start").setBody(body().append(" World!")).to("mock:result");

  在此示例中，我们使用显式Java代码添加自己的处理器

  from("direct:start").process(new** **Processor() {

  **    **public void process(Exchange exchange) {

  **        **Message in = exchange.getIn();

  **        **in.setBody(in.getBody(String.class) + " World!");

  **    **}

  }).to("mock:result");

  最后，我们可以使用Bean Integration在任何bean上使用任何Java方法来充当transformer

  from("activemq:My.Queue").

  **  **beanRef("myBeanName", "myMethodName").

  **  **to("activemq:Another.Queue");

  ### 14.2.1. **使用Spring XML**

  <route>

  **  **<from uri="activemq:Input"/>

  **  **<bean ref="myBeanName" method="doTransform"/>

  **  **<to uri="activemq:Output"/>

  </route>

  ## 14.3. **使用enrichDSL元素进行内容丰富**

  Camel DSL带有丰富风格的enrich可用作内容丰富。另一个是pollEnrich。

  enrich使用Producer获取其他数据。它通常用于请求回复消息传递，例如用于调用外部Web service。

  enrich和pollEnrich都支持使用表达式来计算URI，它允许从当前的Exchange以动态端点使用数据。

  ### 14.3.1. **使用Java的一个简单的例子:**

  AggregationStrategy aggregationStrategy = ...

  from("direct:start")

  **  **.enrich("direct:resource", aggregationStrategy)

  **  **.to("direct:result");

  from("direct:resource")

  ...

  内容enricher（enrich）从资源端点检索其他数据，以丰富传入消息（包含在原始交换中）。聚合策略用于组合原始交换和资源交换。AggregationStrategy.aggregate(Exchange, Exchange)方法的第一个参数对应于原始交换，第二个参数对应资源交换。资源端点的结果存储在资源交换的out消息中。以下是实现聚合策略的示例模板:

  public** **class ExampleAggregationStrategy implements AggregationStrategy {

  **    **public Exchange aggregate(Exchange original, Exchange resource) {

  **        **Object originalBody = original.getIn().getBody();

  **        **Object resourceResponse = resource.getIn().getBody();

  **        **Object mergeResult = ... *// combine original body and resource response*

  **        **if** **(original.getPattern().isOutCapable()) {

  **            **original.getOut().setBody(mergeResult);

  **        **} else** **{

  **            **original.getIn().setBody(mergeResult);

  **        **}

  **        **return** **original;

  **    **}

  }

  使用此模板，原始交换可以是任何模式。由增强器enrich创建的资源交换始终是in-out的。

  ### 14.3.2. **使用Xml丰富示例**

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<route>

  **    **<from uri="direct:start"/>

  **    **<enrich strategyRef="aggregationStrategy">

  **      **<constant>direct:resource</constant>

  **    **</enrich>

  **    **<to uri="direct:result"/>

  **  **</route>

  **  **<route>

  **    **<from uri="direct:resource"/>

  **    **...

  **  **</route>

  </camelContext>

  <bean id="aggregationStrategy" class="..." />

  ## 14.4. **聚合策略是可选的**

  聚合策略是可选的。如果你不提供它，Camel默认只使用从资源获得的body。

  from("direct:start")

  **  **.enrich("direct:resource")

  **  **.to("direct:result");

  在上面的路由中，发送到direct:result端点的消息将包含direct:resource的输出，因为我们不使用任何自定义聚合。

  <route>

  **  **<from uri="direct:start"/>

  **  **<enrich>

  **    **<constant>direct:resource</constant>

  **  **</enrich>

  **  **<to uri="direct:result"/>

  </route>

  ## 14.5. **使用动态URIS**

  **自Camel 2.16起可用**

  enrich和pollEnrich使用计算后动态的URI支持当前的Exchange。例如，要从HTTP端点进行丰富，其中带有键orderId的报文头用作HTTP URL的一部分:

  from("direct:start")

  **  **.enrich().simple("http:myserver/${header.orderId}/order")

  **  **.to("direct:result");

  在Xml DSL中

  <route>

  **  **<from uri="direct:start"/>

  **  **<enrich>

  **    **<simple>http:myserver/${header.orderId}/order</simple>

  **  **</enrich>

  **  **<to uri="direct:result"/>

  </route>

  # 15. [**Event Driven Consumer**](https://camel.apache.org/manual/latest/eventDrivenConsumer-eip.html)

  Camel支持来自[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的[事件驱动消费者](http://www.enterpriseintegrationpatterns.com/EventDrivenConsumer.html)。默认的消费者模型是基于事件的（即异步），因此这意味着Camel容器可以以声明方式为您管理池、线程和并发。

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps56.png)

  事件驱动的消费者由实现[处理器](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Processor.html)接口的消费者实现，当[消息](https://camel.apache.org/manual/latest/message.html)可用于处理时，该接口由[消息端点](https://camel.apache.org/manual/latest/message-endpoint.html)调用。

  ## 15.1. **例**

  下面演示了Camel [注册表中](https://camel.apache.org/manual/latest/registry.html)定义的[处理器](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Processor.html)，当从[JMS](https://camel.apache.org/components/latest/jms-component.html)队列发生事件时调用该[处理器](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Processor.html)。

  **使用**[**流利的建设者**](https://camel.apache.org/manual/latest/fluent-builders.html)

  from("jms:queue:foo")

  **    **.processRef("processor");

  **使用**[**Spring XML Extensions**](https://camel.apache.org/manual/latest/spring-xml-extensions.html)

  <route>

  **    **<from uri="jms:queue:foo"/>

  <to uri="processor"/>

  </route>

  有关更多详情，请参阅

  l [消息](https://camel.apache.org/manual/latest/message.html)

  l [消息端点](https://camel.apache.org/manual/latest/message-endpoint.html)

  ## 15.2. **使用此模式**

  如果您想使用此EIP模式，请阅读" [入门"](https://camel.apache.org/manual/latest/getting-started.html)，您可能还会发现该[体系结构](https://camel.apache.org/manual/latest/architecture.html)特别适用于[端点](https://camel.apache.org/manual/latest/endpoint.html)和[URI](https://camel.apache.org/manual/latest/uris.html)的描述。然后，在尝试使用此模式之前，您可以先尝试一些[示例](https://camel.apache.org/manual/latest/examples.html)。

  # 16. [**Failover EIP**](https://camel.apache.org/manual/latest/failover-eip.html)

  故障转移负载均衡器，在出现故障时使用此策略，将在下一个端点上尝试交换。

  ## 16.1. **选项**

  故障转移EIP支持下面列出的4个选项:


  | **名称**                    | **描述**                                                                                                                                                                                                                                                                                                                                 | **默认** | **类型** |
  | --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
  | **exception**               | 要监视的特定异常的类名列表。如果未配置任何例外，则监视所有异常                                                                                                                                                                                                                                                                           |          | List     |
  | **roundRobin**              | 故障转移负载均衡器是否应以循环模式运行。如果不是，那么当要处理新消息时，它将始终从第一个端点开始。换句话说，它从每个消息的顶部重新启动。如果启用循环，则它保持状态并将以循环方式继续下一个端点。您还可以与循环一起启用粘滞模式，如果是，那么它将选择在启动负载平衡时使用的最后一个已知良好端点（而不是在启动时使用下一个）。             | false    | Boolean  |
  | **sticky**                  | 故障转移负载均衡器是否应在粘滞模式下运行。如果不是，那么当要处理新消息时，它将始终从第一个端点开始。换句话说，它从每个消息的顶部重新启动。如果启用了sticky，则它将保持状态并继续使用最后一个已知的良好端点。您还可以与循环一起启用粘滞模式，如果是，那么它将选择在启动负载平衡时使用的最后一个已知良好端点（而不是在启动时使用下一个）。 | false    | Boolean  |
  | **maximumFailoverAttempts** | 指示在X次故障转移尝试后应该耗尽(放弃)的值。使用-1表示永不放弃并不断尝试故障转移。使用0实现永不故障转移。使用例如3在放弃之前最多进行3次故障转移。无论是否启用了roundRobin，都可以使用他的选项。                                                                                                                                           | -1       | Integer  |

  ## 16.2. **例子**

  在这个用例，我们使用header测试作为相关表达式:

  from("direct:start")

  **    **.loadBalance()

  **    **.failover(MyException.class)

  **    **.to("seda:x", "seda:y", "seda:z");

  在XML中，您将拥有这样的路由

  <from uri="direct:start"/>

  **    **<loadBalance>

  **       **<failover>

  **           **<exception>com.example.camel.MyException</exception>

  **       **</failover>

  **       **<to uri="seda:x"/>

  **       **<to uri="seda:y"/>

  **       **<to uri="seda:z"/>

  **    **</loadBalance>

  # 17. [**Filter EIP**](https://camel.apache.org/manual/latest/filter-eip.html)

  通过[EIP模式中](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的[消息过滤器](http://www.enterpriseintegrationpatterns.com/Filter.html)，您可以过滤消息

  ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps57.png)

  下面的示例显示如何创建一个从名为**queue****:****a**的端点，消费消息的消息过滤器路由，如果[谓词](https://camel.apache.org/manual/latest/predicate.html)为true，则将其分派到**queue****:****b。**

  ## 17.1. **EIP选项**

  筛选器EIP没有选项。

  ## 17.2. **样品**

  这是Java DSL中的一个小示例：

  from("direct:a")

  **    **.filter(simple("${header.foo} == 'bar'"))

  **        **.to("direct:b");

  您可以使用许多不同的语言作为谓词，例如XPath：

  from("direct:start").

  **        **filter().xpath("/person[@name='James']").

  **        **to("mock:result");

  这是使用Bean定义过滤器行为的另一个示例

  from("direct:start")

  **    **.filter().method(MyBean.class, "isGoldCustomer")

  **      **.to("mock:gold")

  **    **.end()

  **    **.to("mock:all");public** **static** **class MyBean {

  **    **public boolean isGoldCustomer(@Header("level") String level) {

  **        **return** **level.equals("gold");

  **    **}

  }

  还有XML中的示例：

  <bean id="myBean" class="com.foo.MyBean"/><camelContext xmlns="http://camel.apache.org/schema/spring">

  **    **<route>

  **        **<from uri="direct:a"/>

  **        **<filter>

  **            **<method ref="myBean" method="isGoldCustomer"/>

  **            **<to uri="direct:b"/>

  **        **</filter>

  </route>

  </camelContext>

  ## 17.3. **使用stop**

  停止与消息过滤器有点不同，因为它会过滤掉所有消息并完全结束路由（过滤器仅适用于其子处理器）。例如，当您需要停止其中一个谓词中的进一步处理时，在[基于内容的路由器中](https://camel.apache.org/manual/latest/content-based-router-eip.html)使用Stop十分方便。

  在下面的示例中，我们不想再路由消息体中带有单词Bye的消息。请注意，如何在when谓词中使用.stop()来防止这种情况。

  ## 17.4. **知道EXCHANGE是否被过滤**

  该[消息过滤器](https://camel.apache.org/manual/latest/filter-eip.html) EIP将在[Exchange](https://camel.apache.org/manual/latest/exchange.html)添加属性，以指示过滤与否。

  该属性具有键Exchange.FILTER_MATCHED，该键的String值为CamelFilterMatched。其值为一个布尔值true或false。如果值为true则将[Exchange](https://camel.apache.org/manual/latest/exchange.html)路由到过滤器中。此属性将在[谓词](https://camel.apache.org/manual/latest/predicate.html)匹配的[消息过滤器](https://camel.apache.org/manual/latest/filter-eip.html)（值设置为true）以及紧随[消息过滤器](https://camel.apache.org/manual/latest/filter-eip.html)之后的步骤中可见（显示的值基于最后计算[消息过滤器](https://camel.apache.org/manual/latest/filter-eip.html)[谓词](https://camel.apache.org/manual/latest/predicate.html)的结果设置）。

  # 18. [**From EIP**](https://camel.apache.org/manual/latest/from-eip.html)

  ## 18.1. **选项**

  From EIP支持下面列出的1个选项:


  | **名称** | **描述**                      | **默认** | **类型** |
  | -------- | ----------------------------- | -------- | -------- |
  | **uri**  | **必需**设置要使用的端点的URI |          | String   |

  ## 18.2. **示例**

  使用File端点启动路由。目录中的每个文件都创建一个交换，并将其放入到camel路由中。

  使用类**Routerieilder**的configure方法启动camel路由

  from("file:c:/in")

  Spring XML Schema中的示例:

  路由在CamelContext中定义。

  <route>

  **  **<from uri="file:c:/in" />

  </route>

  # 19. [**Hystrix EIP**](https://camel.apache.org/manual/latest/hystrix-eip.html)

  **自Camel 2.18起可用**

  Hystrix EIP提供与Netflix [Hystrix的](https://github.com/Netflix/Hystrix)集成，可用作Camel路由中的断路器。Hystrix是一个延迟和容错库，旨在隔离对远程系统、服务和第三方库的访问点、停止级联故障，并在复杂的分布式系统中实现弹性处理，在这些系统中，故障是不可避免的。

  Maven用户需要将以下依赖项添加到他们的pom.xml以使用此EIP:

  <dependency>

  **    **<groupId>org.apache.camel</groupId>

  **    **<artifactId>camel-hystrix</artifactId>

  <version>x.x.x</version>*<!-- use the same version as your Camel core version -->*

  </dependency>

  ## 19.1. **配置选项**

  Hystrix EIP支持2个选项，如下所示:


  | **名称**                    | **描述**                                                | **默认** | **类型**                       |
  | --------------------------- | ------------------------------------------------------- | -------- | ------------------------------ |
  | **hystrixConfiguration**    | 配置完成后，使用end配置Hystrix EIP，以返回Hystrix EIP。 |          | HystrixConfigurationDefinition |
  | **hystrixConfigurationRef** | 用于配置Hystrix EIP的Hystrix配置。                      |          | String                         |

  有关Hystrix EIP上的所有配置选项，请参见[Hystrix Configuration](https://camel.apache.org/manual/latest/hystrixConfiguration-eip.html)。

  ## 19.2. **示例**

  下面的示例路由显示了Hystrix端点，该端点通过回退到内联的回退路由来防止运行缓慢。 默认情况下，超时请求仅为**1000ms** ，因此HTTP端点必须相当快才能成功。

  from("direct:start")

  **    **.circuitBreaker()

  **        **.to("http://fooservice.com/slow")

  **    **.onFallback()

  **        **.transform().constant("Fallback message")

  **    **.end()

  **    **.to("mock:result");

  And in XML DSL:

  <camelContext xmlns="http://camel.apache.org/schema/spring">

  **  **<route>

  **    **<from uri="direct:start"/>

  **    **<circuitBreaker>

  **      **<to uri="http://fooservice.com/slow"/>

  **      **<onFallback>

  **        **<transform>

  **          **<constant>Fallback message</constant>

  **        **</transform>

  **      **</onFallback>

  **    **</circuitBreaker>

  **    **<to uri="mock:result"/>

  **  **</route>

  </camelContext>

  ## 19.3. **配置HYSTRIX**

  您可以通过许多[Hystrix Configuration](https://camel.apache.org/manual/latest/hystrixConfiguration-eip.html)选项来微调Hystrix。 例如，要使用2秒的执行超时，可以执行以下操作：

  from("direct:start")

  **    **.circuitBreaker()

  **        ***// use 2 second timeout*

  **        **.hystrixConfiguration().executionTimeoutInMilliseconds(2000).end()

  **        **.log("Hystrix processing start: ${threadName}")

  **        **.toD("direct:${body}")

  **        **.log("Hystrix processing end: ${threadName}")

  **    **.end()

  **    **.log("After Hystrix ${body}");

  And in XML:

  <route>

  **  **<from uri="direct:start"/>

  **  **<circuitBreaker>

  **    **<hystrixConfiguration executionTimeoutInMilliseconds="2000"/>

  **    **<log message="Hystrix processing start: ${threadName}"/>

  **    **<toD uri="direct:${body}"/>

  **    **<log message="Hystrix processing end: ${threadName}"/>

  **  **</circuitBreaker>

  **  **<log message="After Hystrix: ${body}"/>

  </route>

  ## 19.4. **FALLBACK**

  See [onFallback](https://camel.apache.org/manual/latest/onFallback-eip.html).

  ## 19.5. **OTHER EXAMPLES**

  You can find an example with the source code: [camel-example-hystrix](https://github.com/apache/camel/tree/master/examples/camel-example-hystrix).

  ## 19.6. **USING HYSTRIX WITH SPRING BOOT**

  See the [Hystrix Component](https://camel.apache.org/components/latest/hystrix.html).

  ## 19.7. **Camel的错误处理器和Hystrix EIP**

  默认情况下，Hystrix EIP自己处理错误。这意味着如果断路器打开并且消息失败，那么Camel的错误处理程序也没有做出反应。但是，您可以通过启用该inheritErrorHandler选项为Hystrix启用Camels错误处理程序，如下所示:

  *// Camel's error handler that will attempt to redeliver the message 3 times*

  errorHandler(deadLetterChannel("mock:dead").maximumRedeliveries(3).redeliveryDelay(0));

  from("direct:start")

  **    **.to("log:start")

  **    ***// turn on Camel's error handler on hystrix so it can do redeliveries*

  **    **.hystrix().inheritErrorHandler(true)

  **        **.to("mock:a")

  **        **.throwException(new** **IllegalArgumentException("Forced"))

  **    **.end()

  **    **.to("log:result")

  **    **.to("mock:result");

  此示例来自单元测试，您可以在其中看到Hystrix EIP块已被硬编码，始终通过抛出异常而失败。因为inheritErrorHandler已启用，所以Camel的错误处理程序将尝试再次调用Hystrix EIP块。

  这意味着mock:a端点将再次收到消息，总共1 + 3 = 4条消息（第一次+3次重新发送）。

  如果我们关闭inheritErrorHandler选项（默认），那么Hystrix EIP将只执行一次，因为它自己处理错误。

  # 20. [**Hystrix Configuration EIP**](https://camel.apache.org/manual/latest/hystrixConfiguration-eip.html)

  Hystrix配置EIP支持31个选项，如下所示:


  | **名称**                                                   | **描述**                                                                                                                                                                                                                 | **默认**     | **类型** |
  | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | -------- |
  | **groupKey**                                               | 设置要使用的group键。默认值为CamelHystrix。                                                                                                                                                                              | CamelHystrix | String   |
  | **threadPoolKey**                                          | 设置要使用的线程池key。默认情况下，将使用与groupKey配置使用的值相同的值。                                                                                                                                                | CamelHystrix | String   |
  | **circuitBreakerEnabled**                                  | 是否使用HystrixCircuitBreaker。如果为false，则不使用断路器逻辑并允许所有请求。这与circuitBreakerForceClosed()的效果类似，只是继续跟踪指标并知道它是否应该打开/关闭，此属性甚至不会实例化断路器。                         | TRUE         | Boolean  |
  | **circuitBreakerErrorThresholdPercentage**                 | 错误百分比阈值（如整数，如50），此时断路器将跳闸并拒绝请求。它将在circuitBreakerSleepWindowInMilliseconds中定义的持续时间内保持跳闸; 与之比较的错误百分比来自HystrixCommandMetrics.getHealthCounts()。                  | 50           | Integer  |
  | **circuitBreakerForceClosed**                              | 如果为true，则HystrixCircuitBreaker＃allowRequest()将始终返回true以允许请求，而不管HystrixCommandMetrics.getHealthCounts()的错误百分比。circuitBreakerForceOpen()属性优先，因此如果设置为true，则此属性不执行任何操作。  | FALSE        | Boolean  |
  | **circuitBreakerForceOpen**                                | 如果为true，则HystrixCircuitBreaker.allowRequest()将始终返回false，从而导致电路打开（跳闸）并拒绝所有请求。此属性优先于circuitBreakerForceClosed();                                                                      | FALSE        | Boolean  |
  | **circuitBreakerRequestVolumeThreshold**                   | 在HystrixCircuitBreaker跳闸之前必须存在的metricsRollingStatisticalWindowInMilliseconds()中的最小请求数。如果低于此数值，无论误差百分比如何，电路都不会跳闸。                                                             | 20           | Integer  |
  | **circuitBreakerSleepWindow InMilliseconds**               | HystrixCircuitBreaker打开后的时间（以毫秒为单位），它应该在再次尝试请求之前等待。                                                                                                                                        | 5000         | Integer  |
  | **executionIsolationSemaphoreMaxConcurrentRequests**       | 允许HystrixCommand.run()的并发请求数。超出并发限制的请求将被拒绝。仅在executionIsolationStrategy == SEMAPHORE时适用。                                                                                                    | 20           | Integer  |
  | **executionIsolationStrategy**                             | 将执行什么HystrixCommand.run()隔离策略。如果THREAD那么它将在一个单独的线程上执行，并且并发请求受到线程池中线程数量的限制。如果是SEMAPHORE，那么它将在调用线程上执行，并且并发请求受信号量计数限制。                      | THREAD       | String   |
  | **executionIsolationThread InterruptOnTimeout**            | 当线程超时时，执行线程是否应该尝试中断（使用Future＃cancel）。仅在executionIsolationStrategy()== THREAD时适用。                                                                                                          | TRUE         | Boolean  |
  | **executionTimeoutInMilliseconds**                         | 命令将超时并停止执行的时间（以毫秒为单位）。如果executionIsolationThreadInterruptOnTimeout == true且命令是线程隔离的，则执行线程将被中断。如果该命令是信号量隔离的并且是HystrixObservableCommand，则该命令将被取消订阅。 | 1000         | Integer  |
  | **executionTimeoutEnabled**                                | 是否为此命令启用了超时机制                                                                                                                                                                                               | TRUE         | Boolean  |
  | **fallbackIsolationSemaphoreMaxConcurrentRequests**        | 允许HystrixCommand.getFallback()的并发请求数。超出并发限制的请求将失败，并且不会尝试检索回退。                                                                                                                           | 10           | Integer  |
  | **fallbackEnabled**                                        | 发生故障时是否应尝试HystrixCommand.getFallback()。                                                                                                                                                                       | TRUE         | Boolean  |
  | **metricsHealthSnapshotIntervalInMilliseconds**            | 在允许计算成功和错误百分比的健康快照之间等待的时间（以毫秒为单位）并影响HystrixCircuitBreaker.isOpen()状态。在高容量电路上，错误百分比的连续计算可能会变为CPU密集型，因此可以控制计算频率。                              | 500          | Integer  |
  | **metricsRollingPercentileBucketSize**                     | 滚动百分位数的每个存储桶中存储的最大值数。这将传递到HystrixCommandMetrics内的HystrixRollingPercentile。                                                                                                                  | 10           | Integer  |
  | **metricsRollingPercentile Enabled**                       | 是否应使用HystrixCommandMetrics中的HystrixRollingPercentile捕获百分位度量标准。                                                                                                                                          | TRUE         | Boolean  |
  | **metricsRollingPercentile WindowInMilliseconds**          | 百分位滚动窗口的持续时间（以毫秒为单位）。这将传递到HystrixCommandMetrics内的HystrixRollingPercentile。                                                                                                                  | 10000        | Integer  |
  | **metricsRollingPercentile WindowBuckets**                 | 滚动百分位窗口被分解的桶数。这将传递到HystrixCommandMetrics内的HystrixRollingPercentile。                                                                                                                                | 6            | Integer  |
  | **metricsRollingStatistical WindowInMilliseconds**         | 此属性设置统计滚动窗口的持续时间（以毫秒为单位）。这是为线程池保留指标的时间长度。窗口按这些增量分为buckets和rolls。                                                                                                     | 10000        | Integer  |
  | **metricsRollingStatisticalWindowBuckets**                 | 滚动统计窗口分为多个buckets。这将传递到HystrixCommandMetrics内的HystrixRollingNumber。                                                                                                                                   | 10           | Integer  |
  | **requestLogEnabled**                                      | 是否应将HystrixCommand执行和事件记录到HystrixRequestLog。                                                                                                                                                                | TRUE         | Boolean  |
  | **corePoolSize**                                           | 传递给java.util.concurrent.ThreadPoolExecutor的核心线程池大小#setCorePoolSize(int)                                                                                                                                       | 10           | Integer  |
  | **maximumSize**                                            | 传递给ThreadPoolExecutor的最大线程池大小#setMaximumPoolSize(int)。这是在不开始拒绝HystrixCommands的情况下可以支持的最大并发数。请注意，此设置仅在您设置allowMaximumSizeToDivergeFromCoreSize时生效                       | 10           | Integer  |
  | **keepAliveTime**                                          | 以分钟为单位的保持活动时间传递给{link ThreadPoolExecutor #setKeepAliveTime（long，TimeUnit）}                                                                                                                            | 1            | Integer  |
  | **maxQueueSize**                                           | 在HystrixConcurrencyStrategy.getBlockingQueue(int)中传递给BlockingQueue的最大队列大小这应该只影响线程池的实例化 - 动态更改队列大小是不可能的。为此，请使用queueSizeRejectionThreshold()。                                | -1           | Integer  |
  | **queueSizeRejectionThreshold**                            | 队列大小拒绝阈值是一种人为的最大大小，即使尚未达到maxQueueSize，也会发生拒绝。这样做是因为无法动态更改BlockingQueue的maxQueueSize，我们希望支持动态更改影响拒绝的队列大小。排队线程执行时，HystrixCommand使用此方法。    | 5            | Integer  |
  | **threadPoolRollingNumberStatisticalWindowInMilliseconds** | 统计滚动窗口的持续时间（以毫秒为单位）。这将传递到每个HystrixThreadPoolMetrics实例中的HystrixRollingNumber。                                                                                                             | 10000        | Integer  |
  | **threadPoolRollingNumberStatisticalWindowBuckets**        | 滚动统计窗口分为多个桶。这将传递到每个HystrixThreadPoolMetrics实例中的HystrixRollingNumber。                                                                                                                             | 10           | Integer  |
  | **allowMaximumSizeToDivergeFromCoreSize**                  | 允许maximumSize的配置生效。该值可以等于或高于coreSize                                                                                                                                                                    | FALSE        | Boolean  |

  # 21. [**Idempotent Consumer EIP**](https://camel.apache.org/manual/latest/idempotentConsumer-eip.html)

  来自[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的[幂等消费者](http://www.enterpriseintegrationpatterns.com/IdempotentReceiver.html)用于过滤掉重复的消息。

  幂等消费者本质上像[消息过滤](https://camel.apache.org/manual/latest/filter-eip.html)器一样过滤掉重复项。

  Camel会急切地将消息ID添加到存储库，以检测当前正在进行的Exchange的重复。完成后，如果Exchange失败，Camel将从存储库中删除消息ID，否则它将保留在那里。

  Camel提供以下Idempotent Consumer实现:

  l MemoryIdempotentRepository

  l [FileIdempotentRepository](https://camel.apache.org/components/latest/file-component.html)

  l [HazelcastIdempotentRepository](https://camel.apache.org/components/latest/hazelcast.html)

  l [JdbcMessageIdRepository](https://camel.apache.org/components/latest/sql-component.html)

  l [JpaMessageIdRepository](https://camel.apache.org/components/latest/jpa-component.html)

  l [InfinispanIdempotentRepository](https://camel.apache.org/components/latest/infinispan-component.html)

  l [JCacheIdempotentRepository](https://camel.apache.org/components/latest/jcache-component.html)

  l [SpringCacheIdempotentRepository](https://camel.apache.org/manual/latest/spring.html)

  l [EhcacheIdempotentRepository](https://camel.apache.org/components/latest/ehcache-component.html)

  l [KafkaIdempotentRepository](https://camel.apache.org/components/latest/kafka-component.html)

  ## 21.1. **选项**

  Idempotent Consumer EIP支持5个选项，如下所示:


  | **名称**                   | **描述**                                                                                                                                                                                                                                                                                                                                                                                                               | **默认** | **类型** |
  | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
  | **messageIdRepositoryRef** | **必需**设置消息标识存储库的引用名称                                                                                                                                                                                                                                                                                                                                                                                   |          | String   |
  | **eager**                  | 设置是否急切地将key添加到幂等存储库或等到交换完成。Eager是默认启用的。                                                                                                                                                                                                                                                                                                                                                 | TRUE     | Boolean  |
  | **completionEager**        | 设置是否完成幂等消费者渴望或完成交换。如果此选项为true以完成eager，则当幂交换到达幂等消费者模式的块的末尾时，幂等消费者将触发其完成。因此，如果在块结束后继续路由交换，那么无论发生什么都不会影响状态。如果此选项为false（默认）为不完全急切，则幂等消费者将在完成交换路由时完成。因此，如果在块结束后继续路由交换，那么在那里发生的任何事情也会影响状态。例如，如果交换由于异常而失败，那么幂等消费者的状态将是回滚。 | FALSE    | Boolean  |
  | **skipDuplicate**          | 设置是否跳过重复项。默认行为是跳过重复项。重复消息将Exchange属性org.apache.camel.Exchange＃DUPLICATE_MESSAGE设置为Boolean＃TRUE值。无重复的消息将不会设置此属性。                                                                                                                                                                                                                                                      | TRUE     | Boolean  |
  | **removeOnFailure**        | 设置是否在失败时删除或保持key。默认行为是在失败时删除key。                                                                                                                                                                                                                                                                                                                                                             | TRUE     | Boolean  |

  # 22. [**In Only EIP**](https://camel.apache.org/manual/latest/inOnly-eip.html)

  该**INONLY****:** EIP定义INONLY ExchangePattern。

  ## 22.1. **EIP选项**

  In Only EIP支持下面列出的1个选项:


  | **名称** | **描述**                          | **默认** | **类型** |
  | -------- | --------------------------------- | -------- | -------- |
  | **uri**  | **必需**设置要发送到的端点的URI。 |          | String   |

  # 23. [**In Out EIP**](https://camel.apache.org/manual/latest/inOut-eip.html)

  该**INOUT****:** EIP定义INOUT ExchangePattern。

  ## 23.1. **EIP选项**

  In Out EIP支持以下列出的1个选项:


  | **名称** | **描述**                          | **默认** | **类型** |
  | -------- | --------------------------------- | -------- | -------- |
  | **uri**  | **必需**设置要发送到的端点的URI。 |          | String   |

  # 24. [**Load Balance EIP**](https://camel.apache.org/manual/latest/loadBalance-eip.html)

  Load Balancer Pattern允许您使用各种不同的负载平衡策略委派给多个端点之一。

  ## 24.1. **内置负载均衡策略**

  Camel提供了开箱即用的以下策略:


  | **策略**             | **描述**                                                                                                                                 |
  | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
  | Round Robin          | 交换是以循环方式选择的。这是一个众所周知的经典政策，可以均匀地分摊负载。                                                                 |
  | Random               | 为每个交换选择随机端点。                                                                                                                 |
  | Sticky               | 使用Expression计算相关键以执行粘性负载平衡的粘性负载平衡; 更喜欢网络中的jsessionid或JMS中的JMSXGroupID。                                |
  | Topic                | 发送到所有目的地的主题（更像是JMS主题）                                                                                                  |
  | Failover             | 如果出现故障，将在下一个端点上尝试交换。                                                                                                 |
  | Weighted Round-Robin | 加权负载平衡策略允许您为每个服务器指定相对于其他服务器的处理负载分配比率。除了权重之外，还使用基于权重**的循环**分布进一步细化端点选择。 |
  | Weighted Random      | 加权负载平衡策略允许您为每个服务器指定相对于其他服务器的处理负载分配比率。除了权重之外，还使用基于权重的**随机**分布进一步细化端点选择。 |
  | Custom               | 使用自定义Load Balancer的首选方法是使用此策略，因为不再支持ref属性。                                                                     |

  ## 24.2. **选项**

  Load Balance EIP支持2个选项，如下所示:


  | **名称**                | **描述**                                                                                                                                        | **默认** | **类型**               |
  | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------------------- |
  | **loadBalancerType**    | **必需要**使用的负载均衡器                                                                                                                      |          | LoadBalancerDefinition |
  | **inheritErrorHandler** | 设置是否继承已配置的错误处理程序。默认值是true。您可以使用此选项禁用给定DSL的继承错误处理程序，例如您要使用自定义错误处理程序策略的负载均衡器。 | false    | Boolean                |

  ## 24.3. **Round Robin**

  循环负载平衡器不适用于故障转移，因为您应该使用专用**故障转移**负载平衡器。循环负载平衡器将仅更改为每个消息的下一个端点。循环负载平衡器是有状态的，因为它保持下次使用哪个端点的状态。

  这是一个小例子:

  from("direct:start")

  **    **.loadBalance().roundRobin()

  **        **.to("mock:x")

  **        **.to("mock:y")

  **        **.to("mock:z")

  **    **.end() *// end load balancer*

  在XML中:

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

  **  **<route>

  **    **<from uri="direct:start"/>

  **    **<loadBalance>

  **        **<roundRobin/>

  **        **<to uri="mock:x"/>

  **        **<to uri="mock:y"/>

  **        **<to uri="mock:z"/>

  **    **</loadBalance>

  **  **</route>

  </camelContext>

  上面的示例从**direct:start**向一个可用的**mock****端点**实例加载平衡请求，在这种情况下使用循环策略。

  ## 24.4. **故障转移Failover**

  故障转移负载平衡器能够在Exchange处理失败并且在处理期间发生异常时尝试下一个处理器。只有在指定列表的一个例外发生时，才能将故障转移限制为激活。如果未指定列表，则任何异常都将导致故障转移。此平衡器使用相同的策略来匹配异常，就像Exception子句为onException。


  |  | **如果使用流，则启用流缓存:**如果使用流，则应在使用故障转移负载平衡器时启用流缓存。这是必需的，因此在故障转移到下一个处理器之后可以重新读取流。 |
  | - | ----------------------------------------------------------------------------------------------------------------------------------------------- |

  以下是仅在抛出与IOException相关的异常时才进行故障转移的示例:

  from("direct:start")

  **    ***// here we will load balance if IOException was thrown*

  **    ***// any other kind of exception will result in the Exchange as failed*

  **    ***// to failover over any kind of exception we can just omit the exception*

  **    ***// in the failOver DSL*

  **    **.loadBalance().failover(IOException.class)

  **        **.to("mock:x")

  **        **.to("mock:y")

  **        **.to("mock:z");

  您可以指定多个故障转移exception，因为选项是varargs（不定参数），例如:

  *// enable maximum redelivery so failover can react*

  errorHandler(defaultErrorHandler().maximumRedeliveries(5));

  from("direct:foo").

  **    **loadBalance().failover(IOException.class, MyOtherException.class)

  **        **.to("direct:a")

  **        **.to("direct:b");

  在XML中:

  故障转移也可以在Spring DSL中使用，您可以将其配置为:

  <route errorHandlerRef="myErrorHandler">

  **   **<from uri="direct:foo"/>

  **   **<loadBalance>

  **       **<failover>

  **           **<exception>java.io.IOException</exception>

  **           **<exception>com.mycompany.MyOtherException</exception>

  **       **</failover>

  **       **<to uri="direct:a"/>

  **       **<to uri="direct:b"/>

  **   **</loadBalance>

  ** **</route>

  ## 24.5. **在循环模式下使用故障转移**

  使用Java DSL的示例:

  from("direct:start")

  **    ***// Use failover load balancer in stateful round robin mode*

  **    ***// which mean it will failover immediately in case of an exception*

  **    ***// as it does NOT inherit error handler. It will also keep retrying as*

  **    ***// its configured to newer exhaust.*

  **    **.loadBalance().failover(-1, false, true)

  **        **.to("direct:bad")

  **        **.to("direct:bad2")

  **        **.to("direct:good")

  **        **.to("direct:good2");

  使用Spring XML的相同示例:

  <route>

  **    **<from uri="direct:start"/>

  **    **<loadBalance>

  **        ***<!-- failover using stateful round robin,*

  * which will keep retrying forever those 4 endpoints until success.*
    *         You can set the maximumFailoverAttempt to break out after X attempts -->*
    **        **<failover roundRobin="true"/>
    **        **<to uri="direct:bad"/>
    **        **<to uri="direct:bad2"/>
    **        **<to uri="direct:good"/>
    **        **<to uri="direct:good2"/>
    </loadBalance>

    </route>

    |  | **已禁用inheritErrorHandler**:您可以配置inheritErrorHandler=false是否要尽快故障转移到下一个端点。通过禁用错误处理程序，您可以确保它不会*干预*，从而允许failover负载均衡器尽快处理故障转移。通过启用roundRobin模式，它将继续重试，直到成功。然后，您可以将该maximumFailoverAttempts选项配置为较高的值，以使其最终耗尽（放弃）并失败。 |
    | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

    ## 24.6. **加权循环和随机负载平衡**

    **自Camel 2.5起可用**
    在利用不同处理能力和性能特征的服务器节点来托管服务和处理端点的许多企业环境中，经常需要根据其各自的服务器功能来分配处理负载，以便某些端点不会受到请求的不公平负担。显然，简单的循环或随机负载平衡不能缓解这种性质的问题。加权循环和/或加权随机负载平衡器可用于解决此问题。加权负载平衡策略允许您为每个服务器指定相对于其他服务器的处理负载分配比率。您可以将此指定为每个服务器的正处理权重。数字越大表示服务器可以处理更大的负载。
    可以使用的参数是
    | **选项**                   | **类型** | **默认** | **描述**                                                                                                                                                 |
    | -------------------------- | -------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | roundRobin                 | Boolean  | False    | round-robin的默认值为false。在没有此设置或参数的情况下，使用的负载平衡算法是随机的。                                                                     |
    | distributionRatio          | String   | none     | distributionRatio是一个分隔的字符串，由分隔符分隔的整数权重组成，例如"2,3,5"。distributionRatio必须与负载均衡器列表中指定的端点和/或处理器的数量相匹配。 |
    | distributionRatioDelimiter | String   | ，       | distributionRatioDelimiter是用于指定distributionRatio的分隔符。如果未指定此属性，则应使用默认分隔符","作为用于指定distributionRatio的分隔符。            |

    ## 24.7. **使用加权循环和随机负载平衡**

    **自Camel 2.5起可用**
    使用Java DSL的示例:
    List<integer> distributionRatio = new** **ArrayList<integer>();
    distributionRatio.add(4);
    distributionRatio.add(2);
    distributionRatio.add(1);*// round-robin*
    from("direct:start")
    **    **.loadBalance().weighted(true, distributionRatio)
    **    **.to("mock:x", "mock:y", "mock:z");*//random*
    from("direct:start")
    **    **.loadBalance().weighted(false, distributionRatio)
    **    **.to("mock:x", "mock:y", "mock:z");
    使用Spring XML的相同示例:
    <route>

    **  **<from uri="direct:start"/>
    **  **<loadBalance>
    **    **<weighted roundRobin="false"
              distributionRatio="4 2 1"/>
    **      **<to uri="mock:x"/>

    **      **<to uri="mock:y"/>

    **      **<to uri="mock:z"/>

    **  **</loadBalance>

    </route>

    使用Java DSL的示例:

    *// round-robin*

    from("direct:start")

    **    **.loadBalance().weighted(true, "4:2:1"** **distributionRatioDelimiter=":")

    **    **.to("mock:x", "mock:y", "mock:z");*//random*

    from("direct:start")

    **    **.loadBalance().weighted(false, "4,2,1")

    **    **.to("mock:x", "mock:y", "mock:z");

    使用Spring XML的相同示例:

    <route>

    **  **<from uri="direct:start"/>

    **  **<loadBalance>

    **    **<weighted roundRobin="false"

              distributionRatio="4-2-1" distributionRatioDelimiter="-" />
    **      **<to uri="mock:x"/>

    **      **<to uri="mock:y"/>

    **      **<to uri="mock:z"/>

    **  **</loadBalance>

    </route>

    # 25. [**Log EIP**](https://camel.apache.org/manual/latest/log-eip.html)

    如何记录[消息](https://camel.apache.org/manual/latest/message.html)的处理？

    Camel提供了许多方法来记录您正在处理消息的事实。以下是一些示例:

    l *您可以使用记录消息内容的[Log](https://camel.apache.org/components/latest/log-component.html)组件。

    l *您可以使用[Tracer](https://camel.apache.org/manual/latest/tracer.html)，其跟踪日志消息流。

    l *您还可以使用[Processor](https://camel.apache.org/manual/latest/processor.html)或[Bean](https://camel.apache.org/manual/latest/bean-binding.html)从Java代码记录。

    l *您可以使用日志DSL。

    ## 25.1. **选项**

    Log EIP支持5个选项，如下所示:


    | **名称**         | **描述**                                 | **默认** | **类型**     |
    | ---------------- | ---------------------------------------- | -------- | ------------ |
    | **message**      | **必需**设置日志消息（使用简单语言）     |          | String       |
    | **loggingLevel** | 设置日志记录级别。默认值为INFO           | INFO     | LoggingLevel |
    | **logName**      | 设置记录器的名称                         |          | String       |
    | **marker**       | 使用slf4j标记                            |          | String       |
    | **loggerRef**    | 引用自定义logger实例以从注册表进行查找。 |          | String       |

    ### 25.1.1. **DSL里的Log和Log组件之间的区别**

    日志DSL更轻，用于记录更人性化的日志，如开始做...等。它只能记录基于简单语言的消息。另一方面，Log组件是一个完整的组件，涉及使用端点等。Log组件用于记录Message本身，并且您有许多URI选项来控制您想要记录的内容。

    ## 25.2. **示例**

    您可以使用日志DSL，它允许您使用[简单](https://camel.apache.org/manual/latest/simple-language.html)语言来构建记录的动态消息。

    例如，你可以做到

    from("direct:start")

    **    **.log("Processing ${id}")

    **    **.to("bean:foo");

    这使用Simple语言在运行时构造String消息。日志消息将使用路由ID作为日志名称记录在INFO级别。默认情况下，路由命名为route-1，route-2等。但您可以使用routeId（"myCoolRoute"）来设置选择的路由名称。


    |  | **使用流式消息记录消息体:**如果消息体是基于流的，则记录消息体可能导致消息体随后为空。请参阅此对于流式消息常见问题 ，您可以使用流缓存来允许记录消息体，并能够再次读取消息体。 |
    | - | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

    日志DSL还有重载方法来设置日志记录级别和/或名称。

    from("direct:start")

    **    **.log(LoggingLevel.DEBUG, "Processing ${id}")

    **    **.to("bean:foo");

    设置记录器logger名称

    from("direct:start")

    **    **.log(LoggingLevel.DEBUG, "com.mycompany.MyCoolRoute", "Processing ${id}")

    **    **.to("bean:foo");

    也可以使用logger记录器实例:

    from("direct:start")

    **    **.log(LoggingLeven.DEBUG, org.slf4j.LoggerFactory.getLogger("com.mycompany.mylogger"), "Processing ${id}")

    **    **.to("bean:foo");

    例如，如果使用文件，则可以使用它来记录正在处理的文件名。

    from("file://target/files")

    **    **.log(LoggingLevel.DEBUG, "Processing file ${file:name}")

    **    **.to("bean:foo");

    在Spring DSL中，它也很容易使用log DSL，如下所示:

    <route id="foo">

    **    **<from uri="direct:foo"/>

    **    **<log message="Got ${body}"/>

    <to uri="mock:foo"/>

    </route>

    log标记具有用于设置消息loggingLevel和logName的属性。例如:

    <route id="baz">

    **    **<from uri="direct:baz"/>

    **    **<log message="Me Got ${body}" loggingLevel="FATAL" logName="com.mycompany.MyCoolRoute"/>

    <to uri="mock:baz"/>

    </route>

    从Camel **2.12.4/2.13.1**开始，可以引用logger实例。例如:

    <bean id="myLogger" class="org.slf4j.LoggerFactory" factory-method="getLogger" xmlns="http://www.springframework.org/schema/beans">

    <constructor-arg value="com.mycompany.mylogger" />

    </bean>

    <route id="moo" xmlns="http://camel.apache.org/schema/spring">

    **    **<from uri="direct:moo"/>

    **    **<log message="Me Got ${body}" loggingLevel="INFO" loggerRef="myLogger"/>

    <to uri="mock:baz"/>

    </route>

    ### 25.2.1. **使用Registry中的Logger实例**

    如果没有将记录器名称或记录器实例传递给日志DSL，则执行注册表查找org.slf4j.Logger的单个实例。如果找到这样的实例，则使用它而不是创建新的记录器实例。如果找到更多实例，则默认创建新的logger实例。

    ## 25.3. **配置****全局日志名称**

    **自Camel 2.17起可用**

    默认情况下，日志名称是路由ID。如果要使用其他日志名称，则需要配置logName选项。但是，如果您有许多日志并且希望所有日志都使用相同的日志名称，则需要在所有日志上设置该logName选项。

    您可以配置全局日志名称，而不是路由ID，例如

    camelContext.getProperties().put(Exchange.LOG_EIP_NAME, "com.foo.myapp");

    在XML中

    <camelContext ...>

    **  **<properties>

    **    **<property key="CamelLogEipName" value="com.foo.myapp"/>

    **  **</properties>

    </camelContext>

    ## 25.4. **使用SLF4J Marker**

    **自Camel 2.9起可用**

    您可以在DSL中指定marker名称

    <route id="baz">

    **    **<from uri="direct:baz"/>

    **    **<log loggingLevel="FATAL" logName="com.mycompany.MyCoolRoute" marker="myMarker"

         message="Me Got ${body}"/>
    <to uri="mock:baz"/>

    </route>

    ## 25.5. **在OSGI中使用log DSL**

    在OSGi中使用log DSL时（例如，在Karaf中），底层日志记录机制由PAX日志记录提供。它搜索一个调用org.slf4j.LoggerFactory.getLogger()方法的bundle，并将该bundle与logger实例相关联。仅将记录器名称传递给日志DSL会导致将camel-core bundle与创建的记录器实例相关联。

    在某些情况下，需要与记录器关联的捆绑包应该是包含路由定义的捆绑包。这可以使用为Java DSL和Spring DSL提供的logger实例（参见上面的示例）。

    ## 25.6. **屏蔽密码等敏感信息**

    **自Camel 2.19起可用**

    您可以通过将logMask** **flag 设置为true来启用安全屏蔽以进行日志记录。请注意，此选项也会影响[Log](https://camel.apache.org/components/latest/log-component.html)组件。

    要在CamelContext级别的Java DSL中启用掩码:

    camelContext.setLogMask(true);

    在XML中:

    <camelContext logMask="true">

    ...

    </camelContext>

    您也可以在路由级别打开|关闭。要在路由级别的Java DSL中启用掩码:

    from("direct:start").logMask()

    **    **.log("Processing ${id}")

    **    **.to("bean:foo");

    在XML中:

    <route logMask="true">

    ...

    </route>

    org.apache.camel.support.processor.DefaultMaskingFormatter默认情况下用于屏蔽。如果要使用自定义屏蔽格式化程序，请将其与CamelCustomLogMask名称一起放入注册表中。请注意，屏蔽格式化程序必须实现org.apache.camel.spi.MaskingFormatter。

    # 26. [**Loop EIP**](https://camel.apache.org/manual/latest/loop-eip.html)

    循环允许多次处理消息，每次迭代可能以不同的方式处理。主要在测试期间有用。


    |  | ***默认模式***===默认情况下，循环在整个循环中使用相同的交换。因此，前一次迭代的结果将用于下一次（例如管道和过滤器）。您可以改为启用复制模式。有关更多详细信息，请参阅选项表。=== |
    | - | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

    ## 26.1. **选项**

    Loop EIP支持2个选项，如下所示:


    | **名称**    | **描述**                                                                                                                                                                 | **默认** | **类型** |
    | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- |
    | **copy**    | 如果copy属性为true，则每次迭代都使用输入Exchange的副本。这意味着每次迭代都将从同一消息的副本开始。默认情况下，循环将遍历相同的交换，因此每次迭代可能具有不同的消息内容。 | false    | Boolean  |
    | **doWhile** | 启用循环的while循环，直到谓词计算结果为false或null。                                                                                                                     | false    | Boolean  |

    ## 26.2. **交换属性**

    对于每次迭代，在Exchange上设置两个属性。处理器可以依赖这些属性以不同的方式处理消息。


    | **属性**       | **描述**                                            |
    | -------------- | --------------------------------------------------- |
    | CamelLoopSize  | 循环总数。如果在while循环模式下运行循环，则不可用。 |
    | CamelLoopIndex | 当前迭代的索引（基于0开始）                         |

    ## 26.3. **示例**

    以下示例显示如何从**direct****:****x**端点获取请求，然后将消息重复发送到**mock****:****result**。发送消息的次数要么作为参数传递loop()，要么在运行时通过计算表达式来确定。表达式**必须**求值为int，否则抛出RuntimeCamelException。

    将循环计数作为参数传递

    from("direct:a")

    **    **.loop(8)

    **        **.to("mock:result");

    使用表达式确定循环计数

    from("direct:b")

    **    **.loop(header("loop"))

    **        **.to("mock:result");

    使用表达式确定循环计数

    from("direct:c")

    **    **.loop(xpath("/hello/@times"))

    **        **.to("mock:result");

    以及XML中的示例:

    将循环计数作为参数传递

    <route>

    **  **<from uri="direct:a"/>

    **  **<loop>

    **    **<constant>8</constant>

    **    **<to uri="mock:result"/>

    **  **</loop>

    </route>

    使用表达式确定循环计数

    <route>

    **  **<from uri="direct:b"/>

    **  **<loop>

    **    **<header>loop</header>

    **    **<to uri="mock:result"/>

    **  **</loop>

    </route>

    ## 26.4. **使用copy模式**

    **自Camel 2.8起可用**

    现在假设我们向"direct:start"端点发送包含字母A 的消息。处理此路由的输出将是，每个"mock:loop"端点将接收"AB"作为消息。

    from("direct:start")

    **    ***// instruct loop to use copy mode, which mean it will use a copy of the input exchange*

    **    ***// for each loop iteration, instead of keep using the same exchange all over*

    **    **.loop(3).copy()

    **        **.transform(body().append("B"))

    **        **.to("mock:loop")

    **    **.end() *// end loop*

    **    **.to("mock:result");

    但是，如果我们**不**启用copy模式，那么"mock:loop"将收到"AB"，"ABB"，"ABBB"等消息。

    from("direct:start")

    **    ***// by default loop will keep using the same exchange so on the 2nd and 3rd iteration its*

    **    ***// the same exchange that was previous used that are being looped all over*

    **    **.loop(3)

    **        **.transform(body().append("B"))

    **        **.to("mock:loop")

    **    **.end() *// end loop*

    **    **.to("mock:result");

    复制模式下XML DSL中的等效示例如下:

    <route>

    **  **<from uri="direct:start"/>

    **  ***<!-- enable copy mode for loop eip -->*

    **  **<loop copy="true">

    **    **<constant>3</constant>

    **    **<transform>

    **      **<simple>${body}B</simple>

    **    **</transform>

    **    **<to uri="mock:loop"/>

    **  **</loop>

    **  **<to uri="mock:result"/>

    </route>

    ## 26.5. **使用while模式**

    **自Camel 2.17起可用**

    循环可以像while一样循环，直到表达式求值为false或null。例如，下面的路由循环，消息体的长度是5个或更少字符。请注意，DSL使用**loopDoWhile**。

    from("direct:start")

    **    **.loopDoWhile(simple("${body.length} <= 5"))

    **        **.to("mock:loop")

    **        **.transform(body().append("A"))

    **    **.end() *// end loop*

    **    **.to("mock:result");

    和XML中的相同示例:

    <route>

    **  **<from uri="direct:start"/>

    **  **<loop doWhile="true">

    **    **<simple>${body.length} <= 5</simple>

    **    **<to uri="mock:loop"/>

    **    **<transform>

    **      **<simple>A${body}</simple>

    **    **</transform>

    **  **</loop>

    **  **<to uri="mock:result"/>

    </route>

    请注意，在XML中，使用**doWhile**属性打开了while循环。

    # 27. [**Marshal EIP**](https://camel.apache.org/manual/latest/marshal-eip.html)

    编组（marshal）与解组（unmarshal）相反，其中bean被编组成一些二进制或文本格式，以便通过Camel [组件](https://github.com/apache/camel/tree/master/components)在某些传输上进行传输。编组的使用方式与上面的解组相同; 在[DSL中，](https://github.com/apache/camel/blob/master/docs/user-manual/en/dsl.adoc)您可以使用DataFormat实例，可以使用DSL动态配置DataFormat，也可以在[Registry中](https://github.com/apache/camel/blob/master/docs/user-manual/en/registry.adoc)引用该格式的命名实例。

    ## 27.1. **选项**

    Marshal EIP支持以下列出的1个选项:


    | **名称**           | **描述**                 | **默认** | **类型**             |
    | ------------------ | ------------------------ | -------- | -------------------- |
    | **dataFormatType** | **必需要**使用的数据格式 |          | DataFormatDefinition |

    ## 27.2. **示例**

    以下示例通过序列化解组，然后使用名叫JAXB的数据格式进行编组以执行[Message Translator](https://camel.apache.org/manual/latest/message-translator.html)

    from("file://foo/bar").

    **  **unmarshal().serialization().

    **  **marshal("jaxb").

    **  **to("activemq:Some.Queue");

    ### 27.2.1. **使用Spring Xml**

    此示例显示如何只配置一次数据类型并在多个路由上重复使用它

    您还可以将可复用数据格式定义为Spring bean

    <bean id="myJaxb" class="org.apache.camel.model.dataformat.JaxbDataFormat">

    **  **<property name="prettyPrint" value="true"/>

    **  **<property name="contextPath" value="org.apache.camel.example"/>

    </bean>

    # 28. [**Multicast EIP**](https://camel.apache.org/manual/latest/multicast-eip.html)

    Multicast EIP允许将相同的消息路由到多个端点，并以不同的方式处理它们。Multicast和Splitter之间的主要区别在于Splitter会将消息拆分为多个部分，但Multicast不会修改请求消息。

    ## 28.1. **选项**

    Multicast EIP支持12个选项，如下所示:


    | **名称**                     | **描述**                                                                                                                                                                                                                                                                                                                                | **默认** | **类型** |
    | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
    | **parallelProcessing**       | 如果启用，则同时向多路广播发送消息。请注意，调用方线程仍将等待，直到所有消息都已完全处理完毕，然后再继续。它只发送和处理同时发生的多路广播的回复。                                                                                                                                                                                      | FALSE    | Boolean  |
    | **strategyRef**              | 指用于将来自多路广播的回复组合成来自多路广播的单个传出消息的AggregationStrategy。默认情况下，Camel将使用最后一个回复作为传出消息。您还可以使用POJO作为AggregationStrategy                                                                                                                                                               |          | String   |
    | **strategyMethodName**       | 当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。                                                                                                                                                                                                                                                             |          | String   |
    | **strategyMethodAllowNull**  | 如果此选项为false，则在没有要丰富的数据时不使用聚合方法。如果此选项为true，那么当使用POJO作为AggregationStrategy时，将使用null值作为oldExchange（当没有数据可以充实时）                                                                                                                                                                 | FALSE    | Boolean  |
    | **executorServiceRef**       | 指用于并行处理的自定义线程池。请注意，如果设置此选项，则会自动隐含并行处理，您也不必启用该选项。                                                                                                                                                                                                                                        |          | String   |
    | **streaming**                | 如果启用，则Camel将按顺序处理回复，例如按照它们返回的顺序。如果禁用，Camel将按照多路广播定义的顺序处理回复。                                                                                                                                                                                                                            | FALSE    | Boolean  |
    | **stopOnException**          | 如果在处理org.apache.camel.Exchange期间发生异常或故障，将立即停止进一步处理，并且将引发引起的异常。如果处理Exchange失败（有错误消息）或错误处理程序抛出并处理异常（例如使用onException），也会停止。在所有情况下，多路广播将停止进一步处理。这与路由引擎使用的管道中的行为相同。默认行为是不停止但继续处理直到结束                      | FALSE    | Boolean  |
    | **timeout**                  | 使用并行处理时，设置以毫秒为单位指定的总超时。如果多路广播无法在给定时间范围内发送和处理所有回复，则超时触发并且多路广播突发并继续。请注意，如果您提供TimeoutAwareAggregationStrategy，则会在分解之前调用timeout方法。如果在仍然保持运行任务的情况下达到超时，则Camel难以以正常方式关闭的某些任务可能会继续运行。因此请谨慎使用此选项。 | 0        | Long     |
    | **onPrepareRef**             | 准备要发送的org.apache.camel.Exchange时使用处理器。这可用于深度克隆应发送的消息，或者在发送交换之前所需的任何自定义逻辑。                                                                                                                                                                                                               |          | String   |
    | **shareUnitOfWork**          | 与父级和每个子消息共享org.apache.camel.spi.UnitOfWork。默认情况下，多路广播不会在父Exchange和每个多路广播Exchange之间共享工作单元。这意味着每个子交换都有自己独立的工作单元。                                                                                                                                                           | FALSE    | Boolean  |
    | **parallelAggregate**        | 如果启用，则可以同时调用AggregationStrategy上的聚合方法。请注意，这需要将AggregationStrategy实现为线程安全的。默认情况下，这是错误的，这意味着Camel会将调用同步到聚合方法。虽然在某些用例中，当AggregationStrategy实现为线程安全时，这可用于存档更高的性能。                                                                            | FALSE    | Boolean  |
    | **stopOnAggregateException** | 如果启用，请在使用parallelProcessing时将聚合时发生的异常展开到错误处理程序。目前，聚合时间异常不会在使用parallelProcessing时停止路由处理。启用此选项可以解决此问题。为了向后兼容，默认值为false。                                                                                                                                       | FALSE    | Boolean  |

    ## 28.2. **多路广播示例**

    以下示例显示如何从**direct****:****a**端点发出请求，然后将这些请求多路广播到**direct****:****x**，**direct****:****y**，**direct****:****z**。

    ## 28.3. **使用流利构建器**

    默认情况下，Multicast按顺序调用每个端点。如果需要并行处理，只需使用

    from("direct:a").multicast().parallelProcessing().to("direct:x", "direct:y", "direct:z");

    在使用InOut MEP的情况下，AggregationStrategy用于聚合所有回复消息。默认设置是只使用最新的回复消息并丢弃任何先前的回复。聚合策略是可配置的:

    from("direct:start")

    **  **.multicast(new** **MyAggregationStrategy())

    **  **.parallelProcessing().timeout(500).to("direct:a", "direct:b", "direct:c")

    **  **.end()

    **  **.to("mock:result");


    |  | Multicast，Recipient List和Splitter EIP特别支持使用AggregationStrategy访问原始输入交换。您可能希望在聚合时使用此消息，并且其中一条消息出现故障，然后您希望在原始输入消息上进行丰富并作为响应返回; 它是具有3个交换参数的聚合方法。 |
    | - | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

    ## 28.4. **如果发生异常，就停止处理**

    默认情况下，多路广播EIP将继续处理整个交换，即使其中一个多路广播消息在路由期间抛出异常。例如，如果要多路广播到3个目标，第二个目标因异常而失败。Camel默认做的是处理剩余的目的地。通过AggregationStrategy你有机会补救或处理这个问题。

    但有时你只是希望Camel停止并让异常传播回来，让Camel错误处理程序处理它。您可以通过指定在发生异常时应该停止来执行此操作。这是通过stopOnException如下所示的选项完成的:

    **    **from("direct:start")

    **        **.multicast()

    **            **.stopOnException().to("direct:foo", "direct:bar", "direct:baz")

    **        **.end()

    **        **.to("mock:result");

    **        **from("direct:foo").to("mock:foo");

    **        **from("direct:bar").process(new** **MyProcessor()).to("mock:bar");

    **        **from("direct:baz").to("mock:baz");

    使用XML DSL，您可以按如下方式指定:

    **        **<route>

    **            **<from uri="direct:start"/>

    **            **<multicast stopOnException="true">

    **                **<to uri="direct:foo"/>

    **                **<to uri="direct:bar"/>

    **                **<to uri="direct:baz"/>

    **            **</multicast>

    **            **<to uri="mock:result"/>

    **        **</route>

    **        **<route>

    **            **<from uri="direct:foo"/>

    **            **<to uri="mock:foo"/>

    **        **</route>

    **        **<route>

    **            **<from uri="direct:bar"/>

    **            **<process ref="myProcessor"/>

    **            **<to uri="mock:bar"/>

    **        **</route>

    **        **<route>

    **            **<from uri="direct:baz"/>

    **            **<to uri="mock:baz"/>

    **        **</route>

    ## 28.5. **在准备消息时使用onPrepare执行自定义逻辑**

    多路广播EIP将复制源头交换并对每个副本进行多路广播。但是，副本是浅拷贝，因此如果您有可变异的消息体，则其他复制的消息将随之更改。如果要使用深度克隆副本，则需要使用onPrepare允许使用处理器接口执行此操作的自定义。

    请注意，onPrepare可以在[Exchange](https://camel.apache.org/manual/latest/exchange.html)被多路广播之前用于任何类型的自定义逻辑。

    # 29. [**On Fallback EIP**](https://camel.apache.org/manual/latest/onFallback-eip.html)

    如果您使用的是**onFallback**，则仅在可以进行消息转换或调用Bean或将其作为fallback的地方进行本地处理。

    如果需要通过网络调用外部服务，则应使用**onFallbackViaNetwork**，该网络在另一个独立的**HystrixCommand**中运行，该HystrixCommand使用其自己的线程池不耗尽第一个command。

    ## 29.1. **选项**

    On Fallback EIP支持下面列出的1个选项:


    | **名称**               | **描述**                                                                                                                                                                                                                         | **默认** | **类型** |
    | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
    | **fallbackViaNetwork** | fallback是否通过网络。如果回退将通过网络，那么这是另一个可能的故障点，因此它也需要由HystrixCommand包装。在单独的线程池上执行fallback命令很重要，否则如果主命令变为潜在填充线程池，则两个命令共享同一个池，这将阻止fallback运行。 | False    | Boolean  |

    配置Hystrix示例Hystrix有许多选项，如上表所示。例如，将更高的超时设置为**5**秒，并且在状态被触发打开时再次尝试请求之前让断路器等待**10**秒。

    from("direct:start")

    **    **.hystrix()

    **        **.hystrixConfiguration()

    **             **.executionTimeoutInMilliseconds(5000)

    **             **.circuitBreakerSleepWindowInMilliseconds(10000)

    **        **.end() *// end Hystrix configuration*

    **        **.to("http://fooservice.com/slow")

    **    **.onFallback()

    **        **.transform().constant("Fallback message")

    **    **.end()

    **    **.to("mock:result");

    在XML DSL中:

    <camelContext xmlns="http://camel.apache.org/schema/spring">

    **  **<route>

    **    **<from uri="direct:start"/>

    **    **<hystrix>

    **      **<hystrixConfiguration executionTimeoutInMilliseconds="5000"

                            circuitBreakerSleepWindowInMilliseconds="10000"/>
    **      **<to uri="http://fooservice.com/slow"/>

    **      **<onFallback>

    **        **<transform>

    **          **<constant>Fallback message</constant>

    **        **</transform>

    **      **</onFallback>

    **    **</hystrix>

    **    **<to uri="mock:result"/>

    **  **</route>

    </camelContext>

    您还可以全局配置Hystrix，然后参考该配置:

    <camelContext xmlns="http://camel.apache.org/schema/spring">

    **  ***<!-- a shared config which you can refer to from all your Hystrix EIPs -->*

    **  **<hystrixConfiguration id="sharedConfig"

                        executionTimeoutInMilliseconds="5000"

                        circuitBreakerSleepWindowInMilliseconds="10000"/>
    **  **<route>

    **    **<from uri="direct:start"/>

    **    **<hystrix hystrixConfigurationRef="sharedConfig">

    **      **<to uri="http://fooservice.com/slow"/>

    **      **<onFallback>

    **        **<transform>

    **          **<constant>Fallback message</constant>

    **        **</transform>

    **      **</onFallback>

    **    **</hystrix>

    **    **<to uri="mock:result"/>

    **  **</route>

    </camelContext>

    # 30. [**Otherwise EIP**](https://camel.apache.org/manual/latest/otherwise-eip.html)

    Otherwise EIP是[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的[基于内容的路由器](http://www.enterpriseintegrationpatterns.com/ContentBasedRouter.html)

    ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps58.png)

    ## 30.1. **选项**

    Otherwise EIP没有选项。

    ## 30.2. **例子**

    以下示例显示如何从输入端点**direct:a**路由请求到**direct****:****b**，**direct****:****c**或**direct****:****d，**具体取决于各种[Predicate](https://camel.apache.org/manual/latest/predicate.html)表达式的计算结果

    RouteBuilder builder = new** **RouteBuilder() {

    **    **public void configure() {

    **        **from("direct:a")

    **            **.choice()

    **                **.when(simple("${header.foo} == 'bar'"))

    **                    **.to("direct:b")

    **                **.when(simple("${header.foo} == 'cheese'"))

    **                    **.to("direct:c")

    **                **.otherwise()

    **                    **.to("direct:d");

    **    **}

    };

    使用XML的相同示例:

    <camelContext xmlns="http://camel.apache.org/schema/spring">

    **    **<route>

    **        **<from uri="direct:a"/>

    **        **<choice>

    **            **<when>

    **                **<simple>${header.foo} == 'bar'</simple>

    **                **<to uri="direct:b"/>

    **            **</when>

    **            **<when>

    **                **<simple>${header.foo} == 'cheese'</simple>

    **                **<to uri="direct:c"/>

    **            **</when>

    **            **<otherwise>

    **                **<to uri="direct:d"/>

    **            **</otherwise>

    **        **</choice>

    </route>

    </camelContext>

    # 31. [**Pipeline EIP**](https://camel.apache.org/manual/latest/pipeline-eip.html)

    Camel [EIP模式](https://github.com/apache/camel/blob/master/docs/user-manual/en/enterprise-integration-patterns.adoc)以不同的方式支持[管道和过滤器](http://www.enterpriseintegrationpatterns.com/PipesAndFilters.html)（ [Pipes and Filters](http://www.enterpriseintegrationpatterns.com/PipesAndFilters.html)）。

    ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps59.png)

    使用Camel，您可以将处理拆分为多个独立的[Endpoint](https://github.com/apache/camel/blob/master/docs/user-manual/en/endpoint.adoc)实例，然后可以将它们链接在一起。

    ## 31.1. **选项**

    Pipeline EIP没有选择。

    ## 31.2. **例子**

    您可以使用多个[Endpoint](https://github.com/apache/camel/blob/master/docs/user-manual/en/endpoint.adoc)或[Message Translator](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message-translator.adoc)实例创建逻辑管道，如下所示

    虽然在Camel中指定多个输出时，管道是默认操作模式。与管道相反的是多路广播; 它会向每个输出发出相同的消息。（见下面的例子）。

    在Java中你做:

    from("activemq:SomeQueue")

    **    **.pipeline()

    **      **.bean("foo")

    **      **.bean("bar")

    **      **.to("acitvemq:OutputQueueu");

    管道是默认模式，可以省略，因此您几乎经常写为:

    from("activemq:SomeQueue")

    **    **.bean("foo")

    **    **.bean("bar")

    **    **.to("acitvemq:OutputQueueu");

    在XML中，您可以使用<pipeline>元素

    <route>

    **  **<from uri="activemq:SomeQueue"/>

    **  **<pipeline>

    **    **<bean ref="foo"/>

    **    **<bean ref="bar"/>

    **    **<to uri="activemq:OutputQueue"/>

    **  **</pipeline>

    </route>

    在上面，默认管道元素实际上是不必要的，你可以使用这个:

    <route>

    **  **<from uri="activemq:SomeQueue"/>

    **  **<bean ref="foo"/>

    **  **<bean ref="bar"/>

    **  **<to uri="activemq:OutputQueue"/>

    </route>

    它只是更明确一点。但是，如果您希望使用<multicast/>避免管道 - 将相同的消息发送到多个管道 - 那么该<pipeline>元素就是必需的。

    <route>

    **  **<from uri="activemq:SomeQueue"/>

    **  **<multicast>

    **    **<pipeline>

    **      **<bean ref="something"/>

    **      **<to uri="log:Something"/>

    **    **</pipeline>

    **    **<pipeline>

    **      **<bean ref="foo"/>

    **      **<bean ref="bar"/>

    **      **<to uri="activemq:OutputQueue"/>

    **    **</pipeline>

    **  **</multicast>

    </route>

    # 32. [**Poll Enrich EIP**](https://camel.apache.org/manual/latest/pollEnrich-eip.html)

    Camel带有pollEnrich风格作为DSL内容丰富的选择。另一个是enrich

    pollEnrich使用轮询消费者来获取其他数据。它通常用于事件消息消息传递，例如读取文件或下载FTP文件。


    |  | ***使用超时值的好习惯***===默认情况下，Camel将一直使用receive等待。在有可用消息到来之前可能会阻塞。因此，建议始终提供超时值，以明确我们可能会等待消息，直到达到超时。=== |
    | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

    如果没有数据，那么newExchange聚合策略就是null。

    您可以传入确定要使用的方法的超时值

    l 如果超时为-1或其他负数，则选择receive（**重要****:**receive如果没有消息，方法可能会阻塞）

    l 如果超时为0则选择receiveNoWait

    l 否则receive(timeout)被选中

    超时值以毫秒为单位。

    pollEnrich**不会**从当前Exchange访问任何数据，这意味着在轮询时它无法使用您在Exchange上设置的任何现有报文头。

    例如，您无法在Exchange.FILE_NAME报文头中设置文件名，并且pollEnrich仅用于使用该文件的情况。为此，您**必须**在端点URI中设置文件名。enrich和pollEnrich二者都支持使用一个表达式URI，它允许从当前的Exchange使用数据动态端点。换句话说，上面说的所有内容都不再适用，但它仍是默认约定。

    ## 32.1. **使用pollEnrich进行内容丰富**

    pollEnrich作品就像enrich然而，因为它使用轮询消费者，我们有3种方法轮询

    l receive

    l receiveNoWait

    l receive(timeout)

    ## 32.2. **pollEnrich选项**

    Poll Enrich EIP支持7种选项，如下所示:


    | **名称**                    | **描述**                                                                                                                                                                                                                                                                                                                                                                                | **默认** | **类型** |
    | --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
    | **timeout**                 | 从外部服务轮询时的超时时间。超时对Poll Enrich行为有影响。它基本上以三种不同的模式运行:负值 — 等待消息可用然后返回它。警告如果没有可用消息，此方法可能会无限期阻止。0 — 尝试立即接收消息交换而不等待，如果消息交换尚未可用，则返回null。正值 — 尝试接收消息交换，如果消息尚未可用，则等待给定的超时到期。如果超时则返回null默认值为-1，因此该方法可能无限期阻塞，因此建议使用超时值。 | -1       | Long     |
    | **strategyRef**             | 指用于将来自外部服务的回复合并到单个out消息中的AggregationStrategy。默认情况下，Camel将使用外部服务的回复作为out消息。                                                                                                                                                                                                                                                                  |          | String   |
    | **strategyMethodName**      | 当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。                                                                                                                                                                                                                                                                                                             |          | String   |
    | **strategyMethodAllowNull** | 如果此选项为false，则在没有要丰富的数据时不使用聚合方法。如果此选项为true，则在将POJO用作AggregationStrategy时，将使用null值作为oldExchange（当没有数据可以丰富时）。                                                                                                                                                                                                                   | FALSE    | Boolean  |
    | **aggregateOnException**    | 如果此选项为false，则在尝试检索要从资源中丰富的数据时抛出异常时，不使用聚合方法。将此选项设置为true允许最终用户控制在聚合方法中存在异常时要执行的操作。例如，抑制异常或设置自定义消息体等。                                                                                                                                                                                             | FALSE    | Boolean  |
    | **cacheSize**               | 设置org.apache.camel.spi.ConsumerCache使用的最大大小，用于在重用uris时缓存和复用消费者。                                                                                                                                                                                                                                                                                                |          | Integer  |
    | **ignoreInvalidEndpoint**   | 尝试使用该端点创建生产者时忽略invalidate端点异常                                                                                                                                                                                                                                                                                                                                        | FALSE    | Boolean  |

    ## 32.3. **pollEnrich示例**

    在此示例中，我们通过从名为inbox/data.txt的文件加载内容来丰富消息。

    from("direct:start")

    **  **.pollEnrich("file:inbox?fileName=data.txt")

    **  **.to("direct:result");

    在XML DSL中，您可以:

    <route>

    **  **<from uri="direct:start"/>

    **  **<pollEnrich>

    **    **<constant>file:inbox?fileName=data.txt</constant>

    **  **</pollEnrich>

    **  **<to uri="direct:result"/>

    </route>

    如果没有文件，则消息为空。我们可以使用超时来等待（可能永远）直到文件存在，或使用超时等待一段时间。

    例如，要等待最多5秒钟，您可以执行以下操作:

    <route>

    **  **<from uri="direct:start"/>

    **  **<pollEnrich timeout="5000">

    **    **<constant>file:inbox?fileName=data.txt</constant>

    **  **</pollEnrich>

    **  **<to uri="direct:result"/>

    </route>

    ## 32.4. **使用动态URIS**

    **自Camel 2.16起可用**

    enrich和pollEnrich两者都可使用动态URI支持基于Exchange的消息。例如，pollEnrich使用报文头指示SEDA队列名称的端点:

    from("direct:start")

    **  **.pollEnrich().simple("seda:${header.name}")

    **  **.to("direct:result");

    在XML DSL中

    <route>

    **  **<from uri="direct:start"/>

    **  **<pollEnrich>

    **    **<simple>seda:${header.name}</simple>

    **  **</pollEnrich>

    **  **<to uri="direct:result"/>

    </route>

    # 33. [**Process EIP**](https://camel.apache.org/manual/latest/process-eip.html)

    [Process](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/Processor.html)接口被用于实现消息交换的消费者或[消息翻译](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message-translator.adoc)

    ## 33.1. **选项**

    Process EIP支持以下列出的1个选项:


    | **名称** | **描述**                                     | **默认** | **类型** |
    | -------- | -------------------------------------------- | -------- | -------- |
    | **ref**  | **必需**引用Process 以在注册表中查找以使用。 |          | String   |

    ## 33.2. **示例**

    ### 33.2.1. **在路由中使用处理器**

    一旦你编写了一个实现像这样的Process 的类......

    public** **class MyProcessor implements Processor {

    **  **public void process(Exchange exchange) throws Exception {

    **    ***// do something...*

    **  **}

    }

    然后，您可以通过在Spring中声明bean来轻松地在路由中使用它，例如通过XML（或者在JNDI中注册它，如果这是您的[注册表](https://github.com/apache/camel/blob/master/docs/user-manual/en/registry.adoc)）

    <bean id="myProcessor" class="com.acme.MyProcessor"/>

    然后在Camel你可以做到

    from("activemq:myQueue").to("myProcessor");

    ### 33.2.2. **使用processor DSL**

    在您的路由中，您还可以使用process** **DSL语法来调用处理器Process 。

    Processor myProcessor = new** **MyProcessor();

    ...

    from("activemq:myQueue").process(myProcessor);

    如果您需要在[注册表中](https://github.com/apache/camel/blob/master/docs/user-manual/en/registry.adoc)查找处理器，那么您应该使用**processRef** DSL:

    from("activemq:myQueue").processRef("myProcessor");

    ## 33.3. **使用Process代替**

    该Process 可以在路由中用作匿名内部类，例如:

    **    **from("activemq:myQueue").process(new** **Processor() {

    **        **public void process(Exchange exchange) throws Exception {

    **            **String payload = exchange.getIn().getBody(String.class);

    **            ***// do something with the payload and/or exchange here*

    **           **exchange.getIn().setBody("Changed body");

    **       **}

    **    **}).to("activemq:myOtherQueue");

    这可用于快速实现一些代码。如果内部类中的代码变得有点复杂，那么当然建议将它重构为一个单独的类。

    ## 33.4. **将Processor变为完整的组件**

    有一个名为[ProcessorEndpoint](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/impl/ProcessorEndpoint.html)的基类，它支持Processor实例的完整[Endpoint](https://camel.apache.org/manual/latest/endpoint.html)语义。

    所以你只需要通过从[DefaultComponent](http://camel.apache.org/maven/current/camel-core/apidocs/org/apache/camel/impl/DefaultComponent.html)派生来创建一个[Component](https://github.com/apache/camel/tree/master/components)类，它返回ProcessorEndpoint的实例。有关详细信息，请参阅[编写组件](https://camel.apache.org/manual/latest/writing-components.html)

    # 34. [**Random EIP**](https://camel.apache.org/manual/latest/random-eip.html)

    Random EIP没有选项。

    # 35. [**Recipient List EIP**](https://camel.apache.org/manual/latest/recipientList-eip.html)

    ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps60.png)

    收件人将收到**同一个** Exchange 的副本，Camel将按顺序执行它们。

    ## 35.1. **选项**

    收件人列表EIP（Recipient List EIP）支持15个选项，如下所示:


    | **名称**                     | **描述**                                                                                                                                                                                                                                                                                                                                      | **默认** | **类型** |
    | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
    | **delimiter**                | 如果Expression返回多个端点，则使用分隔符。可以使用false值关闭。默认值是，                                                                                                                                                                                                                                                                     | ,        | String   |
    | **parallelProcessing**       | 如果启用，则同时向收件人发送消息。请注意，调用方线程仍将等待，直到所有消息都已完全处理完毕，然后再继续。它只发送和处理来自收件人的回复同时发生。                                                                                                                                                                                              | FALSE    | Boolean  |
    | **strategyRef**              | 设置对AggregationStrategy的引用，该AggregationStrategy用于将来自收件人的回复组合成来自RecipientList的单个传出消息。默认情况下，Camel将使用最后一个回复作为传出消息。您还可以使用POJO作为AggregationStrategy                                                                                                                                   |          | String   |
    | **strategyMethodName**       | 当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。                                                                                                                                                                                                                                                                   |          | String   |
    | **strategyMethodAllowNull**  | 如果此选项为false，则在没有要丰富的数据时不使用聚合方法。如果此选项为true，那么当使用POJO作为AggregationStrategy时，将使用null值作为oldExchange（当没有数据可以充实时）                                                                                                                                                                       | FALSE    | Boolean  |
    | **executorServiceRef**       | 指用于并行处理的自定义线程池。请注意，如果设置此选项，则会自动隐含并行处理，您也不必启用该选项。                                                                                                                                                                                                                                              |          | String   |
    | **stopOnException**          | 如果在处理org.apache.camel.Exchange期间发生异常或故障，将立即停止进一步处理，并且将引发引起的异常。如果处理交换失败（有错误消息）或错误处理程序抛出并处理异常（例如使用onException），也会停止。在所有情况下，收件人列表将停止进一步处理。这与路由引擎使用的管道中的行为相同。默认行为是不停止但继续处理直到结束                              | FALSE    | Boolean  |
    | **ignoreInvalidEndpoints**   | 尝试使用该端点创建生产者时忽略invalidate端点异常                                                                                                                                                                                                                                                                                              | FALSE    | Boolean  |
    | **streaming**                | 如果启用，则Camel将按顺序处理回复，例如按照它们返回的顺序。如果禁用，Camel将按照收件人列表定义的顺序处理回复。                                                                                                                                                                                                                                | FALSE    | Boolean  |
    | **timeout**                  | 使用并行处理时，设置以毫秒为单位指定的总超时。如果收件人列表无法在给定时间范围内发送和处理所有回复，则超时触发器和收件人列表会中断并继续。请注意，如果您提供TimeoutAwareAggregationStrategy，则会在分解之前调用timeout方法。如果在仍然保持运行任务的情况下达到超时，则Camel难以以正常方式关闭的某些任务可能会继续运行。因此请谨慎使用此选项。 | 0        | Long     |
    | **onPrepareRef**             | 准备要发送的org.apache.camel.Exchange时使用处理器。这可用于深度克隆应发送的消息，或者在发送交换之前所需的任何自定义逻辑。                                                                                                                                                                                                                     |          | String   |
    | **shareUnitOfWork**          | 与父级和每个子消息共享org.apache.camel.spi.UnitOfWork。默认情况下，收件人列表不会共享父Exchange和每个收件人Exchange之间的工作单元。这意味着每个子交换都有自己独立的工作单元。                                                                                                                                                                 | FALSE    | Boolean  |
    | **cacheSize**                | 设置org.apache.camel.spi.ProducerCache使用的最大大小，用于在使用此收件人列表时缓存和重用生成器，同时重用uris。                                                                                                                                                                                                                                |          | Integer  |
    | **parallelAggregate**        | 如果启用，则可以同时调用AggregationStrategy上的聚合方法。请注意，这需要将AggregationStrategy的实现实现为线程安全的。默认情况下，这是错误的，这意味着Camel会将调用同步到聚合方法。虽然在某些用例中，当AggregationStrategy实现为线程安全时，这可用于存档更高的性能。                                                                            | FALSE    | Boolean  |
    | **stopOnAggregateException** | 如果启用，请在使用parallelProcessing时将聚合时发生的异常展开到错误处理程序。目前，聚合时间异常不会在使用parallelProcessing时停止路由处理。启用此选项可以解决此问题。为了向后兼容，默认值为false。                                                                                                                                             | FALSE    | Boolean  |


    |  | 您可以在POJO上使用RecipientList Annotation来创建动态收件人列表。有关更多详细信息，请参阅Bean集成。 |
    | - | -------------------------------------------------------------------------------------------------- |

    ## 35.2. **静态收件人列表**

    以下示例显示如何从输入端点**queue:a**路由请求到静态目标列表

    from("jms:queue:a")

    **    **.recipientList("direct:b,direct:c,direct:d");

    在XML中:

    <camelContext xmlns="http://camel.apache.org/schema/spring">

    **    **<route>

    **        **<from uri="jms:queue:a"/>

    **        **<recipientList>

    **            **<constant>direct:b,direct:c,direct:d</constant>

    **        **</recipientList>

    </route>

    </camelContext>

    ## 35.3. **动态收件人列表**

    通常，使用"收件人列表"模式的主要原因之一是收件人列表是动态的，并在运行时计算。以下示例演示如何使用表达式创建动态收件人列表（在本例中，动态提取已命名的报文头值）以计算端点列表，这些端点可以是Endpoint类型，也可以转换为String，然后使用端点解析URI（以逗号分隔）。

    from("jms:queue:a")

    **    **.recipientList(header("foo"));

    ## 35.4. **Iteratable值**

    报文头中定义的动态收件人列表必须是可迭代的，例如:

    l java.util.Collection

    l java.util.Iterator

    l arrays

    l org.w3c.dom.NodeList

    l 单个字符串，其值以逗号分隔（已配置分隔符）

    l 任何其他类型将被视为单一值

    ## 35.5. **在Spring Xml中使用分隔符**

    在Spring DSL中，如果报文头值是具有多个分隔端点的单个String，则可以设置delimiter属性以设置要使用的分隔符。默认情况下，Camel使用逗号作为分隔符，但此选项允许您指定要使用的自定义分隔符。

    <route>

    **  **<from uri="direct:a"/>

    **  ***<!-- use semi-colon as a delimiter for String based values -->*

    **  **<recipientList delimiter=";">

    **    **<header>myHeader</header>

    **  **</recipientList>

    </route>

    因此，如果**myHeader**包含String带有的值，"activemq:queue:foo;activemq:topic:hello ; log:bar"则Camel将String使用XML中给出的分隔符拆分，从而生成3个要发送的端点。您可以在端点之间使用空格，因为Camel会在查找要发送到的端点时trim该值。

    在Java中:

    from("direct:a")

    **    **.recipientList(header("myHeader"), ";");

    ## 35.6. **并行发送给多个收件人**

    收件人列表现在支持parallelProcessing例如Splitter也支持。您可以使用它来使用线程池来同时执行将Exchange发送给多个收件人的任务。

    from("direct:a")

    **    **.recipientList(header("myHeader")).parallelProcessing();

    在XML中，它是收件人列表tag的属性。

    <route>

    **    **<from uri="direct:a"/>

    **    **<recipientList parallelProcessing="true">

    **        **<header>myHeader</header>

    </recipientList>

    </route>

    ### 35.6.1. **使用自定义线程池**

    线程池仅用于parallelProcessing。您可以通过ExecutorServiceStrategy（参见Camel的线程模型）提供您自己的自定义线程池，就像您为aggregationStrategy做的那样。默认情况下，Camel使用具有10个线程的线程池（在将来的版本中可能会更改）。

    ## 35.7. **如果一个收件人失败，停止继续**

    收件人列表现在支持stopOnException例如Splitter也支持。如果收件人失败，您可以使用它停止发送给任何其他收件人。

    from("direct:a")

    **    **.recipientList(header("myHeader")).stopOnException();

    在XML中，它是收件人列表tag（recipientList）的一个属性。

    <route>

    **    **<from uri="direct:a"/>

    **    **<recipientList stopOnException="true">

    **        **<header>myHeader</header>

    </recipientList>

    </route>


    |  | 您可以将parallelProcessing和stopOnException组合在一起，并使它们都为true。 |
    | - | ------------------------------------------------------------------------- |

    ## 35.8. **忽略无效的端点**

    收件人列表现在支持ignoreInvalidEndpoints（如路由滑动）。您可以使用它来跳过无效的端点。

    from("direct:a")

    **    **.recipientList(header("myHeader")).ignoreInvalidEndpoints();

    在XML中，它是收件人列表tag的属性。

    <route>

    **    **<from uri="direct:a"/>

    **    **<recipientList ignoreInvalidEndpoints="true">

    **        **<header>myHeader</header>

    </recipientList>

    </route>

    然后我们说myHeader包含以下两个端点direct:foo,xxx:bar。第一个端点有效。但是第二个是无效的，会被忽略。Camel在DEBUG级别记录它，因此您可以看到端点无效的原因。

    ## 35.9. **使用自定义AggregationStrategy**

    您现在可以使用自己AggregationStrategy的收件人列表。然而，这很少需要。有益的是，如果您使用请求回复消息，则可以聚合来自收件人的回复。默认情况下，Camel使用UseLatestAggregationStrategy保留最后收到的回复。如果您必须记住所有收件人发回的所有消息体，那么您可以使用自己的自定义聚合器来保存这些消息体。它与Aggregator EIP的原理相同，因此请查看详细信息。

    from("direct:a")

    **    **.recipientList(header("myHeader")).aggregationStrategy(new** **MyOwnAggregationStrategy())

    **    **.to("direct:b");

    而在XML中，它又是收件人列表tag的一个属性。

    <route>

    **    **<from uri="direct:a"/>

    **    **<recipientList strategyRef="myStrategy">

    **        **<header>myHeader</header>

    **    **</recipientList>

    <to uri="direct:b"/>

    </route>

    *<!-- bean with the custom aggregation strategy -->*

    <bean id="myStrategy" class="com.mycompany.MyOwnAggregationStrategy"/>


    |  | Multicast，Recipient List和Splitter EIP特别支持使用AggregationStrategy访问原始输入交换。您可能希望在聚合消息时使用此消息，并且其中一条消息出现故障，然后您希望在原始输入消息上进行丰富并作为响应返回; 它是具有3个交换参数的聚合方法。 |
    | - | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

    ## 35.10. **使用自定义AggregationStrategy时要清楚是哪个端点**

    使用自定义AggregationStrategy时，始终按接收顺序列表正在使用的端点按顺序调用aggregate方法（如果启用了并行处理）。但是，Exchange存储了一个使用端点的uri属性（键是Exchange.RECIPIENT_LIST_ENDPOINT）。因此，您知道要聚合的端点。代码块显示如何在聚合器中访问此属性。

    @Override

    public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

    **    **String uri = newExchange.getProperty(Exchange.RECIPIENT_LIST_ENDPOINT, String.class);

    }

    ## 35.11. **使用方法调用作为收件人列表**

    您可以使用Bean来提供收件人，例如:

    from("activemq:queue:test")

    **    **.recipientList().method(MessageRouter.class, "routeTo");

    然后是MessageRouter Bean:

    public** **class MessageRouter {

    **    **public String routeTo() {

    **        **String queueName = "activemq:queue:test2";

    **        **return** **queueName;

    **    **}

    }


    |  | 当你使用Bean那么就**不能**使用@RecipientList注解，因为这样会添加另一个收件人列表，所以你最终会得到两个。千万**不能像**下面这样: |
    | - | ------------------------------------------------------------------------------------------------------------------------------- |

    public** **class MessageRouter {

    **    ***// do not use recipientList in the Camel route calling a bean with the @RecipientList annotation!*

    **    **@RecipientList

    **    **public String routeTo() {

    **        **String queueName = "activemq:queue:test2";

    **        **return** **queueName;

    **    **}

    }

    如果只是路由的Bean想要充当收件人列表，则应该只使用上面的代码段（使用@RecipientList）。所以原来的路由可以改为:

    from("activemq:queue:test").bean(MessageRouter.class, "routeTo");

    然后，它将调用routeTo方法并检测它是否被@RecipientList注解，然后相应地采取行动，就好像它是收件人列表EIP一样。

    ## 35.12. **使用超时**

    如果您使用parallelProcessing，则可以以毫秒为单位配置总timeout值。然后，Camel将并行处理消息，直到达到超时。如果一个消息消费者很慢，这允许您继续处理。例如，您可以将超时值设置为20秒。


    |  | ***任务可能会继续运行***如果在仍然保持运行任务的情况下达到超时，则Camel难以以正常方式关闭的某些任务可能会继续运行。因此请谨慎使用此选项。我们可能会在将来的Camel版本中改进此功能。 |
    | - | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

    例如，在下面的单元测试中，您可以看到我们将消息多路广播到3个目的地。我们有个超时2秒，这意味着只能在时间范围内完成最后两条消息。这意味着我们只会聚合最后两个产生输出"BC"的结果聚合。

    from("direct:start")

    **    **.multicast(new** **AggregationStrategy() {

    **            **public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

    **                **if** **(oldExchange == null) {

    **                    **return** **newExchange;

    **                **}

    **                **String body = oldExchange.getIn().getBody(String.class);

    **                **oldExchange.getIn().setBody(body + newExchange.getIn().getBody(String.class));

    **                **return** **oldExchange;

    **            **}

    **        **})

    **        **.parallelProcessing().timeout(250).to("direct:a", "direct:b", "direct:c")

    **    ***// use end to indicate end of multicast route*

    **    **.end()

    **    **.to("mock:result");

    from("direct:a").delay(1000).to("mock:A").setBody(constant("A"));

    from("direct:b").to("mock:B").setBody(constant("B"));

    from("direct:c").to("mock:C").setBody(constant("C"));


    |  | ***其他EIP超时***=== Splitter以及multicast和recipientList也支持此超时功能。=== |
    | - | ------------------------------------------------------------------------------ |

    默认情况下，如果发生超时，则不会调用AggregationStrategy。但是，您可以实现timeout方法:这允许您在AggregationStrategy真正需要时处理超时。


    |  | ***超时总计***===超时是总计，这意味着在X时间之后，Camel将聚合在时间范围内完成的消息。剩余部分将被取消。Camel也只会在导致超时的第一个索引中调用TimeoutAwareAggregationStrategy一次timeout方法。=== |
    | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

    ## 35.13. **在准备消息时使用onPrepare执行自定义逻辑**

    请参阅Multicast EIP中的详细信息

    ## 35.14. **在收件人中使用ExchangePattern**

    默认情况下，收件人列表将使用当前的ExchangePatten。虽然人们可以想象一个用户希望使用不同的交换模式向收件人发送消息的情况。例如，您可能有一条路由作为InOnly路由发起，但希望将InOut交换模式与收件人列表一起使用。您可以直接在收件人端点中配置ExchangePatten。

    例如，在下面的路由中，我们选择新文件（将以其身份启动InOnly），然后路由到收件人列表。由于我们希望InOut与ActiveMQ（JMS）端点一起使用，我们现在可以使用exchangePattern=InOut选项指定它。然后，将继续路由来自JMS请求/回复的响应，因此响应将作为outbox目录中的文件存储。

    from("file:inbox")

    **    ***// the exchange pattern is InOnly initially when using a file route*

    **    **.recipientList().constant("activemq:queue:inbox?exchangePattern=InOut")

    .to("file:outbox");


    |  | 收件人列表不会改变原始交换模式。因此，在上面的示例中，消息路由到file:outbox端点 时，交换模式仍将是InOnly。如果要永久更改交换模式，请使用.setExchangePattern选项。请参阅Request Reply和事件消息EIP查看更多详细信息。 |
    | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

    # 36. [**Remove Header EIP**](https://camel.apache.org/manual/latest/removeHeader-eip.html)

    ## 36.1. **选项**

    Remove Header EIP支持下面列出的1个选项:


    | **名称**       | **描述**                   | **默认** | **类型** |
    | -------------- | -------------------------- | -------- | -------- |
    | **headerName** | **必需要**删除的报文头名称 |          | String   |

    ## 36.2. **示例**

    from("seda:b")

    **  **.removeHeader("myHeader")

    **  **.to("mock:result");

    ### 36.2.1. **Spring DSL**

    下面的示例演示了Spring DSL:

    <route>

    **  **<from uri="seda:b"/>

    **  **<removeHeader>

    **     **<constant>myHeader</constant>

    **  **<removeHeader/>

    **  **<to uri="mock:result"/>

    </route>

    # 37. [**Remove Headers EIP**](https://camel.apache.org/manual/latest/removeHeaders-eip.html)

    ## 37.1. **选项**

    Remove Headers EIP支持2个选项，如下所示:


    | **名称**           | **描述**                                                                                                                                                        | **默认** | **类型** |
    | ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
    | **pattern**        | **必需**的要删除的报文头的名称或pattern。模式按以下顺序匹配:1 =完全匹配2 =通配符（模式以a结尾，名称以pattern开头）3 =正则表达式（以上所有都是不区分大小写的）。 |          | String   |
    | **excludePattern** | 要删除的报文头的名称或模式。模式按以下顺序匹配:1 =完全匹配2 =通配符（模式以a结尾，名称以pattern开头）3 =正则表达式（以上所有都是不区分大小写的）。              |          | String   |

    ## 37.2. **示例**

    from("seda:b")

    **  **.removeHeaders(map)

    **  **.to("mock:result");

    # 38. [**Remove Properties EIP**](https://camel.apache.org/manual/latest/removeProperties-eip.html)

    Remove Properties EIP允许您从交换中删除属性。

    ## 38.1. **选项**

    删除属性EIP支持下面列出的2个选项:


    | **名称**           | **描述**                                                                                                                                                   | **默认** | **类型** |
    | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
    | **pattern**        | **必需**的要删除的属性的名称或模式。模式按以下顺序匹配:1 =完全匹配2 =通配符（模式以a结尾，名称以pattern开头）3 =正则表达式（以上所有都是不区分大小写的）。 |          | String   |
    | **excludePattern** | 要删除的属性的名称或模式。模式按以下顺序匹配:1 =完全匹配2 =通配符（模式以a结尾，名称以pattern开头）3 =正则表达式（以上所有都是不区分大小写的）。           |          | String   |

    ## 38.2. **例子**

    以下示例显示如何使用removeProperties EIP

    RouteBuilder builder = new** **RouteBuilder() {

    **    **public void configure() {

    **        **from("direct:a")

    **            **.removeProperties("myProperty", "myProperty1")

    **            **.to("direct:b");

    **    **}

    };

    和使用XML的相同示例:

    <camelContext xmlns="http://camel.apache.org/schema/spring">

    **    **<route>

    **        **<from uri="direct:a"/>

    **           **<removeProperties pattern="myProperty*"/>

    **        **<to uri="direct:b"/>

    </route>

    </camelContext>

    # 39. [**Remove Property EIP**](https://camel.apache.org/manual/latest/removeProperty-eip.html)

    RemoveProperty EIP允许您从交换中删除属性。

    ## 39.1. **选项**

    Remove Property EIP支持下面列出的1个选项:


    | **名称**         | **描述**                   | **默认** | **类型** |
    | ---------------- | -------------------------- | -------- | -------- |
    | **propertyName** | **必需要**删除的属性的名称 |          | String   |

    ## 39.2. **例子**

    以下示例显示如何使用Remove Property EIP

    RouteBuilder builder = new** **RouteBuilder() {

    **    **public void configure() {

    **        **from("direct:a")

    **            **.removeProperty("myProperty")

    **            **.to("direct:b");

    **    **}

    };

    使用XML的相同示例:

    <camelContext xmlns="http://camel.apache.org/schema/spring">

    **    **<route>

    **        **<from uri="direct:a"/>

    **           **<removeProperty propertyName="myProperty"/>

    **        **<to uri="direct:b"/>

    </route>

    </camelContext>

    # 40. [**Request Reply**](https://camel.apache.org/manual/latest/requestReply-eip.html)

    Camel支持来自EIP模式的[请求回复](http://www.enterpriseintegrationpatterns.com/RequestReply.html)，支持消息的Exchange模式，可以将其设置为**InOut**以指示请求/回复。然后，Camel Components使用底层传输或协议实现此模式。

    ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps61.png)

    例如，当[JMS](https://camel.apache.org/components/latest/jms-component.html)与InOut一起使用时，组件将默认执行这些操作

    l 默认情况下创建临时入站inbound队列

    l 在请求消息上设置JMSReplyTo目标

    l 在请求消息上设置JMSCorrelationID

    l 发送请求消息

    l 使用JMSCorrelationID消费响应并将入站消息与请求相关联（因为您可能正在执行许多并发请求/响应）。


    |  | **相关信息**请参阅相关的事件消息 |
    | - | -------------------------------- |

    ## 40.1. **明确指定InOut**

    当从[JMS](https://camel.apache.org/components/latest/jms-component.html)消费消息时，**JMSReplyTo**报文头的存在表示Request-Reply 。

    您可以通过在URI上设置交换模式，明确强制端点处于请求回复模式。例如

    jms:MyQueue?exchangePattern=InOut

    您可以在DSL规则或Spring配置中指定交换模式。

    # 41. [**Resequence EIP**](https://camel.apache.org/manual/latest/resequence-eip.html)

    [EIP模式](https://camel.apache.org/enterprise-integration-patterns.html)的[Resequencer](http://www.enterpriseintegrationpatterns.com/Resequencer.html) 可以让你基于比较器重新组织消息。在Camel中默认使用Expression来创建比较器; 这样你就可以通过消息报文头或消息体或消息等进行比较。

    ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps62.png)

    ## 41.1. **选项**

    Resequence EIP支持下面列出的1个选项:


    | **名称**              | **描述**                                                 | **默认** | **类型**          |
    | --------------------- | -------------------------------------------------------- | -------- | ----------------- |
    | **resequencerConfig** | 使用批处理或流配置重新排序器。默认情况下将使用批量配置。 |          | ResequencerConfig |

    Camel支持两种重新排序算法:

    l **Batch resequencing** **-** **批量重新排序**将消息收集到批处理中，对消息进行排序并将消息发送到其输出。

    l **Stream resequencing** **-** **流****式****重新排序**重新**排序**（连续）消息流，基于检测到消息之间的间隙。

    默认情况下，Resequencer不支持重复消息，并且只保留最后一条消息，以防消息到达时使用相同的消息表达式。但是，在批处理模式下，您可以启用它以允许重复。

    ## 41.2. **批量Resequence**

    以下示例显示如何使用批处理Resequence ，以便按**body****()**表达式的顺序对消息进行排序。即将消息收集到批处理中（通过每批最大数量的消息或使用超时），然后按顺序对它们进行排序，然后将其发送到其输出。

    from("direct:start")

    **    **.resequence().body()

    **    **.to("mock:result");

    这相当于

    from("direct:start")

    **    **.resequence(body()).batch()

    **    **.to("mock:result");

    批处理重定序器可以通过size()和timeout()方法进一步配置。

    from("direct:start")

    **    **.resequence(body()).batch().size(300).timeout(4000L)

    **    **.to("mock:result")

    这将批处理大小设置为300，批处理超时设置为4000毫秒（默认情况下，批处理大小为100，超时为1000毫秒）。或者，您可以提供配置对象。

    from("direct:start")

    **    **.resequence(body()).batch(new** **BatchResequencerConfig(300, 4000L))

    **    **.to("mock:result")

    因此，上面的示例将重新排序来自端点**direct:a的**消息按其消息体的顺序，到端点**mock****:****result**。

    通常你会使用报文头而不是消息体来订购消息; 或者也许是消息体的一部分。所以你可以用这个表达式替换

    resequencer(header("mySeqNo"))

    例如，使用报文头中的自定义序列号mySeqNo重新排序消息。您当然可以使用许多不同的表达式语言，例如XPath，XQuery，SQL或各种脚本语言。

    以XML为例

    <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

    **  **<route>

    **    **<from uri="direct:start" />

    **    **<resequence>

    **      **<simple>body</simple>

    **      **<to uri="mock:result" />

    **      ***<!--*

    * batch-config can be ommitted for default (batch) resequencer settings*
      *  -->*
      **      **<batch-config batchSize="300" batchTimeout="4000" />
      **    **</resequence>
      **  **</route>
      </camelContext>

      ## 41.3. **允许重复**

      在该batch模式下，现在可以允许重复。在Java DSL中有一种allowDuplicates()方法，在Spring XML的<batch-config/>中，您可以使用一个属性allowDuplicates=true来启用它。
      ## 41.4. **反转**

      在batch模式中，您现在可以反转表达式排序。默认情况下，订单基于0..9，A..Z，这将允许首先排序低数字的消息，因此也可以先输出。在某些情况下，您希望逆序，现在可以在Java DSL中有一种reverse()方法，在Spring XML中<batch-config/>，您可以使用一个属性reverse=true来启用它。
      ## 41.5. **根据JMSPriority重新排序JMS消息**

      现在，使用Resequencer根据JMSPriority重新排序来自JMS队列的消息要容易得多。对于工作，你需要使用两个新的选项allowDuplicates和reverse。
      from("jms:queue:foo")
      **    ***// sort by JMSPriority by allowing duplicates (message can have same JMSPriority)*
      **    ***// and use reverse ordering so 9 is first output (most important), and 0 is last*
      **    ***// use batch mode and fire every 3th second*
      **    **.resequence(header("JMSPriority")).batch().timeout(3000).allowDuplicates().reverse()
      **    **.to("mock:result");
      请注意，这**只能**在batch** **Resequencer 的模式下进行。
      ## 41.6. **忽略无效的交换**

      **自Camel 2.9起可用**
      如果传入的Exchange 对Resequencer 无效，则Resequencer  EIP会抛出一个 CamelExchangeException。即无法计算表达式，例如缺少报文头。您可以使用该选项ignoreInvalidExchanges忽略这些异常，这意味着Resequencer将跳过无效的Exchange。
      from("direct:start")
      **    **.resequence(header("seqno")).batch().timeout(1000)
      **        ***// ignore invalid exchanges (they are discarded)*
      **        **.ignoreInvalidExchanges()
      **    **.to("mock:result");
      此选项可用于批处理和流Resequencer 。
      ## 41.7. **拒绝旧Exchange**

      **自Camel 2.11起可用**
      此选项可用于防止发送乱序消息，而不管下游传递消息的事件（容量，超时等）。如果启用了rejectOld()则当传入的Exchange比上次传递的消息"更旧"（基于比较器）时，Resequencer将抛出一个MessageRejectedException。这提供了对延迟消息排序的额外控制级别。
      from("direct:start")
      **    **.onException(MessageRejectedException.class).handled(true).to("mock:error").end()
      **    **.resequence(header("seqno")).stream().timeout(1000).rejectOld()
      **    **.to("mock:result");
      此选项仅适用于流Resequencer 。
      ## 41.8. **流重新排序**

      下一个示例显示了如何使用流Resequencer 。消息根据seqnum报文头给出的序列号进行重新排序，使用间隙检测和各个消息级别的超时。
      from("direct:start").resequence(header("seqnum")).stream().to("mock:result");
      流Resequencer 可以通过capacity()和timeout()方法进一步配置。
      from("direct:start")
      **    **.resequence(header("seqnum")).stream().capacity(5000).timeout(4000L)
      **    **.to("mock:result")
      这将Resequencer 的容量设置为5000，超时设置为4000 ms（默认情况下，容量为1000，超时为1000 ms）。或者，您可以提供配置对象。
      from("direct:start")
      **    **.resequence(header("seqnum")).stream(new** **StreamResequencerConfig(5000, 4000L))
      **    **.to("mock:result")
      流Resequencer 算法基于检测消息流中的间隙而不是固定批量大小。间隙检测结合超时消除了必须预先知道序列的消息数量（即批量大小）的约束。消息必须包含已知前驱和后继的唯一序列号。例如，序列号为3的消息具有序列号为2的前驱消息和序列号为4的后继消息。消息序列2,3,5具有间隙，因为缺少3的后继。因此，重定序器必须保留消息5，直到消息4到达（或发生超时）。
      如果已知消息流中消息之间的最大时间差（具有相对于序列号的后继/先前关系），则应将重定序器的超时参数设置为该值。在这种情况下，保证流的所有消息以正确的顺序传送到下一个处理器。超时值与无序时间差相比越低，该重定序器传递的无序消息的概率越高。足够高的容量值应支持大超时值。capacity参数用于防止重定序器耗尽内存。
      默认情况下，流Resequencer 需要长序列号，但也可以通过提供自定义表达式来支持其他类型序列号。
      public** **class MyFileNameExpression implements Expression {
      **    **public String getFileName(Exchange exchange) {
      **        **return** **exchange.getIn().getBody(String.class);
      **    **}
      **    **public Object evaluate(Exchange exchange) {
      **        ***// parser the file name with YYYYMMDD-DNNN pattern*
      **        **String fileName = getFileName(exchange);
      **        **String[] files = fileName.split("-D");
      **        **Long answer = Long.parseLong(files[0]) * 1000** **+ Long.parseLong(files[1]);
      **        **return** **answer;
      **    **}
      **    **public** **<T> T evaluate(Exchange exchange, Class<T> type) {
      **        **Object result = evaluate(exchange);
      **        **return** **exchange.getContext().getTypeConverter().convertTo(type, result);
      **    **}
      }
      from("direct:start")
      **    **.resequence(new** **MyFileNameExpression()).stream().timeout(100).to("mock:result");
      或通过comparator()方法自定义比较器
      ExpressionResultComparator<Exchange> comparator = new** **MyComparator();
      from("direct:start")
      **    **.resequence(header("seqnum")).stream().comparator(comparator)
      **    **.to("mock:result");
      或通过一个StreamResequencerConfig对象。
      ExpressionResultComparator<Exchange> comparator = new** **MyComparator();
      StreamResequencerConfig config = new** **StreamResequencerConfig(100, 1000L, comparator);
      from("direct:start")
      **    **.resequence(header("seqnum")).stream(config)
      **    **.to("mock:result");
      以XML为例
      <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">

      **  **<route>
      **    **<from uri="direct:start"/>
      **    **<resequence>
      **      **<simple>in.header.seqnum</simple>
      **      **<to uri="mock:result" />
      **      **<stream-config capacity="5000" timeout="4000"/>
      **    **</resequence>
      **  **</route>
      </camelContext>

      # 42. [**Rollback EIP**](https://camel.apache.org/manual/latest/rollback-eip.html)

      Camel EIP模式建议使用spring transaction支持[Transactional Client](http://www.enterpriseintegrationpatterns.com/TransactionalClient.html)。
      ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps63.png)
      像[JMS](https://camel.apache.org/components/latest/jms-component.html)这样的面向事务的端点支持将事务用于入站和出站消息交换。支持事务的端点将参与调用它们的当前事务上下文。
      **重新交付的配置**
      事务模式下的重新交付**不是**由Camel处理，而是由后备系统（事务管理器）处理。在这种情况下，您应该诉诸支持系统如何配置重新交付。
      您应该使用[SpringRouteBuilder](http://camel.apache.org/maven/current/camel-spring/apidocs/org/apache/camel/spring/SpringRouteBuilder.html)来设置路由，因为您将需要使用定义事务管理器配置和策略的TransactionTemplates来设置spring上下文。
      对于要处理的入站端点，通常需要将它们配置为使用Spring PlatformTransactionManager。对于JMS组件，可以通过在spring上下文中查找它来完成。
      您首先在spring配置中定义所需的对象。
      <bean id="jmsTransactionManager" class="org.springframework.jms.connection.JmsTransactionManager">

      **  **<property name="connectionFactory" ref="jmsConnectionFactory" />
      </bean>

      <bean id="jmsConnectionFactory" class="org.apache.activemq.ActiveMQConnectionFactory">

      **  **<property name="brokerURL" value="tcp://localhost:61616"/>
      </bean>

      然后，您可以查找它们并使用它们创建JmsComponent。
      PlatformTransactionManager transactionManager = (PlatformTransactionManager) spring.getBean("jmsTransactionManager");
      ConnectionFactory connectionFactory = (ConnectionFactory) spring.getBean("jmsConnectionFactory");
      JmsComponent component = JmsComponent.jmsComponentTransacted(connectionFactory, transactionManager);
      component.getConfiguration().setConcurrentConsumers(1);
      ctx.addComponent("activemq", component);
      ## 42.1. **选项**

      Rollback EIP支持以下列出的3个选项：
      | **名称**                 | **描述**                                                           | **默认** | **类型** |
      | ------------------------ | ------------------------------------------------------------------ | -------- | -------- |
      | **markRollbackOnly**     | 将事务标记为仅回滚（不能推翻来提交）                               | false    | Boolean  |
      | **markRollbackOnlyLast** | 仅将最后一个子事务标记为仅回滚。使用子事务时（如果交换管理器支持） | false    | Boolean  |
      | **message**              | 回滚异常中消费的消息                                               |          | String   |

      ### 42.1.1. **事务策略**

      出站端点将自动加入当前事务上下文。但是，如果您不希望出站端点与入站端点参与同一笔事务，该怎么办？解决方案是将事务策略添加到process route。首先，您必须定义将要使用的事务策略。这些策略在后台使用了一个Spring TransactionTemplate来声明要使用的事务划分。因此，您需要在spring xml中添加如下内容：
      <bean id="PROPAGATION_REQUIRED" class="org.apache.camel.spring.spi.SpringTransactionPolicy">

      **  **<property name="transactionManager" ref="jmsTransactionManager"/>
      </bean>

      <bean id="PROPAGATION_REQUIRES_NEW" class="org.apache.camel.spring.spi.SpringTransactionPolicy">

      **  **<property name="transactionManager" ref="jmsTransactionManager"/>
      **  **<property name="propagationBehaviorName" value="PROPAGATION_REQUIRES_NEW"/>
      </bean>

      然后在[SpringRouteBuilder中](http://camel.apache.org/maven/current/camel-spring/apidocs/org/apache/camel/spring/SpringRouteBuilder.html)，您只需要为每个模板创建新的SpringTransactionPolicy对象。
      public void configure() {
      **    **...
      **    **Policy required = bean(SpringTransactionPolicy.class, "PROPAGATION_REQUIRED"));
      **    **Policy requirenew = bean(SpringTransactionPolicy.class, "PROPAGATION_REQUIRES_NEW"));
      **    **...
      }
      创建后，您可以在process route中使用策略对象：
      ** ***// Send to bar in a new transaction*
      from("activemq:queue:foo").policy(requirenew).to("activemq:queue:bar");
      *// Send to bar without a transaction.*
      from("activemq:queue:foo").policy(notsupported).to("activemq:queue:bar");
      ### 42.1.2. **OSGI蓝图**

      如果使用的是[OSGi Blueprint，](https://camel.apache.org/manual/latest/using-osgi-blueprint-with-camel.html)则很可能必须明确声明一个策略，并从路由中的事务中引用该策略。
      <bean id="required" class="org.apache.camel.spring.spi.SpringTransactionPolicy">

      **  **<property name="transactionManager" ref="jmsTransactionManager"/>
      **  **<property name="propagationBehaviorName" value="PROPAGATION_REQUIRED"/>
      </bean>

      然后从路由中引用“required”：
      <route>

      **  **<from uri="activemq:queue:foo"/>
      **  **<transacted ref="required"/>
      **  **<to uri="activemq:queue:bar"/>
      </route>

      ## 42.2. **数据库示例**

      在此示例中，我们要确保两个端点处于事务控制之下。这两个端点将数据插入数据库。该示例已作为一个[单元测试完成](https://github.com/apache/camel/blob/master/components/camel-spring/src/test/java/org/apache/camel/spring/interceptor/TransactionalClientDataSourceMinimalConfigurationTest.java)。
      首先，我们在其配置文件中设置常规的spring东西。在这里，我们为HSQLDB定义了一个数据源，最重要的是为Spring数据源定义了TransactionManager确保我们的事务策略繁重的工作。当然，您可以自由使用任何基于Spring的TransactionManager。如果您使用的是J2EE容器，则可以使用JTA或WebLogic或WebSphere特定的管理器。
      当我们使用新的约定优于配置时我们**并不**需要配置事务策略Bean，所以我们没有任何PROPAGATION_REQUIRED Bean。例如，所有需要配置的bean都是**标准的** Spring bean。根本没有Camel特定的配置。https://github.com/apache/camel/blob/master/components/camel-spring/src/test/resources/org/apache/camel/spring/interceptor/springTransactionalClientDataSourceMinimalConfiguration.xml [springTransactionalClientDataSourceMinimalConfiguration]然后，我们准备定义Camel路由了。我们有两条路由：1条成功条件，1条强制回滚条件。
      毕竟这是基于单元测试的。请注意，我们使用已**transacted**将每条路由标记为**transacted**标签。https：//github.com/apache/camel/blob/master/components/camel-spring/src/test/resources/org/apache/camel/spring/interceptor/springTransactionalClientDataSourceMinimalConfiguration.xml [springTransactionalClientDataSourceMinimalConfiguration]需要配置Camel路线进行事务。只要记住要使用**事务****的** DSL。其余的是用于设置事务管理器的标准Spring XML。
      ## 42.3. **JMS示例**

      在此示例中，我们希望侦听队列中的消息，并使用我们的业务逻辑Java代码处理消息并将其发送。由于其基于[TransactionMinimalConfigurationTest.java，](https://github.com/apache/camel/blob/master/components/camel-jms/src/test/java/org/apache/camel/component/jms/tx/TransactionMinimalConfigurationTest.java)因此目标是模拟端点。
      首先，我们配置标准的Spring XML以声明一个JMS连接工厂，一个JMS事务管理器以及我们在路由中使用的ActiveMQ组件.https：//github.com/apache/camel/blob/master/components/camel-jms /src/test/resources/org/apache/camel/component/jms/tx/TransactionMinimalConfigurationTest.xml[TransactionMinimalConfigurationTest.xml]，然后配置路由。请注意，我们要做的就是使用**事务**标记**transacted**将路由标记为已事务**transacted**。https://github.com/apache/camel/blob/master/components/camel-jms/src/test/resources/org/apache/camel/component/jms/tx/TransactionMinimalConfigurationTest.xml[TransactionMinimalConfigurationTest.xml]
      **事务****错误处理程序**
      当使用**transacted**Camel将路由标记为**transacted**时，Camel将自动使用[TransactionErrorHandler](https://camel.apache.org/manual/latest/transactionerrorhandler.html)作为[Error Handler](https://camel.apache.org/manual/latest/error-handler.html)。它支持与[DefaultErrorHandler](https://camel.apache.org/manual/latest/defaulterrorhandler.html)基本上相同的功能集，因此您也可以使用[Exception子句](https://camel.apache.org/manual/latest/exception-clause.html)。
      ## 42.4. **与Spring的集成测试**

      这里的集成测试是指注解了测试运行器类 @RunWith(SpringJUnit4ClassRunner.class).
      在遵循Spring Transactions文档时，很容易用@Transactional注解您的集成测试，然后在启动要测试的路由并发送消息之前为数据库添加种子。这是不正确的，因为Spring将有正在进行的事务，而Camel将等待在继续之前对此进行处理，导致路由超时。
      取而代之的是，从测试方法中删除注解@Transactional，并将测试数据植入TransactionTemplate执行中，这将确保在Camel尝试提取并使用事务管理器之前将数据提交到数据库。一个简单的例子[可以在GitHub上找到](https://github.com/rajivj2/example2/blob/master/src/test/java/com/example/NotificationRouterIT.java)。
      Spring的事务模型确保每个事务都绑定到一个线程。Camel路由可能会调用其他可能发生阻塞的线程。这不是Camel的错，但作为程序员，您必须意识到在测试线程中开始事务并期望由Camel路由创建的单独线程参与的后果，但事实并非如此。您可以在测试中模拟导致单独线程的部分，以避免出现此问题。
      ## 42.5. **使用具有不同传播行为的多条路由**

      假设您要通过两条路由来路由一条消息，并且第二条路由应通过它在自己的事务中运行。你是怎样做的？为此，可以使用传播行为进行配置，如下所示：
      l 第一条路由使用 PROPAGATION_REQUIRED
      l 第二条路由使用 PROPAGATION_REQUIRES_NEW
      这是在Spring XML文件中配置的。https://github.com/apache/camel/blob/master/components/camel-spring/src/test/resources/org/apache/camel/spring/interceptor/MixedTransactionPropagationTest.xml [MixedTransactionPropagationTest.xml]然后在使用事务处理的DSL的路由中指示它使用的是这两种传播中的哪一种。https：//github.com/apache/camel/blob/master/components/camel-spring/src/test/java /org/apache/camel/spring/interceptor/MixedTransactionPropagationTest.java[MixedTransactionPropagationTest.java]请注意，我们在第二条路由中如何配置onException，以指示在出现任何异常的情况下我们应该处理它并回滚此事务。这是通过使用markRollbackOnlyLast来完成的，它告诉Camel仅针对当前事务而不是针对全局事务。
      # 43. [**Round Robin EIP**](https://camel.apache.org/manual/latest/roundRobin-eip.html)

      循环负载均衡器。使用此负载平衡策略，为每个交换选择随机端点。
      ## 43.1. **选项**

      Round Robin EIP没有选择。
      ## 43.2. **例子**

      在这种情况下，我们使用header测试作为相关表达式:
      from("direct:start")
      **    **.loadBalance()
      **    **.roundRobin()
      **    **.to("seda:x", "seda:y", "seda:z");
      在XML中，您将拥有这样的路由
      <from uri="direct:start"/>

      **    **<loadBalance>
      **       **<roundRobin/>
      **       **<to uri="seda:x"/>
      **       **<to uri="seda:y"/>
      **       **<to uri="seda:z"/>
      **    **</loadBalance>
      # 44. [**Routing Slip EIP**](https://camel.apache.org/manual/latest/routingSlip-eip.html)

      ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps64.png)
      ## 44.1. **选项**

      Routing Slip EIP支持3个选项，如下所示:
      | **名称**                   | **描述**                                                                                                           | **默认** | **类型** |
      | -------------------------- | ------------------------------------------------------------------------------------------------------------------ | -------- | -------- |
      | **uriDelimiter**           | 设置uri要使用的分隔符                                                                                              | ，       | String   |
      | **ignoreInvalidEndpoints** | 尝试使用该端点创建生产者时忽略invalidate端点异常                                                                   | false    | Boolean  |
      | **cacheSize**              | 设置org.apache.camel.spi.ProducerCache使用的最大大小，当重用uris时，该大小用于在使用此路由选择时缓存和重用生产者。 |          | Integer  |

      ## 44.2. **例**

      以下路由将消息发送到Apache ActiveMQ的队列SomeQueue，并将它们传递到Routing Slip模式。
      from("activemq:SomeQueue")
      **  **.routingSlip("aRoutingSlipHeader");
      将检查消息是否存在aRoutingSlipHeader报文头。此报文头的值应该是您希望将消息路由到的端点URI的逗号分隔列表。消息将以流水线方式路由，即一个接一个地路由。Routing Slip在Exchange上设置一个Exchange.SLIP_ENDPOINT属性，该属性包含当前端点，如此一边滑动一边前进。这可以让您知道我们在Slip中处理到了什么位置。
      路由滑动Routing Slip将**预先**计算滑动，这意味着滑动仅计算一次。如果您需要即时计算Slip，请使用动态路由器模式。
      ## 44.3. **配置选项**

      在这里，我们将报文头名称和URI分隔符设置为不同的名称。
      ＃===使用Fluent Builders
      from("direct:c").routingSlip(header("aRoutingSlipHeader"), "#");
      ＃===使用Spring XML Extensions
      <camelContext id="buildRoutingSlip" xmlns="http://activemq.apache.org/camel/schema/spring">

      **  **<route>
      **    **<from uri="direct:c"/>
      **    **<routingSlip uriDelimiter="#">
      **       **<header>aRoutingSlipHeader</header>
      **    **</routingSlip>
      **  **</route>
      </camelContext>

      ## 44.4. **忽略无效的端点**

      **自Camel 2.3起可用**
      路由滑动支持收件人列表也支持的ignoreInvalidEndpoints。您可以使用它来跳过无效的端点。
      from("direct:a")
      **  **.routingSlip("myHeader")
      **  **.ignoreInvalidEndpoints();
      在Spring XML中，它是收件人列表tag的一个属性:
      <route>

      **  **<from uri="direct:a"/>
      **  **<routingSlip ignoreInvalidEndpoints="true"/>
      **    **<header>myHeader</header>
      **  **</routingSlip>
      </route>

      然后我们说myHeader直接包含以下两个端点:foo，xxx:bar。第一个端点有效。但是，第二个端点无效，只会被忽略。Camel记录在INFO级别，因此您可以看到端点无效的原因。
      ## 44.5. **表达支持**

      **自Camel 2.4起可用**
      路由滑动支持采用表达式参数作为收件人列表。您可以告诉Camel您要用于获取路由slip的表达式。
      from("direct:a")
      **  **.routingSlip(header("myHeader"))
      **  **.ignoreInvalidEndpoints();
      在Spring XML中，它是收件人列表标记的一个属性。
      <route>

      **  **<from uri="direct:a"/>
      **  ***<!--NOTE from Camel 2.4.0, you need to specify the expression element inside of the routingSlip element -->*
      **  **<routingSlip ignoreInvalidEndpoints="true">
      **    **<header>myHeader</header>
      **  **</routingSlip>
      </route>

      ## 44.6. **更多例子**

      有关此模式的更多示例，您可以查看路由滑动测试用例。
      ## 44.7. **使用此模式**

      如果您想使用此EIP模式，请阅读"入门"，您可能还会发现该体系结构特别适用于端点和URI的描述。然后，在尝试使用此模式之前，您可以先尝试一些示例。
      # 45. [**Saga EIP**](https://camel.apache.org/manual/latest/saga-eip.html)

      **自Camel 2.21起可用**
      Saga EIP提供了一种在Camel路由中定义一系列相关动作的方法，这些动作应该成功完成（**所有这些**）或不执行/补偿。Sagas实现能够协调**使用任何传输**进行**通信以**实现全局**一致结果的分布式服务**。
      虽然它们的主要目的是相似的，但Saga与传统的ACID分布式（XA）事务不同，因为多个参与服务的状态只保证在Saga结束时保持一致，而不是在中间步骤（缺乏隔离）。
      相反，Saga适用于不使用分布式事务的许多用例。例如，参与Saga的服务使用任何类型的数据存储:经典数据库甚至NoSQL非事务数据存储。Sagas也适用于无状态云服务，因为它们不需要将事务日志与服务一起存储。
      与事务不同，Saga也不需要在很短的时间内完成，因为它们不使用数据库级锁。它们可以存活更长的时间:从几秒到几天。基于Microprofile沙箱规范的Saga EIP实现（参见camel-lra，实际上称为LRA，代表"Long Running Action"）。它还支持协调外部**异构服务**，使用任何语言/技术编写，也可以在JVM外部运行。
      Saga不使用数据锁定，而是定义"补偿操作"的概念，这是在标准流遇到错误时应执行的操作，目的是恢复流执行之前存在的状态。补偿操作可以使用Java或XML DSL在Camel路由中声明，并且仅在需要时由Camel调用（如果由于错误而取消Saga）。
      Saga EIP支持6种选项，如下所示:
      | **名称**                  | **描述**                                                                                                                                                                                         | **默认** | **类型**                |
      | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | ----------------------- |
      | **propagation**           | 设置Saga传播模式（REQUIRED，REQUIRES_NEW，MANDATORY，SUPPORTS，NOT_SUPPORTED，NEVER）。                                                                                                          | REQUIRED | SagaPropagation         |
      | **completionMode**        | 确定saga应该如何被认为是完整的。设置为AUTO时，如果成功处理启动saga的交换，或者在异常完成时进行补偿，则完成saga。当设置为MANUAL时，用户必须使用saga完成或补偿saga:complete或saga:compensate端点。 | AUTO     | SagaCompletionMode      |
      | **timeoutInMilliseconds** | 设置Saga的最长时间。超时到期后，saga将自动得到补偿（除非在此期间做出了不同的决定）。                                                                                                             |          | Long                    |
      | **compensation**          | 必须调用补偿端点URI以补偿路由中完成的所有更改。与补偿URI对应的路径必须执行补偿并完成且没有错误。如果在补偿期间发生错误，则saga服务可以再次调用补偿URI以重试。                                    |          | SagaActionUriDefinition |
      | **completion**            | Saga成功完成时将调用的完成端点URI。与完成URI对应的路由必须执行完成任务并终止且没有错误。如果在完成期间发生错误，则saga服务可以再次调用完成URI以重试。                                            |          | SagaActionUriDefinition |
      | **option**                | 允许保存当前交换的属性，以便在补偿/完成回调路由中重用它们。该选项通常是有用的，例如存储和检索应在补偿操作中删除的对象的标识符。选项值将转换为补偿/完成交换的输入报文头。                         |          | List                    |

      ## 45.1. **交换属性**

      在参与Saga的每个Exchange上设置以下属性（正常操作，补偿操作和完成）:
      | **属性**            | **类型** | **描述**                                                             |
      | ------------------- | -------- | -------------------------------------------------------------------- |
      | Long-Running-Action | String   | Saga的全局唯一标识符，可使用传输级报文头（例如HTTP）传播到远程系统。 |

      ## 45.2. **Saga服务配置**

      Saga EIP要求将实现org.apache.camel.saga.CamelSagaService接口的服务添加到Camel上下文中。
      Camel目前支持以下Saga服务:
      l **InMemorySagaService**:它是Saga EIP 的**基本**实现，不支持高级功能（没有远程上下文传播，在应用程序失败时没有一致性保证）。
      l **LRASagaService**:它是基于Microprofile沙箱LRA规范的Saga EIP 的**完全**实现，支持远程上下文传播，并在应用程序失败时提供一致性保证。
      ### 45.2.1. **使用IN-MEMORY SAGA服务**

      in-memory Saga服务不建议用于生产环境，因为它不支持Saga状态的持久性（它仅保留在内存中），因此在应用程序失败（例如JVM崩溃）的情况下，它无法保证Saga的一致性。
      此外，当使用in-memory Saga服务时，无法使用传输级报文头将Saga上下文传播到远程服务（可以使用其他实现来完成）。
      想要使用in-memory Saga服务的用户应添加以下代码来自定义Camel上下文。
      context.addService(new** **org.apache.camel.impl.saga.InMemorySagaService());
      该服务属于camel-core模块。
      ### 45.2.2. **使用LRA Saga服务**

      LRA Saga Service是基于Microprofile沙箱LRA规范的实现。它利用**外部Saga协调****器**来控制**Saga**各步骤的执行。提议的LRA规范的参考实施是[Narayana LRA协调器](http://jbossts.blogspot.it/2017/12/narayana-lra-implementation-of-saga.html)。用户可以按照Narayana网站上的说明**启动协调器的远程实例**。
      LRA协调器的URL是Camel LRA服务的必需参数。Camel应用程序和LRA服务使用HTTP协议进行通信。
      为了使用LRA Saga服务，maven用户需要在他们的pom.xml中添加以下依赖项
      <dependency>

      ** **<groupId>org.apache.camel</groupId>
      ** **<artifactId>camel-lra</artifactId>
      ** ***<!-- use the same version as your Camel core version -->*
      ** **<version>x.y.z</version>
      </dependency>

      还需要Camel REST上下文才能使LRA实现起作用。你可以添加camel-undertow例如。
      <dependency>

      ** **<groupId>org.apache.camel</groupId>
      ** **<artifactId>camel-undertow</artifactId>
      ** ***<!-- use the same version as your Camel core version -->*
      ** **<version>x.y.z</version>
      </dependency>

      |  | Saga EIP的LRA实现将在"/lra-participant"路径下添加一些Web端点。LRA协调器将使用这些端点来回调应用程序。 |
      | - | ----------------------------------------------------------------------------------------------------- |

      *// Configure the LRA saga service*
      org.apache.camel.service.lra.LRASagaService sagaService = new** **org.apache.camel.service.lra.LRASagaService();
      sagaService.setCoordinatorUrl("http://lra-service-host");
      sagaService.setLocalParticipantUrl("http://my-host-as-seen-by-lra-service:8080/context-path");*// Add it to the Camel context*
      context.addService(sagaService);
      #### 45.2.2.1. **在Spring Boot中使用LRA Saga服务**

      Spring Boot用户可以使用LRA Saga Service的简化配置模型。Maven用户可以在他们的项目中包含**camel-lra-starter**模块:
      <dependency>

      ** **<groupId>org.apache.camel</groupId>
      ** **<artifactId>camel-lra-starter</artifactId>*<!-- use the same version as your Camel core version -->*
      ** **<version>x.y.z</version>
      </dependency>

      <dependency>

      ** **<groupId>org.apache.camel</groupId>
      ** **<artifactId>camel-undertow-starter</artifactId>*<!-- use the same version as your Camel core version -->*
      ** **<version>x.y.z</version>
      </dependency>

      配置可以在Spring Boot application.yaml文件中完成:
      ***application.yaml***
      camel:
      service:
      lra:
        enabled:** **true

        coordinator-url:** **[http://lra-service-host](http://lra-service-host)

        local-participant-url:** **[http://my-host-as-seen-by-lra-service:8080/context-path](http://my-host-as-seen-by-lra-service:8080/context-path)
      完成后，Saga EIP可以直接在Camel路由内使用，它将使用LRA Saga服务引擎。

      ## 45.3. **例子**

      假设您要下新订单，并且系统中有两个不同的服务:一个管理订单，另一个管理信用。从逻辑上讲，如果您有足够的信用，您可以下订单。

      使用Saga EIP，您可以模拟*direct:buy*路由作为由两个不同的行动组成的Saga，一个用于创建订单，另一个用于信用。**必须执行这两个操作，或者不执行任何操作**:没有信用的订单可以被视为不一致的结果（以及没有订单的付款）。

      from("direct:buy")

      **  **.saga()

      **    **.to("direct:newOrder")

      **    **.to("direct:reserveCredit");

      **就是这样**。其余示例的购买行为不会改变。我们将在下面看到可用于建模"新订单"和"预留信用"操作的不同选项。


      |  | 我们使用*direct*端点来模拟这两个动作，因为这个例子可以用于Saga服务的两个实现，但我们可以使用**http**或其他类型的端点与LRA Saga服务。 |
      | - | ------------------------------------------------------------------------------------------------------------------------------------ |

      *direct:buy*路由调用的两种服务都可以**参与****saga**并宣布他们的补偿行动。

      from("direct:newOrder")

      **  **.saga()

      **  **.propagation(SagaPropagation.MANDATORY)

      **  **.compensation("direct:cancelOrder")

      **    **.transform().header(Exchange.SAGA_LONG_RUNNING_ACTION)

      **    **.bean(orderManagerService, "newOrder")

      **    **.log("Order ${body} created");

      这里传播模式设置为MANDATORY，意味着在此路由中流动的任何交换必须已经是saga的一部分（在本例中就是这种情况，因为saga是在*direct:buy*路由中创建的）。

      *direct:newOrder*路由宣告补偿的行动，被称为*direct**:**cancelOrder*，负责saga被取消的情况下的顺序。

      每个交换始终包含一个Exchange.SAGA_LONG_RUNNING_ACTION报文头，此处用订单的ID。这样做是为了在相应的补偿操作中识别要删除的顺序，但这不是必需的（选项可以用作替代解决方案）。

      *direct:newOrder*的补偿动作是direct:cancelOrder，如下所示:

      from("direct:cancelOrder")

      **  **.transform().header(Exchange.SAGA_LONG_RUNNING_ACTION)

      **  **.bean(orderManagerService, "cancelOrder")

      **  **.log("Order ${body} cancelled");

      当订单被取消时，Saga EIP实现会自动调用它。

      它不应该以错误终止。如果在direct:cancelOrder路由中引发错误，则EIP实现应定期重试以执行补偿操作直到某个限制。这意味着**任何补偿操作必须是幂等的**，因此它应该考虑到它可能被触发多次并且在任何情况下都不应该失败。

      如果在所有重试后都无法进行补偿，则应通过Saga实现触发手动干预过程。


      |  | 可能会发生由于执行*direct**:**newOrder*路由的延迟，Saga在此期间被另一方取消（由于并行路由中的错误或Saga级别的超时）。因此，当补偿操作*direct**:**cancelOrder*被调用时，它可能找不到应该被取消的Order记录。重要的是，为了保证完全的全局一致性，**任何主要行动及其相应的补偿行动都是可交换的**，即如果在主要行动之前发生补偿则具有相同的效果。当使用交换行为时，另一种可能的方法是不可能的，就是在补偿操作中始终失败，直到找到主要操作产生的数据（或者最大重试次数耗尽）:这种方法可能在许多情况下都有效，但是这是**启发式的**。 |
      | - | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

      信用服务几乎可以与订单服务相同的方式实现。

      *// action*

      from("direct:reserveCredit")

      **  **.saga()

      **  **.propagation(SagaPropagation.MANDATORY)

      **  **.compensation("direct:refundCredit")

      **    **.transform().header(Exchange.SAGA_LONG_RUNNING_ACTION)

      **    **.bean(creditService, "reserveCredit")

      **    **.log("Credit ${header.amount} reserved in action ${body}");*// compensation*

      from("direct:refundCredit")

      **  **.transform().header(Exchange.SAGA_LONG_RUNNING_ACTION)

      **  **.bean(creditService, "refundCredit")

      **  **.log("Credit for action ${body} refunded");

      在这里，信用预订的补偿措施是退款。

      完成了这个例子。它可以与Saga EIP的两种实现一起运行，因为它不涉及远程端点。

      接下来将显示其他选项。

      ### 45.3.1. **处理完成事件**

      当Saga完成时，经常需要进行一些处理。当发生错误并取消Saga时，将调用补偿端点。等效地，当Saga成功完成时，可以调用**完成端点**以进行进一步处理。

      例如，在上面的订单服务中，我们可能需要知道订单何时完成（以及信用保留）以实际开始准备订单。如果未完成付款，我们将不会开始准备订单（与大多数现代CPU不同，它们允许您在确保您有权阅读之前访问保留的内存）。

      使用direct:newOrder端点的修改版本可以轻松完成此操作:

      from("direct:newOrder")

      **  **.saga()

      **  **.propagation(SagaPropagation.MANDATORY)

      **  **.compensation("direct:cancelOrder")

      **  **.completion("direct:completeOrder") *// completion endpoint*

      **    **.transform().header(Exchange.SAGA_LONG_RUNNING_ACTION)

      **    **.bean(orderManagerService, "newOrder")

      .log("Order ${body} created");

      *// direct:cancelOrder is the same as in the previous example*

      *// called on successful completion*

      from("direct:completeOrder")

      **  **.transform().header(Exchange.SAGA_LONG_RUNNING_ACTION)

      **  **.bean(orderManagerService, "findExternalId")

      **  **.to("jms:prepareOrder")

      **  **.log("Order ${body} sent for preparation");

      当Saga完成后，订单将被发送到JMS队列进行准备。

      与补偿操作一样，Saga协调器也可以多次调用完成操作（特别是在出现错误的情况下，如网络错误）。在此示例中，应准备侦听prepareOrder JMS队列的服务以保留可能的重复项（有关如何处理重复项的示例，请参阅Idempotent Consumer EIP）。

      ### 45.3.2. **使用自定义标识符和选项**

      到目前为止显示的示例使用资源（订单和信用）的Exchange.SAGA_LONG_RUNNING_ACTION作为标识符。这并不总是理想的方法，因为它可能污染业务逻辑和数据模型。

      另一种方法是使用Saga选项"register"自定义标识符。例如，信用服务可以重构如下:

      *// action*

      from("direct:reserveCredit")

      **  **.bean(idService, "generateCustomId") *// generate a custom Id and set it in the body*

      **  **.to("direct:creditReservation")

      *// delegate action*

      from("direct:creditReservation")

      **  **.saga()

      **  **.propagation(SagaPropagation.SUPPORTS)

      **  **.option("CreditId", body()) *// mark the current body as needed in the compensating action*

      **  **.compensation("direct:creditRefund")

      **    **.bean(creditService, "reserveCredit")

      .log("Credit ${header.amount} reserved. Custom Id used is ${body}");

      *// called only if the saga is cancelled*

      from("direct:creditRefund")

      **  **.transform(header("CreditId")) *// retrieve the CreditId option from headers*

      **  **.bean(creditService, "refundCredit")

      **  **.log("Credit for Custom Id ${body} refunded");

      **请注意上一个列表根本没有使用****Exchange.SAGA_LONG_RUNNING_ACTION****报文头****。**

      由于direct:creditReservation端点现在也可以从Saga外部调用，因此传播模式可以设置为**SUPPORTS**。

      可以在saga路由中声明**多个选项**。

      ### 45.3.3. **设置超时**

      Saga是长期运行的行为，但这并不意味着他们不应该有一个有限的时间框架来执行。**设置Sagas的超时总是一个很好的做法，**因为它可以保证Saga在机器故障的情况下不会永远停留。


      |  | Saga EIP实现可能在没有明确指定它的所有Saga上设置默认超时 |
      | - | -------------------------------------------------------- |

      当超时到期时，Saga EIP将决定**取消Saga**（并补偿所有参与者），除非之前已做出不同的决定。

      可以在Saga参与者上设置超时，如下所示:

      from("direct:newOrder")

      **  **.saga()

      **  **.timeout(1, TimeUnit.MINUTES) *// newOrder requires that the saga is completed within 1 minute*

      **  **.propagation(SagaPropagation.MANDATORY)

      **  **.compensation("direct:cancelOrder")

      **  **.completion("direct:completeOrder")

      **    ***// ...*

      **    **.log("Order ${body} created");

      所有参与者（例如信用服务，订单服务）都可以设置自己的超时。这些超时的最小值被视为saga组合在一起时的超时。

      也可以在saga级别指定超时，如下所示:

      from("direct:buy")

      **  **.saga()

      **  **.timeout(5, TimeUnit.MINUTES) *// timeout at saga level*

      **    **.to("direct:newOrder")

      **    **.to("direct:reserveCredit");

      ### 45.3.4. **选择传播**

      在上面的示例中，我们使用了MANDATORY和SUPPORTS传播模式，还使用了REQUIRED传播模式，这是在未指定任何其他内容时使用的默认传播。

      这些传播模式将事务上下文中使用的等效模式1:1映射。以下是其含义的摘要:


      | **传播**      | **描述**                                                     |
      | ------------- | ------------------------------------------------------------ |
      | REQUIRED      | 加入现有的saga或如果它不存在创建一个新的saga。               |
      | REQUIRES_NEW  | 总是创造一个新的saga。暂停旧的saga并在新的saga终结时恢复它。 |
      | MANDATORY     | 一个saga必须已经存在。现有的saga加入了。                     |
      | SUPPORTS      | 如果一个saga已经存在，那么加入它。                           |
      | NOT_SUPPORTED | 如果一个saga已经存在，它将被挂起并在当前块完成时恢复。       |
      | NEVER         | 绝不能在saga中调用当前块。                                   |

      ### 45.3.5. **使用手动完成（高级）**

      当Saga不能以同步方式执行时，但它需要例如使用异步通信信道与外部服务进行通信时，完成模式不能设置为AUTO（默认），因为创建它时的交换是未完成的。完成。

      对于具有较长执行时间（小时，天）的Sagas来说，情况通常如此。在这些情况下，应使用MANUAL完成模式。

      from("direct:mysaga")

      **  **.saga()

      **  **.completionMode(SagaCompletionMode.MANUAL)

      **  **.completion("direct:finalize")

      **  **.timeout(2, TimeUnit.HOURS)

      **    **.to("seda:newOrder")

      .to("seda:reserveCredit");

      *// Put here asynchronous processing for seda:newOrder and seda:reserveCredit*

      *// They will send asynchronous callbacks to seda:operationCompleted*

      from("seda:operationCompleted") *// an asynchronous callback*

      **  **.saga()

      **  **.propagation(SagaPropagation.MANDATORY)

      **    **.bean(controlService, "actionExecuted")

      **    **.choice()

      **      **.when(body().isEqualTo("ok"))

      **        **.to("saga:complete") *// complete the current saga manually (saga component)*

      **    **.end()*// You can put here the direct:finalize endpoint to execute final actions*

      将完成模式设置为MANUAL意味着当在直接路由中处理交换时未完成saga:mysaga但它会持续更长时间（最长持续时间设置为2小时）。

      当两个异步操作都完成时，saga就完成了。完成调用是使用Camel Saga Component的saga:complete端点完成的。有一个类似的端点用于手动补偿Saga（saga:compensate）。

      显然，添加saga标记并没有为流程增加太多价值：如果您删除所有Saga EIP配置，它也会起作用。但是Sagas增加了很多价值，因为他们保证即使存在意外问题（服务器崩溃，消息丢失），总会有一致的结果:下订单和信用保留，或者没有一个改变。特别是，如果Saga未在2小时内完成，补偿机制将负责确定状态。

      ## 45.4. **Xml配置**

      Saga功能也适用于想要使用XML配置的用户。

      以下剪辑显示了一个示例:

      <route>

      **  **<from uri="direct:start"/>

      **  **<saga>

      **    **<compensation uri="direct:compensation" />

      **    **<completion uri="direct:completion" />

      **    **<option optionName="myOptionKey">

      **      **<constant>myOptionValue</constant>

      **    **</option>

      **    **<option optionName="myOptionKey2">

      **      **<constant>myOptionValue2</constant>

      **    **</option>

      **  **</saga>

      **  **<to uri="direct:action1" />

      **  **<to uri="direct:action2" />

      </route>

      # 46. [**Sample EIP**](https://camel.apache.org/manual/latest/sample-eip.html)

      采样限制器允许您通过路由从流量中提取交换的示例。它配置有一个采样周期，在此期间只允许一个交换通过。所有其他Exchange将被停止。默认情况下，将使用1秒的采样周期。

      ## 46.1. **选项**

      Sample EIP支持3个选项，如下所示:


      | **名称**             | **描述**                                                           | **默认** | **类型** |
      | -------------------- | ------------------------------------------------------------------ | -------- | -------- |
      | **samplePeriod**     | 设置仅一个Exchange将通过的采样周期。                               | 1        | Long     |
      | **messageFrequency** | 设置采样消息计数，在收到许多Exchange之后，只有一个Exchange将通过。 |          | Long     |
      | **units**            | 设置采样周期的时间单位，默认为秒。                                 | SECONDS  | TimeUnit |

      ## 46.2. **示例**

      您可以将这个EIP与sample** **DSL 一起使用，如这些示例中所示。

      这些示例还说明了如何使用不同的语法配置采样周期:

      from("direct:sample")

      **    **.sample()

      **    **.to("mock:result");

      from("direct:sample-configured")

      **    **.sample(1, TimeUnit.SECONDS)

      **    **.to("mock:result");

      from("direct:sample-configured-via-dsl")

      **    **.sample().samplePeriod(1).timeUnits(TimeUnit.SECONDS)

      **    **.to("mock:result");

      from("direct:sample-messageFrequency")

      **    **.sample(10)

      **    **.to("mock:result");

      from("direct:sample-messageFrequency-via-dsl")

      **    **.sample().sampleMessageFrequency(5)

      **    **.to("mock:result");

      Spring Xml中的相同示例是:

      <route>

      **    **<from uri="direct:sample"/>

      **    **<sample samplePeriod="1" units="seconds">

      **        **<to uri="mock:result"/>

      </sample>

      </route>

      <route>

      **    **<from uri="direct:sample-messageFrequency"/>

      **    **<sample messageFrequency="10">

      **        **<to uri="mock:result"/>

      </sample>

      </route>

      <route>

      **    **<from uri="direct:sample-messageFrequency-via-dsl"/>

      **    **<sample messageFrequency="5">

      **        **<to uri="mock:result"/>

      </sample>

      </route>

      并且默认值为1秒，因此如果您还想使用1秒，则可以省略此配置

      <route>

      **    **<from uri="direct:sample"/>

      **    ***<!-- will by default use 1 second period -->*

      **    **<sample>

      **        **<to uri="mock:result"/>

      </sample>

      </route>

      # 47. [**Script EIP**](https://camel.apache.org/manual/latest/script-eip.html)

      用于执行不更改消息的脚本（默认情况下）。当您需要调用某些不在Java代码中的逻辑（例如JavaScript，Groovy或任何其他语言）时，这非常有用。消息体不会更改（默认情况下），但脚本上下文可以访问当前的Exchange，并且可以直接更改消息或报文头。但是脚本的返回值被丢弃而不使用。如果返回值应该用作已更改的消息体，请使用[Message Translator](https://camel.apache.org/manual/latest/message-translator.html) EIP。

      ## 47.1. **选项**

      Script EIP没有选项。

      ## 47.2. **示例**

      下面的路由将读取文件内容并根据正则表达式验证它们。

      from("file://inbox")

      **  **.script().groovy("// some groovy code goes here")

      **  **.to("bean:MyServiceBean.processLine");

      而且Xml也很容易

      <route>

      **  **<from uri="file://inbox"/>

      **  **<script>

      <groovy>// some groovy code goes here</groovy>
      </script>

      **  **<beanRef ref="myServiceBean" method="processLine"/>

      </route>

      <bean id="myServiceBean" class="com.mycompany.MyServiceBean"/>

      请注意，如果groovy脚本使用< >等，您可以在XML中使用CDATA

      <route>

      **  **<from uri="file://inbox"/>

      **  **<script>

      <groovy><![CDATA[ some groovy script here that can be multiple lines and whatnot ]]></groovy>
      </script>

      **  **<beanRef ref="myServiceBean" method="processLine"/>

      </route>

      <bean id="myServiceBean" class="com.mycompany.MyServiceBean"/>

      ## 47.3. **使用外部脚本文件**

      您可以引用外部脚本文件，而不是内联脚本。例如，要从类路径加载groovy脚本，您需要为值添加前缀resource:，如下所示:

      <route>

      **  **<from uri="file://inbox"/>

      **  **<script>

      <groovy>resource:classpath:com/foo/myscript.groovy</groovy>
      </script>

      **  **<beanRef ref="myServiceBean" method="processLine"/>

      </route>

      <bean id="myServiceBean" class="com.mycompany.MyServiceBean"/>

      您也可以从文件系统引用脚本file:，而不是classpath:如file:/var/myscript.groovy

      # 48. [**Service Call EIP**](https://camel.apache.org/manual/latest/serviceCall-eip.html)

      Service Call EIP允许在分布式系统中调用远程服务。在Kubernetes，Consul，Etcd，Zookeeper，DNS等服务注册表中查找要调用的服务。EIP将服务注册表的配置与服务的调用分开。

      在调用服务时，您可以参考EIP中的服务名称，如下所示:

      from("direct:start")

      **    **.serviceCall("foo")

      **    **.to("mock:result");

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **  **<route>

      **    **<from uri="direct:start"/>

      **    **<serviceCall name="foo"/>

      **    **<to uri="mock:result"/>

      **  **</route>

      </camelContext>

      Camel将:

      l 从Camel上下文和注册表中搜索服务调用配置

      l 使用外部服务注册表中的foo名称查找服务

      l 过滤服务器

      l 选择要使用的服务器

      l 使用所选的服务器信息构建Camel URI

      默认情况下，服务调用EIP使用camel-http，因此假设所选服务实例在80端口上的myhost.com主机上运行，计算的Camel URI将为:

      http:myhost.com:80

      ## 48.1. **服务名称为Camel URI示例**

      通常需要构建更复杂的Camel URI，其中可能包含可通过不同选项实现的选项：name:value

      该**服务名**支持有限的URI语法类似，这里的一些例子


      | **名称**         | **解决方案**                                                                                   |
      | ---------------- | ---------------------------------------------------------------------------------------------- |
      | foo              | [http://host:port](http://host:port/ "http://host:port/")                                      |
      | foo/path         | [http://host:port/path](http://host:port/path "http://host:port/path")                         |
      | foo/path?foo=bar | [http://host:port/path?foo=bar](http://host:port/path?foo=bar "http://host:port/path?foo=bar") |

      from("direct:start")

      **    **.serviceCall("foo/hello")

      **    **.to("mock:result");

      如果您想要更多地控制uri构造，可以使用**uri**指令:


      | **名称** | **URI**                                 | **解决方案**                    |
      | -------- | --------------------------------------- | ------------------------------- |
      | foo      | undertow:http://foo/hello               | undertow:http://host:port/hello |
      | foo      | undertow:http://foo.host:foo.port/hello | undertow:http://host:port/hello |

      from("direct:start")

      **    **.serviceCall("foo", "undertow:http://foo/hello")

      **    **.to("mock:result");

      高级用户可以通过表达式完全控制uri构造:

      from("direct:start")

      **    **.serviceCall()

      **        **.name("foo")

      **        **.expression()

      **            **.simple("undertow:http://${header.CamelServiceCallServiceHost}:${header.CamelServiceCallServicePort}/hello");

      ## 48.2. **选项**

      服务调用EIP支持以下列出的14个选项:


      | **名称**                           | **描述**                                                                                        | **默认** | **类型**                                    |
      | ---------------------------------- | ----------------------------------------------------------------------------------------------- | -------- | ------------------------------------------- |
      | **name**                           | **必需**设置要使用的服务的名称                                                                  |          | String                                      |
      | **uri**                            | 要发送到的端点的uri。可以使用org.apache.camel.language.simple.SimpleLanguage表达式动态计算uri。 |          | String                                      |
      | **component**                      | 要使用的组件。                                                                                  | HTTP     | String                                      |
      | **pattern**                        | 设置用于调用此端点的可选ExchangePattern                                                         |          | ExchangePattern                             |
      | **configurationRef**               | 指要使用的ServiceCall配置                                                                       |          | String                                      |
      | **serviceDiscoveryRef**            | 设置对要使用的自定义ServiceDiscovery的引用。                                                    |          | String                                      |
      | **serviceFilterRef**               | 设置对要使用的自定义ServiceFilter的引用。                                                       |          | String                                      |
      | **serviceChooserRef**              | 设置对要使用的自定义ServiceChooser的引用。                                                      |          | String                                      |
      | **loadBalancerRef**                | 设置对要使用的自定义ServiceLoadBalancer的引用。                                                 |          | String                                      |
      | **expressionRef**                  | 设置对要使用的自定义Expression的引用。                                                          |          | String                                      |
      | **serviceDiscovery Configuration** | **必需**使用给定配置配置ServiceDiscovery。                                                      |          | ServiceCallServiceDiscoveryConfiguration    |
      | **serviceFilterConfiguration**     | **必需**使用给定配置配置ServiceFilter。                                                         |          | ServiceCallServiceFilterConfiguration       |
      | **loadBalancerConfiguration**      | **必需**使用给定配置配置LoadBalancer。                                                          |          | ServiceCallServiceLoadBalancerConfiguration |
      | **expressionConfiguration**        | **必需**使用给定配置配置表达式。                                                                |          | ServiceCallExpressionConfiguration          |

      除了ref/binding配置样式，您还可以利用特定配置DSL来自定义特定选项:

      ## 48.3. **静态服务发现**

      此服务发现实现不查询任何外部服务，以查找与命名服务关联的服务列表，但将其保留在内存中。每项服务应以下列形式提供:

      [service@]host:port


      |  | 该service部分用于区分服务，但如果没有提供，它就像一个通配符，因此无论服务名称是什么，都将返回每个非命名服务。如果您拥有单个服务，则此选项非常有用，因此服务名称是多余的。 |
      | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |


      |  | 此实现由camel-core提供。 |
      | - | ------------------------ |

      可用选项:


      | **名称** | **Java类型** | **描述**                                                                                             |
      | -------- | ------------ | ---------------------------------------------------------------------------------------------------- |
      | servers  | String       | 以逗号分隔的服务器列表，格式为:[service @] host:port，[service @] host2:port，[service @] host3:port |

      from("direct:start")

      **    **.serviceCall("foo")

      **        **.staticServiceDiscovery()

      **            **.servers("service1@host1:80,service1@host2:80")

      **            **.servers("service2@host1:8080,service2@host2:8080,service2@host3:8080")

      **            **.end()

      **    **.to("mock:result");

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **  **<route>

      **    **<from uri="direct:start"/>

      **    **<serviceCall name="foo">

      **      **<staticServiceDiscovery>

      **        **<servers>service1@host1:80,service1@host2:80</servers>

      **        **<servers>service2@host1:8080,service2@host2:8080,service2@host3:8080</servers>

      **      **</staticServiceDiscovery>

      **    **</serviceCall

      <to uri="mock:result"/>
      **  **</route>

      </camelContext>

      ## 48.4. **Consul服务发现**

      要利用Consul进行服务发现，maven用户需要将以下依赖项添加到其pom.xml中

      <dependency>

      **    **<groupId>org.apache.camel</groupId>

      **    **<artifactId>camel-consul</artifactId>*<!-- use the same version as your Camel core version -->*

      <version>x.y.z</version>

      </dependency>

      可用选项:


      | **名称**             | **Java类型** | **描述**                      |
      | -------------------- | ------------ | ----------------------------- |
      | url                  | String       | Consul代理URL                 |
      | datacenter           | String       | 数据中心                      |
      | aclToken             | String       | 设置与Consul一起使用的ACL令牌 |
      | userName             | String       | 设置用于基本身份验证的用户名  |
      | password             | String       | 设置用于基本身份验证的密码    |
      | connectTimeoutMillis | Long         | 连接OkHttpClient的超时        |
      | readTimeoutMillis    | Long         | 读取OkHttpClient的超时        |
      | writeTimeoutMillis   | Long         | 为OkHttpClient写入超时        |

      以Java为例

      from("direct:start")

      **    **.serviceCall("foo")

      **        **.consulServiceDiscovery()

      **            **.url("http://consul-cluster:8500")

      **            **.datacenter("neverland")

      **            **.end()

      **    **.to("mock:result");

      ## 48.5. **DNS服务发现**

      要利用DNS进行服务发现，maven用户需要将以下依赖项添加到其pom.xml中

      <dependency>

      **    **<groupId>org.apache.camel</groupId>

      **    **<artifactId>camel-dns</artifactId>*<!-- use the same version as your Camel core version -->*

      <version>x.y.z</version>

      </dependency>

      可用选项:


      | **名称** | **Java类型** | **描述**                         |
      | -------- | ------------ | -------------------------------- |
      | proto    | String       | 所需服务的传输协议，默认为"_tcp" |
      | domain   | String       | 用于基本身份验证的用户名         |

      Java中的示例:

      from("direct:start")

      **    **.serviceCall("foo")

      **        **.dnsServiceDiscovery("my.domain.com")

      **    **.to("mock:result");

      在Xml中:

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **  **<route>

      **    **<from uri="direct:start"/>

      **    **<serviceCall name="foo">

      **      **<dnsServiceDiscovery domain="my.domain.com"/>

      **    **</serviceCall>

      **    **<to uri="mock:result"/>

      **  **</route>

      </camelContext>

      ## 48.6. **Etcd服务发现**

      要利用Etcd进行服务发现，maven用户需要将以下依赖项添加到其pom.xml中

      <dependency>

      **    **<groupId>org.apache.camel</groupId>

      **    **<artifactId>camel-etcd</artifactId>*<!-- use the same version as your Camel core version -->*

      <version>x.y.z</version>

      </dependency>

      可用选项:


      | **名称**    | **Java类型** | **描述**                               |
      | ----------- | ------------ | -------------------------------------- |
      | uris        | String       | 客户端可以连接的URI                    |
      | userName    | String       | 用于基本身份验证的用户名               |
      | password    | String       | 用于基本身份验证的密码                 |
      | timeout     | Long         | 设置操作可能需要完成的最长时间         |
      | servicePath | String       | 寻找服务发现的路径，默认为"/services"  |
      | type        | String       | 要设置发现类型，有效值是"按需"和"观看" |

      Java中的示例

      from("direct:start")

      .serviceCall("foo")

          .etcdServiceDiscovery()

              .uris("http://etcd1:4001,http://etcd2:4001")

              .servicePath("/camel/services")

              .end()

      .to("mock:result");
      在XML中

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **  **<route>

      **    **<from uri="direct:start"/>

      **    **<serviceCall name="foo">

      **      **<etcdServiceDiscovery uris="http://etcd1:4001,http://etcd2:4001" servicePath="/camel/services"/>

      **    **</serviceCall>

      **    **<to uri="mock:result"/>

      **  **</route>

      </camelContext>

      ## 48.7. **Kubernetes服务发现**

      要利用Kubernetes进行服务发现，maven用户需要将以下依赖项添加到其pom.xml中

      <dependency>

      **    **<groupId>org.apache.camel</groupId>

      **    **<artifactId>camel-kubernetes</artifactId>*<!-- use the same version as your Camel core version -->*

      <version>x.y.z</version>

      </dependency>

      可用选项:


      | **名称**            | **Java类型** | **描述**                                                                            |
      | ------------------- | ------------ | ----------------------------------------------------------------------------------- |
      | lookup              | String       | 如何执行服务查找。可能的值:client，dns，environment                                 |
      | apiVersion          | String       | 使用客户端查找时的Kubernetes API版本                                                |
      | caCertData          | String       | 使用客户端查找时设置证书颁发机构数据                                                |
      | caCertFile          | String       | 设置使用客户端查找时从文件加载的证书颁发机构数据                                    |
      | clientCertData      | String       | 使用客户端查找时设置客户端证书数据                                                  |
      | clientCertFile      | String       | 设置使用客户端查找时从文件加载的客户端证书数据                                      |
      | clientKeyAlgo       | String       | 使用客户端查找时设置客户端密钥库算法，例如RSA                                       |
      | clientKeyData       | String       | 使用客户端查找时设置客户端密钥库数据                                                |
      | clientKeyFile       | String       | 设置使用客户端查找时从文件加载的客户端密钥库数据                                    |
      | clientKeyPassphrase | String       | 使用客户端查找时设置客户端密钥库密码                                                |
      | dnsDomain           | String       | 设置用于dns查找的DNS域                                                              |
      | namespace           | String       | 要使用的Kubernetes命名空间。默认情况下，名称空间的名称取自环境变量KUBERNETES_MASTER |
      | oauthToken          | String       | 使用客户端查找时，设置OAUTH令牌以进行身份验证（而不是用户名/密码）                  |
      | username            | String       | 使用客户端查找时设置身份验证的用户名                                                |
      | password            | String       | 使用客户端查找时设置身份验证的密码                                                  |
      | trustCerts          | Boolean      | 设置在使用客户端查找时是否打开信任证书检查                                          |

      Java中的示例

      from("direct:start")

      **    **.serviceCall("foo")

      **        **.kubernetesServiceDiscovery()

      **            **.lookup("dns")

      **            **.namespace("myNamespace")

      **            **.dnsDomain("my.domain.com")

      **            **.end()

      **    **.to("mock:result");

      在XML中

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **  **<route>

      **    **<from uri="direct:start"/>

      **    **<serviceCall name="foo">

      **      **<kubernetesServiceDiscovery lookup="dns" namespace="myNamespace" dnsDomain="my.domain.com"/>

      **    **</serviceCall>

      **    **<to uri="mock:result"/>

      **  **</route>

      </camelContext>

      ## 48.8. **黑名单服务过滤器**

      此服务筛选器实现将列出的服务从服务发现找到的服务中删除。每项服务应以下列形式提供:

      [service@]host:port


      |  | 如果服务完全匹配，则会删除这些服务 |
      | - | ---------------------------------- |

      可用选项:


      | **名称** | **Java类型** | **描述**                                                                                                 |
      | -------- | ------------ | -------------------------------------------------------------------------------------------------------- |
      | servers  | String       | 以逗号分隔的服务器列表，列入黑名单:[service @] host:port，[service @] host2:port，[service @] host3:port |

      Java中的示例

      from("direct:start")

      **    **.serviceCall("foo")

      **        **.staticServiceDiscovery()

      **            **.servers("service1@host1:80,service1@host2:80")

      **            **.servers("service2@host1:8080,service2@host2:8080,service2@host3:8080")

      **            **.end()

      **        **.blacklistFilter()

      **            **.servers("service2@host2:8080")

      **            **.end()

      **    **.to("mock:result");

      在XML中

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **  **<route>

      **    **<from uri="direct:start"/>

      **    **<serviceCall name="foo">

      **      **<staticServiceDiscovery>

      **        **<servers>service1@host1:80,service1@host2:80</servers>

      **        **<servers>service2@host1:8080,service2@host2:8080,service2@host3:8080</servers>

      **      **</staticServiceDiscovery>

      **      **<blacklistServiceFilter>

      **        **<servers>service2@host2:8080</servers>

      **      **</blacklistServiceFilter>

      **    **</serviceCall

      <to uri="mock:result"/>
      **  **</route>

      </camelContext>

      ## 48.9. **负载均衡器**

      服务调用EIP带有自己的负载均衡器，如果未配置自定义，则默认情况下会对其进行身份验证，并将服务发现、服务文件管理器、服务选择和服务表达式粘合在一起，以便在可用服务之间进行负载均衡请求。

      如果您需要更复杂的负载均衡器，可以通过添加camel-ribbon来使用Ribbon，maven用户需要将以下依赖项添加到他们的pom.xml中

      <dependency>

      **    **<groupId>org.apache.camel</groupId>

      **    **<artifactId>camel-ribbon</artifactId>*<!-- use the same version as your Camel core version -->*

      <version>x.y.z</version>

      </dependency>

      可用选项:


      | **名称**   | **Java类型**             | **描述**             |
      | ---------- | ------------------------ | -------------------- |
      | clientName | String                   | Ribbon客户端名称     |
      | properties | List<PropertyDefinition> | 自定义客户端配置属性 |

      要利用Ribbon，需要显式启用它:

      Java示例

      from("direct:start")

      **    **.serviceCall("foo")

      **        **.ribbonLoadBalancer()

      **    **.to("mock:result");

      在XML中

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **  **<route>

      **    **<from uri="direct:start"/>

      **    **<serviceCall name="foo">

      **      **<ribbonLoadBalancer/>

      **    **</serviceCall>

      **    **<to uri="mock:result"/>

      **  **</route>

      </camelContext>

      您可以使用RibbonConfiguration以下方法配置Ribbon key programmatic :

      RibbonConfiguration configuration = new** **RibbonConfiguration();

      configuration.addProperty("listOfServers", "localhost:9090,localhost:9091");

      from("direct:start")

      **    **.serviceCall("foo")

      **        **.loadBalancer(new** **RibbonServiceLoadBalancer(configuration))

      **    **.to("mock:result");

      或者利用XML配置:

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **  **<route>

      **    **<from uri="direct:start"/>

      **    **<serviceCall name="foo">

      **      **<ribbonLoadBalancer>

      **          **<properties key="listOfServers" value="localhost:9090,localhost:9091"/>

      **      **</ribbonLoadBalancer>

      **    **</serviceCall>

      **    **<to uri="mock:result"/>

      **  **</route>

      </camelContext>

      ## 48.10. **共享配置**

      可以在路由定义上直接配置服务调用EIP，也可以通过共享配置配置服务调用EIP，这里有一个在Camel上下文中注册的两个配置的示例:

      ServiceCallConfigurationDefinition globalConf = new** **ServiceCallConfigurationDefinition();

      globalConf.setServiceDiscovery(

      **    **name -> Arrays.asList(

      **        **new** **DefaultServiceDefinition(name, "my.host1.com", 8080),

      **        **new** **DefaultServiceDefinition(name, "my.host2.com", 443))

      );

      globalConf.setServiceChooser(

      **    **list -> list.get(ThreadLocalRandom.current().nextInt(list.size()))

      );

      ServiceCallConfigurationDefinition httpsConf = new** **ServiceCallConfigurationDefinition();

      httpsConf.setServiceFilter(

      **    **list -> list.stream().filter(s -> s.getPort() == 443).collect(toList())

      );

      getContext().setServiceCallConfiguration(globalConf);

      getContext().addServiceCallConfiguration("https", httpsConf);

      每个服务调用定义和配置都将继承globalConf，globalConf可以看作默认配置，然后您可以在路由中引用httpsConf如下:

      from("direct:start")

      **    **.serviceCall()

      **        **.name("foo")

      **        **.serviceCallConfiguration("https")

      **        **.end()

      **    **.to("mock:result");

      该路由将利用globalConf的服务发现和服务选择器以及httpsConf的服务过滤器，但是如果需要，可以直接在路由上覆盖其中的任何一个：

      from("direct:start")

      **    **.serviceCall()

      **        **.name("foo")

      **        **.serviceCallConfiguration("https")

      **        **.serviceChooser(list -> list.get(0))

      **        **.end()

      **    **.to("mock:result");

      ## 48.11. **Spring Boot支持**

      在Spring-Boot应用程序中，您可以外部化大多数配置选项:

      ***application.properties***

      *# this can be configured stright tot he route and it has been included to show*

      *# property placeholders support*

      service.name** **= foo

      *# this property is not mandatory and it has been included to show how to configure*

      *# the service discovery implementation provided by**camel-consul*

      camel.cloud.consul.service-discovery.url** **= http://localhost:8500

      *# Add a static list of servers for the service named *

      *foo*camel.cloud.service-discovery.services[foo]** **= host1.static:8080,host2.static:8080

      ***路由***

      @Componentpublic** **class MyRouteBuilder implements RouteBuilder {

      **    **@Override

      **    **public void configure() throws Exception {

      **        **from("direct:start")

      **            **.serviceCall("{{service.name}}");

      **    **}

      }

      ## 48.12. **Spring Cloud支持**

      如果您在基于Spring Cloud的应用程序中使用Camel，除了Camel自己的camel-spring-cloud依赖性之外，您还可以通过添加与Spring Cloud相关的依赖性(即spring-cloud-consul，spring-cloud-kubernetes)来利用Spring Cloud服务发现和负载平衡能力。

      <dependency>

      **    **<groupId>org.apache.camel</groupId>

      **    **<artifactId>camel-spring-cloud dependency</artifactId>*<!-- use the same version as your Camel core version -->*

      <version>x.y.z</version>

      </dependency>

      # 49. [**Set Body EIP**](https://camel.apache.org/manual/latest/setBody-eip.html)

      SetBody EIP允许您设置交换的消息体。

      ## 49.1. **选项**

      Set Body EIP没有选项。

      ## 49.2. **例子**

      以下示例显示如何使用SetBody EIP

      RouteBuilder builder = new** **RouteBuilder() {

      **    **public void configure() {

      **        **from("direct:a")

      **            **.setBody(constant("test"))

      **            **.to("direct:b");

      **    **}

      };

      和使用XML的相同示例:

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **    **<route>

      **        **<from uri="direct:a"/>

      **        **<setBody><constant>test</constant></setBody>

      **        **<to uri="direct:b"/>

      </route>

      </camelContext>

      # 50. [**Set Header EIP**](https://camel.apache.org/manual/latest/setHeader-eip.html)

      SetHeader EIP允许您在Exchange设置和报文头。

      ## 50.1. **选项**

      Set Header EIP支持下面列出的1个选项:


      | **名称** | **描述**                                                                                           | **默认** | **类型** |
      | -------- | -------------------------------------------------------------------------------------------------- | -------- | -------- |
      | **name** | **必需**的用于设置新值的消息头的名称简单语言可用于定义要使用的动态计算头名称。否则将使用常量名称。 |          | String   |

      ## 50.2. **例子**

      以下示例显示如何使用SetHeader EIP

      RouteBuilder builder = new** **RouteBuilder() {

      **    **public void configure() {

      **        **from("direct:a")

      **            **.setHeader("myHeader", constant("test"))

      **            **.to("direct:b");

      **    **}

      };

      和使用XML的相同示例:

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **    **<route>

      **        **<from uri="direct:a"/>

      **        **<setHeader name="myHeader">

      **            **<constant>test</constant>

      **        **</setHeader>

      **        **<to uri="direct:b"/>

      </route>

      </camelContext>

      # 51. [**Set Out Header EIP ****(deprecated)**](https://camel.apache.org/manual/latest/setOutHeader-eip.html)

      此EIP已弃用。SetOutHeader EIP允许您在交换的输出消息上设置报文头。

      ## 51.1. **选项**

      Set Out Header EIP支持下面列出的1个选项:


      | **名称**       | **描述**                         | **默认** | **类型** |
      | -------------- | -------------------------------- | -------- | -------- |
      | **headerName** | **必需要**设置新值的消息头的名称 |          | String   |

      ## 51.2. **例子**

      以下示例显示如何使用SetOutHeader EIP

      RouteBuilder builder = new RouteBuilder() {

      **    **public void configure() {

      **        **from("direct:a")

      **            **.setOutHeader("myHeader", constant("test"))

      **            **.to("direct:b");

      **    **}

      };

      和使用XML的相同示例:

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **    **<route>

      **        **<from uri="direct:a"/>

      **        **<setOutHeader headerName="myHeader">

      **            **<constant>test</constant>

      **        **</setOutHeader>

      **        **<to uri="direct:b"/>

      **    **</route>

      </camelContext>

      # 52. [**Set Property EIP**](https://camel.apache.org/manual/latest/setProperty-eip.html)

      SetProperty EIP允许您在Exchange设置属性。

      ## 52.1. **选项**

      Set Property EIP支持下面列出的1个选项:


      | **名称** | **描述**                                                                                                 | **默认** | **类型** |
      | -------- | -------------------------------------------------------------------------------------------------------- | -------- | -------- |
      | **name** | **必需要**设置新值的交换属性的名称。简单语言可用于定义要使用的动态计算交换属性名称。否则将使用常量名称。 |          | String   |

      ## 52.2. **例子**

      以下示例显示如何使用SetProperty EIP

      RouteBuilder builder = new** **RouteBuilder() {

      **    **public void configure() {

      **        **from("direct:a")

      **            **.setProperty("myProperty", constant("test"))

      **            **.to("direct:b");

      **    **}

      };

      和使用XML的相同示例:

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **    **<route>

      **        **<from uri="direct:a"/>

      **        **<setProperty name="myProperty">

      **            **<constant>test</constant>

      **        **</setProperty>

      **        **<to uri="direct:b"/>

      </route>

      </camelContext>

      # 53. [**Sort EIP**](https://camel.apache.org/manual/latest/sort-eip.html)

      Sort可用于对消息进行排序。想象一下，您使用文本文件并在处理每个文件之前要确保内容已排序。

      默认情况下，Sort将使用处理数值或使用字符串表示形式的默认比较器对消息体进行排序。您可以提供自己的比较器，甚至是表达式以返回要排序的值。排序要求表达式计算返回的值可以转换为JDK排序操作所需的java.util.List值。

      ## 53.1. **选项**

      Sort EIP支持下面列出的1个选项:


      | **名称**          | **描述**                       | **默认** | **类型** |
      | ----------------- | ------------------------------ | -------- | -------- |
      | **comparatorRef** | 设置查找比较器以用于排序的引用 |          | String   |

      ## 53.2. **示例**

      在下面的路由中，它将读取文件内容并通过换行符进行标记，以便对每一行进行排序。

      from("file://inbox")

      **    **.sort(body().tokenize("\n"))

      **    **.to("bean:MyServiceBean.processLine");

      您可以将自己的比较器作为第二个参数传递:

      from("file://inbox")

      **    **.sort(body().tokenize("\n"), new** **MyReverseComparator())

      **    **.to("bean:MyServiceBean.processLine");

      在下面的路由中，它将读取文件内容并通过换行符进行标记，以便对每一行进行排序。

      <route>

      **  **<from uri="file://inbox"/>

      **  **<sort>

      **    **<simple>body</simple>

      **  **</sort>

      **  **<beanRef ref="myServiceBean" method="processLine"/>

      </route>

      要使用我们自己的比较器，我们可以将它称为spring bean:

      <route>

      **  **<from uri="file://inbox"/>

      **  **<sort comparatorRef="myReverseComparator">

      **    **<simple>body</simple>

      **  **</sort>

      **  **<beanRef ref="MyServiceBean" method="processLine"/>

      </route>

      <bean id="myReverseComparator" class="com.mycompany.MyReverseComparator"/>

      此外，您可以使用您喜欢的任何语言提供表达式，比如<simple>，只要它返回一个列表即可。

      # 54. [**Split EIP**](https://camel.apache.org/manual/latest/split-eip.html)

      [EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的[分离器](http://www.enterpriseintegrationpatterns.com/patterns/messaging/Sequencer.html)可以让你拆分消息分成若干块，并分别处理它们。

      ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps65.png)

      您需要将Splitter指定为split()。在早期版本的Camel中，您需要使用splitter()。

      Split EIP支持12个选项，如下所示:


      | **名称**                     | **描述**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | **默认** | **类型** |
      | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
      | **parallelProcessing**       | 如果启用，则同时处理每个分割的消息。请注意，调用方线程仍将等待，直到所有消息都已完全处理完毕，然后再继续。它只处理来自分离器的子消息，它同时发生。                                                                                                                                                                                                                                                                                                                                                                                                      | FALSE    | Boolean  |
      | **strategyRef**              | 设置对AggregationStrategy的引用，该AggregationStrategy用于将来自拆分消息的回复组合成来自Splitter的单个传出消息。默认情况下，Camel将使用原始传入消息到分离器（保持不变）。您还可以使用POJO作为AggregationStrategy                                                                                                                                                                                                                                                                                                                                        |          | String   |
      | **strategyMethodName**       | 当使用POJO作为AggregationStrategy时，此选项可用于显式声明要使用的方法名称。                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |          | String   |
      | **strategyMethodAllowNull**  | 如果此选项为false，则在没有要丰富的数据时不使用聚合方法。如果此选项为true，那么当使用POJO作为AggregationStrategy时，将使用null值作为oldExchange（当没有数据可以充实时）                                                                                                                                                                                                                                                                                                                                                                                 | FALSE    | Boolean  |
      | **executorServiceRef**       | 指用于并行处理的自定义线程池。请注意，如果设置此选项，则会自动隐含并行处理，您也不必启用该选项。                                                                                                                                                                                                                                                                                                                                                                                                                                                        |          | String   |
      | **streaming**                | 在流式传输模式下，拆分器按需拆分原始消息，然后对每个拆分的消息进行逐一处理。 这会减少内存使用量，因为拆分器不会首先拆分所有消息，但是随后我们不知道总大小，因此org.apache.camel.Exchange＃SPLIT_SIZE为空。 在非流模式下（默认），拆分器将首先拆分每条消息，以了解总大小，然后逐个处理每条消息。 这需要将所有拆分的消息保留在内存中，因此需要更多的内存。 总大小在org.apache.camel.Exchange＃SPLIT_SIZE报文头中提供。 流模式也影响聚合行为。 如果启用，则Camel将无序处理答复，例如按照返回的顺序。 如果禁用，则Camel将按照与拆分消息相同的顺序处理回复。 | FALSE    | Boolean  |
      | **stopOnException**          | 如果在处理org.apache.camel.Exchange期间发生异常或故障，将立即停止进一步处理，并且将引发引起的异常。如果处理交换失败（有错误消息）或错误处理程序抛出并处理异常（例如使用onException），也会停止。在所有情况下，分离器将停止进一步处理。这与路由引擎使用的管道中的行为相同。默认行为是不停止但继续处理直到结束                                                                                                                                                                                                                                            | FALSE    | Boolean  |
      | **timeout**                  | 使用并行处理时，设置以毫秒为单位指定的总超时。如果Splitter无法在给定时间范围内拆分和处理所有子消息，则超时触发器和Splitter会中断并继续。请注意，如果您提供TimeoutAwareAggregationStrategy，则会在分解之前调用timeout方法。如果在仍然保持运行任务的情况下达到超时，则Camel难以以正常方式关闭的某些任务可能会继续运行。因此请谨慎使用此选项。                                                                                                                                                                                                             | 0        | Long     |
      | **onPrepareRef**             | 准备要发送的org.apache.camel.Exchange时使用处理器。这可用于深度克隆应发送的消息，或者在发送交换之前所需的任何自定义逻辑。                                                                                                                                                                                                                                                                                                                                                                                                                               |          | String   |
      | **shareUnitOfWork**          | 与父级和每个子消息共享org.apache.camel.spi.UnitOfWork。默认情况下，拆分器不会在父Exchange和每个拆分Exchange之间共享工作单元。这意味着每个分拆Exchange都有自己独立的工作单元。                                                                                                                                                                                                                                                                                                                                                                           | FALSE    | Boolean  |
      | **parallelAggregate**        | 如果启用，则可以同时调用AggregationStrategy上的聚合方法。请注意，这需要将AggregationStrategy的实现实现为线程安全的。默认情况下，这是错误的，这意味着Camel会将调用同步到聚合方法。虽然在某些用例中，当AggregationStrategy实现为线程安全时，这可用于存档更高的性能。                                                                                                                                                                                                                                                                                      | FALSE    | Boolean  |
      | **stopOnAggregateException** | 如果启用，请在使用parallelProcessing时将聚合时发生的异常展开到错误处理程序。目前，聚合时间异常不会在使用parallelProcessing时停止路由处理。启用此选项可以解决此问题。为了向后兼容，默认值为false。                                                                                                                                                                                                                                                                                                                                                       | FALSE    | Boolean  |

      ## 54.1. **交换属性**

      在拆分的每个Exchange上设置以下属性:


      | **属性**           | **类型** | **描述**                                                                                                           |
      | ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------ |
      | CamelSplitIndex    | int      | 拆分计数器，每个Exchange被拆分增加。计数器从0开始。                                                                |
      | CamelSplitSize     | int      | 已拆分的Exchange总数。此报文头不适用于基于流的拆分。此报文头也在基于流的拆分中设置，但仅在已完成的Exchange上设置。 |
      | CamelSplitComplete | boolean  | 这个Exchange是否是最后一个。                                                                                       |

      ## 54.2. **例子**

      以下示例显示如何从端点**direct:a**获取请求使用Expression将其拆分为多个部分，然后将每个部分转发到**direct****:****b**

      from("direct:a")

      **    **.split(body(String.class).tokenize("\n"))

      **        **.to("direct:b");

      拆分器可以使用任何表达式语言，因此您可以使用任何支持的语言（如XPath，XQuery，SQL或其中一种脚本语言）来执行拆分。例如

      from("activemq:my.queue")

      **    **.split(xpath("//foo/bar"))

      **        **.to("file://some/directory")

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **    **<route>

      **        **<from uri="activemq:my.queue"/>

      **        **<split>

      **            **<xpath>//foo/bar</xpath>

      **            **<to uri="file://some/directory"/>

      **        **</split>

      </route>

      </camelContext>

      ## 54.3. **拆分Collection、Iterator、Array**

      常见的用例是从消息中拆分Collection，Iterator或Array。在下面的示例中，我们只需使用Expression来标识要拆分的值。

      from("direct:splitUsingBody")

      **    **.split(body())

      **        **.to("mock:result");

      from("direct:splitUsingHeader")

      **    **.split(header("foo"))

      **        **.to("mock:result");

      在XML中，您可以使用简单语言来标识要拆分的值。

      <route>

      **  **<from uri="direct:splitUsingBody"/>

      **  **<split>

      **     **<simple>${body}</simple>

      **     **<to uri="mock:result"/>

      **  **</split>

      </route>

      <route>

      **  **<from uri="direct:splitUsingHeader"/>

      **  **<split>

      **     **<simple>${header.foo}</simple>

      **     **<to uri="mock:result"/>

      **  **</split>

      </route>

      ## 54.4. **使用Spring Xml Extensions中的Tokenizer ***

      您可以使用Spring DSL中的tokenizer表达式用token拆分实体或报文头。这是一个常见的用例，因此我们为此提供了一个特殊的**tokenizer**标记。在下面的示例中，我们使用@作为分隔符拆分消息体。你当然可以使用逗号或空格甚至是正则表达式模式，当然要设置regex=true。

      <camelContext xmlns="http://camel.apache.org/schema/spring">

      **    **<route>

      **        **<from uri="direct:start"/>

      **        **<split>

      **            **<tokenize token="@"/>

      **            **<to uri="mock:result"/>

      **        **</split>

      </route>

      </camelContext>

      ## 54.5. **Splitter返回的是什么**

      Splitter默认返回原始输入消息。

      您可以通过提供自己的AggregationStrategy策略来覆盖它。此页面上有一个示例（拆分聚合请求/回复示例）。请注意其与Aggregate EIP支持的策略相同。可以将此拆分器视为具有轻量级聚合EIP的构建。


      |  | Multicast，Recipient List和Splitter EIP特别支持使用AggregationStrategy访问原始输入交换。您可能希望在聚合消息时使用此消息，并且其中一条消息出现故障，然后您希望在原始输入消息上进行丰富并作为响应返回; 它是具有3个交换参数的聚合方法。 |
      | - | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

      ## 54.6. **并行执行不同的部分**

      如果要并行执行所有部分，可以使用parallelProcessing:

      XPathBuilder xPathBuilder = new** **XPathBuilder("//foo/bar");

      from("activemq:my.queue")

      **  **.split(xPathBuilder).parallelProcessing()

      **    **.to("activemq:my.parts");

      ## 54.7. **基于流**


      |  | ***拆分大的XML有效负载***=== Java和saxon中的XPath引擎将整个XML内容加载到内存中。因此它们不适合非常大的XML有效载荷。相反，您可以使用自定义Expression，它将以流方式迭代XML有效内容。您可以在提供开始和结束令牌时使用支持此功能的Tokenizer语言。您可以使用专门为XML文档标记的XMLTokenizer语言。=== |
      | - | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

      您可以使用流构建器方法启用流模式来拆分流。

      from("direct:streaming")

      **  **.split(body().tokenize(",")).streaming()

      **    **.to("activemq:my.parts");

      您还可以提供自定义Bean作为分割器，以便像这样使用流:

      from("direct:streaming")

      **  **.split(method(new** **MyCustomIteratorFactory(), "iterator")) .streaming()

      **    **.to("activemq:my.parts")

      ## 54.8. **使用Tokenizer语言流式传输大型XML有效负载**

      有两个tokenizer可用于标记XML有效负载。第一个标记化程序使用与文本标记生成器相同的原理来扫描XML有效内容并提取标记序列。

      如果您有一个大的XML有效负载，来自文件源，并希望将其拆分为流模式，那么您可以使用具有开始/结束令牌的Tokenizer语言来实现此目的，内存占用量较低。


      |  | ***StAX组件***=== Camel StAX组件还可用于在流模式下拆分大型XML文件。在StAX上查看更多详情。=== |
      | - | -------------------------------------------------------------------------------------------- |

      例如，您可能具有如下结构的XML有效负载

      <orders>

      **  **<order>

      **    ***<!-- order stuff here -->*

      **  **</order>

      **  **<order>

      **    ***<!-- order stuff here -->*

      **  **</order>

      ...

      **  **<order>

      **    ***<!-- order stuff here -->*

      **  **</order>

      </orders>

      现在使用XPath拆分这个大文件会导致整个内容被加载到内存中。因此，我们可以使用Tokenizer语言执行此操作，如下所示:

      from("file:inbox")

      **  **.split().tokenizeXML("order").streaming()

      **     **.to("activemq:queue:order");

      在XML DSL中，路由如下:

      <route>

      **  **<from uri="file:inbox"/>

      **  **<split streaming="true">

      **    **<tokenize token="order" xml="true"/>

      **    **<to uri="activemq:queue:order"/>

      **  **</split>

      </route>

      请注意tokenizeXML使用子节点的标记名称拆分文件的方法（更确切地说，如果有的话，没有名称空间前缀的元素的本地名称），这意味着它将获取<order>和</order>（包括令牌）之间的内容。 例如，拆分后的消息如下:

      <order>

      **  ***<!-- order stuff here -->*

      </order>

      如果要从根/父tag继承名称空间，则可以通过提供根/父tag的名称来执行此操作:

      <route>

      **  **<from uri="file:inbox"/>

      **  **<split streaming="true">

      **    **<tokenize token="order" inheritNamespaceTagName="orders" xml="true"/>

      **    **<to uri="activemq:queue:order"/>

      **  **</split>

      </route>

      而在Java DSL中它如下:

      from("file:inbox")

      **  **.split().tokenizeXML("order", "orders").streaming()

      **     **.to("activemq:queue:order");

      您可以将以上inheritNamsepaceTagName属性设置为 *** **在每个tag中包含前面的上下文（即，生成包含在其祖先元素中的每个tag）。注意，在这种情况下，每个令牌必须共享相同的祖先元素。上述tokenizer在简单结构上运行良好，但在处理更复杂的XML结构时有一些固有的局限性。

      第二个tag生成器使用StAX解析器来克服这些限制。此标记化程序可识别XML名称空间，还可以更自然、更有效地处理简单和复杂的XML结构。要在{urn:shop}订单中使用此标记器进行拆分，我们可以编写

      Namespaces ns = new** **Namespaces("ns1", "urn:shop");

      ...

      from("file:inbox")

      **  **.split().xtokenize("//ns1:order", 'i', ns).streaming()

      **    **.to("activemq:queue:order)

      两个参数控制着标记器的行为。第一个参数使用路径表示法指定元素。此路径表示法使用带有通配符支持的xpath子集。第二个参数表示提取模式。可用的提取模式是:


      | **模式** | **描述**                                   |
      | -------- | ------------------------------------------ |
      | i        | 将上下文命名空间绑定注入提取的令牌（默认） |
      | w        | 将提取的标记包装在其祖先上下文中           |
      | u        | 将提取的令牌展开到其子内容中               |
      | t        | 提取指定元素的文本内容                     |

      有输入XML

      <m:orders xmlns:m="urn:shop" xmlns:cat="urn:shop:catalog">

      **  **<m:order><id>123</id><date>2014-02-25</date>...</m:order>

      ...

      </m:orders>

      每种模式都会产生以下令牌，


      | **模式** | **描述**                                                                                                                      |
      | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
      | i        | <m:order xmlns:m="urn:shop" xmlns:cat="urn:shop:catalog"><id>123</id><date>2014-02-25</date>…</m:order>                      |
      | w        | <m:orders xmlns:m="urn:shop" xmlns:cat="urn:shop:catalog"><m:order><id>123</id><date>2014-02-25</date>…</m:order></m:orders> |
      | u        | <id>123</id><date>2014-02-25</date>…                                                                                         |
      | t        | 1232014-02-25…                                                                                                               |

      在XML DSL中，等效路由将按如下方式编写:

      <camelContext xmlns:ns1="urn:shop">

      **  **<route>

      **    **<from uri="file:inbox"/>

      **    **<split streaming="true">

      **      **<xtokenize>//ns1:order</xtokenize>

      **      **<to uri="activemq:queue:order"/>

      **    **</split>

      **  **</route>

      </camelContext>

      或者将提取模式明确地设置为

      <xtokenize mode="i">//ns1:order</xtokenize>

      请注意，这个基于StAX的标记器使用StAX Location API并且需要StAX Reader实现（例如，woodstox）正确返回指向每个事件触发段开始的偏移位置（例如，<** **每个开始和结束元素事件的偏移位置）。如果您使用未正确实现该API的StAX Reader，则会在拆分后导致无效的xml片段。例如，代码段可能被错误终止:

      <Start>...<</Start>** **.... <Start>...</</Start>

      ## 54.9. **通过将N行分组在一起来拆分文件**

      Tokenizer语言有一个新的选项组，允许您将N个部分组合在一起，例如将大文件拆分为1000行的块。

      from("file:inbox")

      **  **.split().tokenize("\n", 1000).streaming()

      **     **.to("activemq:queue:order");

      在XML DSL中

      <route>

      **  **<from uri="file:inbox"/>

      **  **<split streaming="true">

      **    **<tokenize token="\n" group="1000"/>

      **    **<to uri="activemq:queue:order"/>

      **  **</split>

      </route>

      组选项是一个数字，必须是一个正数，表示要组合在一起的组数。每个部分将使用令牌组合。

      因此，在上面的示例中，发送到activemq订单队列的消息将包含1000行，每行由令牌分隔（这是一个新的行令牌）。

      使用组选项时的输出始终是java.lang.String类型。

      ## 54.10. **指定自定义聚合策略**

      这与Aggregate EIP类似。

      ## 54.11. **指定自定义ThreadPoolExecutor**

      您可以通过executorService选项自定义并行拆分器中使用的基础ThreadPoolExecutor。在Java DSL中尝试这样的事情:

      XPathBuilder xPathBuilder = new** **XPathBuilder("//foo/bar");

      ExecutorService pool = ...

      from("activemq:my.queue")

      **    **.split(xPathBuilder).executorService(pool)

      **        **.to("activemq:my.parts");

      ## 54.12. **使用Pojo进行拆分**

      由于Splitter可以使用任何Expression来进行实际拆分，因此我们利用这一事实并使用**方法**表达式来调用Bean来获取拆分部分。

      Bean应该返回一个值，该值是可迭代如:java.util.Collection，java.util.Iterator或Arrays。

      因此，返回的值将由Camel在运行时使用，以拆分消息。


      |  | ***流模式和使用pojo***===当你启用了流模式时，你应该返回一个Iterator以确保流线型时尚。例如，如果消息是一个大文件，那么通过使用迭代器，它将以块的形式返回文件的一部分，在下一个Iterator确保内存占用量低的方法中。这避免了将整个内容读入存储器的需要。有关示例，请参阅TokenizePair实现的源代码。=== |
      | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

      在路由中，我们将Expression定义为一个方法调用，用于调用我们在注册表中使用mySplitterBean注册的Bean id 。

      from("direct:body")

      **    ***// here we use a POJO bean mySplitterBean to do the split of the payload*

      **    **.split().method("mySplitterBean", "splitBody")

      **      **.to("mock:result");

      from("direct:message")

      **    ***// here we use a POJO bean mySplitterBean to do the split of the message*

      **    ***// with a certain header value*

      **    **.split().method("mySplitterBean", "splitMessage")

      **      **.to("mock:result");

      我们Bean的逻辑很简单。请注意，我们使用Camel Bean Binding将消息体作为String对象传递。

      public** **class MySplitterBean {

      **    ***/***

      * * The split body method returns something that is iteratable such as a java.util.List.*
      ---

      *     * **@param** body the payload of the incoming message*

      *     * **@return** a list containing each part splitted** */*
      **    **public List<String> splitBody(String body) {

      **        ***// since this is based on an unit test you can of cause*

      **        ***// use different logic for splitting as Camel have out*

      **        ***// of the box support for splitting a String based on comma*

      **        ***// but this is for show and tell, since this is java code*

      **        ***// you have the full power how you like to split your messages*

      **        **List<String> answer = new** **ArrayList<String>();

      **        **String[] parts = body.split(",");

      **        **for** **(String part : parts) {

      **            **answer.add(part);

      **        **}

      **        **return** **answer;

      **    **}

      **    ***/**** * The split message method returns something that is iteratable such as a java.util.List.*
      ---

      *     * **@param** header the header of the incoming message with the name user*

      *     * **@param** body the payload of the incoming message*

      *     * **@return** a list containing each part splitted** */*
      **    **public List<Message> splitMessage(@Header(value = "user") String header, @Body String body, CamelContext camelContext) {

      **        ***// we can leverage the Parameter Binding Annotations*

      **        ***// http://camel.apache.org/parameter-binding-annotations.html*

      **        ***// to access the message header and body at same time,*

      **        ***// then create the message that we want, splitter will*

      **        ***// take care rest of them.*

      **        ***// *NOTE* this feature requires Camel version >= 1.6.1*

      **        **List<Message> answer = new** **ArrayList<Message>();

      **        **String[] parts = header.split(",");

      **        **for** **(String part : parts) {

      **            **DefaultMessage message = new** **DefaultMessage(camelContext);

      **            **message.setHeader("user", part);

      **            **message.setBody(body);

      **            **answer.add(message);

      **        **}

      **        **return** **answer;

      **    **}

      }

      ## 54.13. **拆分聚合REQUEST/REPLY示例**

      此示例显示如何拆分Exchange，处理每个拆分的消息，聚合并使用请求/回复将组合响应返回给原始调用方。下面的路由说明了这一点以及拆分如何支持aggregationStrategy来保存正在处理的消息:

      *// this routes starts from the direct:start endpoint*

      *// the body is then splitted based on @ separator*

      *// the splitter in Camel supports InOut as well and for that we need*

      *// to be able to aggregate what response we need to send back, so we provide our*

      *// own strategy with the class MyOrderStrategy.*

      from("direct:start")

      **    **.split(body().tokenize("@"), new** **MyOrderStrategy())

      **        ***// each splitted message is then send to this bean where we can process it*

      **        **.to("bean:MyOrderService?method=handleOrder")

      **        ***// this is important to end the splitter route as we do not want to do more routing*

      **        ***// on each splitted message*

      **    **.end()

      **    ***// after we have splitted and handled each message we want to send a single combined*

      **    ***// response back to the original caller, so we let this bean build it for us*

      **    ***// this bean will receive the result of the aggregate strategy: MyOrderStrategy*

      **    **.to("bean:MyOrderService?method=buildCombinedResponse")

      OrderService bean如下:

      public** **static** **class MyOrderService {

      **    **private** **static** **int** **counter;

      **    ***/**** * We just handle the order by returning a id line for the order*
        * */*
        **    **public String handleOrder(String line) {
        **        **LOG.debug("HandleOrder: "** **+ line);
        **        **return** **"(id="** **+ ++counter + ",item="** **+ line + ")";
        **    **}
        **    ***/***
        * * We use the same bean for building the combined response to send*
          * * back to the original caller*

            * */*
            **    **public String buildCombinedResponse(String line) {

            **        **LOG.debug("BuildCombinedResponse: "** **+ line);

            **        **return** **"Response["** **+ line + "]";

            **    **}

            }

            我们的自定义aggregationStrategy负责保存正在进行的聚合消息，该消息在拆分器结束后将被发送到buildCombinedResponse方法进行最终处理，然后可以将组合响应返回给等待的调用者。

            */***

            * * This is our own order aggregation strategy where we can control*
            * * how each splitted message should be combined. As we do not want to*
            * * loos any message we copy from the new to the old to preserve the*
            * * order lines as long we process them*
            * */*

            public** **static** **class MyOrderStrategy implements AggregationStrategy {

            **    **public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

            **        ***// put order together in old exchange by adding the order from new exchange*

            **        **if** **(oldExchange == null) {

            **            ***// the first time we aggregate we only have the new exchange,*

            **            ***// so we just return it*

            **            **return** **newExchange;

            **        **}

            **        **String orders = oldExchange.getIn().getBody(String.class);

            **        **String newLine = newExchange.getIn().getBody(String.class);

            **        **LOG.debug("Aggregate old orders: "** **+ orders);

            **        **LOG.debug("Aggregate new order: "** **+ newLine);

            **        ***// put orders together separating by semi colon*

            **        **orders = orders + ";"** **+ newLine;

            **        ***// put combined order back on old to preserve it*

            **        **oldExchange.getIn().setBody(orders);

            **        ***// return old as this is the one that has all the orders gathered until now*

            **        **return** **oldExchange;

            **    **}

            }

            因此，让我们运行示例并查看其工作原理。

            我们将Exchange发送到**direct****:****start**端点，其中包含一个带有String值A@B@C的IN消息体流程是:

            HandleOrder:** **AHandleOrder:** **B

            Aggregate old orders:** **(id=1,item=A)

            Aggregate new** **order:** **(id=2,item=B)HandleOrder:** **C

            Aggregate old orders:** **(id=1,item=A);(id=2,item=B)

            Aggregate new** **order:** **(id=3,item=C)BuildCombinedResponse:** **(id=1,item=A);(id=2,item=B);(id=3,item=C)

            Response to caller:** **Response[(id=1,item=A);(id=2,item=B);(id=3,item=C)]

            ## 54.14. **如果发生异常，请停止处理**

            默认情况下，Splitter将继续处理整个Exchange，即使其中一个拆分的消息在路由期间会抛出异常。例如，如果您有一个包含1000行的Exchange，则可以拆分并路由每个子消息。在处理这些子消息期间，在17日抛出异常。Camel默认执行的操作是处理剩余的983条消息。你有机会在AggregationStrategy补救或处理这个问题。但有时你只是希望Camel停止并让异常传播回来，让Camel错误处理程序处理它。你可以在Camel 2.1中通过指定它应该在发生异常时停止来执行此操作。这是通过如下所示的选项stopOnException完成的:

            from("direct:start")

            **    **.split(body().tokenize(",")).stopOnException()

            **        **.process(new** **MyProcessor())

            **        **.to("mock:split");

            使用XML DSL，您可以按如下方式指定:

            <route>

            **    **<from uri="direct:start"/>

            **    **<split stopOnException="true">

            **        **<tokenize token=","/>

            **        **<process ref="myProcessor"/>

            **        **<to uri="mock:split"/>

            </split>

            </route>

            ## 54.15. **在准备消息时使用onPrepare执行自定义逻辑**

            请参阅Multicast EIP的详细信息

            ## 54.16. **分享工作单位**

            默认情况下，Splitter不会在父Exchange和每个拆分Exchange之间共享工作单元。这意味着每个子Exchange都有自己独立的工作单元。例如，您可能有一个用例，您要在其中拆分大消息。并且您希望将该过程视为原子隔离操作，无论是成功还是失败。如果发生故障，您希望将大消息移动到死信队列中。要支持此用例，您必须在Splitter上共享工作单元。

            这是Java DSL中的一个示例

            errorHandler(deadLetterChannel("mock:dead").useOriginalMessage()

            **        **.maximumRedeliveries(3).redeliveryDelay(0));

            from("direct:start")

            **    **.to("mock:a")

            **    ***// share unit of work in the splitter, which tells Camel to propagate failures from*

            **    ***// processing the splitted messages back to the result of the splitter, which allows*

            **    ***// it to act as a combined unit of work*

            **    **.split(body().tokenize(",")).shareUnitOfWork()

            **        **.to("mock:b")

            **        **.to("direct:line")

            **    **.end()

            **    **.to("mock:result");

            from("direct:line")

            **    **.to("log:line")

            **    **.process(new** **MyProcessor())

            **    **.to("mock:line");

            现在在这个例子中，如果处理每个子消息时出现问题，错误处理程序将启动（是的错误处理仍然适用于子消息）。**但是**没有发生的事情是，如果子消息未能通过所有重新传递尝试（其耗尽），那么它就**不会**搬进死信队列。原因是我们共享了工作单元，因此子消息将报告共享工作单元上的错误。Splitter完成后，它会检查共享工作单元的状态，并检查是否发生了错误。如果发生错误，它将在Exchange上设置异常并将其标记为回滚。错误处理程序将再次启动，因为Exchange已标记为回滚，并且它也有异常。没有执行重新传递尝试（因为它标记为回滚）并且Exchange将被移动到死信队列中。

            从XML DSL中使用它就像您只需将shareUnitOfWork属性设置为true一样简单:

            <camelContext errorHandlerRef="dlc" xmlns="http://camel.apache.org/schema/spring">

            **  ***<!-- define error handler as DLC, with use original message enabled -->*

            **  **<errorHandler id="dlc" type="DeadLetterChannel" deadLetterUri="mock:dead" useOriginalMessage="true">

            **    **<redeliveryPolicy maximumRedeliveries="3" redeliveryDelay="0"/>

            **  **</errorHandler>

            **  **<route>

            **    **<from uri="direct:start"/>

            **    **<to uri="mock:a"/>

            **    ***<!-- share unit of work in the splitter, which tells Camel to propagate failures from*

            * processing the splitted messages back to the result of the splitter, which allows*
              *     it to act as a combined unit of work -->*
              **    **<split shareUnitOfWork="true">
              **      **<tokenize token=","/>
              **      **<to uri="mock:b"/>
              **      **<to uri="direct:line"/>
              **    **</split>
              **    **<to uri="mock:result"/>
              **  **</route>
              **  ***<!-- route for processing each splitted line -->*
              **  **<route>
              **    **<from uri="direct:line"/>
              **    **<to uri="log:line"/>
              **    **<process ref="myProcessor"/>
              **    **<to uri="mock:line"/>
              **  **</route>
              </camelContext>

              |  | ***共享工作单元的实现***===所以实际上，工作单元不作为单个对象实例共享。而是SubUnitOfWork附加到其父级，并向父级发出有关其状态（提交或回滚）的回调。这可以在Camel 3.0中进行重构，其中可以进行更大的API更改。=== |
              | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

              # 55. [**Step EIP**](https://camel.apache.org/manual/latest/step-eip.html)

              Camel [EIP模式](https://github.com/apache/camel/blob/master/docs/user-manual/en/enterprise-integration-patterns.adoc)以不同的方式支持[管道和过滤器](http://www.enterpriseintegrationpatterns.com/PipesAndFilters.html)。
              ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps66.png)
              使用Camel，您可以将处理拆分为多个独立处理，然后可以将这些处理作为一个步骤在逻辑单元中链接在一起。
              Step将子处理器组合成单个复合单元。这允许在组级别捕获度量，这可以通过使用更高级别的抽象来更轻松地管理和监视Camel路由。您还可以将此视为路径与路径中每个处理器之间的中间层。
              当您有大型路由并希望将路由分解为逻辑步骤时，您可能希望这样做。
              这意味着您可以监控Camel应用程序并收集4层统计信息:
              l context level
              l route(s) level
              n step(s) level
              n processor(s) level
              ## 55.1. **JMX管理**

              每个Step EIP都在type=steps下的JMX树中注册，这允许监视CamelContext中的所有步骤。它也可以通过CamelContext或Route mbeans上的dumpStepStatsAsXml操作转储XML格式的统计信息。
              ## 55.2. **选项**

              Step EIP没有选项。
              ## 55.3. **例子**

              在Java中:
              from("activemq:SomeQueue")
              **    **.step("foo")
              **      **.bean("foo")
              **      **.to("acitvemq:OutputQueue")
              **    **.end()
              在XML中，您可以使用<step>元素
              <route>

              **  **<from uri="activemq:SomeQueue"/>
              **  **<step id="foo">
              **    **<bean ref="foo"/>
              **    **<to uri="activemq:OutputQueue"/>
              **  **</step>
              </route>

              您可以有多个Step 步骤:
              from("activemq:SomeQueue")
              **    **.step("foo")
              **      **.bean("foo")
              **      **.to("acitvemq:OutputQueue")
              **    **.end()
              **    **.step("bar")
              **      **.bean("something")
              **      **.to("log:Something")
              **    **.end()
              在XML中
              <route>

              **  **<from uri="activemq:SomeQueue"/>
              **  **<step id="foo">
              **    **<bean ref="foo"/>
              **    **<to uri="activemq:OutputQueue"/>
              **  **</step>
              **  **<step id="bar">
              **    **<bean ref="something"/>
              **    **<to uri="log:Something"/>
              **  **</step>
              </route>

              # 56. [**Sticky EIP**](https://camel.apache.org/manual/latest/sticky-eip.html)

              Sticky负载平衡器。Sticky Load balancing使用Expression来计算相关键以执行粘性负载平衡。
              ## 56.1. **选项**

              Sticky EIP支持下面列出的1个选项:
              | **名称**                  | **描述**                           | **默认** | **类型**                 |
              | ------------------------- | ---------------------------------- | -------- | ------------------------ |
              | **correlationExpression** | **必需**用于计算相关键的相关表达式 |          | NamespaceAwareExpression |

              ## 56.2. **例子**

              在这种情况下，我们使用test报文头作为相关表达式:
              from("direct:start")
              **    **.loadBalance()
              **    **.sticky(header("test"))
              **    **.to("seda:x", "seda:y", "seda:z");
              在XML中，您将拥有这样的路由
              <from uri="direct:start"/>

              **    **<loadBalance>
              **       **<sticky>
              **           **<correlationExpression>
              **               **<header>test</header>
              **           **</correlationExpression>
              **       **</sticky>
              **       **<to uri="seda:x"/>
              **       **<to uri="seda:y"/>
              **       **<to uri="seda:z"/>
              **    **</loadBalance>
              # 57. [**Stop EIP**](https://camel.apache.org/manual/latest/stop-eip.html)

              ## 57.1. **选项**

              Stop EIP没有选项。
              ## 57.2. **例子**

              from("direct:start")
              **    **.choice()
              **        **.when(body().contains("Hello")).to("mock:hello")
              **        **.when(body().contains("Bye")).to("mock:bye").stop()
              **        **.otherwise().to("mock:other")
              **    **.end()
              .to("mock:result");
              # 58. [**Stream-Config EIP**](https://camel.apache.org/manual/latest/stream-config-eip.html)

              Stream-processing重新排序EIP
              Stream-config EIP支持6个选项，如下所示:
              | **名称**                    | **描述**                                                             | **默认** | **类型** |
              | --------------------------- | -------------------------------------------------------------------- | -------- | -------- |
              | **capacity**                | 设置重新排序器的入站队列的容量。                                     | 100      | Integer  |
              | **timeout**                 | 设置等待缺少元素（消息）的最短时间。                                 | 1000     | Long     |
              | **deliveryAttemptInterval** | 设置流重定序器在等待能够传送的条件时最多等待的间隔（以毫秒为单位）。 | 1000     | Long     |
              | **ignoreInvalidExchanges**  | 是否忽略无效的交换                                                   | FALSE    | Boolean  |
              | **comparatorRef**           | 要使用自定义比较器                                                   |          | String   |
              | **rejectOld**               | 如果为true，则在处理早于上次传递的消息的消息时抛出异常               | FALSE    | Boolean  |

              # 59. [**Threads EIP**](https://camel.apache.org/manual/latest/threads-eip.html)

              ## 59.1. **选项**

              Threads EIP支持10个选项，如下所示:
              | **名称**                   | **描述**                                                                                                                                                     | **默认** | **类型**                 |
              | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | ------------------------ |
              | **executorServiceRef**     | 引用自定义线程池或使用线程池配置文件（作为叠加层）                                                                                                           |          | String                   |
              | **poolSize**               | 设置核心池大小                                                                                                                                               |          | Integer                  |
              | **maxPoolSize**            | 设置最大池大小                                                                                                                                               |          | Integer                  |
              | **KeepAliveTime**          | 设置空闲线程的保持活动时间                                                                                                                                   |          | Long                     |
              | **TIMEUNIT**               | 设置保持活动时间单位。默认情况下使用SECONDS。                                                                                                                |          | TimeUnit                 |
              | **maxQueueSize**           | 设置工作队列中的最大任务数。对于无界队列使用-1或Integer.MAX_VALUE                                                                                            |          | Integer                  |
              | **allowCoreThreadTimeOut** | 是否允许空闲核心线程超时，因此可以将池大小缩小到核心池大小以下默认为false                                                                                    | FALSE    | Boolean                  |
              | **threadName**             | 设置要使用的线程名称。                                                                                                                                       | Threads  | String                   |
              | **rejectedPolicy**         | 设置线程池无法执行的任务的处理程序。                                                                                                                         |          | ThreadPoolRejectedPolicy |
              | **callerRunsWhenRejected** | 当任务被拒绝时是否将调用程序作为后备运行添加到线程池（当它已满时）。如果未配置rejectedPolicy，或者线程池没有配置拒绝处理程序，则仅用作后备。默认情况下是真的 | TRUE     | Boolean                  |

              ## 59.2. **示例**

              下面的示例将在发送到**mock****:****result**之前添加一个大小为5个线程的线程池。
              from("seda:a")
              **  **.threads(5)
              **  **.to("mock:result");
              ### 59.2.1. **Spring DSL**

              下面的示例演示了Spring DSL中的线程EIP:
              <camelContext xmlns="http://camel.apache.org/schema/spring">

              **    **<route>
              **        **<from uri="seda:a"/>
              **        **<threads poolSize="5"/>
              **        **<to uri="mock:result"/>
              </route>

              </camelContext>

              # 60. [**Throttle EIP**](https://camel.apache.org/manual/latest/throttle-eip.html)

              Throttler模式允许您确保特定端点不会过载，或者不会超过与某些外部服务达成一致的SLA。
              ## 60.1. **选项**

              Throttle EIP支持6个选项，如下所示:
              | **名称**                   | **描述**                                                                                    | **默认** | **类型**                 |
              | -------------------------- | ------------------------------------------------------------------------------------------- | -------- | ------------------------ |
              | **correlationExpression**  | 用于计算用于油门分组的相关键的表达式。具有相同关联key的Exchange被限制在一起。               |          | NamespaceAwareExpression |
              | **executorServiceRef**     | 由throttler使用自定义线程池（ScheduledExecutorService）。                                   |          | String                   |
              | **timePeriodMillis**       | 设置最大请求计数有效的时间段                                                                | 1000     | Long                     |
              | **asyncDelayed**           | 启用异步延迟，这意味着线程在延迟时不会阻塞。                                                | FALSE    | Boolean                  |
              | **callerRunsWhenRejected** | 调用者是否应该在线程池拒绝任务时运行该任务。默认情况下是真的                                | TRUE     | Boolean                  |
              | **rejectExecution**        | 当交换超过请求限制时，throttler是否抛出ThrottlerRejectedExecutionException默认情况下为false | FALSE    | Boolean                  |

              ## 60.2. **示例**

              from("seda:a")
              **  **.throttle(3).timePeriodMillis(10000)
              **  **.to("log:result", "mock:result");
              因此，上面的示例将限制消息在**seda****:****a上**收到的所有消息在发送到**mock:result**之前确保在任何10秒窗口中最多发送3条消息。请注意，由于timePeriodMillis默认设置为1000毫秒，因此只需设置maximumRequestsPerPeriod设置即可设置每秒最大请求数。因此，要在两个端点之间以每秒100个请求限制请求，它看起来更像是......
              from("seda:a")
              **  **.throttle(100)
              **  **.to("seda:b");
              有关此模式的更多示例，您可以查看junit测试用例。
              以XML为例
              <route>

              **  **<from uri="seda:a"/>
              **  ***<!-- throttle 3 messages per 10 sec -->*
              **  **<throttle timePeriodMillis="10000">
              **    **<constant>3</constant>
              **    **<to uri="log:result"/>
              **    **<to uri="mock:result"/>
              **  **</throttle>
              </route>

              ## 60.3. **动态更改每个时段的最大请求数**

              **自Camel 2.8起可用**
              由于我们使用Expression，您可以在运行时调整此值，例如，您可以提供带有值的报文头。在运行时，Camel会计算表达式并将结果转换为java.lang.Long类型。在下面的示例中，我们使用消息中的报文头来确定每个周期的最大请求数。如果报文头不存在，则Throttler使用旧值。因此，如果要更改值，则只允许提供报文头:
              <route>

              **  **<from uri="direct:expressionHeader"/>
              **  **<throttle timePeriodMillis="500">
              **    ***<!-- use a header to determine how many messages to throttle per 0.5 sec -->*
              **    **<header>throttleValue</header>
              **    **<to uri="log:result"/>
              **    **<to uri="mock:result"/>
              **  **</throttle>
              </route>

              ## 60.4. **异步延迟**

              您可以让Throttler使用非阻塞异步延迟，这意味着Camel将使用scheduler来安排将来要执行的任务。然后该任务将继续路由。这允许调用者线程不阻塞并能够服务其他消息等。
              from("seda:a")
              **  **.throttle(100).asyncDelayed()
              **  **.to("seda:b");
              # 61. [**To EIP**](https://camel.apache.org/manual/latest/to-eip.html)

              请参阅消息相关文档
              l [消息](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message.adoc)
              l [消息总线](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message-bus.adoc)
              l [消息信道](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message-channel.adoc)
              l [消息端点](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message-endpoint.adoc)
              l [消息路由器](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message-router.adoc)
              l [消息翻译](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message-translator.adoc)
              ## 61.1. **选项**

              To EIP支持以下列出的2个选项:
              | **名称**    | **描述**                                | **默认** | **类型**        |
              | ----------- | --------------------------------------- | -------- | --------------- |
              | **URI**     | **必需**设置要发送到的端点的URI。       |          | String          |
              | **pattern** | 设置用于调用此端点的可选ExchangePattern |          | ExchangePattern |

              ## 61.2. **示例**

              以下示例路由演示了文件消费者端点和JMS生成器端点的使用。
              from("file://local/router/messages/foo")
              **    **.to("jms:queue:foo");
              在XML中:
              <route>

              **    **<from uri="file://local/router/messages/foo"/>
              <to uri="jms:queue:foo"/>

              </route>

              ## 61.3. **TO-EIP模式**

              您可能希望继续使用to而不是inOnly和inOut您可以指定交换模式，如下所示:
              from("direct:startInOnly")
              **  **.to(ExchangePattern.InOnly, "bean:process");
              from("direct:startInOut")
              **  **.to(ExchangePattern.InOut, "bean:process");
              以下是如何在XML中执行此操作:
              <route>

              **  **<from uri="direct:startInOnly"/>
              **  **<inOnly uri="bean:process"/>
              </route>

              <route>

              **  **<from uri="direct:startInOut"/>
              **  **<inOut uri="bean:process"/>
              </route>

              在这里，我们使用<to>与pattern设置交换模式属性:
              <route>

              **  **<from uri="direct:startInOnly"/>
              **  **<to pattern="InOnly" uri="bean:process"/>
              </route>

              <route>

              **  **<from uri="direct:startInOut"/>
              **  **<to pattern="InOut" uri="bean:process"/>
              </route>

              # 62. [**To D EIP**](https://camel.apache.org/manual/latest/toD-eip.html)

              有一个新的.toD** **/ <toD>允许使用一个或多个连接在一起的[表达式](https://camel.apache.org/manual/latest/expression.html)将消息发送到动态计算的[端点](https://camel.apache.org/manual/latest/endpoint.html)。默认情况下，[Simple](https://camel.apache.org/manual/latest/simple-language.html)语言用于计算端点。
              ## 62.1. **选项**

              To D EIP支持下列5个选项:
              | **名称**                     | **描述**                                                                                                | **默认** | **类型**        |
              | ---------------------------- | ------------------------------------------------------------------------------------------------------- | -------- | --------------- |
              | **uri**                      | **必需要**发送到的端点的URI。可以使用org.apache.camel.language.simple.SimpleLanguage表达式动态计算uri。 |          | String          |
              | **pattern**                  | 设置用于调用此端点的可选ExchangePattern                                                                 |          | ExchangePattern |
              | **cacheSize**                | 设置org.apache.camel.spi.ConsumerCache使用的最大大小，该大小用于缓存和重用生产者。                      |          | Integer         |
              | **ignoreInvalidEndpoint**    | 尝试使用该端点创建生产者时忽略invalidate端点异常                                                        | FALSE    | Boolean         |
              | **allowOptimisedComponents** | 是否允许组件优化toD，如果它们是org.apache.camel.spi.SendDynamicAware。                                  | TRUE     | Boolean         |

              ## 62.2. **示例**

              例如，要将消息发送到由报文头定义的端点，您可以执行以下操作:
              from("direct:start")
              **  **.toD("${header.foo}");
              在XML中:
              <route>

              **  **<from uri="direct:start"/>
              **  **<toD uri="${header.foo}"/>
              </route>

              您还可以在uri前面加上一个值，因为默认情况下，使用[Simple](https://camel.apache.org/manual/latest/simple-language.html)语言计算uri
              from("direct:start")
              **  **.toD("mock:${header.foo}");
              在XML中:
              <route>

              **  **<from uri="direct:start"/>
              **  **<toD uri="mock:${header.foo}"/>
              </route>

              在上面的例子中，我们计算一个前缀为"mock:"的端点，然后附加报文头foo。因此，例如，如果报文头foo具有值order，则端点计算为"mock:order"。
              您还可以使用除[Simple](https://camel.apache.org/manual/latest/simple-language.html)之外的其他语言，例如[XPath](https://camel.apache.org/components/latest/xpath-language.html) - 这需要使用language:作为前缀:如下所示（简单语言是默认语言）。如果未指定language:则端点是组件名称。在某些情况下，有一个组件和语言同名的，如xquery。
              <route>

              **  **<from uri="direct:start"/>
              **  **<toD uri="language:xpath:/order/@uri"/>
              </route>

              这是通过指定语言名称后跟冒号来完成的。
              from("direct:start")
              **  **.toD("language:xpath:/order/@uri");
              您还可以使用加号将多个[语言](https://camel.apache.org/components/latest/language-component.html)连接在一起+，如下所示:
              <route>

              **  **<from uri="direct:start"/>
              **  **<toD uri="jms:${header.base}+language:xpath:/order/@id"/>
              </route>

              在上面的例子中，uri是[Simple](https://camel.apache.org/manual/latest/simple-language.html)语言和[XPath](https://camel.apache.org/manual/latest/simple-language.html)的组合，其中第一部分是简单的（简单是默认语言）。然后加号分离到另一种语言，我们在其中指定语言名称后跟冒号
              from("direct:start")
              **  **.toD("jms:${header.base}+language:xpath:/order/@id");
              您可以根据需要连接多种语言，只需将它们与加号分开即可
              ## 62.3. **避免创建占用资源的无限动态端点**

              当使用toD动态计算端点时，您可能会计算大量动态端点，这会导致每个动态端点uri及其关联生产者使用的资源开销。
              例如，基于HTTP的端点，在调用HTTP服务时，您可以在URI参数中包含动态值，例如:
              from("direct:login")
              **  **.toD("http:myloginserver:8080/login?userid=${header.userName}");
              在上面的示例中，参数userid是动态计算的，并且将为每个不同的用户标识生成一个端点和生成器实例。为避免动态端点过多，您可以配置toD以减少其缓存大小，例如:
              from("direct:login")
              **  **.toD("http:myloginserver:8080/login?cacheSize=10&userid=${header.userName}");
              chacheSize为10。 **是重要的，**这只会减少toD有可能被重用的端点缓存，以防消息被路由到相同的userName头。因此，减小高速缓存大小将无法解决无穷无尽的动态endpoints问题。相反，您应该使用静态端点to并在Camel消息头中提供动态部分（如果可能）。
              ### 62.3.1. **使用静态端点**

              在上面的示例中，参数userid是动态计算的，并且将为每个不同的用户标识生成一个端点和生成器实例。要避免使用过于动态的端点，请使用单个静态端点并使用报文头提供动态部分:
              from("direct:login")
              **  **.setHeader(Exchange.HTTP_PATH, constant("/login"))
              **  **.setHeader(Exchange.HTTP_QUERY, simple("userid=${header.userName}"))
              **  **.toD("http:myloginserver:8080");
              但是，您可以使用其优化的组件toD来解决这个问题，如下所述。
              ## 62.4. **使用优化组件**

              更好的解决方案是，如果可以优化HTTP组件来处理动态计算端点uris的变化。这是针对以下组件进行优化的toD:
              l camel-http
              l camel-jetty
              l camel-netty-http
              l camel-undertow
              为了优化工作，那么:
              1. 在使用`toD'启动Camel路由期间检测并激活优化。
              2. 动态uri in toD必须将组件名称提供为静态或通过属性占位符解析。
              3. 支持的组件必须位于类路径上。

              基于HTTP的组件将进行优化，以便为每个端点使用相同的hostname:port，并将上下文路径和查询参数的动态值作为报文头提供:
              例如这条路由:
              from("direct:login")
              **  **.toD("http:myloginserver:8080/login?userid=${header.userName}");
              将基本上优化为（伪路由）:
              from("direct:login")
              **  **.setHeader(Exchange.HTTP_PATH, expression("/login"))
              **  **.setHeader(Exchange.HTTP_QUERY, expression("userid=${header.userName}"))
              **  **.toD("http:myloginserver:8080")
              **  **.removeHeader(Exchange.HTTP_PATH)
              **  **.removeHeader(Exchange.HTTP_QUERY);
              其中表达式将被动态地计算。注意uri in toD现在是static（\http:myloginserver:8080）。此优化允许Camel为所有动态变化重用相同的端点及其关联的生产者。这会产生更低的资源开销，因为相同的http生成器将用于userid的所有不同变量。
              |  | 当优化组件正在使用时，您不能使用报文头Exchange.HTTP_PATH和Exchange.HTTP_QUERY提供动态值来覆盖toD 的uri。如果要使用这些报文头，请改用普通to DSL。换句话说，这些报文头在toD内部用于携带端点的动态细节。 |
              | - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

              如果出现问题，您可以打开org.apache.camel.processor.SendDynamicProcessor上的DEBUG日志级别，如果toD已经过优化，则会在启动期间记录，或者如果加载优化组件时出现故障，则会记录堆栈跟踪。
              Detected SendDynamicAware component: http optimising toD: http:myloginserver:8080/log
              # 63. [**Topic EIP**](https://camel.apache.org/manual/latest/topic-eip.html)

              主题负载均衡器，使用此策略，您将通过发送到所有目标来获得主题行为。
              ## 63.1. **选项**

              主题EIP没有选项。
              ## 63.2. **例子**

              在这种情况下，我们使用test报头作为相关表达式:
              from("direct:start")
              **    **.loadBalance()
              **    **.topic()
              **    **.to("seda:x", "seda:y", "seda:z");
              在XML中，您将拥有这样的路由
              <from uri="direct:start"/>

              **    **<loadBalance>
              **       **<topic/>
              **       **<to uri="seda:x"/>
              **       **<to uri="seda:y"/>
              **       **<to uri="seda:z"/>
              **    **</loadBalance>
              # 64. [**Transform EIP**](https://camel.apache.org/manual/latest/transform-eip.html)

              请参阅下文了解详情
              l [消息翻译](https://github.com/apache/camel/blob/master/camel-core/src/main/docs/eips/message-translator.adoc)
              ## 64.1. **选项**

              Transform EIP没有选项。
              # 65. [**Unmarshal EIP**](https://camel.apache.org/manual/latest/unmarshal-eip.html)

              如果您收到来自其中一个Camel [组件](https://camel.apache.org/components/latest/index.html)（如File，[HTTP](https://camel.apache.org/components/latest/http-component.html)或[JMS）的消息，](https://camel.apache.org/components/latest/jms-component.html)您通常希望将有效负载解组为某个bean，以便您可以使用某些[Bean集成](https://camel.apache.org/manual/latest/bean-integration.html)处理它或执行[Predicate](https://camel.apache.org/manual/latest/predicate.html)计算等等。为此，请使用Java 中的[DSL](https://camel.apache.org/manual/latest/dsl.html)或[Xml配置中](https://camel.apache.org/manual/latest/xml-configuration.html)的**unmarshal**单词。
              ## 65.1. **选项**

              Unmarshal EIP支持以下列出的1个选项:
              | **名称**           | **描述**                 | **默认** | **类型**             |
              | ------------------ | ------------------------ | -------- | -------------------- |
              | **dataFormatType** | **必需要**使用的数据格式 |          | DataFormatDefinition |

              ## 65.2. **示例**

              例如
              DataFormat jaxb = new** **JaxbDataFormat("com.acme.model");
              from("activemq:My.Queue").
              **  **unmarshal(jaxb).
              **  **to("mqseries:Another.Queue");
              上面使用了一个名为jaxb的DataFormat，它配置了Java包名。如果您愿意，可以使用对数据格式的命名引用，然后可以在[注册表中](https://github.com/apache/camel/blob/master/docs/user-manual/en/registry.adoc)定义，例如通过[Spring](https://camel.apache.org/components/latest/spring.html) XML文件。
              您也可以使用DSL本身在使用时定义数据格式。例如，以下使用Java序列化来解组二进制文件，然后将其作为ObjectMessage发送到[ActiveMQ](https://camel.apache.org/components/latest/activemq-component.html)
              from("file://foo/bar").
              **  **unmarshal().serialization().
              **  **to("activemq:Some.Queue");
              # 66. [**Validate EIP**](https://camel.apache.org/manual/latest/validate-eip.html)

              Validate使用表达式或断言来验证消息的内容。在尝试处理消息之前确保消息有效非常有用。您可以将Validate DSL与所有类型的断言和表达式一起使用。Validate计算Predicate / Expression，如果为false，则抛出PredicateValidationException。如果是true，则继续消息处理。
              ## 66.1. **选项**

              Validate EIP没有选项。
              ## 66.2. **示例**

              下面的路由将读取文件内容并根据正则表达式验证它们。
              from("file://inbox")
              **  **.validate(body(String.class).regex("^\\w{10}\\,\\d{2}\\,\\w{24}$"))
              **  **.to("bean:MyServiceBean.processLine");
              验证EIP不仅限于消息体。您还可以验证消息头。
              from("file://inbox")
              **  **.validate(header("bar").isGreaterThan(100))
              **  **.to("bean:MyServiceBean.processLine");
              您也可以使用validate和simple。
              from("file://inbox")
              **  **.validate(simple("${in.header.bar} == 100"))
              **  **.to("bean:MyServiceBean.processLine");
              要在Spring DSL中使用validate，最简单的方法是使用简单表达式。
              <route>

              **  **<from uri="file://inbox"/>
              **  **<validate>
              **    **<simple>${body} regex ^\\w{10}\\,\\d{2}\\,\\w{24}$</simple>
              **  **</validate>
              **  **<beanRef ref="myServiceBean" method="processLine"/>
              </route>

              <bean id="myServiceBean" class="com.mycompany.MyServiceBean"/>

              验证消息头的XML DSL如下所示:
              <route>

              **  **<from uri="file://inbox"/>
              **  **<validate>
              **    **<simple>${in.header.bar} == 100</simple>
              **  **</validate>
              **  **<beanRef ref="myServiceBean" method="processLine"/>
              </route>

              <bean id="myServiceBean" class="com.mycompany.MyServiceBean"/>

              # 67. [**Weighted EIP**](https://camel.apache.org/manual/latest/weighted-eip.html)

              加权负载均衡器，在出现故障时使用此策略，将在下一个端点上尝试交换。
              ## 67.1. **选项**

              加权EIP支持3个选项，如下所示:
              | **名称**                       | **描述**                                                                                                                                              | **默认** | **类型** |
              | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
              | **roundRobin**                 | 启用robin模式。默认情况下，使用加权分配模式。默认值为false。                                                                                          | FALSE    | Boolean  |
              | **distributionRatio**          | **必需**分配比率是一个分隔的字符串，由分隔符分隔的整数权重组成，例如2,3,5。distributionRatio必须与负载均衡器列表中指定的端点和/或处理器的数量相匹配。 |          | String   |
              | **distributionRatioDelimiter** | 分隔符用于指定分配比率。默认值是逗号“，”                                                                                                            | ,        | String   |

              ## 67.2. **例子**

              在这种情况下，我们使用头测试作为相关表达式:
              from("direct:start")
              **    **.loadBalance()
              **    **.weighted(false, "4,2,1")
              **    **.to("seda:x", "seda:y", "seda:z");
              在XML中，您将拥有这样的路由
              <from uri="direct:start"/>

              **  **<loadBalance>
              **    **<weighted roundRobin="false" distributionRatio="4 2 1"/>
              **    **<to uri="seda:x"/>
              **    **<to uri="seda:y"/>
              **    **<to uri="seda:z"/>
              **  **</loadBalance>
              # 68. [**When EIP**](https://camel.apache.org/manual/latest/when-eip.html)

              [EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)的When EIP是与[基于内容的路由器](http://www.enterpriseintegrationpatterns.com/ContentBasedRouter.html)
              ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps67.png)
              ## 68.1. **选项**

              When EIP没有选项。
              ## 68.2. **例子**

              以下示例显示如何从输入**direct:a**端点路由请求到**direct****:****b**，**direct****:****c**或**direct****:****d，**具体取决于各种[Predicate](https://camel.apache.org/manual/latest/predicate.html)表达式的计算
              RouteBuilder builder = new** **RouteBuilder() {
              **    **public void configure() {
              **        **from("direct:a")
              **            **.choice()
              **                **.when(simple("${header.foo} == 'bar'"))
              **                    **.to("direct:b")
              **                **.when(simple("${header.foo} == 'cheese'"))
              **                    **.to("direct:c")
              **                **.otherwise()
              **                    **.to("direct:d");
              **    **}
              };
              和使用XML的相同示例:
              <camelContext xmlns="http://camel.apache.org/schema/spring">

              **    **<route>
              **        **<from uri="direct:a"/>
              **        **<choice>
              **            **<when>
              **                **<simple>${header.foo} == 'bar'</simple>
              **                **<to uri="direct:b"/>
              **            **</when>
              **            **<when>
              **                **<simple>${header.foo} == 'cheese'</simple>
              **                **<to uri="direct:c"/>
              **            **</when>
              **            **<otherwise>
              **                **<to uri="direct:d"/>
              **            **</otherwise>
              **        **</choice>
              </route>

              </camelContext>

              # 69. [**Wire Tap EIP**](https://camel.apache.org/manual/latest/wireTap-eip.html)

              [Wire Tap](http://www.enterpriseintegrationpatterns.com/WireTap.html)（来自[EIP模式](https://camel.apache.org/manual/latest/enterprise-integration-patterns.html)）允许您在将消息转发到最终目的地时将消息路由到单独的位置。
              ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps68.png)
              ![](file:///C:\Users\johnfeng\AppData\Local\Temp\ksohtml20168\wps69.png)
              ## 69.1. **流Stream**

              如果有一个[Wire Tap](https://camel.apache.org/manual/latest/wireTap-eip.html) 流消息主体，则应考虑启用[流缓存](https://camel.apache.org/manual/latest/stream-caching.html)以确保可以在每个端点读取该消息体。在[流缓存中](https://camel.apache.org/manual/latest/stream-caching.html)查看更多详细信息。
              ## 69.2. **选项**

              Wire Tap EIP支持以下11个选项：
              | **名称**                     | **描述**                                                                                                                                                                      | **默认** | **类型**                  |
              | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------------------- |
              | **processorRef**             | 引用用于创建新实体的处理器，作为用于窃听的消息                                                                                                                                |          | String                    |
              | **body**                     | 使用用于创建新实体的表达式作为要用于攻丝的消息                                                                                                                                |          | NamespaceAware Expression |
              | **executorServiceRef**       | 使用自定义线程池                                                                                                                                                              |          | String                    |
              | **copy**                     | 使用原始交换的副本                                                                                                                                                            | TRUE     | Boolean                   |
              | **dynamicUri**               | uri是动态的还是静态的。如果uri是动态的，则使用简单的语言来评估动态uri，以用作每个传入消息的窃听目的地。这类似于toD EIP模式的工作方式。如果是静态的，则将uri原样用作窃听目标。 | TRUE     | Boolean                   |
              | **onPrepareRef**             | 在准备发送org.apache.camel.Exchange时使用处理器。这可用于深克隆应发送的消息，或发送交换之前所需的任何自定义逻辑。                                                             |          | String                    |
              | **uri**                      | **必需要**发送到的端点的uri。可以使用org.apache.camel.language.simple.SimpleLanguage表达式动态计算uri。                                                                       |          | String                    |
              | **pattern**                  | 设置用于调用此端点的可选ExchangePattern                                                                                                                                       |          | ExchangePattern           |
              | **cacheSize**                | 设置org.apache.camel.spi.ConsumerCache使用的最大大小，该大小用于缓存和重用生产者。                                                                                            |          | Integer                   |
              | **ignoreInvalidEndpoint**    | 尝试使用该端点创建生产者时，请忽略无效端点异常                                                                                                                                | FALSE    | Boolean                   |
              | **allowOptimisedComponents** | 如果组件是org.apache.camel.spi.SendDynamicAware，是否允许组件优化toD。                                                                                                        | TRUE     | Boolean                   |

              ## 69.3. **WIRETAP线程池**

              WireTap使用线程池来处理窃听的消息。默认情况下，该线程池将使用“ [线程模型](https://camel.apache.org/manual/latest/threading-model.html) ”中详细介绍的设置。特别是，当池耗尽（使用了所有线程）时，调用线程将同步执行其他窃听。为了解决这个问题，您可以在[Wire Tap](https://camel.apache.org/manual/latest/wireTap-eip.html)上配置一个显式线程池，该池具有不同的拒绝策略，较大的工作队列或更多的工作线程。
              ## 69.4. **WIRETAP节点**

              Camel的Wire Tap节点在窃听[Exchange](https://camel.apache.org/manual/latest/exchange.html)时支持两种风格：
              l 使用传统的Wire Tap，Camel将复制原始[Exchange](https://camel.apache.org/manual/latest/exchange.html)，并将其[Exchange Pattern](https://camel.apache.org/manual/latest/exchange-pattern.html)设置为**InOnly**，因为我们希望以轻而易举的方式发送被窃听的[Exchange](https://camel.apache.org/manual/latest/exchange.html)。然后，被窃听的[Exchange](https://camel.apache.org/manual/latest/exchange.html)在单独的线程中发送，因此它可以与原始线程并行运行。请注意，仅复制了Exchange-Wire Tap不会进行深层克隆（除非您指定通过**onPrepareRef**其进行复制的自定义处理器）。因此，所有副本都可以共享原始Exchange中的对象。
              l Camel还提供了发送新[Exchange](https://camel.apache.org/manual/latest/exchange.html)的选项，允许您使用新值填充它。
              ## 69.5. **发送副本（传统窃听）**

              l 使用[Fluent Builders](https://camel.apache.org/manual/latest/fluent-builders.html)
              **    **protected RouteBuilder createRouteBuilder() {
              **        **return** **new** **RouteBuilder() {
              **            **public void configure() {
              **                ***// START SNIPPET: e1*
              **                **from("direct:start")
              **                    **.to("log:foo")
              **                    **.wireTap("direct:tap")
              **                    **.to("mock:result");
              **                ***// END SNIPPET: e1*
              **                **from("direct:tap")
              **                    **.delay(1000).setBody().constant("Tapped")
              **                    **.to("mock:result", "mock:tap");
              **                **from("direct:test").wireTap("direct:a").id("wiretap_1").to("mock:a");
              **                **from("direct:a").to("mock:b");
              **            **}
              **        **};
              **    **}
              ## 69.6. **发送新的Exchange**

              **使用**[**Fluent Builders**](https://camel.apache.org/manual/latest/fluent-builders.html)
              Camel支持processor或[表达式](https://camel.apache.org/manual/latest/expression.html)来填充新的[Exchange](https://camel.apache.org/manual/latest/exchange.html)。使用processor为您提供了如何填充[Exchange的](https://camel.apache.org/manual/latest/exchange.html)全部功能，因为您可以设置属性、报文头等。[表达式](https://camel.apache.org/manual/latest/expression.html)只能用于设置**IN**消息体。
              表达式或处理器预先填充了原始Exchange的副本，当您准备发送新的Exchange时，该副本可让您访问原始消息。 您可以使用**copy**选项（默认情况下启用）来指示是否要这样做。
              下面是processor变体，我们通过传递false来创建一个新的空[Exchange](https://camel.apache.org/manual/latest/exchange.html)来禁用**copy**
              **    **public void testFireAndForgetUsingProcessor() throws Exception {
              **        **context.addRoutes(new** **RouteBuilder() {
              **            **@Override
              **            **public void configure() throws Exception {
              **                ***// START SNIPPET: e1*
              **                **from("direct:start")
              **                    **.wireTap("direct:foo", false, new** **Processor() {
              **                        **public void process(Exchange exchange) throws Exception {
              **                            **exchange.getIn().setBody("Bye World");
              **                            **exchange.getIn().setHeader("foo", "bar");
              **                        **}
              **                    **}).to("mock:result");
              **                **from("direct:foo").to("mock:foo");
              **                ***// END SNIPPET: e1*
              **            **}
              **        **});
              **    **}
              ## 69.7. **使用动态URI**

              例如，将tap连接到动态URI，则它支持与消息端点中记录的相同的动态URI。例如，将tap连接到JMS队列，其中消息头ID是队列名称的一部分：
              **    **from("direct:start") .wireTap("jms:queue:backup-$\{header.id}")
              **        **.to("bean:doSomething");
              ## 69.8. **在DSL中发送新的交换和设置报文头**

              如果使用[Wire Tap](https://camel.apache.org/manual/latest/wireTap-eip.html)发送新消息，则只能使用来自DSL 的[表达式](https://camel.apache.org/manual/latest/expression.html)来设置消息体。如果还需要设置消息头，则必须使用[Processor](https://camel.apache.org/manual/latest/processor.html)。也可以使用DSL设置报文头。
              以下示例发送了一条新消息，其中包含
              l **Bye World** 作为消息体。
              l 消息头**id**的值为**123**。
              l 消息头**date**的代表当前日期作为值。
              ## 69.9. **JAVA DSL**

              **    **@Override
              **    **protected RouteBuilder createRouteBuilder() throws Exception {
              **        **return** **new** **RouteBuilder() {
              **            **@Override
              **            **public void configure() throws Exception {
              **                ***// START SNIPPET: e1*
              **                **from("direct:start")
              **                    ***// tap a new message and send it to direct:tap*
              **                    ***// the new message should be Bye World with 2 headers*
              **                    **.wireTap("direct:tap")
              **                        ***// create the new tap message body and headers*
              **                        **.newExchangeBody(constant("Bye World"))
              **                        **.newExchangeHeader("id", constant(123))
              **                        **.newExchangeHeader("date", simple("${date:now:yyyyMMdd}"))
              **                    **.end()
              **                    ***// here we continue routing the original messages*
              **                    **.to("mock:result");
              **                ***// this is the tapped route*
              **                **from("direct:tap")
              **                    **.to("mock:tap");
              **                ***// END SNIPPET: e1*
              **            **}
              **        **};
              **    **}
              ## 69.10. **使用ONPREPARE消息时执行自定义逻辑**

              查看[多播的](https://camel.apache.org/manual/latest/multicast-eip.html)详细信息
              [使用此模式](https://camel.apache.org/manual/latest/using-this-pattern.html)
