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

## 是可变性最小化
