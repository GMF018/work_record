## Spring

> - 强大的基于 [JavaBeans](https://zh.wikipedia.org/wiki/JavaBeans) 的采用[控制反转](https://zh.wikipedia.org/wiki/控制反转)（Inversion of Control，IoC）原则的配置管理，使得应用程序的组建更加简易快捷。
>- 一个可用于 [Java EE](https://zh.wikipedia.org/wiki/Java_EE) 等运行环境的核心 [Bean](https://zh.wikipedia.org/w/index.php?title=Enterprise_Java_Beans&action=edit&redlink=1)[工厂](https://zh.wikipedia.org/w/index.php?title=虚拟工厂模式&action=edit&redlink=1)。
> - 数据库[事务](https://zh.wikipedia.org/wiki/事务处理)的一般化抽象层，允许声明式（Declarative）事务管理器，简化事务的划分使之与底层无关。
>- 内建的针对 [JTA](https://zh.wikipedia.org/wiki/Java事务API) 和单个 [JDBC](https://zh.wikipedia.org/wiki/Java_Database_Connectivity) 数据源的一般化策略，使Spring的事务支持不要求 [Java EE](https://zh.wikipedia.org/wiki/Java_EE) 环境，这与一般的 JTA 或者 [EJB](https://zh.wikipedia.org/wiki/EJB) CMT 相反。
> - JDBC 抽象层提供了有针对性的异常等级（不再从 SQL 异常中提取原始代码），简化了错误处理，大大减少了程序员的编码量。再次利用 JDBC 时，你无需再写出另一个'终止'（finally）模块。并且面向 JDBC 的异常与 Spring 通用[数据访问对象](https://zh.wikipedia.org/wiki/数据访问对象)（Data Access Object）异常等级相一致。
>- 以资源容器，[DAO](https://zh.wikipedia.org/wiki/DAO) 实现和事务策略等形式与 [Hibernate](https://zh.wikipedia.org/wiki/Hibernate)，[JDO](https://zh.wikipedia.org/w/index.php?title=Java_Data_Objects&action=edit&redlink=1) 和 [MyBatis](https://zh.wikipedia.org/wiki/MyBatis) 、[SQL Maps](https://zh.wikipedia.org/w/index.php?title=SQL_Maps&action=edit&redlink=1) 集成。利用控制反转机制全面解决了许多典型的 Hibernate 集成问题。所有这些全部遵从 Spring 通用事务处理和通用数据访问对象异常等级规范。
> - 灵活的基于核心 Spring 功能的 [MVC](https://zh.wikipedia.org/wiki/模型-视图-程序控制) [网页应用程序](https://zh.wikipedia.org/wiki/网页应用程序)框架。开发者通过策略接口将拥有对该框架的高度控制，因而该框架将适应于多种呈现（View）技术，例如 [JSP](https://zh.wikipedia.org/wiki/JSP)、[FreeMarker](https://zh.wikipedia.org/wiki/FreeMarker)、[Velocity](https://zh.wikipedia.org/wiki/Apache_Velocity)、[Thymeleaf](https://zh.wikipedia.org/wiki/Thymeleaf) 等。值得注意的是，Spring 中间层可以轻易地结合于任何基于 MVC 框架的网页层，例如 [Struts](https://zh.wikipedia.org/wiki/Struts)、[WebWork](https://zh.wikipedia.org/w/index.php?title=WebWork&action=edit&redlink=1) 或 [Tapestry](https://zh.wikipedia.org/wiki/Tapestry_(programming))。
>- 提供诸如事务管理等服务的[AOP](https://zh.wikipedia.org/wiki/面向切面编程)框架。
> - 为了解决企业级应用开发的复杂性而创建的、简化开发

### IOC

对象由spring 创建、管理、装配

###  自动装配

+  **byType **:根据类型装配，可省略id ，但不可有多个相同类型
+  **byName**:根据名称装配

