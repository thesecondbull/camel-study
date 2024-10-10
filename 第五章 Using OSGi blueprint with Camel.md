第五章 [**Using OSGi blueprint with Camel**](https://camel.apache.org/manual/latest/using-osgi-blueprint-with-camel.html)

**从Camel 2.4开始可用**

已经为Blueprint创建了一个自定义XML名称空间，以使您可以利用漂亮的XML方言。给定Blueprint自定义名称空间尚未标准化，因此只能在[Apache Karaf](http://karaf.apache.org/)使用的[Apache Aries](http://incubator.apache.org/aries/) Blueprint实现上使用此名称空间。

# 1. **总览**

XML模式与Spring的XML模式基本相同，因此整个文档中所有涉及Spring XML的xml代码段也适用于Blueprint路由。

这是一个使用blueprint的非常简单的路由定义：

<blueprint xmlns="http://www.osgi.org/xmlns/blueprint/v1.0.0">

<camelContext xmlns="http://camel.apache.org/schema/blueprint">

**        **<route>

**            **<from uri="timer:test" />

**            **<to uri="log:test" />

**        **</route>

**    **</camelContext>

</blueprint>

关于受支持的xml元素，目前存在一些限制（与Spring xml语法相比）：

l beanPostProcessor是特定于Spring的，不允许使用

但是，在OSGi环境中部署应用程序时使用blueprint有几个优点：

l 升级到新的Camel版本时，无需更改名称空间，因为将根据捆绑软件导入的Camel软件包选择正确的版本。

l 关于自定义名称空间和捆绑包，没有启动顺序问题

l 您可以使用Blueprint属性占位符，有关更多信息，请参见[使用PropertyPlaceholder](https://camel.apache.org/manual/latest/using-propertyplaceholder.html)

# 2. **使用****Camel****Blueprint**

要在OSGi中利用Camelblueprint，除了camel-core及其依赖项之外，您仅需要Aries Blueprint捆绑包和camel-blueprint捆绑包。

如果您使用Karaf，则可以使用名为的功能camel-blueprint来安装所有必需的捆绑软件。
