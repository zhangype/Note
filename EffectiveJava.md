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
&emsp;&emsp;枚举天生就是不可变的，因此所有的域都应该声明为final的。
&emsp;&emsp;可以将不同行为与每个枚举常量关联起来：在枚举类型中声明一个抽象的apply方法，并在特定于常量的的类主体中，用具体的方法覆盖每个常量的apply方法。
``` java
// Enum type with constant-specific method implementations
// 特定于常量的方法实现（constant-specific method implementation）

public enum Operation {
    PLUS {
        double apply(double x, double y) {
            return x + y;
        }
    },
    MINUS {
        double apply(double x, double y) {
            return x - y;
        }
    },
    TIMES {
        double apply(double x, double y) {
            return x * y;
        }
    },
    DIVIDE {
        double apply(double x, double y) {
            return x / y;
        }
    };

    abstract double apply(double x, double y);
}
```

## 用实例域代替序数

## 用EnumSet实例域代替序数

## 用EnumMap代替序数索引

## 可以用接口模拟可伸缩的枚举
&emsp;&emsp;虽然枚举类型不是可扩展的，但是接口类型则是可扩展的。
``` java
public interface Opertiaon {
    double apply(double x, double y);
}

public enum BasicOperation implements Operation {
    PLUS("+") {
        public double apply(double x, double y) {
            return x + y;
        }
    };

    private final String symbol;

    BasicOperation(String symbol) {
        this.symbol = symbol;
    }

    @Override
    public String toString() {
        return symbol;
    }
}

public enum ExtendedOperation implements Operation {
    REMAINDER("%") {
        public double apply(double x, double y) {
            return x % y;
        }
    };

    private final String symbol;

    BasicOperation(String symbol) {
        this.symbol = symbol;
    }

    @Override
    public String toString() {
        return symbol;
    }
}
```

## 注解优先命名模式
&emsp;&emsp;通过Method.invoke的调用，反射机制会将异常封装在InvocationTargetException。

## 坚持使用Override注解

## 用标记接口定义类型
&emsp;&emsp;标记接口（marker interface）是没有包含方法声明的接口，只是指明（或者“标明”）一个类实现了具有某周属性的接口。例如，Serializable。通过实现这个接口，类表明它的实例可以被写到ObjectOutputStream（或者“被序列化”）。

## 检查参数有效性

## 必要时进行保护性拷贝
```java
public final class Period {
    private Date start;
    private Date end;

    public Period(Date start, Date end) {
        if (start.compareTo(end) > 0) {
            throw new IllegalArgumentException(start + "after" + end);
        }
        this.start = start;
        this.end = end;
    }

    public Date getStart() {
        return start;
    }

    public void setStart(Date start) {
        this.start = start;
    }

    public Date getEnd() {
        return end;
    }

    public void setEnd(Date end) {
        this.end = end;
    }

    public static void main(String[] args) {
        Date start = new Date();
        Date end = new Date();

        Period period = new Period(start, end);
        end.setYear(78);
        System.out.println("startDate:" + start);
        System.out.println("endDate:" + end);
        System.out.println("period startDate:" + period.getStart());
        System.out.println("period endDate:" + period.getEnd());
    }
}
```
&emsp;&emsp;由于Date类本身是可变的，因此很容易违反“start不能在end之后”的约束。
&emsp;&emsp;为了保护Period实例的内部信息避免受到攻击，**对于构造器的每个可变参数进行保护性拷贝是必要的**。
``` java
    public Period(Date start, Date end) {
        this.start = new Date(start.getTime());
        this.end = new Date(end.getTime());
        if (start.compareTo(end) > 0) {
            throw new IllegalArgumentException(start + "after" + end);
        }
    }
```
&emsp;&emsp;``对于参数类型可以被不可信任方子类化的参数，请不要使用clone方法进行保护性拷贝。``

## 谨慎设计方法签名
&emsp;&emsp;1、谨慎地选择方法的名称。
&emsp;&emsp;2、不要过于追求提供便利的方法。
&emsp;&emsp;3、避免过长的参数列表。目标是四个参数，或者更少。

## 谨慎重载
&emsp;&emsp;``要调用哪个重载（overloading）方法是在编译时做出决定的。``
&emsp;&emsp;``对于重载方法的选择是静态的，而对于被覆盖的方法的选择是动态的。``
&emsp;&emsp;**“能够重载方法”并不意味着就“应该重载方法”。一般情况下，对于多个具有相同参数数目的方法来说，应该尽量避免重载方法。应该避免这样的情形：同一组参数只需经过类型转换就可以被传递给不同的重载方法。如果不能避免这种情形，例如，因为正在改造一个现有的类似实现新的接口，就应该保证：当传递同样的参数时，所有重载方法的行为必须一致。如果不能做到这一点，程序员就很难有效地使用被重载的方法或者构造器，他们就不能理解它为什么不能正常工作。**

## 慎用可变参数
&emsp;&emsp;在重视性能的情况下，使用可变参数机制要特别小心。可变参数方法的每次调用都会导致进行一次数组分配和初始化。

## 返回零长度的数组或者集合，而不是null
&emsp;&emsp;集合值的方法也可以做成在每当需要返回空集合时都返回同一个不可变的空集合。例如Collections.emptySet、emptyList和emptyMap方法。

## 为所有导出的API元素编写文档注释
&emsp;&emsp;为了正确地编写API文档，必须在每个被导出的类、接口、构造器、方法和域声明之前增加一个文档注释。如果类是可序列化的，也应该对它的序列化形式编写文档。
&emsp;&emsp;Javadoc的{@code}标签有两个作用：造成该代码片段以代码体进行呈现，并限制HTML标记和嵌套的Javadoc标签在代码片段中进行处理。
&emsp;&emsp;为了产生包含HTML元字符的文档，比如小于号（<）、大于号（>）以及“与”（&），必须采取特殊的动作。让这些字符出现在文档中的最佳方法是用{@literal}标签将它们包围起来，这样就限制了HTML标记和嵌套的Javadoc便签的处理。

## 将局部变量的作用域最小化
&emsp;&emsp;要使局部变量的作用域最小化，最有力的方法就是在第一次使用它的地方声明。
&emsp;&emsp;几乎每个局部变量的声明都应该包含一个初始化表达式。如果没有足够的信息来对一个变量进行有意义的初始化，就应该推迟这个声明，直到可以初始化为止。&emsp;&emsp;最后一种“将局部变量的作用域最小化”的方法是使方法小而集中。如果把两个操作合并到同一个方法中，与其中一个操作相关的局部变量就有可能会出现在执行另一个操作的代码范围之内。为了防止这种情况发生，只要把这个方法分成两个，每个方法各执行一个操作。

## for-each循环优先于传统的for循环
&emsp;&emsp;for-each循环在简洁性和预防Bug方面有着传统的for循环无法比拟的优势，并且没有性能损失。
&emsp;&emsp;有三种常见的情况无法使用for-each循环：
> &emsp;&emsp;**1.过滤**——如果需要遍历集合，并删除选定的元素，就需要使用显示的迭代器，以便可以调用它的remove方法。
> &emsp;&emsp;**2.转换**——如果需要遍历列表或者数组，并取代它部分或者全部的元素值，就需要列表迭代器或者数组的索引，以便设定元素的值。
> &emsp;&emsp;**3.平行迭代**——如果需要并行地遍历多个集合，就需要显式地控制迭代器或者索引变量，以便所有的迭代器或者索引变量都可以得到同步前移。例如下代码：
``` java
enum Face { ONE, TWO, THREE, FOUR, FIVE, SIX}
Collection<Face> faces = Arrays.asList(Face.values());

for (Iterator<Face> i = faces.iterator(); i.hasNext();)
    for(Iterator<Face> j = faces.iterator(); j.hasNext();)
        System.out.println(i.next() + " " + j.next());
```
## 了解和使用类库

## 如果需要精确的答案，请避免使用float和double
&emsp;&emsp;``float和double类型尤其不适合用于货币计算``，因为要让一个float或者double精确地表示0.1（或者10的任何其他负数次方值）是不可能的。正确的方法是使用BigDecimal、int或者long进行货币计算。
&emsp;&emsp;BigDecimal允许完全控制舍入，每当一个操作涉及舍入的时候，它允许你从8种舍入模式中选择一个。
&emsp;&emsp;如果性能非常关键，并且你又不介意自己记录十进制小数点，而且涉及的数值又不是太大，就可以使用int或者long。如果数值范围没有超过9位十进制数字，就可以使用int；如果不超过18位数字，就可以使用long。如果数值可能超过18位数字，就必须使用BigDecimal。

## 基本类型优先于装箱基本类型
&emsp;&emsp;使用装箱基本类型场景：
&emsp;&emsp;如果作为集合中的元素、键和值。不能将基本类型放在集合中，因此必须使用装箱基本类型。
&emsp;&emsp;在参数化类型中，必须使用装箱基本类型作为类型参数，例如：ThreadLocal&lt;Integer&gt;。
&emsp;&emsp;在进行反射的方法调用时，必须使用装箱基本类型。

## 如果其它类型更合适，则尽量避免使用字符串
&emsp;&emsp;**字符串不适合代替其他的值类型。**当一段数据从文件、网络或者键盘设备，进入到程序中之后，它通常以字符串的形式存在。有一种自然的倾向是让它继续保留这种形式，但是，只有当这段数据本质上确实是文本信息时，这种想法才合理。如果它的数值，就应该转换为适当的数值类型，比如int、float或者BigInteger类型。
&emsp;&emsp;**字符串不适合代替枚举类型。**
&emsp;&emsp;**字符串不适合代替聚集类型。**

## 当心字符串连接的性能
&emsp;&emsp;**为连接n个字符串而重复地使用字符串连接操作符，需要n的平方级的时间。这是由于字符串不可变而导致的不幸结果。**当两个字符串被连接在一起时，它们的内容都要被拷贝。

## 通过接口引用对象

## 接口优先于反射机制
&emsp;&emsp;反射机制允许一个类使用一个类，即使当前者在编译的时候后者还根本不存在。然而，这种能力也要付出代价：
&emsp;&emsp;●**丧失了编译时类型检查的好处**
&emsp;&emsp;●**执行反射访问所需要的代码非常笨拙和冗长**
&emsp;&emsp;●**性能损失**
> &emsp;&emsp;核心反射机制最初是为了基于组件的应用创建工具而设计的。这类工具通常要根据需要装载类，并且用反射功能找出它们支持哪些方法和构造器。这些工具允许用户交互式地构建出访问这些类的应用程序，但是所产生出来的这些应用程序能够以正常的方式访问这些类，而不是以反射的方式。反射功能只是在设计时被用到。通常，普通应用程序在运行时不应该以反射方式访问对象。

&emsp;&emsp;如果编写的程序必须要与编译时未知的类一起工作，如有可能，就应该仅仅使用反射机制来实例化对象，而访问对象时则使用编译时已知的某个接口或者超类。

## 谨慎地使用本地方法
&emsp;&emsp;Java Native Interface（JNI）允许Java应用程序可以调用本地方法（native method），所谓本地方法是指用本地程序设计语言（比如C或者C++）来编写的特殊方法。本地方法在本地语言中可以执行任意的计算任务，并返回到Java程序设计语言。
>&emsp;&emsp;本地方法主要有三种用途：
&emsp;&emsp;1、提供了“访问特定平台的机制”的能力，比如注册表和文件锁。
&emsp;&emsp;2、提供了访问遗留代码库的能力，从而可以访问遗留数据。
&emsp;&emsp;3、可以通过本地语言，编写应该用程序中注重性能的部分，以提高系统的性能。

## 谨慎地进行优化
&emsp;&emsp;要努力编写好的程序而不是快的程序。
&emsp;&emsp;当一个系统设计完成之后，其中最难以更改的组件是那些指定了模块之间交互关系以及模块与外界交互关系的组件。
&emsp;&emsp;为获得好的性能而对API进行包装，这是一种非常不好的想法。导致对API进行包装的性能因素可能会在平台未来的发行版本中，或者在将来的底层软件中不复存在，但是被包装的API以及有它引起的问题将永远困扰着你。

## 遵守普遍接受的命名惯例
&emsp;&emsp;类型参数名称通常由单个字母组成。这个字母通常是以下五种类型之一：T表示任意的类型，E表示集合的元素类型，K和V表示映射的键和值类型，X表示异常。任何类型的序列可以是T、U、V或者T1、T2、T3。

## 只针对异常的情况才使用异常
&emsp;&emsp;**设计良好的API不应该强迫它的客户端为了正常的控制流而使用异常。**如果类具有“状态相关”的方法，即只有在特定状态的不可预知的条件下才可以被调用的方法，这个类往往也应该有个单独的“状态测试（state-testing）”方法，即指示是否可以调用这个状态相关的方法。例如Iterator接口有一个“状态相关”的next方法，和相应的状态测试方法hasNext。
&emsp;&emsp;另一种提供单独的状态测试方法的做法是，如果“状态相关的”方法被调用时，该对象处于不适当的状态之中，它就会返回一个可识别的值，比如null。这种方法对于Iterator而言并不合适，因为null是next方法的合法返回值。
&emsp;&emsp;对于“状态测试方法”和“可识别的返回值”这两种做法，有些指导原则可以帮助你在两者只用做出选择。如果对象将在缺少外部同步的情况下被并发访问，或者可被外界改变状态，使用可被识别的返回值可能很有必要的，因为在调用“状态测试”方法和调用相应的“状态相关”方法的时间间隔之中，对象的状态有可能会发生变化。如果单独的“状态测试”方法必须重复“状态相关”方法的工作，从性能的角度考虑，就应该使用可被识别的返回值。如果所有其他方面都是等同的，那么“状态测试”方法则略优于可被识别的返回值。它提供了更好的可读性，对于使用不同的情形，可能更加易于检测和改正：如果忘了去调用状态测试方法，状态相关的方法就会抛出异常，是这个Bug变得很明显；如果忘记了去检查可识别的返回值，这个Bug就很难会被发现。

## 对可恢复的情况使用受检异常，对编程错误使用运行时异常
&emsp;&emsp;如果期望调用者能够适当地恢复，对于这种情况就应该使用受检的异常。通过抛出受检的异常，强迫调用者在一个catch子句中处理该异常，或者将它传播出去。因此，方法中声明要抛出的每个受检异常，都是对API用户的一种潜在提示：与异常相关联的条件是调用这个方法的一种可能结果。
&emsp;&emsp;**对于可恢复的情况，使用受检异常；对于程序错误，则使用运行时异常。如果不清楚是否可能恢复，最好使用未受检的异常。**

## 避免不必要地使用受检的异常

## 优先使用标准的异常
| 异常        | 使用场合         |
| ------------- |:-------------|
| IllegalArgumentException   | 非null的参数值不正确 |
| IllegalStateException     | 对于方法方法调用而言，对象状态不合适     |
| NullPointerException | 在禁止使用null的情况下参数值为null     |
| IndexOutOfBoundsException| 下标参数值越界      |
| ConcurrentModificationException | 在禁止并发修改的情况下，检测到对象的并发修改      |
| UnsupportedOperationException| 对象不支持用户请求的方法     |

## 抛出与抽象相应的异常
&emsp;&emsp;更高层的实现应该捕获低层的异常，同时抛出可以按照高层抽象进行解释的异常。这种做法被称为异常转义。

## 每个方法抛出的异常都要有文档
&emsp;&emsp;```永远不要声明一个方法“throws Exception”，或者更糟糕的是声明“throws Throwble”，这是一个非常极端的例子。```

## 在细节消息中包含能捕获失败的信息

## 努力使失败保持原子性
&emsp;&emsp;一般而言，失败的方法调用应该使对象保持在被调用之前的状态。具有这种属性的方法被称为具有失败原子性。
&emsp;&emsp;有几种途径可以实现这种效果：
&emsp;&emsp;最简单的方法，设计一个不可变的对象。如果一个操作失败了，它可能会阻止创建新的对象，但是永远也不会使已有的对象保持在不一致的状态之中，因为当每个对象被创建之后，它处于一致的状态之中，以后也不会再发生变化。

## 同步访问共享的数据
&emsp;&emsp;如果读和写操作没有都被同步，同步就不会起作用。

## 避免过度同步
&emsp;&emsp;在同步区域之外被调用的外来方法被称作“开放调用（open call）”。除了可以避免死锁之外，开放调用还可以极大地增加并发性。
&emsp;&emsp;外来方法的运行时间可能会任意长。如果在同步区域内调用外来方法，其他线程对受保护资源的访问就会遭到不必要的拒绝。
&emsp;&emsp;**通常，应该在同步区域内做尽可能少的工作。**获得锁，检查共享数据，根据需要转换数据，然后放掉锁。如果你必须要执行某个很耗时的工作，则应该设法把这个动作移到同步区域的外面。
&emsp;&emsp;如果一个可变的类要并发使用，应该使这个类变成是线程安全的，通过内部同步，还可以获得明显比从外部锁定整个对象更高的并发性。否则，就不要在内部同步。让客户在必要的时候从外部同步。
&emsp;&emsp;如果你在内部同步了类，就可以使用不同的方法来实现高并发性，例如分拆锁（lock splitting）、分离锁（lock striping）和非阻塞（nonblocking）并发控制。
&emsp;&emsp;如果方法修改了静态域，那么必须同步对这个域的访问，即使它往往只用于单个线程。客户要在这种方法上执行外部同步是不可能的，因为不可能保证其他的客户也会执行外部同步。

## executor和task优先于线程
&emsp;&emsp;Executor Framework相关内容可参考《Java Concurrency in Practice》一书。

## 并发工具优先于wait和notify
&emsp;&emsp;java.util.concurrent中更高级的工具分成三类：Executor Framework、并发集合（Concurrent Collection）以及同步器（Synchronizer）。
&emsp;&emsp;**并发集合中不可能排除并发活动；将它锁定没有什么作用，只会使程序的速度变慢。**
&emsp;&emsp;同步器（Synchronizer）是一些使线程能够等待另一个线程的对象，允许它们协调动作。最常用的同步器是CountDownLatch和Semaphore。较不常用的是CyclicBarrier和Exchanger。
&emsp;&emsp;对于间歇式的定时，始终应该优先使用System.nanoTime，而不是使用System.currentTimeMills。
&emsp;&emsp;使用wait方法的标准模式：
``` java
synchronized(obj){
    while(<condition does not hold>){
        obj.wait();//(Releases lock, and reacquires on wakeup)
    }
    ...// Perform action appropriate to condition 
}
```
&emsp;&emsp;**始终应该使用wait循环模式来调用wait方法；永远不要在循环之外调用wait方法。**循环会在等待之前和之后测试条件。

## 线程安全性的文档化
&emsp;&emsp;线程安全性有多个级别：
&emsp;&emsp;1、不可变的（immutable）——这个类的实例时不可变的。所以，不需要外部的同步。这样的例子包括String、Long和BigInteger。
&emsp;&emsp;2、无条件的线程安全（unconditionally thread-safe）——这个类的实例时可变的，但是这类有着足够的内部同步，所以，它的实例可以被并发使用，无需任何外部同步。其例子包括Random和ConcurrentHashMap。
&emsp;&emsp;3、有条件的线程安全（conditionally thread-safe）——除了有些方法为进行安全的并发使用而需要外部同步之外，这种线程安全级别与无条件的线程安全相同。这样的例子包括Collecitons.synchronized包装返回的集合。它们的迭代器是（iterator）要求外部同步。
&emsp;&emsp;4、非线程安全（not thread-safe）——这个类的实例是可变的。为了并发地使用它们，客户必须利用自己选择的外部同步包围每个方法调用（或者调用序列）。这样的例子包括通用的集合实现，例如ArrayList和HashMap。
&emsp;&emsp;5、线程对立的（thread-hostile）——这个类不能安全地被多个线程并发使用，即使所有的方法调用都被外部同步包围。线程对立的根源通常在于，没有同步地修改静态数据。

## 慎用延迟初始化

## 不要依赖于线程调度器

## 避免使用线程组

## 谨慎地实现Serializable接口
&nbsp;&nbsp;**实现Serializable接口而付出的最大代价是，一旦一个类被发布，就大大降低了“改变这个类的实现”的灵活性。
&nbsp;&nbsp;序列化会使类的演变收到限制，这种限制的一个例子与**流的唯一标识符（stream unique identifier）**有关，通常它也被称为**序列版本UID（serial version UID）**。每个可序列化的类都有一个唯一标识号与它想关联。如果你没在一个名为serialVersionUID的稀有静态fianl的long域中显式地指定该标志符号，系统就会自动地根据这个类来调用一个复杂的运算过程，从而在运行时产生该标识号。这个自动产生的值会受到类名称、它所实现的接口的名称、以及所有共有的和受保护的成员的名称所受影响。如果你通过任何方式改变了这些信息，比如增加了一个不是很重要的工具方法，自动产生的序列版本UID也会发生变化。因此，如果没有声明一个显式的序列版本UID，兼容性将会遭到破坏，在运行时导致InvalidClassException异常。
&nbsp;&nbsp;**为了继承而设计的类应该尽可能少地去实现Serializable接口，用户的接口也应该尽可能少地继承Serializable接口。**在为了继承而设计的类中，真正实现了Serializable接口的有Throwable类、Component和HttpServlet抽象类。因为Throwable类实现了Serializable接口，所以RMI的异常可以从服务器端传到客户端。Component实现了Serializable接口，因此GUI可以被发送、保存和恢复。HttpServlet实现了Serializable接口，因此会话状态可以被（session state）缓存。
&nbsp;&nbsp;**内部类（inner class）不应该实现Serializable。内部类的默认序列化形式是定义不清楚的。然而，静态成员类（static member class）却可以实现Serializable接口。**``实现Serializable接口是个很严肃的承诺，必须认真对待。``在“允许子类实现Serializable接口”或“禁止子类实现Serializable接口”两者之间的一个折中设计方案是，提供一个可访问的无参构造器。这种设计方案（但不要求）子类实现Serializable接口。

## 考虑使用自定义的序列化形式
&nbsp;&nbsp;当一个对象的物理表示法与它的逻辑数据内容有实质性的区别时，使用默认序列化形式会有以下4个缺点：  
&nbsp;&nbsp;**1、它是这个类的导出API永远地束缚在该类的内部表示法上。**
&nbsp;&nbsp;**2、它会消耗很多的空间。**  
&nbsp;&nbsp;**3、它会消耗很多的时间。**序列化逻辑并不了解对象图的拓扑关系，所以它必须经过一个昂贵的图遍历过程。
&nbsp;&nbsp;**4、它会引起栈溢出**
&nbsp;&nbsp;**如果所有的实例域都是瞬时的，从技术角度而言，不调用defaultWriteObject和defaultReadObject也是允许的，但是不推荐这么做。**即使所有的实例域都是transient的，调用defaultWriteObject也会影响该类的序列化形式，从而极大地增强灵活性。这样得到德尔序列化形式允许在以后的发行版本中增加非transient的实例域，并且还能保持向前或者向后的兼容性。
&nbsp;&nbsp;以下情况应当将域标记为transient：
&nbsp;&nbsp;●值可以根据其他“基本数据域”计算而得到。
&nbsp;&nbsp;●值依赖与JVM的某一次运行。
&nbsp;&nbsp;如果使用默认的序列化形式，并且把域标记为transient，当实例被反序列化的时候，这些域将被初始化为它们的默认值。对于对象引用域，默认值为null。
&nbsp;&nbsp;无论是否使用默认的序列化形式，**如果在读取整个对象状态的任何其他方法上强制任何同步，则也必须在对象序列化上强制这种同步。**因此，如果有一个线程安全的对象，通过同步每个方法实现了它的线程安全，并且选择使用默认的序列化形式。就要使用下列的writeObject方法：
``` java
private synchronized void writeObject(ObjectOutputStream s) throws IOExceprtion {
    s.defaultWriteObject();
}
```

## 保护性地编写readObject方法
&nbsp;&nbsp;对于非final的可序列化的类，在readObject方法和构造器之间还有其他类似的地方。readObject方法不可以调用可被覆盖的方法，无论是直接使用还是间接调用都不可以。
&nbsp;&nbsp;以下指导方正有助于编写出更加及健壮的readObject方法：
>&nbsp;&nbsp;●对于对象引用域必须保持为私有的类，要保护性地拷贝这些域中的每个对象。不可变类的可变组件就属于这一类别。
>&nbsp;&nbsp;●对于任何约束条件检查动作，都应该跟在所有的保护性拷贝之后。
>&nbsp;&nbsp;●如果整个对象图在被反序列化之后进行验证，就应该使用ObjectInputValidation接口。
>&nbsp;&nbsp;●无论是直接方式还是间接方式，都不要调用类中任何可被覆盖的方法。

## 对于实例控制，枚举类型优先于readResolve
