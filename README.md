# Effective Java, Third Edition
![EJ3e Book Cover](https://www.pearsonhighered.com/assets/bigcovers/0/1/3/4/0134685997.jpg)
## Hot News! Source code finally available on GitHub. Happy Hacking!

## 注意：项目基于 Java9 运行，虽然大部分是关于 Java8 及以下的，若环境为纯 Java8，则需要对不少代码做调整。

## 具体条目
### 创建和销毁对象
1. 用静态工厂方法代替构造器  
优点：  
 1）使用静态工厂方法相比构造器而言可以共享之前创造的对象，而不是每次都创建一个新对象。
2. 遇到多个构造器参数时要考虑使用构建器
3. 用私有构造器或者枚举类型强化 Singleton 属性
4. 通过抛出异常的私有构造器强化不可实例化的能力
5. 优先考虑依赖注入来引用资源，而不要使用 Singleton 和 静态工具类 来实现依赖一个或多个底层资源的类。  
 1）将这些资源传给工厂或构造器（或构建器），通过它们来创建类，这个过程就叫依赖注入
6. 避免创建不必要的对象  
 1）在对于像数据库连接这样的大对象（创建它比较耗费性能和资源），重用是有意义的；  
 2）但是对于一些轻量级的且场景要求我们创建的新对象，也不要吝惜创建  
7. 消除过期的对象引用  
内存泄漏的来源：  
 1）类是自己管理内存，容易造成内存泄漏；  
 2）缓存的积累容易造成内存泄漏；  
 3）监听器和其他回调，如果不及时取消注册，会积累慢慢造成内存泄漏
8. 避免使用终结方法和清除方法
9. try-with-resources 优先于 try-finally

### 对于所有对象都通用的方法
10. 覆盖 equals 时请遵守通用约定  
 面向对象语言的关于等价关系的一个基本问题：  
  1）我们无法在扩展可实例化的类的同时，既增加新的值组件，同时又保留 equals 约定
11. 覆盖 equals 时总要覆盖 hashCode  
 1）如果两个对象调用 equals 相等，则对这两个对象调用 hashCode 所得的结果必须相等，反之不一定成立
12. 始终要覆盖 toString
13. 谨慎地覆盖 clone
14. 考虑实现 Comparable 接口  
 1）如果一个类已经实现了 Comparable 接口，请不要使用继承的方式扩展这个类，可以考虑使用聚合的方式，使这个类的对象作为另一个类的域，这样不影响新的类去实现 Comparable 接口

### 类和接口
15. 使类和成员的可访问性最小化
16. 要在共有类而非公有域中使用访问方法
 1）公有类永远都不应该暴露可变的域，不可变的域（final 的）最好也不要暴露，只不过不可变的域暴露了危害性小一点
17. 使可变性最小化  
 优点：  
  1）不可变对象本质上是线程安全的，它们不要求同步；  
  2）不可变对象可以被自由地共享，也不再需要对它们进行保护性拷贝  
 缺点：  
  1）不可变对象对于每个不同的值都需要创建一个单独的对象，创建这些对象的代价可能很高
18. 复合优先于继承  
 1）只有当子类和超类之间确实存在子类型关系时（is-a），使用继承才是恰当的，否则，为了程序的健壮性和降低对于实现细节的依赖，应该使用复合  
19. 要么设计继承并提供文档说明，要么禁止继承  
 1）好的 API 文档应该描述一个给定的方法做了什么工作，而不是描述它是如何做到的，但是在涉及到关于继承的文档的时候，我们必须描述清楚相应实现的细节，尤其是对于其中可覆盖方法的自用情况（自己调用了自己的可覆盖方法，在子类重写这些方法时，可能会对父类的调用它们的方法造成破坏）；  
 2）为了继承而设计的类，必须在发布之前先编写其子类对其进行测试；  
 3）父类的构造器决不能调用可被覆盖的方法
20. 接口优于抽象类  
 1）接口允许构造非层次结构的类型框架；  
 2）在设计类结构的时候可以考虑用一个抽象类去实现接口的一些方法，以获取继承的好处，这被称为“骨架实现类”  
21. 为后代设计接口
22. 接口只用于定义类型，而不应该用它来导出常量，即将公有的常量放在其中
23. 类层次优先于标签类，实际上就是用继承的方式来设计多种类型事物的代码，对其进行合理的抽象
24. 静态成员类优先于非静态成员类
25. 限制源文件为单个顶级类或接口，这么做可以确保编译时一个类不会多个定义

### 泛型
26. 请不要使用原生态类型  
 1）原生类型：不带任何实际类型参数的泛型名称
27. 消除非受检的警告（而非抑制）
28. 列表优于数组
29. 优先考虑泛型
30. 优先考虑泛型方法
31. 利用有限制的通配符来提升 API 的灵活性  
 1）为获得最大限度的灵活性，要在表示生产者或消费者的输入参数上使用通配符类型，如：<? extends E> 或 <? super E>；  
 2）PECS原则：procedure-extends, consumer-super。即：如果泛型的参数是作为数据的生产者，则对于这个参数的类型 T，使用<? extends T>；如果泛型的参数是作为数据的消费者，则对于这个参数的类型 T，使用 <? super T>；  
 3）上述规则以容器的泛型为例，本质上是父类的容器里可以放子类的对象，而从容器中拿出来的东西需要灵活地被另一个存放父类对象的容器接收；  
 4）不要使用通配符类型作为返回类型  
32. 谨慎并用泛型可变参数  
 1）对于每一个带有泛型可变参数或者参数化类型的方法，都要使用 @SafeVarargs 进行注解  
33. 优先考虑类型安全的异构容器  
 1）集合 API 限制每个容器只能有固定数目的类型参数，我们可以通过将类型参数放在键上而不是容器上来避开这一限制。对于这种类型安全的异构容器，可以用 Class 对象作为键，以这种方式使用的 Class 对象称为类型令牌

### 枚举和注解
34. 用 enum 代替 int 常量  
 1）枚举类型中的抽象方法必须被它的所有常量中的具体方法所覆盖；  
 2）每当需要一组固定常量，并且在编译时就知道成员的时候，就应该使用枚举  
35. 用实例域代替序数，就是代替由枚举类型的 ordinal() 导出的序数
36. 用 EnumSet 代替位域，主要用于在传递多组常量集时的操作
37. 用 EnumMap 代替序数索引（序数是使用枚举的 ordinal() 获得的）
38. 用接口模拟可扩展的枚举
39. 注解优先于命名模式
40. 坚持使用 Override 注解
41. 用标记接口定义类型  
 1）标记接口是不包含方法声明的接口，它只是指明一个类实现了具有某种属性的接口

### Lambda 和 Stream
42. Lambda 优先于匿名类
43. 方法引用优先于 Lambda
44. 坚持使用标准的函数接口（如：Predicate、Supplier、Consumer、Function、BinaryOperator、UnaryOperator 等）  
 1）对自己编写的函数式接口要使用 @FunctionalInterface 注解修饰（这个注解类似于 @Override）  
45. 谨慎使用 Stream  
 1）Stream pipeline 通常是 lazy 的，直到调用终止操作时才开始计算
46. 优先选择 Stream 中无副作用的函数  
 1）forEach 操作是 Stream 终止操作中最没有威力的，也是对 Stream 最不友好的，它是显示迭代的，因而不适合并行。forEach 操作应该只用于报告 Stream 计算的结果，而不是执行计算  
47. Stream 要优先用 Collection 作为返回类型
48. 谨慎使用 Stream 并行  
 1）在 Stream 上通过并行获得的性能，最好是通过 ArrayList、HashMap、HashSet 和 ConcurrentHashMap 实例，数组，int 范围和 long 范围等。这些数据结构的共性是，都可以被精确、轻松地分成任意大小的子范围，使并行线程中的分工变得更加轻松；  
 2）并行 Stream 是一项严格的性能优化，对于任何优化都必须在改变前后对性能进行测试，以确保值得这么做；  
 3）如果对 Stream 进行不恰当的并行操作，可能导致程序运行失败，或者造成性能灾难

### 方法
49. 检查参数的有效性  
 1）设计方法时，要考虑方法的参数有哪些限制，要根据这些限制在方法的开头处对参数的有效性进行校验  
50. 必要时进行保护性拷贝  
 1）如果一个类包含有从客户端得到或者返回到客户端的可变组件，这个类就必须保护性地拷贝这些组件。如果拷贝的成本受到限制，并且类信任它的客户端不会不恰当地修改组件，就可以在文档中指明客户端的职责是不得修改受到影响的组件，以此来代替保护性拷贝  
51. 谨慎设计方法签名  
 1）谨慎地选择方法名称；  
 2）不要过于追求提供便利的方法；  
 3）避免过长的参数列表；  
 4）对于参数类型，要优先使用接口而不是类；  
 5）对于 boolean 参数，要优先使用两个元素的枚举类型  
52. 慎用重载  
 1）调用哪个重载方法是在编译时决定的，所以对于重载方法的选择是静态的；与之相对的是，对于被覆盖方法的选择则是动态的  
53. 慎用可变重载
54. 返回零长度的数组或者集合，而不是 null
55. 谨慎返回 optional  
 1）容器类型包括集合、映射、Stream、数组和 optional，都不应该被包装在 optional 中；  
 2）Optional 是一个必须进行分配和初始化的对象，从 optional 读取值时需要额外的开销，这使得 optional 不适用于注重性能的情况；  
 3）如果发现自己编写的方法始终无法返回值，并且相信该方法的用户每次在调用它时都要考虑到这种可能性，那么就应该返回一个 optional。但是尽量不要将 optional 用作返回值以外的任何其他用途
56. 为所有导出的 API 元素编写文档注释  
 1）方法的文档注释应该简洁地描述出它和客户端之间的约定，即这个约定应该说明这个方法做了什么，而不说明它是如何完成工作的；  
 2）文档还应当描述每个方法的副作用，就是指运行方法后系统状态中可以观察到的变化  

### 通用编程
57. 将局部变量的作用域最小化  
 1）尽量在第一次要使用局部变量的地方对其进行声明；  
 2）几乎每一个局部变量的声明都应该包含一个初始化表达式  
58. for-each 循环优先于传统的 for 循环  
 1）for-each 循环不会有性能损失，它们产生的代码本质上与手工编写的一样  
59. 了解和使用类库  
 1）应当熟悉 java.lang、java.util 和 java.io 及其子包的内容；  
 2）不要重复造轮子  
60. 如果需要精确的答案，请避免使用 float 和 double  
 1）对于货币计算，要使用 BigDecimal、int 或 long 进行，实际上精确计算就是使用这几种类型  
61. 基本类型优先于装箱基本类型
62. 如果其他类型更合适，则尽量避免使用字符串  
 1）字符串不适合代替其他的值类型；  
 2）字符串不适合代替枚举类型  
63. 了解字符串连接的性能  
 1）当字符串的规模较大时，会导致较大的性能损失，因为 String 是不可变对象，在使用 “+” 进行连接时，会拷贝原字符串。应该考虑使用 StringBuilder 或使用字符数组来连接字符串，以获得性能的提高  
64. 通过接口引用对象
65. 接口优先于反射机制  
 反射机制的缺点：  
  1）损失了编译时类型检查的优势；  
  2）执行反射访问所需要的代码非常笨拙和冗长；  
  3）性能损失  
66. 谨慎地使用本地方法
67. 谨慎地进行优化  
 1）不要随便进行优化，不成熟的优化会导致一些严重的问题；  
 2）要努力编写结构好的程序而不是快的程序；  
 3）努力避免那些限制性能的设计决策；  
 4）要考虑 API 设计决策的性能后果；  
 5）在每次试图做优化之前和之后，要对性能进行测量
68. 遵守普遍接受的命名惯例

### 异常
69. 只针对异常的情况才使用异常，不要将异常用于普通的控制流
70. 对可恢复的情况使用受检异常，对编程错误使用运行时异常  
 1）对于异常，如果期望调用者能够适当地恢复，那就应该使用受检异常；  
 2）用运行时异常来表明编程错误，即 API 的客户没有遵守 API 规范建立的约定；  
 3）最好不要实现任何新的 Error 子类，我们实现的任何非受检的抛出结构都是 RuntimeException 的子类；  
 4）要在受检异常上提供方法，以帮助恢复  
71. 避免不必要地使用受检异常
72. 优先使用标准的异常
73. 抛出与抽象对应的异常  
 1）更高层的实现应该捕获底层的异常，同时抛出可以按照高层实现进行解释的异常  
74. 每个方法抛出的所有异常都要建立文档
75. 在细节消息中包含失败-捕获信息  
 1）不要在细节消息中包含密码、密钥以及类似的信息
76. 努力使失败保持原子性  
 1）所谓保持原子性，就是指失败的方法调用应该使对象保持在调用方法之前的状态；  
 2）如果不能使失败保持原子性，也应该在 API 文档中清楚地指明对象会处于什么状态
77. 不要忽略异常  
 1）空的 catch 块会使异常达不到应有的目的