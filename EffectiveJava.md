## 考虑用静态工厂方法代替构造器：
### 静态工厂方法与构造器不同的第一大优势在于，它们有名称：  
&emsp;&emsp;如果构造器的参数本身没有确切地描述正被返回的对象，那么具有适当名称的静态工厂会更容易使用，产生的客户端代码也更容易阅读。例如，构造器BitInteger(int, int, Random)返回BigInteger可能为素数，如果用名为BigInteger.probablePrime的静态工厂方法标识，显然更为清楚。（1.4的发行版本中最终增加了这个方法。）  
### 静态工厂方法与构造器不同的第二大优势在于，不必在每次调用它们的时候都创建一个新对象。  
&emsp;&emsp;可以将构建好的实例缓存起来，进行重复利用。
### 静态工厂方法与构造器不同的第三大优势在于，它们可以返回原返回类型的任何子类型对象。
&emsp;&emsp;这种灵活性的一种应用是，API可以返回对象，同时又不会是对象的类变成共有的。以这种方式隐藏实现类会使API变得非常简洁。
  静态工厂方法返回的对象所属的类，在编写包含该静态工厂方法的类时可以不必存在。
>### 服务提供者框架：  
>&emsp;&emsp;静态工作方法返回的对象所属的类，在编写包含该静态工厂方法的类时可以不必存在。这种灵活的静态工厂方法构成了服务提供者框架（Service Provider Framework）的基础，例如JDBC API。服务提供者框架是指这样一个系统：多个服务提供者实现一个服务，系统为服务提供者的客户端提供多个实现，并把它们从多个实现中解耦出来。  
>#### 重要组件：  
>__服务接口（Service Interface）：__ 提供者实现。  
**提供者注册API（Provider Registration API）：** 这是系统用来注册实现，让客户端访问它们的。  
**服务访问API（Service Access API）：** 客户端用来获取服务实例。  
**服务提供者接口（Service Provider Interface）[可选]：** 这些提供者负责创建其服务实现的实例。如果没有提供者接口，实现就按照类名称注册，并通过反射方式进行实例化。  
>
>&emsp;&emsp;对于JDBC来说，Connection就是它的服务接口，DriverManager.registerDriver是提供者注册API，DriverManager.getConnection是服务访问API，Driver就是服务提供者接口。
### 静态工厂方法的第四大优势在于，在创建参数化类型实例的时候，它们使代码变得更加简洁。

### 静态工厂方法的主要缺点在于，类如果不含有共有的或者受保护的构造器，就不能被子类化。

### 静态工厂方法的第二个缺点在于，它们与其他的静态方法实际上没有任何区别。

## 遇到多个构造器参数时要考虑使用构建器

## 用私有构造器或者枚举类型强化Singleton属性：
&emsp;&emsp;使用私有构造器时，享有特权的客户端可以借助AccessibleObject.setAccessible()方法，通过反射机制调用私有构造器。如果需要抵御这种攻击，可以修改构造器，让它在被要求创建第二个实例的时候抛出异常。
&emsp;&emsp;为了使用Singleton类变成是可序列化的，仅仅声明中加上“implements Serializable”是不够的。为了维护并保证Singleton，必须声明所有实例域都是瞬时（transient）的，否则每次反序列化一个序列化的实例时，都会创建一个新的实例。
&emsp;&emsp; **单元素的枚举类型已经成为实现Singleton的最佳方法。**

## 通过私有构造器强化不可实例化的能力

## 避免创建不必要的对象

## 消除过期的对象引用
&emsp;&emsp;一般而言，只要类是自己管理内存，就应该警惕内存泄漏问题。一旦元素被释放掉，则给元素中包含的任何对象引用都应该被清空。

## 避免使用终结方法
&emsp;&emsp;finalize()（终结方法）无法保证何时被调用以及是否被调用。
&emsp;&emsp;**终结方法的用处：**
&emsp;&emsp;1、当对象的所有者忘记调用显式终止方法时，终结方法可以充当“安全网（safety net）”。
&emsp;&emsp;2、本地对等体是一个本地对象（native object），普通对象通过本地方法（native method）委托给一个本地对象。因为本地对等体不是一个普通对象，所以垃圾回收器不会知道它，当它的Java对等体被回收的时候，它不会被回收。在本地对等体并不拥有关键资源的前提下，终结方法正是执行这项任务最合适的工具。如果本地对等体用友必须被及时终止的资源，那么该类就应该有一个显式的终结方法。
>&emsp;&emsp;**"终结方法链（finalizer chaining）"并不会被自动执行**
>&emsp;&emsp;如果子类实现者覆盖了超类的终结方法，但是忘记了手工调用超类的终结方法，那么超类的终结方法将永远也不会被调用到。为了防范，需要把终结方法放在一个匿名的类中，该匿名类的唯一用途就是终结它的外围实例。该匿名类的单个实例被称为终结方法守卫者，外围类的每个实例都会创建这样一个守卫者。外围实例在它的私有实例域中保存着一个对其终结方法守卫者的唯一引用，因此终结方法守卫者与外围实例可以同时启动终结过程。
``` java
public class Foo {

    @Override
    protected void finalize() throws Throwable {
        System.out.println("Foo finalize");
        super.finalize();
    }

    private final Object finalizerGuardian = new Object() {
        @Override
        protected void finalize() throws Throwable {
            System.out.println("finalizerGuardian finalize");
            super.finalize();
        }
    };
}
```

``` java
public class FooSon extends Foo {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("FooSon finalize");
//        super.finalize();
    }
}
```

``` java
public static void main(String[] args) {
    FooSon son = new FooSon();
    son = null;
    System.gc();
}
```
&emsp;&emsp;输出效果
>finalizerGuardian finalize  
FooSon finalize

## 覆盖equals时请遵守通用约定
> 自反性  
对称性  
传递性  
一致性  
非空性

## 覆盖equals时总要覆盖hashCode
> ●在应用程序的执行期间，只要对象的equals方法的比较操作所用到的信息没有被修改，那么对这个对象调用多次，hashCode方法都必须始终如一地返回同一个整数。在同一个应用程序的多次执行过程中，每次执行所返回的整数可以不一致。
> ●如果两个对象根据equals(Object)方法比较是相等的，那么调用这两个对象任意一个对象的hashCode方法都必须产生相同的整数结果。
> ●如果两个对象根据equals(Object)方法比较是不相等的，那么调用这两个对象任意一个对象的hashCode方法，则不一定要产生不同的整数效果。但是给不相等的对象产生截然不同的整数结果，有可能提高散列表（hash table）的性能。

## 始终要覆盖toString

## 谨慎地覆盖clone
> Cloneable接口中没有任何方法，它决定了Object中受保护的clone方法实现的行为：如果一个类实现了Cloneable，Object的clone方法就返回该对象的逐域拷贝，否则就会抛出CloneNotSupportedException异常。这是接口的一种极端非典型的用法，也不值得效仿。对于Cloneable接口，它改变了超类中受保护的方法的行为。

&emsp;&emsp;`永远不要让客户去做任何类库能够替客户完成的事情。`
&emsp;&emsp;如果专门为了继承而设计的类覆盖了clone方法，覆盖版本的clone方法就应该模拟Object.clone的行为：它应该被声明为proteced，抛出CloneNotSupportedException异常，并且该类不应该实现Cloneable接口。这样做可以使子类具有实现或不实现Cloneable接口的自由，就仿佛它们直接拓展了Object一样。
&emsp;&emsp;如果决定使用线程安全的类实现Cloneable接口，要记得它的clone方法必须得到很好的同步。
&emsp;&emsp;**另一个实现对象拷贝的好办法是提供一个拷贝的构造器或拷贝工厂**
``` java
public Yum(Yum yum);
```
``` java
public static Yum newInstance(Yum yum);
```
## 考虑实现Comparable接口
&emsp;&emsp;如果想为一个实现了Comparable接口的类增加值组件，请不要拓展这个类；而是要编写一个不相关的类，其中包含第一个类的实例。然后提供一个“视图（view）”方法返回这个实例。这样既可以自由地在第二个类上实现compareTo方法，同时也允许它的客户端在必要的时候，把第二个类的实例视同第一个类的实例。

## 使类和成员的可访问性最小化

&emsp;&emsp;**尽可能地使每个类或者成员不被外界访问。**
&emsp;&emsp;如果这个类实现了Serializable接口，私有成员和包级私有成员可能被“泄漏（leak）”到导出的API中。
&emsp;&emsp;**实例域绝不能是公有的。包含公有可变域的类并不是线程安全的。**
&emsp;&emsp;即使域是fianl的，并且引用不可变的对象，当把这个域变成公有的时候，也就放弃了“切换到一种新的内部数据表示法”的灵活性。
&emsp;&emsp;**类具有公有的静态final数组域，或者返回这种域的访问方法，这几乎总是错误的。**
&emsp;&emsp;客户端将能够修改数组中的内容。这是安全漏洞的一个常见根源。
``` java
// Pontential security hole!
public static final Thing[] VALUES = { ... };
```
&emsp;&emsp;修正这个问题有两种方法。可以使公有数组变成私有的，并增加一个公有的不可变列表：
``` java
private static final Thing[] PRIVATE_VALUES = { ... };
public static final List<Thing> VAlUES = Collections.unmodifiableList(Arrays.asList(PRIVATE_VALUES));
```
&emsp;&emsp;另一个方法是，可以使数组变成私有的，并添加一个公有方法，它返回私有数组的一个备份：
``` java
private static final Thing[] PRIVATE_VALUES = { ... };
public static final Thing[] values(){
    return PRIVATE_VALUES.clone();
}
```

## 在公有类中使用访问方法而非公有域

## 使可变性最小化
&emsp;&emsp;为了使类成为不可变，要遵循五条原则：
&emsp;&emsp;1.不要提供任何会修改对象状态的方法。
&emsp;&emsp;2.保证类不会被拓展。
&emsp;&emsp;3.使所有的域都是final的。
&emsp;&emsp;4.使所有的域都成为私有的。
&emsp;&emsp;5.确保对于任何可变组件的互斥访问。如果类具有指向可变对象的域，则必须确保该类的客户端无法获取指向这些对象的引用。
&emsp;&emsp;`不可变类真正唯一的缺点是，对于每个不同的值都需要一个单独的对象。`
&emsp;&emsp;如果你执行一个多步骤的操作，并且每个步骤都会产生一个新的对象，除了最后的结果之外其它的对象都会被抛弃，此时性能的问题就会显露出来。
&emsp;&emsp;处理这种问题有两种办法：
&emsp;&emsp;第一种，先猜测一下会经常用到哪些多步骤的操作，然后将它们作为基本类型提供。如果某个多步骤的操作已经作为基本类型提供，不可变的类就可以不必在每个步骤单独创建一个对象。不可变的类在内部可以更加灵活。例如，BigInteger有一个包级私有的可变“配套类（companing class）”。
&emsp;&emsp;第二种，提供一个公有的可变配套类。在Java平台类库中，这种方法的主要例子是String类，它的可变配套类是StringBuilder（和基本废弃的StringBuffer）。
&emsp;&emsp;让不可变的类变成final的另一种办法是，让类的所有构造器都变成私有或者包级私有的，并添加公有的静态工厂来代替公有的构造器。
&emsp;&emsp;虽然这种方法并不常用，但它经常是最好的替代方法。它最灵活，因为它允许使用多个包级私有的实现类。
&emsp;&emsp;没有方法会修改对象，并且它的所有域都必须是final的。实际上，可以为了提高性能有所放松：没有一个方法能够对对象的状态产生外部可见（externally visible）的改变。
&emsp;&emsp;如果选择不可变类实现Serializable接口，并且它包含一个或者多个指向可变对象的域，就必须提供一个显示的readObject或者readResolve方法，或者使用ObjectOutputStream.writeUnshared方法和ObjectOutputStream.readUnshared方法，即使默认的序列化形式是可以接受的，也是如此。否则攻击者可能从不可变的类创建可变的实例。
&emsp;&emsp;`除非有很好的理由要让类成为可变的类，否则就应该是不可变的。`不可变的类有许多优点，唯一的缺点是在特定的情况下存在潜在的性能问题。

## 复合优先于继承
&emsp;&emsp;在包的内部使用继承是非常安全的。然而，对普通的具体类（concrete class）进行跨越包边界的继承，则是非常危险的。
&emsp;&emsp;`与方法调用不同的是，继承打破了封装性。`子类依赖于其超类中特定功能的实现细节。
&emsp;&emsp;包装类不适合用在回调框架（callback framework）中：在回调框架中，对象把自身的引用传递给其他的对象，用于后续的调用（“回调”）。因为被包装起来的对象并不知道它外面的包装对象，所以它传递一个指向自身的引用（this），回调时避开了外面的包装对象。

## 要么为继承而设计，并提供文档说明，要么就禁止继承
&emsp;&emsp;对于专门为了继承而设计并且具有良好文档说明的类而言，**该类的文档必须精确地描述覆盖每个方法所带来的影响。**该类必须有文档说明它可覆盖（overridable）的方法的自用性（self-use）。对于每个公有的或者受保护的方法或者构造器，它的文档必须指明该方法或者构造器调用了哪些可覆盖的方法，以什么顺序调用的，每个调用的结果又是如何影响后续的处理过程的。更一般地，类必须在文档中说明，在哪些情况下它会调用可覆盖的方法。
&emsp;&emsp;**为了允许继承，构造器绝不能调用可被覆盖的方法。**
&emsp;&emsp;如果决定在一个为了继承而设计的类中实现Cloneable或者Serializable接口，应该意识到clone和readObject方法在行为上非常类似构造器。所以**无论是clone还是readObject，都不可以调用可覆盖的方法，不管是直接还是间接的方式。**
&emsp;&emsp;如果决定在一个为了继承而设计的类中实现Serializable接口，并且该类有一个readResolve或者writeReplace方法，就必须使readResolve或者writeReplace成为受保护的方法，而不是私有方法。如果这些方法是私有的，那么子类将会不声不响地忽略掉这连个方法。

## 接口优于抽象类
&emsp;&emsp;**现有的类可以容易被更新，以实现新的接口。**
&emsp;&emsp;**接口是定义mixin（混合类型）的理想选择。**
&emsp;&emsp;**接口允许我们构造非层次结构的类型框架。**
&emsp;&emsp;编写骨架实现类，必须认真研究接口，并确定哪些方法是最基本的（primitive），其他的方法则可以根据它们来实现，这些基本方法将成为骨架实现类中的抽象方法。然后必须为接口中所有其他的方法提供具体的实现。

## 接口只用于定义类型
&emsp;&emsp;如果大量利用工具类导出的常量，可以通过**静态导入（static import）机制**，避免使用了类名来修饰常量名。

## 类层次优于标签类

## 用函数对象表示策略

## 优先考虑静态成员类
&emsp;&emsp;当非静态成员类的实例被创建的时候，它和外围实例之间的关联关系也随之被建立起来；而且，这种关联关系以后不能被修改。
&emsp;&emsp;Map接口的实现往往使用非静态成员类来实现它们的集合视图，这些集合视图是有Map和keySet、entrySet和Values方法返回的。同样地，诸如Set和List这种集合接口的实现往往也使用非静态成员类来实现它们的跌代器。
&emsp;&emsp;`如果声明成员类不要求访问外围实例，就要始终把static修饰符放在它的声明中`，使它成为静态成员类，而不是非静态成员类。如果省略了static修饰符，则每个实例都将包含一个额外的指向外围对象的引用。保存这份引用需要消耗时间和空间，并且会导致外围实例在符合垃圾回收是却仍然得以保留。如果在没有外围实例的情况下，也需要分配实例，就不能使用非静态成员类，因为非静态成员类的实例必须要有一个外围实例（例如许多Map实现的内部都有一个Entry对象，Entry对象上的方法getKey、getValue和setValue并不需要访问该Map）。

## 请不要在新代码中使用原生态类型
&emsp;&emsp;泛型有子类型化（subtyping）的规则，List&lt;String&gt;是原生态类型List的一个子类型，而不是参数化类型List&lt;Object&gt;的子类型。

## 消除非受检警告
&emsp;&emsp;应该始终在尽可能小的范围中使用SuppressWarnings注解。
&emsp;&emsp;每当使用@SuppressWarnings("unchecked")注解时，都要加一条注释，说明为什么这么做。
&emsp;&emsp;在结合使用可变参数（varargs）方法和泛型时会出现令人费解的警告。这是由于每当调用可变参数方法时，就会创建一个数组来存放varargs参数。如果这个数组的元素类型不是可具体化的，就会得到一条警告。所以应避免混合使用泛型与可变参数方法。

## 优先考虑泛型

## 优先考虑泛型方法

## 利用有限制通配符来提升API的灵活性
&emsp;&emsp;为了获得最大限度的灵活性，要在表示生产者或者消费者的输入参数上使用通配符类型。如果某个输入参数既是生产者，又是消费者，那么则需要严格的类型匹配。
&emsp;&emsp;**如果参数化类型表示一个T生产者，就使用<? extends T>；如果它表示一个T消费者，就使用<? super T>。**例如pushAll和pushAll方法。
``` java
package com.zhangype;

import java.util.Collection;

public class MyStack<E> {
    public MyStack();

    public void put(E e);

    public E pop();

    public boolean isEmpty();

    // Wildcard type for parameter that serves as an E producer
    public void pushAll(Iterable<? extends E> src) {
        for (E e : src) {
            put(e);
        }
    }

    // Wildcard type for parameter that serves as an E consumer
    public void putAll(Collection<? super E> dst) {
        while (!isEmpty()) {
            dst.add(pop());
        }
    }
}
```
&emsp;&emsp;``不要用通配符类型作为返回类型。除了为用户提供额外的灵活性之外，它还会强制用户在客户端代码中使用通配符类型。``
&emsp;&emsp;类型推导规则相当复杂，而且它们并非总能完成需要它们完成的工作。
``` java
public static <E> Set<E> union(Set<? extends E> s1, Set<? extends E> s2)
```
&emsp;&emsp;如果这样编写，会编译错误：
``` java
Set<Integer> integers = ...;
Set<Double> doubles = ...;
Set<Number> numbers = union(integers, doubles);
```
&emsp;&emsp;如果编译器不能推断你希望它拥有的类型，可以通过一个显式的参数类型告诉编译器。如：
``` java
Set<Number> numbers = Union.<Number>union(integers, doubles);
```
&emsp;&emsp;类型参数和通配符之间具有双重性，许多方法都可以利用其中一个或者另一个进行申明。
``` java
public static <E> void swap(List<E> list, int i, int j);
public static <E> void swap(List<?> list, int i, int j);
```
&emsp;&emsp;在公共API中，第二种更好一些，因为它更简单。**一般来说，如果类型参数只在方法声明中出现一次，就可以用通配符取代它。**
``` java
public static <E> void swap(List<E> list, int i, int j){
        list.set(i, list.set(j, list.get(i)));
};
```
&emsp;&emsp;当出现这种无法通过变编译的简单实现，可以编写私有的辅助方法来捕捉通配符类型，为了捕捉类型，辅助方法必须是泛型方法，就像下面这样：
``` java
public static <E> void swap(List<E> list, int i, int j){
        swapHelper(list, i, j);
};
// Private helper method for wildcard capture
public static <E> void swapHelper(List<E> list, int i, int j){
        list.set(i, list.set(j, list.get(i)));
};
```
&emsp;&emsp;swapHelper允许我们导出比较好的基于通配符的声明，同时在内部利用更加复杂的泛型方法。

## 优先考虑类型安全的异构容器
&emsp;&emsp;通过将键（key）进行参数化而不是将容器（container）参数化，将参数化的键提交给容器，来插入或者获取值。用泛型来确保值的类型与它的键相符。可以获得更多的灵活性。
&emsp;&emsp;当一个类的字面文字被用在方法中，来传达编译时和运行时的类型信息时，就被称作type token（类型令牌）。
``` java
import java.util.HashMap;
import java.util.Map;

// Typesafe heterogeneous container pattern - implementation
// 类型安全的异构容器实现
public class Favorites {
    private Map<Class<?>, Object> favorites = new HashMap<>();

    public <T> void putFavorite(Class<T> key, T value) {
        if (value == null)
            throw new NullPointerException("value is null");
        favorites.put(key, value);
    }

    public <T> T getFavorite(Class<T> key) {
        return key.cast(favorites.get(key));
    }
}
```
&emsp;&emsp;此处利用了Class的cast方法，将对象引用动态转换成了Class对象所表示的类型。
&emsp;&emsp;cast方法是Java的cast操作符的动态模拟。它只检测它的参数是否为Class对象所表示的类型的实例。
&emsp;&emsp;**注解API广泛利用了有限制的类型令牌。例如AnnotatedElement接口的getAnnotation()方法。**
&emsp;&emsp;类Class提供了asSubclass，它将调用它的Class对象转换成用其参数表示的一个子类。

## 用enum代替int常量