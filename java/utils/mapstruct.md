# MapStruct

### 什么是 MapStruct

MapStruct 是一个用来生成类型安全的、高性能的、无依赖的 bean 映射代码的 Java 注解处理器。你只需要定义一个 Mapper 接口，并且声明你需要转换 bean 的方法，MapStruct 就会为你生成这个接口的实现。原理是它基于 [JSR 269: Pluggable Annotation Processing API](https://jcp.org/en/jsr/detail?id=269) 规范，在编译期间，通过在注解处理器插件生成接口的实现，并且该实现使用纯 Java 方法调用来实现 source bean 和 target bean 之间的映射过程，完全不使用注解或其它低性能的方法。

相较于其它的动态映射框架，MapStruct 的优势有：

1. 通过纯 Java 方法代码的执行而非反射执行获得更高的性能。
2. 编译时类型安全：只能映射相互映射的对象和属性，不能将 Order 实体意外映射到客户 DTO 等。
3. 如果无法映射实体或属性，则在编译时清除错误报告。

### 安装

MapStruct 包括两部分工件：

* _org.mapstruct:mapstruct：包含了需要的注解比如 `@Mapper`_
* org.mapstruct:mapstruct-processor: 包含了生成 mapper 实现的注解处理器

由于我主要使用 Maven 作为项目管理和构建工具，因此这里我在 Maven 的环境中使用 MapStruct 来进行演示。

首先，在 Maven 项目的 pom.xml 文件中添加必要的依赖和注解处理器插件。

```markup
<properties>
    <org.mapstruct.version>1.5.3.Final</org.mapstruct.version>
</properties>

<dependencies>
    <dependency>
        <groupId>org.mapstruct</groupId>
        <artifactId>mapstruct</artifactId>
        <version>${org.mapstruct.version}</version>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
                <annotationProcessorPaths>
                    <path>
                        <groupId>org.mapstruct</groupId>
                        <artifactId>mapstruct-processor</artifactId>
                        <version>${org.mapstruct.version}</version>
                    </path>
                </annotationProcessorPaths>
            </configuration>
        </plugin>
    </plugins>
</build>
```

> 注意：MapStruct 官方要求 JDK 版本必须要在 1.8 及以上，否则无法使用。

接着，可以考虑使用 IDEA 的 [MapStruct 插件](https://plugins.jetbrains.com/plugin/10036-mapstruct-support)来更方便地在项目中使用，它提供了如下的便利性：

* Code completion in `target`, `source`, `expression`
* Go To Declaration for properties in `target` and `source`
* Find Usages of properties in `target` and `source`
* Refactoring support
* Errors and Quick Fixes

> 这些便利性，自己下完插件使用的时候便感觉出来了，无需看这些文字描述，鼠标玄乎在这些 mapper 接口上 IDEA 就会进行相关的提示。

### 入门使用

因为在生产中我主要使用 MapStruct 作为 bean 之间的映射工具，所以对于它的其它功能特性就不再过多学习使用了，所以在这里只是演示如何进行 bean 转换的简单操作。对于更多其它功能特性请参阅官方文档：[MapStruct 1.5.3.Final Reference Guide](https://mapstruct.org/documentation/stable/reference/html/)

下面的示例基于你是否按照上述的安装步骤已经正确安装了 MapStruct 的依赖和注解处理器。

下面我们从定义一个简单的 Mapper 开始，来实现 User bean 之间的相互转换。

前文提到，要使用 MapStruct 来实现 bean 之间的映射，我们只需要定义一个 Mapper 接口即可，现在在这个的基础上，用 org.mapstruct.Mapper 注解修饰这个接口，注解处理器会在编译期扫描并生成对应的实现类。

{% tabs %}
{% tab title="UserMapper.java" %}
```java
@Mapper // org.mapstruct.Mapper
public interface UserMapper {
	// 通过 org.mapstruct.factory.Mappers 类获得 Mapper 实现类对象
	UserMapper INSTANCE = Mappers.getMapper(UserMapper.class);

	UserVO convertUserPOToOrderPO(UserPO userPO);
}
```
{% endtab %}

{% tab title="UserPO.java" %}
```java
public class UserPO {
	private Long id;
	private String username;
	private String password;
	// omits setters and getters
}
```
{% endtab %}

{% tab title="UserVO.java" %}
```java
public class UserVO {
	private Long id;
	private String name;
	// omits setters and getters
}
```
{% endtab %}
{% endtabs %}

接着，执行 Maven 的构建命令 mvn compile 来生成 UserMapper 的实现类，生成的实现类如下，

默认实现类以 Impl 结尾，在 Mappers 类里进行的规定。

```java
import com.guhe.mapstruct.pojo.UserPO;
import com.guhe.mapstruct.pojo.UserVO;
import javax.annotation.Generated;

@Generated(
    value = "org.mapstruct.ap.MappingProcessor",
    date = "2023-03-23T23:15:18+0800",
    comments = "version: 1.5.3.Final, compiler: javac, environment: Java 1.8.0_221 (Oracle Corporation)"
)
public class UserMapperImpl implements UserMapper {

    @Override
    public UserVO convertUserPOToOrderPO(UserPO userPO) {
        if ( userPO == null ) {
            return null;
        }

        UserVO userVO = new UserVO();

        userVO.setId( userPO.getId() );
        userVO.setUsername( userPO.getUsername() );

        return userVO;
    }
}

```

下面，我们创建一个 UserMapperTest 测试类来对 UserMapper 进行测试。

> 在要测试的类上使用快捷键 Alt+Ins 可以快速地生成被测试的类及要被测试的方法以及设置一些测试周期的方法如 `@Before` `@After` 注解修饰的方法。

```java
public class UserConvertTest extends TestCase {
	@Test
	public void convertUserPOToOrderPOTest() {
		UserPO userPO = new UserPO();
		userPO.setId(1L);
		userPO.setUsername("stein");
		userPO.setPassword("stein283036");
		UserVO userVO = UserMapper.INSTANCE.convertUserPOToOrderPO(userPO);
		System.out.println("userVO = " + userVO);
		// userVO = UserVO{id=1, username='stein'}
	}
}
```

可以看到，通过 `UserMapper` 接口已经实现了 User bean 之间的转换。

#### @Mapping 注解的使用

在上面的例子中，我们可以看到，`UserPO` 和 `UserVO` 这两个类的属性名称是一样的，如果不一样的话这两个属性之间就不会存在映射关系，除非我们显示地 使用 `org.mapstruct.Mapping` 注解来指定 source bean 和 target bean 之间的属性映射关系。

下面举个例子来演示以下，现在我有两个 POJO 类，一个是 `OrderPO`，一个是 `OrderVO`，其中有两个属性名称是不相同的，因此无法直接建立映射关系，这时候 IDEA MapStruct 插件也会提示并给出解决方案，那就是使用 `@Mapping` 注解。以及一个 `OrderMapper` 类用来做 Order bean 之间的转换。

{% tabs %}
{% tab title="OrderPO.java" %}
```java
public class OrderPO {
	private Long id;
	private Long orderNum;
	private LocalDateTime orderTime;
	// omits setters and getters, etc
}
```
{% endtab %}

{% tab title="OrderVO.java" %}
```java
public class OrderVO {
	private Long id;
	private Long order_num;
	private LocalDateTime order_time;
	// // omits setters and getters, etc
}
```
{% endtab %}

{% tab title="OrderMapper.java" %}
```java
@Mapper
public interface OrderMapper {
	OrderMapper INSTANCE = Mappers.getMapper(OrderMapper.class);

	@Mapping(target = "order_time", source = "orderTime")
	@Mapping(target = "order_num", source = "orderNum")
	OrderVO convertOrderPOToOrderVO(OrderPO orderPO);
}
// 上面的两个独立的可重复 @Mapping 注解也可以使用一个 @Mappings 注解来将它们包含。
	@Mappings({
			@Mapping(source = "orderTime", target = "order_time"),
			@Mapping(source = "orderNum", target = "order_num")
	})
```
{% endtab %}
{% endtabs %}

现在写一个测试类测试下：

```java
public class OrderMapperTest extends TestCase {

	public void testConvertOrderPOToOrderVO() {
		OrderPO orderPO = new OrderPO();
		orderPO.setId(100L);
		orderPO.setOrderNum(new Random().nextLong());
		orderPO.setOrderTime(LocalDateTime.now());
		OrderVO orderVO = OrderMapper.INSTANCE.convertOrderPOToOrderVO(orderPO);
		System.out.println("orderVO = " + orderVO);
		// orderVO = OrderVO{id=100, order_num=2877641383680709843, order_time=2023-03-23T23:38:40.491}
	}
}
```

可以看到，通过显示地使用 @Mapping 注解可以实现不同属性名称之间的映射关系。

### 结尾

这篇文章简单地介绍并使用了 MapStruct 工具库来简化日常开发中的 bean 转换，除了使用这个库以外，还有其它类似的库比如 Spring BeanUtils、Apache BeanUtils 等，但性能都不如 MapStruct，读者有兴趣可以自行尝试。这是我在这里正式写的第一篇正式文章，之前一直说要写文章，不过一直没有开始，这次写完之后才发现写文章真是个耗时又耗精力的事情，需要查阅大量的资料还要保证语法内容的准确性。好了，不过现在结束了，来听首歌放松下吧。

{% embed url="https://soundcloud.com/toosii2x/toosii-favorite-song" %}

