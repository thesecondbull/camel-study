第六章 **支持的表达语言**

# 1. **常量****语言**

**自****Camel****1.5**

常量表达式语言实际上只是将常量字符串指定为表达式类型的一种方法。


|  | 这是一个固定的常数值，仅在启动路由时设置一次，如果要在路由过程中使用动态值，则不要使用此值。 |
| - | -------------------------------------------------------------------------------------------- |

## 1.1. **常****量****选项**

常量语言支持1个选项，如下所示。


| **名称** | **默认** | **Java类型** | **描述**                                 |
| -------- | -------- | ------------ | ---------------------------------------- |
| trim     | true     | Boolean      | 是否修剪值以除去开头和结尾的空格和换行符 |

## 1.2. **用法示例**

Spring DSL的setHeader元素可以使用如下常量表达式：

<route>

<from uri="seda:a"/>

<setHeader name="theHeader">

<constant>the value</constant>

</setHeader>

<to uri="mock:b"/>

</route>

在这种情况下，来自seda:a端点的消息会将'theHeader'报头设置为常量值'the value'。

使用Java DSL的相同示例：

from("seda:a")

.setHeader("theHeader", constant("the value"))

.to("mock:b");

## 1.3. **从外部资源加载常量**

你可以外部化常数，有Camel从资源加载它，例如"classpath:"，"file:"或"http:"。

可以使用以下语法完成此操作："resource:scheme:location"，例如，可以引用类路径上的文件：

.setHeader("myHeader").constant("resource:classpath:constant.txt")

## 1.4. **依赖****关系**

常量语言是**Camel****核心的**一部分。

# 2. **ExchangeProperty****语言**

**自****Camel****2.0**

ExchangeProperty表达式语言允许您提取交换属性的值。

## 2.1. **ExchangeProperty****选项**

ExchangeProperty语言支持以下1个选项。


| **名称** | **默认** | **Java类型** | **描述**                                 |
| -------- | -------- | ------------ | ---------------------------------------- |
| trim     | true     | Boolean      | 是否修剪值以除去开头和结尾的空格和换行符 |

## 2.2. **用法示例**

Spring DSL的receiverList元素可以利用exchangeProperty表达式，例如：

在这种情况下，收件人列表包含在"myProperty"属性中。

<route>

<from uri="direct:a" />

<recipientList>

<exchangeProperty>myProperty</exchangeProperty>

</recipientList>

</route>

Java DSL中的相同示例：

from("direct:a").recipientList(exchangeProperty("myProperty"));

并且在语法上稍有不同，在此语法中，您可以最大程度地使用构建器（即，避免使用参数，而要使用堆叠操作，请注意exchangeProperty不是参数，而是堆叠方法调用，stacked method call）

from("direct:a").recipientList().exchangeProperty("myProperty");

## 2.3. **依赖****关系**

ExchangeProperty语言是**camel-core的**一部分。

# 3. **File****语言**

**自****Camel****1.1**

文件语言与[简单](https://camel.apache.org/manual/latest/simple-language.html)语言合并，这意味着您可以直接在简单语言中使用所有文件语法。

文件表达语言是对[简单](https://camel.apache.org/manual/latest/simple-language.html)语言的扩展，增加了与文件相关的功能。这些功能与使用文件路径和名称的常见用例有关。目的是允许将表达式与File和FTP组件一起使用，以为消费者和生产者设置动态文件模式。

## 3.1. **文件语言选项**

文件语言支持2个选项，如下所示。


| **名称**   | **默认** | **Java类型** | **描述**                                 |
| ---------- | -------- | ------------ | ---------------------------------------- |
| resultType |          | String       | 设置结果类型的类名（类型从输出）         |
| trim       | true     | Boolean      | 是否修剪值以除去开头和结尾的空格和换行符 |

## 3.2. **语法**

该语言是对[简单](https://camel.apache.org/manual/latest/simple-language.html)语言的**扩展**，因此，[简单](https://camel.apache.org/manual/latest/simple-language.html)语法也适用。因此，下表仅列出了其他内容。与[简单](https://camel.apache.org/manual/latest/simple-language.html)语言相反，[文件语言](https://camel.apache.org/manual/latest/file-language.html)还支持[常量](https://camel.apache.org/manual/latest/constant-language.html)表达式，因此您可以输入固定的文件名。

所有文件语言符号都使用与java.io.File对象上的方法相同的表达式名称，例如，file:absolute引用java.io.File.getAbsolute()方法。请注意，当前Exchange并不支持所有表达式。例如，[FTP](https://camel.apache.org/components/latest/ftp-component.html)组件支持某些选项，而File组件则支持所有选项。


| **表达式**                 | **类型** | **文件消费者** | **文件生产者** | **FTP消费者** | **FTP生产者** | **描述**                                                                                                                                                                     |
| -------------------------- | -------- | -------------- | -------------- | ------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| file:name                  | String   | yes            | no             | yes           | no            | 指文件名（相对于起始目录，请参见下面的注释）                                                                                                                                 |
| file:name.ext              | String   | yes            | no             | yes           | no            | 仅指文件扩展名                                                                                                                                                               |
| file:name.ext.single       | String   | yes            | no             | yes           | no            | 指文件扩展名。如果文件扩展名具有多个点，则此表达式将被删除，并且仅返回最后一部分。                                                                                           |
| file:name.noext            | String   | yes            | no             | yes           | no            | 指没有扩展名的文件名（相对于起始目录，请参见下面的注释）                                                                                                                     |
| file:name.noext.single     | String   | yes            | no             | yes           | no            | 指没有扩展名的文件名（相对于起始目录，请参见下面的注释）。如果文件扩展名具有多个点，则此表达式仅去除最后一部分，而保留其他部分。                                             |
| file:onlyname              | String   | yes            | no             | yes           | no            | 仅指没有前导路径的文件名。                                                                                                                                                   |
| file:onlyname.noext        | String   | yes            | no             | yes           | no            | 指的是仅具有扩展名和前导路径的文件名。                                                                                                                                       |
| file:onlyname.noext.single | String   | yes            | no             | yes           | no            | 指的是仅具有扩展名和前导路径的文件名。如果文件扩展名具有多个点，则此表达式仅去除最后一部分，而保留其他部分。                                                                 |
| file:ext                   | String   | yes            | no             | yes           | no            | 仅指文件扩展名                                                                                                                                                               |
| file:parent                | String   | yes            | no             | yes           | no            | 指文件父                                                                                                                                                                     |
| file:path                  | String   | yes            | no             | yes           | no            | 指文件路径                                                                                                                                                                   |
| file:absolute              | Boolean  | yes            | no             | no            | no            | 指文件是绝对文件还是相对文件                                                                                                                                                 |
| file:absolute.path         | String   | yes            | no             | no            | no            | 指的是绝对文件路径                                                                                                                                                           |
| file:length                | Long     | yes            | no             | yes           | no            | 指的是作为Long类型返回的文件长度                                                                                                                                             |
| file:size                  | Long     | yes            | no             | yes           | no            | 指的是作为Long类型返回的文件长度                                                                                                                                             |
| file:modified              | Date     | yes            | no             | yes           | no            | 引用最后修改为日期类型的文件                                                                                                                                                 |
| date:_command:pattern_     | String   | yes            | yes            | yes           | yes           | 使用java.text.SimpleDateFormat模式格式化日期。是对简单语言的**扩展**。附加命令是：**file**（仅适用于消费者）**文件**的最后修改时间戳。注意：也可以使用简单语言中的所有命令。 |

## 3.3. **文件****token****示例**

### 3.3.1. **相对路径**

在以下**相对**目录中有文件hello.txt的java.io.File句柄：.\filelanguage\test。然后，我们将端点配置为使用此起始目录.\filelanguage。文件token将返回为：


| **Expression**      | **Returns**                                                    |
| ------------------- | -------------------------------------------------------------- |
| file:name           | test\hello.txt                                                 |
| file:name.ext       | txt                                                            |
| file:name.noext     | test\hello                                                     |
| file:onlyname       | hello.txt                                                      |
| file:onlyname.noext | hello                                                          |
| file:ext            | txt                                                            |
| file:parent         | filelanguage\test                                              |
| file:path           | filelanguage\test\hello.txt                                    |
| file:absolute       | FALSE                                                          |
| file:absolute.path  | \workspace\camel\camel-core\target\filelanguage\test\hello.txt |

### 3.3.2. **绝对路径**

在以下**绝对**目录中有文件hello.txt的java.io.File句柄：\workspace\camel\camel-core\target\filelanguage\test。然后我们将端点配置为使用绝对起始目录\workspace\camel\camel-core\target\filelanguage。文件token将返回为：


| **Expression**      | **Returns**                                                    |
| ------------------- | -------------------------------------------------------------- |
| file:name           | test\hello.txt                                                 |
| file:name.ext       | txt                                                            |
| file:name.noext     | test\hello                                                     |
| file:onlyname       | hello.txt                                                      |
| file:onlyname.noext | hello                                                          |
| file:ext            | txt                                                            |
| file:parent         | \workspace\camel\camel-core\target\filelanguage\test           |
| file:path           | \workspace\camel\camel-core\target\filelanguage\test\hello.txt |
| file:absolute       | TRUE                                                           |
| file:absolute.path  | \workspace\camel\camel-core\target\filelanguage\test\hello.txt |

## 3.4. **示例**

您可以输入固定的[常量](https://camel.apache.org/manual/latest/constant-language.html)表达式，例如myfile.txt：

fileName="myfile.txt"

假设我们使用文件消费者来读取文件，并希望将读取的文件移动到当前日期为子文件夹的备份文件夹。可以使用以下表达式来归档：

fileName="backup/${date:now:yyyyMMdd}/${file:name.noext}.bak"

还支持相对文件夹名称，因此假设备份文件夹应该是同级文件夹，则可以将..附加为：

fileName="../backup/${date:now:yyyyMMdd}/${file:name.noext}.bak"

由于这是对[简单](https://camel.apache.org/manual/latest/simple-language.html)语言的扩展，因此我们也可以访问该语言的所有功能，因此在此用例中，我们希望将in.header.type用作动态表达式中的参数：

fileName="../backup/${date:now:yyyyMMdd}/type-${in.header.type}/backup-of-${file:name.noext}.bak"

如果您有要在表达式中使用的自定义日期，则Camel支持从消息header中检索日期。

fileName="orders/order-${in.header.customerId}-${date:in.header.orderDate:yyyyMMdd}.xml"

最后，我们还可以使用bean表达式来调用POJO类，该类生成一些要使用的String输出（或可转换为String）：

fileName="uniquefile-${bean:myguidgenerator.generateid}.txt"

当然，所有这些都可以组合在一个表达式中，您可以在一个组合表达式中使用[File Language](https://camel.apache.org/manual/latest/file-language.html)，[Simple](https://camel.apache.org/manual/latest/file-language.html)和[Bean](https://camel.apache.org/components/latest/bean-component.html)语言。对于那些常见的文件路径模式，这是非常强大的。

## 3.5. **结合使用****Spring PropertyPlaceholderConfigurer****和****File****组件**

在Camel中，您可以直接从[简单](https://camel.apache.org/manual/latest/simple-language.html)语言中使用[文件语言](https://camel.apache.org/manual/latest/file-language.html)，这使基于内容的路由器更易于在Spring XML中实现，我们可以在其中基于文件扩展名进行路由，如下所示：

<from uri="file://input/orders"/>

**   **<choice>

**     **<when>

**         **<simple>${file:ext} == 'txt'</simple>

**         **<to uri="bean:orderService?method=handleTextFiles"/>

**     **</when>

**     **<when>

**         **<simple>${file:ext} == 'xml'</simple>

**         **<to uri="bean:orderService?method=handleXmlFiles"/>

**     **</when>

**     **<otherwise>

**         **<to uri="bean:orderService?method=handleOtherFiles"/>

**     **</otherwise>

**  **</choice>

如果您在File端点上使用fileName选项通过[File Language](https://camel.apache.org/manual/latest/file-language.html)设置动态文件名，请确保您使用替代语法以避免与Springs PropertyPlaceholderConfigurer发生冲突。

**bundle-context.xml**

<bean id="propertyPlaceholder" class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">

<property name="location" value="classpath:bundle-context.cfg" />

</bean>

<bean id="sampleRoute" class="SampleRoute">

**    **<property name="fromEndpoint" value="${fromEndpoint}" />

<property name="toEndpoint" value="${toEndpoint}" />

</bean>

**bundle-context.cfg**

fromEndpoint=activemq:queue:testtoEndpoint=file://fileRoute/out?fileName=test-$simple{date:now:yyyyMMdd}.txt

注意上面toEndpoint我们如何使用$simple\{ }语法。

如果您不这样做，则会发生冲突，Spring会抛出异常，例如

org.springframework.beans.factory.BeanDefinitionStoreException:

Invalid bean definition with name 'sampleRoute'** **defined in class path resource [bundle-context.xml]:Could not resolve placeholder 'date:now:yyyyMMdd'

## 3.6. **依赖****关系**

File语言是**camel-core的**一部分。

# 4. **Header****语言**

**自****Camel****1.5**

Header表达语言允许您提取报头的值。

## 4.1. **Header****选项**

Header语言支持以下1个选项。


| **名称** | **默认** | **Java类型** | **描述**                                 |
| -------- | -------- | ------------ | ---------------------------------------- |
| trim     | true     | Boolean      | 是否修剪值以除去开头和结尾的空格和换行符 |

## 4.2. **用法示例**

Spring DSL的receiverList元素可以利用Header表达式，例如：

在这种情况下，收件人列表包含在报头"myHeader"中。

和Java DSL中的相同示例：

并在语法上稍有不同，在此语法中，您可以最大程度地使用构建器（即，避免使用参数，而是使用堆叠操作，请注意，报头不是参数，而是堆叠方法调用）

from("direct:a").recipientList().header("myHeader");

## 4.3. **依赖****关系**

Header语言是**camel-core的**一部分。

# 5. **properties****组件**

**自****Camel****2.3**

属性组件用于Camel应用程序中的属性占位符，例如端点URI。它**不是**由生产者和消费者使用的路由消息的常规Camel组件。但是，由于历史原因，它被命名为PropertiesComponent并且这个名称是众所周知的，因此我们继续使用它。

## 5.1. **Spring Boot****自动配置**

该组件支持10个选项，如下所示。


| **名称**                                                        | **描述**                                                                                                                                                                   | **默认** | **类型** |
| --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
| **camel.component.properties.auto-discover-properties-sources** | 是否从注册表和服务工厂自动发现PropertiesSource实例。                                                                                                                       | TRUE     | Boolean  |
| **camel.component.properties.default-fallback-enabled**         | 如果为false，则组件不会照顾冒号分隔符来尝试查找键的默认值。                                                                                                                | TRUE     | Boolean  |
| **camel.component.properties.encoding**                         | 从文件系统或类路径加载属性文件时使用的编码。如果未设置编码，则使用java.util.Properties＃load（java.io.InputStream）记录的ISO-8859-1编码（latin-1）加载属性文件。           |          | String   |
| **camel.component.properties.environment-variable-mode**        | 设置OS环境变量模式（0 = never, 1 = fallback, 2 = override）。默认模式（override）是使用OS环境变量（如果存在），并覆盖任何现有属性。在JVM系统属性模式之前检查OS环境变量模式 | 2        | Integer  |
| **camel.component.properties.ignore-missing-location**          | 是否静默忽略是否无法找到位置，例如找不到属性文件。                                                                                                                         | FALSE    | Boolean  |
| **camel.component.properties.initial-properties**               | 设置将在解析任何位置之前使用的初始属性。该选项是java.util.Properties类型。                                                                                                 |          | String   |
| **camel.component.properties.location**                         | 加载属性的位置列表。您可以使用逗号分隔多个位置。此选项将覆盖所有默认位置，并且仅使用此选项中的位置。                                                                       |          | String   |
| **camel.component.properties.override-properties**              | 设置优先级优先的特殊列表，如果属性存在，将优先使用。该选项是java.util.Properties类型。                                                                                     |          | String   |
| **camel.component.properties.properties-parser**                | 要使用自定义的PropertiesParser。该选项是org.apache.camel.component.properties.PropertiesParser类型。                                                                       |          | String   |
| **camel.component.properties.system-properties-mode**           | 设置JVM系统属性模式（0 =从不，1 =后备，2 =覆盖）。默认模式（覆盖）是使用系统属性（如果存在），并覆盖任何现有属性。在JVM系统属性模式之前检查OS环境变量模式                  | 2        | Integer  |


|  | **从Java代码解析属性**您可以使用CamelContext的方法resolvePropertyPlaceholders从Java代码解析属性。 |
| - | ------------------------------------------------------------------------------------------------- |

## 5.2. **使用****PropertyPlaceHolder**

Camel现在**camel-core**提供了一个新的PropertiesComponent，它允许您在定义Camel Endpoint URI时使用属性占位符。

这就像使用Spring的<property-placeholder>标签一样工作。但是，Spring有一个局限性，它阻止了第3方框架充分利用Spring属性占位符。请参阅[如何将Spring属性占位符与Camel XML结合使用](https://camel.apache.org/manual/latest/faq/how-do-i-use-spring-property-placeholder-with-camel-xml.html)。


|  | **桥接Spring和Camel属性占位符**您可以将Spring属性占位符与Camel桥接，请参见下面的更多详细信息。 |
| - | ---------------------------------------------------------------------------------------------- |

通常在执行以下操作时使用属性占位符：

l 查找或创建端点

l 在注册表查找Bean

l Spring XML支持的其他功能（请参见下面的示例）

l 将Blueprint PropertyPlaceholder与Camel [Properties](https://camel.apache.org/manual/latest/properties-component.html)组件一起使用

l 使用@PropertyInject在一个POJO注入属性

l 如果属性不存在，则使用默认值

l 包括开箱即用的功能，以从OS环境变量，JVM系统属性或服务习惯用语中查找属性值。

l 使用自定义函数，可以将其插入属性组件。

## 5.3. **语****法**

使用Camel的属性占位符的语法是{{key}}例如使用{{file.uri}}其中 file.uri是属性的键。

您可以在端点URI的某些部分中使用属性占位符，例如，可以将占位符用于URI中的参数。

如果不存在带有键的属性，则可以指定要使用的默认值，例如file.url:/some/path，默认值是冒号后面的文本（例如/some/path）。


|  | 请勿在属性键中使用冒号。提供默认值时，冒号用作分隔符。 |
| - | ------------------------------------------------------ |

## 5.4. **位置****定义**

属性组件需要知道解析属性的位置。您可以定义1对多位置。如果在单个String属性中定义位置，则可以用逗号分隔多个位置，例如：

pc.setLocation("com/mycompany/myprop.properties,com/mycompany/other.properties");

您可以通过设置optional属性来设置被去除的的位置（如果丢失），默认情况下为false，即：

pc.setLocations(

**    **"com/mycompany/override.properties;optional=true"

**    **"com/mycompany/defaults.properties");

## 5.5. **在位置上使用系统和环境变量**

现在，位置location支持使用JVM系统属性或OS环境变量。

例如：

location=file:${karaf.home}/etc/foo.properties

在上面的位置，我们使用JVM系统属性键karaf.home定义了一个位置。

要使用OS环境变量，您必须以env作为前缀：

location=file:${env:APP_HOME}/etc/foo.properties

这里APP_HOME操作系统环境变量。


|  | 某些操作系统（例如Linux）不支持在环境变量名称中使用破折号，像我们在这里使用的APP_HOME。但是，如果您指定，APP-HOME则Camel 3将自动将查找APP_HOME（带有下划线）作为后备值。 |
| - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

您可以在同一位置使用多个占位符，例如：

location=file:${env:APP_HOME}/etc/${prop.name}.properties

## 5.6. **在****Java** **DSL中配置**

您必须在名称properties下创建并注册PropertiesComponent，例如：

PropertiesComponent pc = camelContext.getPropertiesComponent();

pc.setLocation("classpath:com/mycompany/myprop.properties");

## 5.7. **在****Spring Xml****中配置**

Spring XML提供了两种配置方式。您可以将PropertiesComponent定义为spring bean类似于Java DSL中完成的方式。或者，您可以使用<propertyPlaceholder>标签。

<bean id="properties" class="org.apache.camel.component.properties.PropertiesComponent">

<property name="location" value="classpath:com/mycompany/myprop.properties"/>

</bean>

使用<propertyPlaceholder>标签可以使配置更加新鲜，例如：

<camelContext ...>

**   **<propertyPlaceholder id="properties" location="com/mycompany/myprop.properties"/>

</camelContext>

通过location标记设置属性位置可以很好地工作，但是有时您需要考虑很多资源，从**Camel 2.19.0**开始，可以使用专用的propertiesLocation设置属性位置：

<camelContext ...>

**  **<propertyPlaceholder id="myPropertyPlaceholder">

**    **<propertiesLocation

  resolver = "classpath"

  path     = "com/my/company/something/my-properties-1.properties"

  optional = "false"/>
**    **<propertiesLocation

  resolver = "classpath"

  path     = "com/my/company/something/my-properties-2.properties"

  optional = "false"/>
**    **<propertiesLocation

  resolver = "file"

  path     = "${karaf.home}/etc/my-override.properties"

  optional = "true"/>
**   **</propertyPlaceholder>

</camelContext>


|  | **在XML中指定缓存选项**Camel支持在Spring和Blueprint XML中**指定缓存选项**的值。 |
| - | ------------------------------------------------------------------------------- |

## 5.8. **使用注册表中的属性**

例如，在OSGi中，您可能希望公开一个将属性返回为java.util.Properties对象的服务。

然后，您可以按如下所示设置[属性](https://camel.apache.org/manual/latest/properties-component.html)组件：

** **<propertyPlaceholder id="properties" location="ref:myProperties"/>

这里myProperties是用于在OSGi注册表中查找的ID 。注意，我们使用ref:前缀来告诉Camel，它应该查找注册表的属性。

## 5.9. **使用属性组件的示例**

在端点URI中使用属性占位符时，可以使用属性:组件，也可以直接在URI中定义占位符。我们将从前者开始展示这两种情况的示例。

*// properties*

cool.end=mock:result

*// route*

from("direct:start").to("{{cool.end}}");

您还可以将占位符用作端点uri的一部分：

*// properties*

cool.foo=result

*// route*

from("direct:start").to("mock:{{cool.foo}}");

在上面的示例中，to端点将解析为mock:result。

您还可以具有相互引用的属性，例如：

*// properties*

cool.foo=result

cool.concat=mock:{{cool.foo}}

*// route*

from("direct:start").to("mock:{{cool.concat}}");

注意cool.concat如何引用另一个属性。

您可以多次使用占位符：

*// properties*

cool.start=direct:start

cool.showid=true

cool.result=result

*// route*

from("{{cool.start}}")

**    **.to("log:{{cool.start}}?showBodyType=false&showExchangeId={{cool.showid}}")

**    **.to("mock:{{cool.result}}");

您还可以在使用ProducerTemplate时使用属性占位符，例如：

template.sendBody("{{cool.start}}", "Hello World");

## 5.10. [**简单**](https://camel.apache.org/manual/latest/simple-language.html)**语言示例**

现在，[简单](https://camel.apache.org/manual/latest/simple-language.html)语言还支持使用属性占位符，例如，在以下路由中：

*// properties*

cheese.quote=Camel rocks

*// route*

from("direct:start")

**    **.transform().simple("Hi ${body} do you think ${properties:cheese.quote}?");

## 5.11. **Spring** **XML支持的其他属性占位符**

在许多Camel Spring XML标签（例如<package>, <packageScan>, <contextScan>, <jmxAgent>, <endpoint>, <routeBuilder>, <proxy>和其他标签）中也支持属性占位符。

以下示例在<jmxAgent>标记中具有属性占位符：

您还可以在<camelContext>标记的各种属性中定义属性占位符，trace如下所示：

## 5.12. **使用JVM系统属性或环境变量作为覆盖或回退值**

属性组件支持使用JVM系统属性以及OS环境变量作为值，这些值可以用作覆盖值或后备值。

默认模式是它们两个都处于覆盖模式，并且按照以下顺序检查它们：

1. 操作系统环境变量（覆盖模式）
2. JVM系统属性（覆盖模式）
3. 属性文件和其他位置
4. 操作系统环境变量（后备模式）
5. JVM系统属性（回退模式）

该检查在该键的第一个找到的属性值处停止。

您可以使用属性组件上的systemPropertiesMode和environmentVariableMode选项来控制这些模式。

## 5.13. **对****Xml** **DSL中的任何类型的属性使用属性占位符**

在下面的示例中，我们使用prop作为命名空间camel.apache.org/schema/placeholder 的前缀，通过该prop前缀，我们可以在XML DSL的属性中使用前缀。请注意，我们如何在"广播"中使用它来指示选项stopOnException应为带有"stop"键的占位符的值。

在属性文件中，我们将值定义为

stop=true

## 5.14. **在****Camel****路****由****中使用****Blueprint****属性占位符**

Camel支持Blueprint，Blueprint也提供属性占位符服务。Camel支持约定优于配置，因此您要做的就是在XML文件中定义OSGi Blueprint属性占位符，如下所示：

<blueprint xmlns="http://www.osgi.org/xmlns/blueprint/v1.0.0"

       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xmlns:cm="http://aries.apache.org/blueprint/xmlns/blueprint-cm/v1.0.0"

       xsi:schemaLocation="

       http://www.osgi.org/xmlns/blueprint/v1.0.0 https://www.osgi.org/xmlns/blueprint/v1.0.0/blueprint.xsd">
**    ***<!-- OSGI blueprint property placeholder -->*

**    **<cm:property-placeholder id="myblueprint.placeholder" persistent-id="camel.blueprint">

**        ***<!-- list some properties as needed -->*

**        **<cm:default-properties>

**            **<cm:property name="result" value="mock:result"/>

**        **[/cm:default-properties](/cm:default-properties)

**    **[/cm:property-placeholder](/cm:property-placeholder)

**    **<camelContext xmlns="http://camel.apache.org/schema/blueprint">

**        ***<!-- in the route we can use {{ }} placeholders which will lookup in blueprint*

*         as Camel will auto detect the OSGi blueprint property placeholder and use it -->*
**        **<route>

**            **<from uri="direct:start"/>

**            **<to uri="mock:foo"/>

**            **<to uri="{{result}}"/>

**        **</route>

</camelContext>

</blueprint>

### 5.14.1. **在****Camel****路线中使用OSGI****Blueprint****属性占位符**

默认情况下，Camel检测并使用OSGi Blueprint属性占位符服务。您可以通过useBlueprintPropertyResolver在<camelContext>定义中将属性设置为false 来禁用此功能。

### 5.14.2. **关于占位符语法**

注意，我们如何在Camel路由中使用Camel占位符语法 {{** **和 }}** **，这将从OSGi Blueprint中查找值。

占位符的Blueprint语法为${ }。因此，您必须在<camelContext>外部使用${ }语法。在内部<camelContext>必须使用 {{** **和 }}** **语法。

OSGi Blueprint允许您配置语法，因此您可以根据需要实际对齐它们。

您还可以通过其ID显式引用特定的OSGi Blueprint属性占位符。为此，您需要使用<propertyPlaceholder>以下示例中所示的Camel ：

<blueprint xmlns="http://www.osgi.org/xmlns/blueprint/v1.0.0"

       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

       xmlns:cm="http://aries.apache.org/blueprint/xmlns/blueprint-cm/v1.0.0"

       xsi:schemaLocation="

       http://www.osgi.org/xmlns/blueprint/v1.0.0 https://www.osgi.org/xmlns/blueprint/v1.0.0/blueprint.xsd">
**    ***<!-- OSGI blueprint property placeholder -->*

**    **<cm:property-placeholder id="myblueprint.placeholder" persistent-id="camel.blueprint">

**        ***<!-- list some properties as needed -->*

**        **<cm:default-properties>

**            **<cm:property name="prefix.result" value="mock:result"/>

**        **[/cm:default-properties](/cm:default-properties)

**    **[/cm:property-placeholder](/cm:property-placeholder)

**    **<camelContext xmlns="http://camel.apache.org/schema/blueprint">

**        ***<!-- using Camel properties component and refer to the blueprint property placeholder by its id -->*

**        **<propertyPlaceholder id="properties" location="blueprint:myblueprint.placeholder"/>

**        ***<!-- in the route we can use {{ }} placeholders which will lookup in blueprint -->*

**        **<route>

**            **<from uri="direct:start"/>

**            **<to uri="mock:foo"/>

**            **<to uri="{{prefix.result}}"/>

**        **</route>

</camelContext>

</blueprint>

## 5.15. **明确引用****Camel****中的OSGI****Blueprint****占位符**

注意我们如何使用blueprint方案通过其ID引用OSGi Blueprint占位符。这允许您混合搭配，例如，您还可以在该位置添加其他方案。例如，要从类路径加载文件，您可以执行以下操作：

location="blueprint:myblueprint.placeholder,classpath:myproperties.properties"

每个位置均以逗号分隔。

## 5.16. **在****CamelContext外覆盖Blueprint****属性占位符**

在Blueprint XML文件中使用Blueprint属性占位符时，可以直接在XML文件中声明属性，如下所示：

请注意，我们有一个<bean>引用其中一个属性。在Camel路由中，我们使用 {{** **和 }}表示法引用另一个。

现在，如果要从单元测试中覆盖这些"Blueprint"属性，则可以执行以下操作：

为此，我们重写并实现useOverridePropertiesWithConfigAdmin方法。然后，我们可以将要覆盖的属性放在给定的props参数上。并且返回值**必须**是您在Blueprint XML文件中定义<cm:property-placeholder>标签的persistence-id。

## 5.17. **将.****cfg或.properties文件用于Blueprint****属性占位符**

在Blueprint XML文件中使用Blueprint属性占位符时，可以在.properties或.cfg文件中声明属性。如果你使用Apache ServieMix / Karaf那么这个容器有它与命名etc目录文件加载性能的约定etc/pid.cfg，其中pid为persistence-id。

例如，在Blueprint XML文件中，我们具有persistence-id="stuff"，这意味着它将把配置文件加载为etc/stuff.cfg。

现在，如果您要对该Blueprint XML文件进行单元测试，则可以覆盖loadConfigAdminConfigurationFile并告诉Camel如下所示加载哪个文件：

请注意，此方法需要返回带有2个值的String[]。第一个值是配置文件要加载的路径。第二个值是在<cm:property-placeholder>标签的persistence-id。

该stuff.cfg文件只是具有属性占位符的普通属性文件，例如：

== this is a comment

greeting=Bye

## 5.18. **使****用.cfg****文件和****Blueprint****属性占位符的替代属性**

您也可以同时做。这是一个完整的例子。首先，我们有Blueprint XML文件：

在单元测试类中，我们执行以下操作：

并且etc/stuff.cfg配置文件包含

greeting=Byeecho=Yaydestination=mock:result

## 5.19. **桥接Spring和Camel属性占** **位符**

Spring框架不允许诸如Apache Camel之类的第三方框架无缝连接到Spring属性占位符机制。然而，你可以很容易地通过声明一个Spring bean桥接Spring和Camel，这个bean类型是org.apache.camel.spring.spi.BridgePropertyPlaceholderConfigurer，它又是Spring的一个org.springframework.beans.factory.config.PropertyPlaceholderConfigurer的类型。

要桥接Spring和Camel，您必须定义一个bean，如下所示：

**桥接Spring和Camel属性占位符**

您**不能同时**使用spring <context：property-placeholder>命名空间。这是不可能的。

声明此bean之后，可以在<camelContext>标记内使用Spring样式和Camel样式定义属性占位符，如下所示：

**使用桥****接****属性占位符**

请注意，hello bean如何通过${ }符号使用纯Spring属性占位符。而在Camel的路线我们使用Camel占位符符号 {{** **和 }}。

## 5.20. **Spring属性占** **位符****与****Camel****简单语言****的****冲突**

使用Spring桥接占位符时要注意，Spring ${ }语法与Camel [Simple](https://camel.apache.org/manual/latest/simple-language.html)中的冲突，因此要小心。例如：

<setHeader name="Exchange.FILE_NAME">

**  **<simple>{{file.rootdir}}/${in.header.CamelFileName}</simple>

</setHeader>

与Spring属性占位符冲突，您应该使用Camel $simple{ }来指示使用[简单](https://camel.apache.org/manual/latest/simple-language.html)语言。

<setHeader name="Exchange.FILE_NAME">

**  **<simple>{{file.rootdir}}/$simple{in.header.CamelFileName}</simple>

</setHeader>

另一种方法是使用ignoreUnresolvablePlaceholders选项将PropertyPlaceholderConfigurer配置为true。

## 5.21. **重写****Camel Test Kit****中的属性**

使用Camel进行测试并使用"[属性"](https://camel.apache.org/manual/latest/properties-component.html)组件时，您可能希望能够直接在单元测试源代码中提供要使用的属性。Camel测试套件，例如，CamelTestSupport类提供以下方法

l useOverridePropertiesWithPropertiesComponent

l ignoreMissingLocationWithPropertiesComponent

因此，例如在单元测试类中，您可以重写useOverridePropertiesWithPropertiesComponent方法并返回一个java.util.Properties包含应首选使用的属性。

### 5.21.1. **从单元测试源****代码****中提供属性**

这可以通过任何Camel测试套件来完成，例如camel-test, camel-test-spring, 和 camel-test-blueprint。

ignoreMissingLocationWithPropertiesComponent可用于指示Camel忽略不可发现的任何位置，例如，如果你运行单元测试，在环境里访问不到属性的位置时。

## 5.22. **使用@****Propertyinject**

Camel允许在POJO中注入属性占位符，使用@PropertyInject注解在字段和setter方法上设置注入。

例如，您可以将其与RouteBuilder类一起使用，如下所示：

public** **class MyRouteBuilder extends RouteBuilder {

**    **@PropertyInject("hello")

**    **private** **String greeting;

**    **@Override

**    **public void configure() throws Exception {

**        **from("direct:start")

**            **.transform().constant(greeting)

**            **.to("{{result}}");

**    **}

}

注意，我们已经用@PropertyInject注入了greeting字段，并定义它以使用"hello"键 。然后，Camel使用此键查找属性，将其转换为String类型，并注入其值。

您还可以在键中使用多个占位符和文本，例如，我们可以执行以下操作：

@PropertyInject("Hello {{name}} how are you?")

private** **String greeting;

这将使用键"name"查找占位符

如果键不存在，您还可以添加默认值，例如：

@PropertyInject(value = "myTimeout", defaultValue = "5000")

private** **int** **timeout;

## 5.23. **使用开箱即用的功能**

[属性](https://camel.apache.org/manual/latest/properties-component.html)组件包括以下功能开箱

l env - 从OS环境变量中查找属性的功能

l sys - 从Java JVM系统属性中查找属性的功能

l service - 使用服务命名习惯用法从OS环境变量中查找属性的功能

l service.name - 使用服务命名习惯用法从OS环境变量中查找属性的功能，仅返回主机名部分

l service.port - 使用服务命名习惯用法从OS环境变量中查找属性的功能，仅返回端口部分

如您所见，这些功能旨在简化从环境中查找值的过程。由于它们是开箱即用的，因此可以轻松使用，如下所示：

**  **<camelContext xmlns="http://camel.apache.org/schema/blueprint">

**    **<route>

**      **<from uri="direct:start"/>

**      **<to uri="{`{env:SOMENAME}`}"/>

**      **<to uri="{`{sys:MyJvmPropertyName}`}"/>

**    **</route>

**  **</camelContext>

您也可以使用默认值，如果该属性不存在值，则可以定义一个默认值，如下所示，其中默认值为log:foo和log:bar。

**  **<camelContext xmlns="http://camel.apache.org/schema/blueprint">

**    **<route>

**      **<from uri="direct:start"/>

**      **<to uri="{`{env:SOMENAME:log:foo}`}"/>

**      **<to uri="{`{sys:MyJvmPropertyName:log:bar}`}"/>

**    **</route>

**  **</camelContext>

服务功能用于使用服务命名惯用语查找OS环境变量定义的服务，以使用 hostname : port引用服务位置

l NAME **_SERVICE_HOST**

l NAME **_SERVICE_PORT**

换句话说，服务使用_SERVICE_HOST和_SERVICE_PORT作为前缀。因此，如果该服务名为FOO，则应将OS环境变量设置为

export** **$FOO_SERVICE_HOST=myserverexport** **$FOO_SERVICE_PORT=8888

例如，如果FOO服务是远程HTTP服务，那么我们可以在Camel端点uri中引用该服务，并使用HTTP组件进行HTTP调用：

<camelContext xmlns="http://camel.apache.org/schema/blueprint">

**  **<route>

**    **<from uri="direct:start"/>

**    **<to uri="http://{`{service:FOO}`}/myapp"/>

**  **</route>

</camelContext>

如果服务尚未定义，我们可以使用默认值，例如在本地主机上调用服务，可能用于单元测试等。

<camelContext xmlns="http://camel.apache.org/schema/blueprint">

**  **<route>

**    **<from uri="direct:start"/>

**    **<to uri="http://{`{service:FOO:localhost:8080}`}/myapp"/>

**  **</route>

</camelContext>

## 5.24. **使用自定义功能（高级）**

通过" [属性"](https://camel.apache.org/manual/latest/properties-component.html)组件，可以插入第三方功能，以供解析属性占位符期间使用。然后，这些功能能够执行自定义逻辑来解析占位符，例如在数据库中查找，执行自定义计算等。功能名称成为占位符中使用的前缀。最好在下面的示例代码中说明

<bean id="beerFunction" class="MyBeerFunction"/>

<camelContext xmlns="http://camel.apache.org/schema/blueprint">

**  **<propertyPlaceholder id="properties">

**    **<propertiesFunction ref="beerFunction"/>

**  **</propertyPlaceholder>

**  **<route>

**    **<from uri="direct:start"/>

**    **<to uri="{`{beer:FOO}`}"/>

**    **<to uri="{`{beer:BAR}`}"/>

**  **</route>

</camelContext>


|  | 位置属性（在propertyPlaceholder标签上）不是必需的 |
| - | ------------------------------------------------- |

在这里，我们有一个Camel XML路由，在其中定义了<propertyPlaceholder>使用自定义功能，我们将引用其bean id - 例如beerFunction。由于啤酒功能用"beer"作其名称，因此占位符语法可以通过以beer:value开头来触发啤酒功能。

该功能的实现只有两种方法，如下所示：

public** **static** **final** **class MyBeerFunction implements PropertiesFunction {

**    **@Override

**    **public String getName() {

**        **return** **"beer";

**    **}

**    **@Override

**    **public String apply(String remainder) {

**        **return** **"mock:"** **+ remainder.toLowerCase();

**    **}

}

该功能必须实现org.apache.camel.component.properties.PropertiesFunction接口。方法getName是功能的名称，例如beer。apply方法是我们实现自定义逻辑的地方。由于示例代码来自单元测试，因此它仅返回一个值来引用mock端点。

要从Java代码注册自定义功能，如下所示：

PropertiesComponent pc = (org.apache.camel.componennt.properties.PropertiesComponent) context.getPropertiesComponent();

pc.addFunction(new** **MyBeerFunction());

## 5.25. **使用第三方属性资源**

属性组件允许插件式使用第三方资源通过camel-api中的API PropertySource加载和查找属性。例如，camel-microprofile-config组件是使用此组件实现的。Camel启动时，可以从类路径中自动发现第三方PropertySource。这可以通过包含文件META-INF/services/org/apache/camel/property-source-factory来完成，该文件引用PropertySource实现的完全限定的类名。参见camel-microprofile-config示例。

您还可以通过Java API注册第三方属性源

PropertiesComponent pc = ...

pc.addPropertySource(myPropertySource);

### 5.25.1. **loadable****property****source**

 PropertySource可以定义从源（例如从文件系统）一次加载其所有属性。这允许Camel属性组件在启动期间立即加载这些属性。

### 5.25.2. **PropertySource**

常规PropertySource将按需查找属性，例如从后端源（例如数据库或HashiCorp Vault等）查找值。

# 6. **Ref****语言**

**自****Camel****2.8**

Ref表达式语言实际上只是从注册表中查找自定义表达式或断言的一种方法。

这在Xml DSL中特别有用。

## 6.1. **Ref****语言选项**

引用语言支持以下1个选项。


| **名称** | **默认** | **Java类型** | **描述**                                 |
| -------- | -------- | ------------ | ---------------------------------------- |
| trim     | true     | Boolean      | 是否修剪值以除去开头和结尾的空格和换行符 |

## 6.2. **用法示例**

Xml DSL中的Splitter可以使用以下自定义<ref>表达式：

<bean id="myExpression" class="com.mycompany.MyCustomExpression"/>

<route>

**  **<from uri="seda:a"/>

**  **<split>

**    **<ref>myExpression</ref>

**    **<to uri="mock:b"/>

**  **</split>

</route>

在这种情况下，来自seda:a端点的消息将使用在注册表中具有myExpression的ID自定义表达式进行拆分。

使用Java DSL的相同示例：

from("seda:a").split().ref("myExpression").to("seda:b");

## 6.3. **依赖****关系**

Ref语言是**camel-core的**一部分。

# 7. **Simple****语言**

**自****Camel****1.1**

创建时，"简单表达语言（Simple Expression Language）"是一种非常简单的语言，但此后变得更加强大。它的主要目的是成为一种非常小巧的语言，用于计算表达式和断言，不需要任何新的依赖或[XPath的](https://camel.apache.org/components/latest/xpath-language.html)知识; 因此，它是在camel-core中进行测试的理想选择。当您需要在Camel路由中使用一些基于表达式的脚本时，我们的想法是覆盖95%的常见用例。

但是，对于更复杂的用例，通常建议您选择一种更具表达能力的强大语言，例如：

l [Groovy](https://camel.apache.org/components/latest/groovy-language.html)

l [SpEL](https://camel.apache.org/components/latest/spel-language.html)

l [MVEL](https://camel.apache.org/components/latest/mvel-component.html)

l [OGNL](https://camel.apache.org/components/latest/ognl-language.html)

简单语言对复杂表达式使用${body}占位符，其中表达式包含常量文字。如果表达式仅是token本身，则可以省略$\{}占位符。


|  | **替代语法**您还可以使用$simple{ }用作占位符的替代语法。例如，在将Spring属性占位符与Camel一起使用时，可以在这种情况下避免冲突。 |
| - | ------------------------------------------------------------------------------------------------------------------------------- |

## 7.1. **简单语言选项**

简单语言支持2个选项，如下所示。


| **名称**   | **默认** | **Java类型** | **描述**                                 |
| ---------- | -------- | ------------ | ---------------------------------------- |
| resultType |          | String       | 设置结果类型的类名（类型从输出）         |
| trim       | true     | Boolean      | 是否修剪值以除去开头和结尾的空格和换行符 |

## 7.2. **变量**


| **变量**                                      | **类型** | **描述**                                                                                                                                                                                                                                                                                                                   |
| --------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| camelId                                       | String   | CamelContext名称                                                                                                                                                                                                                                                                                                           |
| camelContext.**OGNL**                         | Object   | 使用Camel OGNL表达式调用的CamelContext。                                                                                                                                                                                                                                                                                   |
| exchange                                      | Exchange | the Exchange                                                                                                                                                                                                                                                                                                               |
| exchange.**OGNL**                             | Object   | 使用Camel OGNL表达式调用的Exchange。                                                                                                                                                                                                                                                                                       |
| exchangeId                                    | String   | the exchange id                                                                                                                                                                                                                                                                                                            |
| id                                            | String   | 输入消息ID                                                                                                                                                                                                                                                                                                                 |
| body                                          | Object   | the input body                                                                                                                                                                                                                                                                                                             |
| in.body                                       | Object   | **不推荐使用** 输入body                                                                                                                                                                                                                                                                                                    |
| body.**OGNL**                                 | Object   | 使用Camel OGNL表达式调用的输入body。                                                                                                                                                                                                                                                                                       |
| in.body.**OGNL**                              | Object   | **不推荐使用**Camel OGNL表达式调用的输入body。                                                                                                                                                                                                                                                                             |
| bodyAs(*type*)                                | Type     | 将body转换为由其类名确定的给定类型。转换后的body可以为null。                                                                                                                                                                                                                                                               |
| bodyAs(*type*).**OGNL**                       | Object   | 将body转换为由其类名确定的给定类型，然后使用Camel OGNL表达式调用方法。转换后的body可以为null。                                                                                                                                                                                                                             |
| bodyOneLine                                   | String   | 将body转换为字符串，并删除所有换行符，以便字符串位于一行中。                                                                                                                                                                                                                                                               |
| mandatoryBodyAs(*type*)                       | Type     | 将body转换为由其类名确定的给定类型，并期望body不为null。                                                                                                                                                                                                                                                                   |
| mandatoryBodyAs(*type*).**OGNL**              | Object   | 将body转换为由其类名确定的给定类型，然后使用Camel OGNL表达式调用方法。                                                                                                                                                                                                                                                     |
| header.foo                                    | Object   | 引用输入foo报头                                                                                                                                                                                                                                                                                                            |
| header:foo                                    | Object   | 引用输入foo报头                                                                                                                                                                                                                                                                                                            |
| header[foo]                                   | Object   | 引用输入foo报头                                                                                                                                                                                                                                                                                                            |
| headers.foo                                   | Object   | 引用输入foo报头                                                                                                                                                                                                                                                                                                            |
| headers:foo                                   | Object   | 引用输入foo报头                                                                                                                                                                                                                                                                                                            |
| headers[foo]                                  | Object   | 引用输入foo报头                                                                                                                                                                                                                                                                                                            |
| in.header.foo                                 | Object   | **不推荐使用，**引用输入foo报头                                                                                                                                                                                                                                                                                            |
| in.header:foo                                 | Object   | **不推荐使用，**引用输入foo报头                                                                                                                                                                                                                                                                                            |
| in.header[foo]                                | Object   | **不推荐使用，**引用输入foo报头                                                                                                                                                                                                                                                                                            |
| in.headers.foo                                | Object   | **不推荐使用，**引用输入foo报头                                                                                                                                                                                                                                                                                            |
| in.headers:foo                                | Object   | **不推荐使用，**引用输入foo报头                                                                                                                                                                                                                                                                                            |
| in.headers[foo]                               | Object   | **不推荐使用，**引用输入foo报头                                                                                                                                                                                                                                                                                            |
| header.foo[bar]                               | Object   | 将输入foo报头视为map，并使用bar作为键在map上执行查找                                                                                                                                                                                                                                                                       |
| in.header.foo[bar]                            | Object   | **不推荐使用** 将输入foo报头视为map，并使用bar作为键在map上执行查找                                                                                                                                                                                                                                                        |
| in.headers.foo[bar]                           | Object   | **不推荐使用** 将输入foo报头视为map，并使用bar作为键在map上执行查找                                                                                                                                                                                                                                                        |
| header.foo.**OGNL**                           | Object   | 引用输入的foo报头，并使用Camel OGNL表达式调用其值。                                                                                                                                                                                                                                                                        |
| in.header.foo.**OGNL**                        | Object   | **不推荐使用，**引用输入foo报头，并使用Camel OGNL表达式调用其值。                                                                                                                                                                                                                                                          |
| in.headers.foo.**OGNL**                       | Object   | **不推荐使用，**引用输入foo报头，并使用Camel OGNL表达式调用其值。                                                                                                                                                                                                                                                          |
| headerAs(*key*,*type*)                        | Type     | 将报头转换为由其类名确定的给定类型                                                                                                                                                                                                                                                                                         |
| headers                                       | Map      | 引用输入header                                                                                                                                                                                                                                                                                                             |
| in.headers                                    | Map      | **不推荐使用，**引用输入header                                                                                                                                                                                                                                                                                             |
| exchangeProperty.foo                          | Object   | 引用Exchange的foo属性                                                                                                                                                                                                                                                                                                      |
| exchangeProperty[foo]                         | Object   | 引用Exchange的foo属性                                                                                                                                                                                                                                                                                                      |
| exchangeProperty.foo.**OGNL**                 | Object   | 引用交换上的foo属性，并使用Camel OGNL表达式调用其值。                                                                                                                                                                                                                                                                      |
| sys.foo                                       | String   | 引用JVM系统属性                                                                                                                                                                                                                                                                                                            |
| sysenv.foo                                    | String   | 引用系统环境变量                                                                                                                                                                                                                                                                                                           |
| env.foo                                       | String   | 引用系统环境变量                                                                                                                                                                                                                                                                                                           |
| exception                                     | Object   | 引用交换上的异常对象，如果未在交换上设置异常，则为**null**。如果Exchange有任何异常，将回退并捕获捕获的异常（Exchange.EXCEPTION_CAUGHT）。                                                                                                                                                                                  |
| exception.**OGNL**                            | Object   | 引用使用Camel OGNL表达式对象调用的交换异常                                                                                                                                                                                                                                                                                 |
| exception.message                             | String   | 引用交换上的exception.message，如果未在交换上设置任何异常，则为**null**。如果Exchange有任何异常，将回退并捕获捕获的异常（Exchange.EXCEPTION_CAUGHT）。                                                                                                                                                                     |
| exception.stacktrace                          | String   | 引用交换上的exception.stracktrace，如果在交换上未设置任何异常，则为**null**。如果Exchange有任何异常，将回退并捕获捕获的异常（Exchange.EXCEPTION_CAUGHT）。                                                                                                                                                                 |
| date:_command_                                | Date     | 评估为Date对象。支持的命令是：**now**用于当前时间戳，在**in.header.xxx**或**header.xxx**中使用带xxx键的Date对象报头。**exchangeProperty.xxx**可以将交换属性中的Date对象与xxx键一起使用。**文件**的最后修改时间戳（可用于文件使用方）。命令接受偏移量，例如：**now-24h**或**in.header.xxx + 1h**或甚至**now + 1h30m-100**。 |
| date:_command:pattern_                        | String   | 使用java.text.SimpleDataFormat模式格式化日期。                                                                                                                                                                                                                                                                             |
| date-with-timezone:_command:timezone:pattern_ | String   | 使用java.text.SimpleDataFormat时区和模式进行日期格式化。                                                                                                                                                                                                                                                                   |
| bean:_bean expression_                        | Object   | 使用Bean语言调用Bean表达式。指定方法名称时，必须使用点作为分隔符。我们还支持Bean组件使用的?method=methodname语法。                                                                                                                                                                                                         |
| properties:key:default                        | String   | 使用给定的键查找属性。如果键不存在或没有值，则可以指定可选的默认值。                                                                                                                                                                                                                                                       |
| routeId                                       | String   | 返回Exchange正在路由的当前路由的ID。                                                                                                                                                                                                                                                                                       |
| stepId                                        | String   | 返回Exchange正在路由的当前步骤的ID。                                                                                                                                                                                                                                                                                       |
| threadName                                    | String   | 返回当前线程的名称。可用于日志用途。                                                                                                                                                                                                                                                                                       |
| ref:xxx                                       | Object   | 从注册表中查找具有给定ID的bean。                                                                                                                                                                                                                                                                                           |
| type:name.field                               | Object   | 通过FQN名称引用类型或字段。要引用字段，您可以附加.FIELD_NAME。例如，您可以将Exchange中的常量字段引用为：org.apache.camel.Exchange.FILE_NAME                                                                                                                                                                                |
| null                                          | null     | 代表一个**null**                                                                                                                                                                                                                                                                                                           |
| random_(value)_                               | Integer  | 返回介于0（包含）和*值*（不包含）之间的随机Integer                                                                                                                                                                                                                                                                         |
| random_(min,max)_                             | Integer  | 返回介于*min*（包含）和*max*（不包含）之间的随机Integer                                                                                                                                                                                                                                                                    |
| collate(group)                                | List     | collate函数迭代消息正文并将数据分组为指定大小的子列表。可以将其与Splitter EIP一起使用，以将消息正文拆分，然后将拆分后的子消息分组/批量N个子列表。此方法的工作方式与Groovy中的collate方法类似。                                                                                                                             |
| skip(number)                                  | Iterator | 跳过功能迭代消息正文，并跳过第一个条目数。可以与Splitter EIP一起使用，以拆分消息正文并跳过前N个条目。                                                                                                                                                                                                                      |
| messageHistory                                | String   | 当前交换的消息历史记录，其路由方式。这类似于错误处理程序在未处理异常的情况下记录的路由堆栈跟踪消息历史记录。                                                                                                                                                                                                               |
| messageHistory(false)                         | String   | 作为messageHistory，但没有交换详细信息（仅包括路由strack-trace）。如果您不想从消息本身记录敏感数据，可以使用此方法。                                                                                                                                                                                                       |

## 7.3. **OGNL表达****式****支持**

资讯：Camel的OGNL支持仅用于调用方法。您无法访问字段。Camel支持访问Java数组的长度字段。

现在，[Simple](https://camel.apache.org/manual/latest/simple-language.html)和[Bean](https://camel.apache.org/manual/latest/simple-language.html)语言支持Camel OGNL表示法，以类似链式的方式调用Bean。假设Message IN主体包含一个具有getAddress()方法的POJO 。

然后，您可以使用Camel OGNL表示法访问地址对象：

simple("${body.address}")

simple("${body.address.street}")

simple("${body.address.zip}")

Camel理解getter的简写名称，但是您可以调用任何方法或使用真实名称，例如：

simple("${body.address}")

simple("${body.getAddress.getStreet}")

simple("${body.address.getZip}")

simple("${body.doSomething}")

如果例如正文body没有地址，您也可以使用null安全运算符（?.）避免NPE

simple("${body?.address?.street}")

也可以索引Map或List类型，因此您可以执行以下操作：

simple("${body[foo].name}")

假定主体是基于Map，并使用键foo查找值，然后在该值上调用getName方法。

如果键有空格，则**必须**用引号将键括起来，例如'foo bar'：

simple("${body['foo bar'].name}")

您可以使用其键名（带或不带点）直接访问Map或List对象：

simple("${body[foo]}")

simple("${body[this.is.foo]}")

假设键foo没有值，则可以使用null安全运算符避免NPE，如下所示：

simple("${body[foo]?.name}")

您还可以访问List类型，例如从可以执行的地址中获取行：

simple("${body.address.lines[0]}")

simple("${body.address.lines[1]}")

simple("${body.address.lines[2]}")

有一个特殊的last关键字，可用于从列表中获取最后一个值。

simple("${body.address.lines[last]}")

要获得倒数第二个，您可以减去一个数字，因此我们可以使用last-1来表示：

simple("${body.address.lines[last-1]}")

第三名当然是：

simple("${body.address.lines[last-2]}")

您可以使用以下命令在列表上调用size方法

simple("${body.address.lines.size}")

Camel也支持Java数组的length字段，例如：

String[] lines = new** **String[]{"foo", "bar", "cat"};

exchange.getIn().setBody(lines);

simple("There are ${body.length} lines")

是的，您可以将其与操作符结合使用，如下所示：

simple("${body.address.zip} > 1000")

## 7.4. **操作****符****支持**

解析器被限制为仅支持单个运算符。

要启用它，必须将左值括在$\{}中。语法为：

${leftValue}** **OP rightValue

其中rightValue可以是一个字符串文字封入引号' '，null，常量值或封闭在$\{}的另一种表达。


|  | **必须**是前后空格分割。 |
| - | ------------------------ |

Camel会自动将rightValue类型转换为leftValue类型，因此可以将字符串转换为数字，以便可以对数字值使用>比较。

支持以下运算符：


| **Operator** | **描述**                                                                                                                                                             |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ==           | 等于                                                                                                                                                                 |
| =~           | 等于忽略大小写（比较字符串值时将忽略大小写）                                                                                                                         |
| >            | 大于                                                                                                                                                                 |
| >=           | 大于或等于                                                                                                                                                           |
| <            | 少于                                                                                                                                                                 |
| ⇐           | 小于或等于                                                                                                                                                           |
| !=~          | 不等于                                                                                                                                                               |
| !=~          | 不等于忽略大小写（比较字符串值时将忽略大小写）                                                                                                                       |
| contains     | 用于测试是否包含基于字符串的值                                                                                                                                       |
| !contains    | 用于测试是否不包含基于字符串的值                                                                                                                                     |
| ~~           | 用于通过忽略基于字符串的值中的区分大小写来测试是否包含                                                                                                               |
| !~~          | 通过忽略基于字符串的值中的区分大小写来测试是否包含                                                                                                                   |
| regex        | 用于匹配定义为String值的给定正则表达式模式                                                                                                                           |
| !regex       | 不匹配定义为字符串值的给定正则表达式模式                                                                                                                             |
| in           | 为了在一组值中进行匹配，每个元素必须用逗号分隔。如果要包括一个空值，则必须使用双逗号来定义它，例如"、、青铜，银，金"，这是一组四个具有空值的值，然后是三枚奖牌。     |
| !in          | 如果不在一组值中进行匹配，则每个元素必须用逗号分隔。如果要包括一个空值，则必须使用双逗号来定义它，例如"、、青铜，银，金"，这是一组四个具有空值的值，然后是三枚奖牌。 |
| is           | 如果左侧类型是该值的实例，则用于匹配。                                                                                                                               |
| !is          | 如果左侧类型不是该值的实例，则用于匹配。                                                                                                                             |
| range        | 为了匹配，如果左侧在定义为数字的值的范围内：from..to..                                                                                                               |
| !range       | 用于匹配如果左手侧是不是一个范围定义为数字值的范围内：from..to。。                                                                                                   |
| startsWith   | 用于测试左侧字符串是否以右侧字符串开头。                                                                                                                             |
| endsWith     | 用于测试左侧弦是否以右侧弦结尾。                                                                                                                                     |

并且可以使用以下一元运算符：


| **Operator** | **描述**                                                                                                                                                                                                                                                                             |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ++           | 将数字加一。左侧必须是一个函数，否则将解析为文字。                                                                                                                                                                                                                                   |
| —           | 将数字减一。左侧必须是一个函数，否则将解析为文字。                                                                                                                                                                                                                                   |
| \            | [转义一个值，例如\$表示一个$符号。特殊：\n用于换行，\t用于制表符，\r用于回车。注意：使用文件语言不支持转义。注意：不支持转义符，请使用以下三个特殊的转义符。](https://camel.apache.org/manual/latest/file-language.html "https://camel.apache.org/manual/latest/file-language.html") |
| \n           | 使用换行符。                                                                                                                                                                                                                                                                         |
| \t           | 使用制表符。                                                                                                                                                                                                                                                                         |
| \r           | 使用回车符。                                                                                                                                                                                                                                                                         |
| \}           | 要将}字符用作文本                                                                                                                                                                                                                                                                    |

并且可以使用以下逻辑运算符对表达式进行分组：


| **Operator** | **描述**                               |
| ------------ | -------------------------------------- |
| &&           | 逻辑和运算符用于对两个表达式进行分组。 |
|              |                                        |

AND的语法为：

${leftValue}** **OP rightValue && ${leftValue}** **OP rightValue

并且OR的语法是：

${leftValue} OP rightValue ||** **${leftValue} OP rightValue

一些例子：

*// exact equals match*

simple("${in.header.foo} == 'foo'")

*// ignore case when comparing, so if the header has value FOO this will match*

simple("${in.header.foo} =~ 'foo'")

*// here Camel will type convert '100' into the type of in.header.bar and if it is an Integer '100' will also be converter to an Integer*

simple("${in.header.bar} == '100'")

simple("${in.header.bar} == 100")

*// 100 will be converter to the type of in.header.bar so we can do > comparison*

simple("${in.header.bar} > 100")

### 7.4.1. **与不同类型的比较**

当您与诸如String和int之类的不同类型进行比较时，则必须多加注意。Camel将使用左侧的类型作为第一优先。如果无法根据该类型比较两个值，则退回到右侧类型。

这意味着您可以翻转值以强制使用特定类型。假设上面的bar值为String。然后可以翻转方程式：

simple("100 < ${in.header.bar}")

然后确保将int类型用作第一优先级。

如果Camel小组改进了二进制比较操作，而不是基于String的数字类型，则将来可能会改变。与数字比较时，最常见的字符串类型会引起问题。

*// testing for null*

simple("${in.header.baz} == null")

*// testing for not null*

simple("${in.header.baz} != null")

还有一个更高级的示例，其中正确的值是另一个表达式

simple("${in.header.date} == ${date:now:yyyyMMdd}")

simple("${in.header.type} == ${bean:orderService?method=getOrderType}")

并包含一个示例，测试header是否包含单词Camel

simple("${in.header.title} contains 'Camel'")

并以regex为例，测试数字报头是否为4位数字值：

simple("${in.header.number} regex '\\d{4}'")

最后一个示例，说明header是否等于列表中的任何值。每个元素必须用逗号分隔，并且周围没有空格。

这也适用于数字等，因为Camel会将每个元素转换为左侧的类型。

simple("${in.header.type} in 'gold,silver'")

对于后3个，我们还使用not支持否定测试：

simple("${in.header.type} !in 'gold,silver'")

您可以测试类型是否是某个实例，例如一个字符串

simple("${in.header.type} is 'java.lang.String'")

我们为所有java.lang类型添加了速记，因此您可以将其编写为：

simple("${in.header.type} is 'String'")

也支持范围。范围间隔要求数字，并且从开始到结束都包括在内。例如，测试一个值是否在100到199之间：

simple("${in.header.number} range 100..199")

注意我们在没有空格的范围内使用..。它基于与Groovy相同的语法。

从**Camel 2.9**起，范围值必须用单引号引起来

simple("${in.header.number} range '100..199'")

### 7.4.2. **使用Spring Xml**

由于Spring XML不具备Java DSL的全部构建器方法所具有的全部功能，因此您必须诉诸于使用其他一些语言来通过简单的运算符进行测试。现在，您可以使用简单的语言执行此操作。在下面的示例中，我们要测试header是否为小部件订单：

<from uri="seda:orders">

**   **<filter>

**       **<simple>${in.header.type} == 'widget'</simple>

**       **<to uri="bean:orderService?method=handleWidget"/>

**   **</filter>

</from>

## 7.5. **使用AND / OR**

如果您有两个表达式，可以将它们与&&或||运算符组合在一起。

例如：

simple("${in.header.title} contains 'Camel' && ${in.header.type'} == 'gold'")

并且当然||也受支持。示例将是：

simple("${in.header.title} contains 'Camel' || ${in.header.type'} == 'gold'")

**注意：**当前&&或||仅在简单语言表达式中只能使用**一次**。将来可能会改变。因此，您**无法**执行以下操作：

simple("${in.header.title} contains 'Camel' && ${in.header.type'} == 'gold' && ${in.header.number} range 100..200")

## 7.6. **示例**

在下面的Spring XML示例中，我们根据报头值进行过滤：

<from uri="seda:orders">

**   **<filter>

**       **<simple>${in.header.foo}</simple>

**       **<to uri="mock:fooOrders"/>

**   **</filter>

</from>

可以在消息过滤器模式中的上面的断言测试中使用简单语言，在该模式中，我们测试in消息是否具有foo报头（具有foo键的报头存在）。如果表达式的计算结果为**true，**则将消息路由到mock:fooOrders端点，否则丢弃消息。

Java DSL中的相同示例：

from("seda:orders")

**    **.filter().simple("${in.header.foo}")

**        **.to("seda:fooOrders");

您还可以将简单语言用于简单的文本串联，例如：

from("direct:hello")

**    **.transform().simple("Hello ${in.header.user} how are you?")

**    **.to("mock:reply");

注意，我们现在必须在表达式中使用$\{}占位符，以允许Camel正确解析它。

并且此示例使用date命令输出当前日期。

from("direct:hello")

**    **.transform().simple("The today is ${date:now:yyyyMMdd} and it is a great day.")

**    **.to("mock:reply");

在下面的示例中，我们调用Bean语言，在要包含返回的字符串中的Bean上调用方法：

from("direct:order")

**    **.transform().simple("OrderId: ${bean:orderIdGenerator}")

**    **.to("mock:reply");

orderIdGenerator是在注册表中注册的bean的ID 。如果使用Spring，则为Spring bean ID。

如果要声明要在订单ID生成器Bean上调用的generateId方法，则必须在调用该方法的前加上.method name。

from("direct:order")

**    **.transform().simple("OrderId: ${bean:orderIdGenerator.generateId}")

**    **.to("mock:reply");

我们可以使用?method=methodname我们熟悉的[Bean](https://camel.apache.org/components/latest/bean-component.html)组件本身的选项：

from("direct:order")

**    **.transform().simple("OrderId: ${bean:orderIdGenerator?method=generateId}")

**    **.to("mock:reply");

您还可以将主体body转换为给定类型，例如，确保它是字符串，您可以执行以下操作：

<transform>

**  **<simple>Hello ${bodyAs(String)} how are you?</simple>

</transform>

有几种类型有简写形式，因此我们可以使用String代替java.lang.String。这些是：byte[], String, Integer, Long。所有其他类型必须使用其FQN名称，例如org.w3c.dom.Document。

也可以从报头中查找值Map：

<transform>

**  **<simple>The gold value is ${header.type[gold]}</simple>

</transform>

在上面的代码中，我们使用名称查找header type并将其视为java.util.Map，然后使用gold键进行查找并返回值。如果报头不可转换为Map，则会引发异常。如果header名称type不存在，则返回null。

您可以嵌套函数，如下所示：

<setHeader name="myHeader">

**  **<simple>${properties:${header.someKey}}</simple>

</setHeader>

## 7.7. **引用常量或枚举**

假设您有一个供客户使用的枚举

在基于内容的路由器中，我们可以使用[简单](https://camel.apache.org/manual/latest/simple-language.html)语言来引用此枚举，以检查与之匹配的消息。

## 7.8. **在****Xml** **DSL中使用换行或制表符**

在Xml DSL中指定新行或制表符比较容易，因为您现在可以转义该值

<transform>

**  **<simple>The following text\nis on a new line</simple>

</transform>

## 7.9. **前后空格的处****理**

表达式的trim属性可用于控制是否删除或保留前导和尾随空格字符。默认值为true，它将删除空格字符。

<setBody>

**  **<simple trim="false">You get some trailing whitespace characters. </simple>

</setBody>

## 7.10. **设定结果类型**

现在，您可以向[Simple](https://camel.apache.org/manual/latest/simple-language.html)表达式提供结果类型，这意味着计算结果将转换为所需的类型。这最适用于定义类型，例如布尔，整数等。

例如，可以将报头设置为布尔类型，可以执行以下操作：

.setHeader("cool", simple("true", Boolean.class))

而在Xml DSL中

<setHeader name="cool">

**  ***<!-- use resultType to indicate that the type should be a java.lang.Boolean -->*

**  **<simple resultType="java.lang.Boolean">true</simple>

</setHeader>

## 7.11. **从外部资源加载脚本**

你可以外部化脚本，并Camel从资源加载它，例如"classpath:"，"file:"或"http:"。

可以使用以下语法完成此操作："resource:scheme:location"，例如，可以引用类路径上的文件：

.setHeader("myHeader").simple("resource:classpath:mysimple.txt")

## 7.12. **将****Spring Bean设置为Exchange****属性**

您可以将spring bean设置为exchange属性，如下所示：

<bean id="myBeanId" class="my.package.MyCustomClass" />

...

<route>

**  **...

**  **<setProperty name="monitoring.message">

**    **<simple>ref:myBeanId</simple>

**  **</setProperty>

**  **...

</route>

# 8. **Tokenize****语言**

**自****Camel****2.0**

Tokenize语言是camel-core中的一种内置语言，通常仅与Splitter EIP一起使用，以使用基于token的策略来分割消息。tokenizer语言旨在使用指定的定界符模式标记文本文档。它也可以用于以一些有限的功能标记XML文档。对于真正的XML-aware tokenization，建议使用XMLTokenizer语言，因为它为XML文档提供了更快，更有效的符号化。有关更多详细信息，请参见Splitter。

## 8.1. **Tokenize****选项**

令牌化语言支持以下11个选项。


| **名称**                | **默认** | **Java类型** | **描述**                                                                                             |
| ----------------------- | -------- | ------------ | ---------------------------------------------------------------------------------------------------- |
| token                   |          | String       | 用作token生成器的（开始）token，例如，您可以使用换行符。您可以使用简单语言作为token来支持动态token。 |
| endToken                |          | String       | 如果使用开始/结束token对，则用作token生成器的结束token。您可以使用简单语言作为token来支持动态token。 |
| InheritNameSpaceTagName |          | String       | 使用XML时从根/父标签名继承名称空间可以使用简单语言作为标记名来支持动态名称。                         |
| headerName              |          | String       | 要标记化而不是使用消息正文的报头名称。                                                               |
| regex                   | false    | Boolean      | 如果token是正则表达式模式。默认值为false                                                             |
| xml                     | false    | Boolean      | 输入是否为XML消息。如果使用XML有效负载，则必须将此选项设置为true。                                   |
| includeTokens           | false    | Boolean      | 使用配对时是否在配对部分中包括token，默认值为false                                                   |
| group                   |          | String       | 将N个部分组合在一起，例如将大文件分割成1000行的块。您可以使用简单语言作为组来支持动态组大小。        |
| groupDelimiter          |          | String       | 设置分组时要使用的定界符。如果尚未设置，则token将用作定界符。                                        |
| skipFirst               | false    | Boolean      | 跳过第一个元素                                                                                       |
| trim                    | true     | Boolean      | 是否修剪值以除去开头和结尾的空格和换行符                                                             |
