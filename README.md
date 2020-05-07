# 面向对象和面向过程的区别
面向过程 ：面向过程性能比面向对象高。 因为类调用时需要实例化，开销比较大，比较消耗资源，所以当性能是最重要的考量因素的时候，比如单片机、嵌入式开发、Linux/Unix等一般采用面向过程开发。但是，面向过程没有面向对象易维护、易复用、易扩展。

面向对象 ：面向对象易维护、易复用、易扩展。 因为面向对象有封装、继承、多态性的特性，所以可以设计出低耦合的系统，使系统更加灵活、更加易于维护。但是，面向对象性能比面向过程低。

# 关于 JVM JDK 和 JRE 最详细通俗的解答
Java虚拟机（JVM）是运行 Java 字节码的虚拟机。JVM有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果。

JDK是Java Development Kit，它是功能齐全的Java SDK。它拥有JRE所拥有的一切，还有编译器（javac）和工具（如javadoc和jdb）。它能够创建和编译程序。

JRE 是 Java运行时环境。它是运行已编译 Java 程序所需的所有内容的集合，包括 Java虚拟机（JVM），Java类库，java命令和其他的一些基础构件。但是，它不能用于创建新程序。

# Java基本数据类型
1.整型

	类型              存储需求     bit数    取值范围      备注

	int               4字节        4*8 

	short             2字节        2*8    －32768～32767

	long              8字节        8*8

	byte              1字节        1*8     －128～127

2.浮点型

	类型              存储需求     bit数    取值范围      备注

	float              4字节      4*8                  float类型的数值有一个后缀F(例如：3.14F)

	double             8字节      8*8                  没有后缀F的浮点数值(如3.14)默认为double类型

3.char类型

	类型              存储需求     bit数     取值范围      备注

	char              2字节       2*8

4.boolean类型

	类型           存储需求    bit数    取值范围      备注

	boolean        1字节      1*8      false、true

# public、private、protecte、default
public： Java语言中访问限制最宽的修饰符，一般称之为“公共的”。被其修饰的类、属性以及方法不仅可以跨类访问，而且允许跨包（package）访问。

private: Java语言中对访问权限限制的最窄的修饰符，一般称之为“私有的”。被其修饰的类、属性以及方法只能被该类的对象访问，其子类不能访问，更不能允许跨包访问。

protect: 介于public 和 private 之间的一种访问修饰符，一般称之为“保护形”。被其修饰的类、属性以及方法只能被类本身的方法及子类访问，即使子类在不同的包中也可以访问。

default：即不加任何访问修饰符，通常称为“默认访问模式“。该模式下，只允许在同一个包中进行访问。

# 浅拷贝与深拷贝
## 浅拷贝
所谓的浅拷贝就是拷贝指向对象的指针,意思就是说:拷贝出来的目标对象的指针和源对象的指针指向的内存空间是同一块空间.
浅拷贝只是一种简单的拷贝,让几个对象公用一个内存,然而当内存销毁的时候,指向这个内存空间的所有指针需要重新定义,不然会造成野指针错误

## 深拷贝
所谓的深拷贝指拷贝对象的具体内容,其内容地址是自助分配的,拷贝结束之后,内存中的值是完全相同的,但是内存地址是不一样的,两个对象之间相互不影响,也互不干涉.


# Servlet生命周期
主要有三个方法：

init()初始化阶段

service()处理客户端请求阶段

destroy()终止阶段

## 初始化阶段：
Servlet容器加载Servlet，加载完成后，Servlet容器会创建一个Servlet实例并调用init()方法，init()方法只会调用一次，
Servlet容器会在一下几种情况装载Servlet：

1，Servlet容器启动时自动装载某些servlet，实现这个需要在web.xml文件中添加load-on-startup=1

2，在Servlet容器启动后，客户首次向Servlet发送请求

3，Servlet类文件被更新后，重新装载

## 处理客户端请求阶段：
每收到一个客户端请求，服务器就会产生一个新的线程去处理。
对于用户的Servlet请求，Servlet容器会创建一个特定于请求的ServletRequest和ServletResponse。
对于tomcat来说，它会将传递来的参数放入一个HashTable中，这是一个String-->String[]的键值映射

## 终止阶段：
当web应用被终止，或者Servlet容器终止运行，或者Servlet重新装载Servlet新实例时，Servlet容器会调用Servlet的destroy()方法

# Java 序列化及实现
## 序列化
序列化：把对象转换为字节序列的过程称为对象的序列化。

反序列化：把字节序列恢复为对象的过程称为对象的反序列化。

## 实现
	/**
     * 序列化
     */
    private static void serializeFlyPig() throws IOException {
        FlyPig flyPig = new FlyPig();
        flyPig.setColor("black");
        flyPig.setName("naruto");
        flyPig.setCar("0000");
        // ObjectOutputStream 对象输出流，将 flyPig 对象存储到E盘的 flyPig.txt 文件中，完成对 flyPig 对象的序列化操作
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(new File("d:/flyPig.txt")));
        oos.writeObject(flyPig);
        System.out.println("FlyPig 对象序列化成功！");
        oos.close();
    }
 
    /**
     * 反序列化
     */
    private static FlyPig deserializeFlyPig() throws Exception {
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream(new File("d:/flyPig.txt")));
        FlyPig person = (FlyPig) ois.readObject();
        System.out.println("FlyPig 对象反序列化成功！");
        return person;
    }


# Java和C++的区别
都是面向对象的语言，都支持封装、继承和多态

Java 不提供指针来直接访问内存，程序内存更加安全

Java 的类是单继承的，C++ 支持多重继承；虽然 Java 的类不可以多继承，但是接口可以多继承。

Java 有自动内存管理机制，不需要程序员手动释放无用内存

# 字符型常量和字符串常量的区别
形式上: 字符常量是单引号引起的一个字符; 字符串常量是双引号引起的若干个字符

含义上: 字符常量相当于一个整型值( ASCII 值),可以参加表达式运算; 字符串常量代表一个地址值(该字符串在内存中存放位置)

占内存大小 字符常量只占2个字节; 字符串常量占若干个字节(至少一个字符结束标志) (注意： char在Java中占两个字节)

# 重载和重写的区别
重载： 发生在同一个类中，方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同，发生在编译时。

重写： 发生在父子类中，方法名、参数列表必须相同，返回值范围小于等于父类，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类；如果父类方法访问修饰符为 private 则子类就不能重写该方法。

# 构造器 Constructor 是否可被 override
在讲继承的时候我们就知道父类的私有属性和构造方法并不能被继承，所以 Constructor 也就不能被 override（重写）,但是可以 overload（重载）,所以你可以看到一个类中有多个构造函数的情况。

# Java 面向对象编程三大特性: 封装 继承 多态
封装把一个对象的属性私有化，同时提供一些可以被外界访问的属性的方法，如果属性不想被外界访问，我们大可不必提供方法给外界访问。但是如果一个类没有提供给外界访问的方法，那么这个类也没有什么意义了。

继承是使用已存在的类的定义作为基础建立新类的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能，但不能选择性地继承父类。通过使用继承我们能够非常方便地复用以前的代码。

关于继承如下 3 点请记住：

子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，只是拥有。
子类可以拥有自己属性和方法，即子类可以对父类进行扩展。
子类可以用自己的方式实现父类的方法。（以后介绍）。

多态就是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量到底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。

在Java中有两种形式可以实现多态：继承（多个子类对同一方法的重写）和接口（实现接口并覆盖接口中同一方法）。

## 继承与聚合的区别
继承指的是一个类继承另外的一个类的功能，并可以增加它自己的新功能的能力，继承是类与类或者接口与接口之间最常见的关系；在Java中此类关系通过关键字extends明确标识。

聚合指的是聚合体现的是整体与部分、拥有的关系，此时整体与部分之间是可分离的，他们可以具有各自的生命周期；

# Java对象实例化顺序
Java程序在执行过程中，类，对象以及它们成员加载、初始化的顺序如下： 

1、首先加载要创建对象的类及其直接与间接父类。 

2、在类被加载的同时会将静态成员进行加载，主要包括静态成员变量的初始化，静态语句块的执行，在加载时按代码的先后顺序进行。 

3、需要的类加载完成后，开始创建对象，首先会加载非静态的成员，主要包括非静态成员变量的初始化，非静态语句块的执行，在加载时按代码的先后顺序进行。 

4、最后执行构造器，构造器执行完毕，对象生成。

所以java对象实例化时的顺序为：

1，父类的静态成员变量和静态代码块加载

2，子类的静态成员变量和静态代码块加载

3，父类成员变量和方法块加载

4，父类的构造函数加载

5，子类成员变量和方法块加载

6，子类的构造函数加载


# 反射机制与使用场景
JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。

## 优缺点
优点： 运7行期类型的判断，动态加载类，提高代码灵活度。
缺点： 性能瓶颈：反射相当于一系列解释操作，通知 JVM 要做的事情，性能比直接的java代码要慢很多。

## 三种方式
对象.getClass()方式

类名.Class方式

Class.forName( 类的包名 ) 方式

### Class.forName和classloader的区别
class.forName()前者除了将类的.class文件加载到jvm中之外，还会对类进行解释，执行类中的static块。
而classLoader只干一件事情，就是将.class文件加载到jvm中，不会执行static中的内容,只有在newInstance才会去执行static块。
Class.forName(name, initialize, loader)带参函数也可控制是否加载static块。并且只有调用了newInstance()方法采用调用构造函数，创建类的对象


## 场景
①我们在使用JDBC连接数据库时使用Class.forName()通过反射加载数据库的驱动程序；②Spring框架也用到很多反射机制，最经典的就是xml的配置模式。Spring 通过 XML 配置模式装载 Bean 的过程：1) 将程序内所有 XML 或 Properties 配置文件加载入内存中; 2)Java类里面解析xml或properties里面的内容，得到对应实体类的字节码字符串以及相关的属性信息; 3)使用反射机制，根据这个字符串获得某个类的Class实例; 4)动态配置实例的属性

# 无参构造方法的作用
Java 程序在执行子类的构造方法之前，如果没有用 super() 来调用父类特定的构造方法，则会调用父类中“没有参数的构造方法”。因此，如果父类中只定义了有参数的构造方法，而在子类的构造方法中又没有用 super() 来调用父类中特定的构造方法，则编译时将发生错误，因为 Java 程序在父类中找不到没有参数的构造方法可供执行。解决办法是在父类里加上一个不做事且没有参数的构造方法。 

# 自动装箱与拆箱
装箱：将基本类型用它们对应的引用类型包装起来；
拆箱：将包装类型转换为基本数据类型；

# 接口和抽象类的区别
接口的方法默认是 public，所有方法在接口中不能有实现(Java 8 开始接口方法可以有默认实现），而抽象类可以有非抽象的方法。

接口中除了static、final变量，不能有其他变量，而抽象类中则不一定。

一个类可以实现多个接口，但只能继承一个抽象类。接口自己本身可以通过extends关键字扩展多个接口。

接口方法默认修饰符是public，抽象方法可以有public、protected和default这些修饰符（抽象方法就是为了被重写所以不能使用private关键字修饰！）。

从设计层面来说，抽象是对类的抽象，是一种模板设计，而接口是对行为的抽象，是一种行为的规范。

# 对象的相等与指向他们的引用相等
对象的相等，比的是内存中存放的内容是否相等。而引用相等，比较的是他们指向的内存地址是否相等。

# == 与 equals
== : 它的作用是判断两个对象的地址是不是相等。即，判断两个对象是不是同一个对象(基本数据类型==比较的是值，引用数据类型==比较的是内存地址)。

equals() : 它的作用也是判断两个对象是否相等。但它一般有两种使用情况：

情况1：类没有覆盖 equals() 方法。则通过 equals() 比较该类的两个对象时，等价于通过“==”比较这两个对象。

情况2：类覆盖了 equals() 方法。一般，我们都覆盖 equals() 方法来比较两个对象的内容是否相等；若它们的内容相等，则返回 true (即，认为这两个对象相等)。

String 中的 equals 方法是被重写过的，因为 object 的 equals 方法是比较的对象的内存地址，而 String 的 equals 方法比较的是对象的值。
当创建 String类型的对象时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋给当前引用。如果没有就在常量池中重新创建一个 String 对象。

# String 
## equals()

	public boolean equals(Object anObject) {
	        if (this == anObject) {
	            return true;
	        }
	        if (anObject instanceof String) {
	            String anotherString = (String)anObject;
	            int n = value.length;
	            if (n == anotherString.value.length) {
	                char v1[] = value;
	                char v2[] = anotherString.value;
	                int i = 0;
	                while (n-- != 0) {
	                    if (v1[i] != v2[i])
	                        return false;
	                    i++;
	                }
	                return true;
	            }
	        }
	        return false;
	    }

## hashcode()

	public int hashCode() {
	        int h = hash;
	        if (h == 0 && value.length > 0) {
	            char val[] = value;

	            for (int i = 0; i < value.length; i++) {
	                h = 31 * h + val[i];
	            }
	            hash = h;
	        }
	        return h;
	    }


# String StringBuffer 和 StringBuilder 的区别是什么? String 为什么是不可变的?
## 可变性

简单的来说：String 类中使用 final 关键字修饰字符数组来保存字符串，private　final　char　value[]，所以 String 对象是不可变的。而StringBuilder 与 StringBuffer 都继承自 AbstractStringBuilder 类，在 AbstractStringBuilder 中也是使用字符数组保存字符串char[]value 但是没有用 final 关键字修饰，所以这两种对象都是可变的。

## 线程安全性

String 中的对象是不可变的，也就可以理解为常量，线程安全。AbstractStringBuilder 是 StringBuilder 与 StringBuffer 的公共父类，定义了一些字符串的基本操作，如 expandCapacity、append、insert、indexOf 等公共方法。StringBuffer 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。StringBuilder 并没有对方法进行加同步锁，所以是非线程安全的。　

## 性能

每次对 String 类型进行改变的时候，都会生成一个新的 String 对象，然后将指针指向新的 String 对象。StringBuffer 每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 StringBuilder 相比使用 StringBuffer 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

## 实现
### String
	public final class String implements java.io.Serializable, Comparable<String>, CharSequence {

    private final char value[];


    private int hash; // Default to 0


    private static final long serialVersionUID = -6849794470754667710L;

    private static final ObjectStreamField[] serialPersistentFields =
        new ObjectStreamField[0];

    .....

	}

### StringBuilder
	public final class StringBuilder extends AbstractStringBuilder implements java.io.Serializable, CharSequence
	{

	    /** use serialVersionUID for interoperability */
	    static final long serialVersionUID = 4383685877147921099L;

	    @Override
	    public StringBuilder append(String str) {
	        super.append(str);
	        return this;
	    }

	    ...

	}


### StringBuffer
	public final class StringBuffer extends AbstractStringBuilder implements java.io.Serializable, CharSequence{

	    /**
	     * A cache of the last value returned by toString. Cleared
	     * whenever the StringBuffer is modified.
	     */
	    private transient char[] toStringCache;

	    /** use serialVersionUID from JDK 1.0.2 for interoperability */
	    static final long serialVersionUID = 3388685877147921107L;

	    @Override
	    public synchronized StringBuffer append(String str) {
	        toStringCache = null;
	        super.append(str);
	        return this;
	    }

	    .....
	}

## 对于三者使用的总结：

操作少量的数据: 适用String；

单线程操作字符串缓冲区下操作大量数据: 适用StringBuilder；

多线程操作字符串缓冲区下操作大量数据: 适用StringBuffer；

选择数字31是因为它是一个奇质数，如果选择一个偶数会在乘法运算中产生溢出，导致数值信息丢失，因为乘二相当于移位运算。选择质数的优势并不是特别的明显，但这是一个传统。同时，数字31有一个很好的特性，即乘法运算可以被移位和减法运算取代，来获取更好的性能：31 * i == (i << 5) - i，现代的 Java 虚拟机可以自动的完成这个优化。

# hashCode 与 equals
面试官可能会问你：“你重写过 hashcode 和 equals 么，为什么重写equals时必须重写hashCode方法？”

## hashCode（）介绍

hashCode() 的作用是获取哈希码，也称为散列码；它实际上是返回一个int整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。hashCode() 定义在JDK的Object.java中，这就意味着Java中的任何类都包含有hashCode() 函数。

散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）

为什么要有 hashCode

我们先以“HashSet 如何检查重复”为例子来说明为什么要有 hashCode： 当你把对象加入 HashSet 时，HashSet 会先计算对象的 hashcode 值来判断对象加入的位置，同时也会与其他已经加入的对象的 hashcode 值作比较，如果没有相符的hashcode，HashSet会假设对象没有重复出现。但是如果发现有相同 hashcode 值的对象，这时会调用 equals（）方法来检查 hashcode 相等的对象是否真的相同。如果两者相同，HashSet 就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。（摘自我的Java启蒙书《Head first java》第二版）。这样我们就大大减少了 equals 的次数，相应就大大提高了执行速度。

通过我们可以看出：hashCode() 的作用就是获取哈希码，也称为散列码；它实际上是返回一个int整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。**hashCode() 在散列表中才有用，在其它情况下没用。**在散列表中hashCode() 的作用是获取对象的散列码，进而确定该对象在散列表中的位置。

## hashCode（）与equals（）的相关规定

如果两个对象相等，则hashcode一定也是相同的

两个对象相等,对两个对象分别调用equals方法都返回true 

两个对象有相同的hashcode值，它们也不一定是相等的

因此，equals 方法被覆盖过，则 hashCode 方法也必须被覆盖

hashCode() 的默认行为是对堆上的对象产生独特值。如果没有重写 hashCode()，则该 class 的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）

# final
对于一个final变量，如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。

当用final修饰一个类时，表明这个类不能被继承。final类中的所有成员方法都会被隐式地指定为final方法。

使用final方法的原因有两个。第一个原因是把方法锁定，以防任何继承类修改它的含义；第二个原因是效率。在早期的Java实现版本中，会将final方法转为内嵌调用。但是如果方法过于庞大，可能看不到内嵌调用带来的任何性能提升（现在的Java版本已经不需要使用final方法进行这些优化了）。类中所有的private方法都隐式地指定为final。

# static
修饰成员变量和成员方法: 被 static 修饰的成员属于类，不属于单个这个类的某个对象，被类中所有对象共享，可以并且建议通过类名调用。被static 声明的成员变量属于静态成员变量，静态变量 存放在 Java 内存区域的方法区。调用格式：类名.静态变量名 类名.静态方法名()

静态代码块: 静态代码块定义在类中方法外, 静态代码块在非静态代码块之前执行(静态代码块—>非静态代码块—>构造方法)。 该类不管创建多少对象，静态代码块只执行一次.

静态内部类（static修饰类的话只能修饰内部类）： 静态内部类与非静态内部类之间存在一个最大的区别: 非静态内部类在编译完成之后会隐含地保存着一个引用，该引用是指向创建它的外围类，但是静态内部类却没有。没有这个引用就意味着：1. 它的创建是不需要依赖外围类的创建。2. 它不能使用任何外围类的非static成员变量和方法。

静态导包(用来导入类中的静态资源，1.5之后的新特性): 格式为：import static 这两个关键字连用可以指定导入某个类中的指定静态资源，并且不需要使用类名调用类中静态成员，可以直接使用类中静态成员变量和成员方法。

# transient
对于不想进行序列化的变量，使用transient关键字修饰。

transient关键字的作用是：阻止实例中那些用此关键字修饰的的变量序列化；当对象被反序列化时，被transient修饰的变量值不会被持久化和恢复。transient只能修饰变量，不能修饰类和方法。

# volatile (可保证可见性和有序性，不保证原子性)
volatile的用法比较简单，只需要在声明一个可能被多线程同时访问的变量时，使用volatile修饰就可以了。

如果一个变量被volatile所修饰的话，在每次数据变化之后，其值都会被强制刷入主存。而其他处理器的缓存由于遵守了缓存一致性协议，也会把这个变量的值从主存加载到自己的缓存中。这就保证了一个volatile在并发编程中，其值在多个缓存中是可见的。

volatile可以禁止指令重排，这就保证了代码的程序会严格按照代码的先后顺序执行。这就保证了有序性。被volatile修饰的变量的操作，会严格按照代码顺序执行，load->add->save 的执行顺序就是：load、add、save.

原子性是指一个操作是不可中断的，要全部执行完成，要不就都不执行.volatile是不能保证原子性的。

# volatile 与 synchronized
volatile本质是在告诉jvm当前变量在寄存器（工作内存）中的值是不确定的，需要从主存中读取；

synchronized则是锁定当前变量，只有当前线程可以访问该变量，其他线程被阻塞住。

volatile仅能使用在变量级别；synchronized则可以使用在变量、方法、和类级别的

volatile仅能实现变量的修改可见性，不能保证原子性；而synchronized则可以保证变量的修改可见性和原子性

volatile不会造成线程的阻塞；synchronized可能会造成线程的阻塞。

volatile标记的变量不会被编译器优化；synchronized标记的变量可以被编译器优化

# BIO,NIO,AIO
BIO (Blocking I/O): 同步阻塞I/O模式，数据的读取写入必须阻塞在一个线程内等待其完成。在活动连接数不是特别高（小于单机1000）的情况下，这种模型是比较不错的，可以让每一个连接专注于自己的 I/O 并且编程模型简单，也不用过多考虑系统的过载、限流等问题。线程池本身就是一个天然的漏斗，可以缓冲一些系统处理不了的连接或请求。但是，当面对十万甚至百万级连接的时候，传统的 BIO 模型是无能为力的。因此，我们需要一种更高效的 I/O 处理模型来应对更高的并发量。

NIO (New I/O): NIO是一种同步非阻塞的I/O模型，在Java 1.4 中引入了NIO框架，对应 java.nio 包，提供了 Channel , Selector，Buffer等抽象。NIO中的N可以理解为Non-blocking，不单纯是New。它支持面向缓冲的，基于通道的I/O操作方法。 NIO提供了与传统BIO模型中的 Socket 和 ServerSocket 相对应的 SocketChannel 和 ServerSocketChannel 两种不同的套接字通道实现,两种通道都支持阻塞和非阻塞两种模式。阻塞模式使用就像传统中的支持一样，比较简单，但是性能和可靠性都不好；非阻塞模式正好与之相反。对于低负载、低并发的应用程序，可以使用同步阻塞I/O来提升开发速率和更好的维护性；对于高负载、高并发的（网络）应用，应使用 NIO 的非阻塞模式来开发

AIO (Asynchronous I/O): AIO 也就是 NIO 2。在 Java 7 中引入了 NIO 的改进版 NIO 2,它是异步非阻塞的IO模型。异步 IO 是基于事件和回调机制实现的，也就是应用操作之后会直接返回，不会堵塞在那里，当后台处理完成，操作系统会通知相应的线程进行后续的操作。AIO 是异步IO的缩写，虽然 NIO 在网络操作中，提供了非阻塞的方法，但是 NIO 的 IO 行为还是同步的。对于 NIO 来说，我们的业务线程是在 IO 操作准备好时，得到通知，接着就由这个线程自行进行 IO 操作，IO操作本身是同步的。

# Reactor和Proactor模型（https://blog.csdn.net/u013074465/article/details/46276967
 Reactor模式是处理并发I/O比较常见的一种模式，用于同步I/O，中心思想是将所有要处理的I/O事件注册到一个中心I/O多路复用器上，同时主线程/进程阻塞在多路复用器上；一旦有I/O事件到来或是准备就绪(文件描述符或socket可读、写)，多路复用器返回并将事先注册的相应I/O事件分发到对应的处理器中。

　　Reactor是一种事件驱动机制，和普通函数调用的不同之处在于：应用程序不是主动的调用某个API完成处理，而是恰恰相反，Reactor逆置了事件处理流程，应用程序需要提供相应的接口并注册到Reactor上，如果相应的事件发生，Reactor将主动调用应用程序注册的接口，这些接口又称为“回调函数”。用“好莱坞原则”来形容Reactor再合适不过了：不要打电话给我们，我们会打电话通知你。

       Reactor模式与Observer模式在某些方面极为相似：当一个主体发生改变时，所有依属体都得到通知。不过，观察者模式与单个事件源关联，而反应器模式则与多个事件源关联 。

在Reactor模式中，有5个关键的参与者：

1，描述符（handle）：由操作系统提供的资源，用于识别每一个事件，如Socket描述符、文件描述符、信号的值等。在Linux中，它用一个整数来表示。事件可以来自外部，如来自客户端的连接请求、数据等。事件也可以来自内部，如信号、定时器事件。

2，同步事件多路分离器（event demultiplexer）：事件的到来是随机的、异步的，无法预知程序何时收到一个客户连接请求或收到一个信号。所以程序要循环等待并处理事件，这就是事件循环。在事件循环中，等待事件一般使用I/O复用技术实现。在linux系统上一般是select、poll、epol_waitl等系统调用，用来等待一个或多个事件的发生。I/O框架库一般将各种I/O复用系统调用封装成统一的接口，称为事件多路分离器。调用者会被阻塞，直到分离器分离的描述符集上有事件发生。

3，事件处理器（event handler）：I/O框架库提供的事件处理器通常是由一个或多个模板函数组成的接口。这些模板函数描述了和应用程序相关的对某个事件的操作，用户需要继承它来实现自己的事件处理器，即具体事件处理器。因此，事件处理器中的回调函数一般声明为虚函数，以支持用户拓展。

4，具体的事件处理器（concrete event handler）：是事件处理器接口的实现。它实现了应用程序提供的某个服务。每个具体的事件处理器总和一个描述符相关。它使用描述符来识别事件、识别应用程序提供的服务。

5， 管理器（reactor）：定义了一些接口，用于应用程序控制事件调度，以及应用程序注册、删除事件处理器和相关的描述符。它是事件处理器的调度核心。 Reactor管理器使用同步事件分离器来等待事件的发生。一旦事件发生，Reactor管理器先是分离每个事件，然后调度事件处理器，最后调用相关的模 板函数来处理这个事件。

Reactor管理器并不是应用程序负责等待事件、分离事件和调度事件。Reactor并没有被具体的事件处理器调度，而是管理器调度具体的事件处理器，由事件处理器对发生的事件作出处理，这就是Hollywood原则。应用程序要做的仅仅是实现一个具体的事件处理器，然后把它注册到Reactor管理器中。接下来的工作由管理器来完成：如果有相应的事件发生，Reactor会主动调用具体的事件处理器，由事件处理器对发生的事件作出处理。


# Java 集合（https://www.jianshu.com/p/50e19038e361

# List,Set,Map
List(对付顺序的好帮手)： List接口存储一组不唯一（可以有多个元素引用相同的对象），有序的对象

Set(注重独一无二的性质): 不允许重复的集合。不会有多个元素引用相同的对象。

Map(用Key来搜索的专家): 键值对存储。Map会维护与Key有关联的值。两个Key可以引用相同的对象，但Key不能重复，典型的Key是String类型，但也可以是任何对象。

# Arraylist 与 LinkedList
## ArrayList
	public class ArrayList<E> extends AbstractList<E> implements List<E>, RandomAccess, Cloneable, java.io.Serializable{
	    private static final long serialVersionUID = 8683452581122892189L;

	    /**
	     * Default initial capacity.
	     */
	    private static final int DEFAULT_CAPACITY = 10;

	    /**
	     * Shared empty array instance used for empty instances.
	     */
	    private static final Object[] EMPTY_ELEMENTDATA = {};

	    /**
	     * Shared empty array instance used for default sized empty instances. We
	     * distinguish this from EMPTY_ELEMENTDATA to know how much to inflate when
	     * first element is added.
	     */
	    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

	    /**
	     * The array buffer into which the elements of the ArrayList are stored.
	     * The capacity of the ArrayList is the length of this array buffer. Any
	     * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
	     * will be expanded to DEFAULT_CAPACITY when the first element is added.
	     */
	    transient Object[] elementData; // non-private to simplify nested class access

	    /**
	     * The size of the ArrayList (the number of elements it contains).
	     *
	     * @serial
	     */
	    private int size;

	    ...
    }

## LinkedList
	public class LinkedList<E> extends AbstractSequentialList<E> implements List<E>, Deque<E>, Cloneable, java.io.Serializable{
	    transient int size = 0;

	    /**
	     * Pointer to first node.
	     * Invariant: (first == null && last == null) ||
	     *            (first.prev == null && first.item != null)
	     */
	    transient Node<E> first;

	    /**
	     * Pointer to last node.
	     * Invariant: (first == null && last == null) ||
	     *            (last.next == null && last.item != null)
	     */
	    transient Node<E> last;

	    ...

	}

1. 是否保证线程安全： ArrayList 和 LinkedList 都是不同步的，也就是不保证线程安全；

2. 底层数据结构： Arraylist 底层使用的是 Object 数组；LinkedList 底层使用的是 双向链表 数据结构（JDK1.6之前为循环链表，JDK1.7取消了循环。注意双向链表和双向循环链表的区别，下面有介绍到！）

3. 插入和删除是否受元素位置的影响： ① ArrayList 采用数组存储，所以插入和删除元素的时间复杂度受元素位置的影响。 比如：执行add(E e) 方法的时候， ArrayList 会默认在将指定的元素追加到此列表的末尾，这种情况时间复杂度就是O(1)。但是如果要在指定位置 i 插入和删除元素的话（add(int index, E element) ）时间复杂度就为 O(n-i)。因为在进行上述操作的时候集合中第 i 和第 i 个元素之后的(n-i)个元素都要执行向后位/向前移一位的操作。 ② LinkedList 采用链表存储，所以插入，删除元素时间复杂度不受元素位置的影响，都是近似 O（1）而数组为近似 O（n）。

4. 是否支持快速随机访问： LinkedList 不支持高效的随机元素访问，而 ArrayList 支持。快速随机访问就是通过元素的序号快速获取元素对象(对应于get(int index) 方法)。

5. 内存空间占用： ArrayList的空 间浪费主要体现在在list列表的结尾会预留一定的容量空间，而LinkedList的空间花费则体现在它的每一个元素都需要消耗比ArrayList更多的空间（因为要存放直接后继和直接前驱以及数据）。

# HashMap, Hashtable, HashSet
线程是否安全： HashMap 是非线程安全的，HashTable 是线程安全的；HashTable 内部的方法基本都经过synchronized 修饰。（如果你要保证线程安全的话就使用 ConcurrentHashMap 吧！）；

效率： 因为线程安全的问题，HashMap 要比 HashTable 效率高一点。另外，HashTable 基本被淘汰，不要在代码中使用它；

对Null key 和Null value的支持： HashMap 中，null 可以作为键，这样的键只有一个，可以有一个或多个键所对应的值为 null。但是在 HashTable 中 put 进的键值只要有一个 null，直接抛出 NullPointerException。

初始容量大小和每次扩充容量大小的不同 ： ①创建时如果不指定容量初始值，Hashtable 默认的初始大小为11，之后每次扩充，容量变为原来的2n+1。HashMap 默认的初始化大小为16。之后每次扩充，容量变为原来的2倍。②创建时如果给定了容量初始值，那么 Hashtable 会直接使用你给定的大小，而 HashMap 会将其扩充为2的幂次方大小（HashMap 中的tableSizeFor()方法保证，下面给出了源代码）。也就是说 HashMap 总是使用2的幂作为哈希表的大小,后面会介绍到为什么是2的幂次方。

底层数据结构： JDK1.8 以后的 HashMap 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为8）时，将链表转化为红黑树，以减少搜索时间。红黑树就是为了解决二叉查找树的缺陷，因为二叉查找树在某些情况下会退化成一个线性结构。Hashtable 没有这样的机制。

HashSet 底层就是基于 HashMap 实现的。（HashSet 的源码非常非常少，因为除了 clone() 、writeObject()、readObject()是 HashSet 自己不得不实现之外，其他方法都是直接调用 HashMap 中的方法。

# HashMap的底层实现
JDK1.8 之前 HashMap 底层是 数组和链表 结合在一起使用也就是 链表散列。HashMap 通过 key 的 hashCode 经过扰动函数处理过后得到 hash 值，然后通过 (n - 1) & hash 判断当前元素存放的位置（这里的 n 指的是数组的长度），如果当前位置存在元素的话，就判断该元素与要存入的元素的 hash 值以及 key 是否相同，如果相同的话，直接覆盖，不相同就通过拉链法（https://blog.csdn.net/a544879146/article/details/71122725 ）解决冲突。

## 实现源码
 	public HashMap(int initialCapacity, float loadFactor) {
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " +
                                               loadFactor);
 
        // Find a power of 2 >= initialCapacity
        int capacity = 1;
        while (capacity < initialCapacity)
            capacity <<= 1;
 
        this.loadFactor = loadFactor;
        threshold = (int)(capacity * loadFactor);
        table = new Entry[capacity];
        init();
    }

## 拉链法解决冲突
1）拉链法解决冲突的做法是：将所有关键字为同义词的结点链接在同一个单链表中。若选定的散列表长度为m，则可将散列表定义为一个由m个头指针组成的指针数组T[0..m-1]。凡是散列地址为i的结点，均插入到以T[i]为头指针的单链表中。T中各分量的初值均应为空指针。在拉链法中，装填因子α可以大于1，但一般均取α≤1
 （2）拉链法的优点
    　与开放定址法相比，拉链法有如下几个优点：
　　(1)拉链法处理冲突简单，且无堆积现象，即非同义词决不会发生冲突，因此平均查找长度较短；
　　(2)由于拉链法中各链表上的结点空间是动态申请的，故它更适合于造表前无法确定表长的情况；
　　(3)开放定址法为减少冲突，要求装填因子α较小，故当结点规模较大时会浪费很多空间。而拉链法中可取α≥1，且结点较大时，拉链法中增加的指针域可忽略不计，因此节省空间；
　　(4)在用拉链法构造的散列表中，删除结点的操作易于实现。只要简单地删去链表上相应的结点即可。而对开放地址法构造的散列表，删除结点不能简单地将被删结点的空间置为空，否则将截断在它之后填人散列表的同义词结点的查找路径。这是因为各种开放地址法中，空地址单元(即开放地址)都是查找失败的条件。因此在用开放地址法处理冲突的散列表上执行删除操作，只能在被删结点上做删除标记，而不能真正删除结点。
（3）拉链法的缺点 　拉链法的缺点是：指针需要额外的空间，故当结点规模较小时，开放定址法较为节省空间，而若将节省的指针空间用来扩大散列表的规模，可使装填因子变小，这又减少了开放定址法中的冲突，从而提高平均查找速度

# HashMap 的长度为什么是2的幂次方
为了能让 HashMap 存取高效，尽量较少碰撞，也就是要尽量把数据分配均匀。我们上面也讲到了过了，Hash 值的范围值-2147483648到2147483647，前后加起来大概40亿的映射空间，只要哈希函数映射得比较均匀松散，一般应用是很难出现碰撞的。但问题是一个40亿长度的数组，内存是放不下的。所以这个散列值是不能直接拿来用的。用之前还要先做对数组的长度取模运算，得到的余数才能用来要存放的位置也就是对应的数组下标。这个数组下标的计算方法是“ (n - 1) & hash”。（n代表数组长度）。这也就解释了 HashMap 的长度为什么是2的幂次方。

这个算法应该如何设计呢？

我们首先可能会想到采用%取余的操作来实现。但是，重点来了：“取余(%)操作中如果除数是2的幂次则等价于与其除数减一的与(&)操作（也就是说 hash%length==hash&(length-1)的前提是 length 是2的 n 次方；）。” 并且 采用二进制位操作 &，相对于%能够提高运算效率，这就解释了 HashMap 的长度为什么是2的幂次方。

# ConcurrentHashMap(初始容量16) 和 Hashtable 的区别
ConcurrentHashMap 和 Hashtable 的区别主要体现在实现线程安全的方式上不同。

底层数据结构： JDK1.7的 ConcurrentHashMap 底层采用 分段的数组+链表 实现，JDK1.8 采用的数据结构跟HashMap1.8的结构一样，数组+链表/红黑二叉树。Hashtable 和 JDK1.8 之前的 HashMap 的底层数据结构类似都是采用 数组+链表 的形式，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的；

实现线程安全的方式（重要）： ① 在JDK1.7的时候，ConcurrentHashMap（分段锁） 对整个桶数组进行了分割分段(Segment)，每一把锁只锁容器其中一部分数据，多线程访问容器里不同数据段的数据，就不会存在锁竞争，提高并发访问率。 到了 JDK1.8 的时候已经摒弃了Segment的概念，而是直接用 Node 数组+链表+红黑树的数据结构来实现，并发控制使用 synchronized 和 CAS 来操作。（JDK1.6以后 对 synchronized锁做了很多优化） 整个看起来就像是优化过且线程安全的 HashMap，虽然在JDK1.8中还能看到 Segment 的数据结构，但是已经简化了属性，只是为了兼容旧版本；② Hashtable(同一把锁) :使用 synchronized 来保证线程安全，效率非常低下。当一个线程访问同步方法时，其他线程也访问同步方法，可能会进入阻塞或轮询状态，如使用 put 添加元素，另一个线程不能使用 put 添加元素，也不能使用 get，竞争会越来越激烈效率越低。

## JAVA8 的 ConcurrentHashMap 为什么放弃了分段锁,有什么问题吗,如果你来设计,你如何设计

它摒弃了Segment（锁段）的概念，而是启用了一种全新的方式实现,利用CAS算法，段锁性能也不是很高，而CAS操作是CPU支持的操作，是一种原子操作

# LinkedHashMap(顺序HashMap) 实现有序
1，重新定义了数组中保存的元素Entry（继承于HashMap.Entry)，该Entry除了保存当前对象的引用外，还保存了其上一个元素before和下一个元素after的引用，从而在哈希表的基础上又构成了双向链接列表。仍然保留next属性，所以既可像HashMap一样快速查找，用next获取该链表下一个Entry，也可以通过双向链接，通过after完成所有数据的有序迭代。

2，accessOrder为true时，按访问顺序排序，false时，按插入顺序排序。默认false。

3，存储put。
LinkedHashMap并未重写父类HashMap的put方法，而是重写了父类HashMap的put方法调用的子方法void recordAccess(HashMap m)，void addEntry(int hash, K key, V value, int bucketIndex) 和void createEntry(int hash, K key, V value, int bucketIndex)，提供了自己特有的双向链接列表的实现。

	1）put时，key已存在，替换value（同HashMap），并调用recordAccess方法，方法作用为根据accessOrder的值保持链表顺序不变或者将将访问的当前节点移到链表尾部(头结点的前一个节点)。

	2）key不存在，添加新的Entry，仍然是Table[i]= newEntry，旧链表首个为newEntry.next（同HashMap）,将newEntry加到双向链表末尾（即header前，这样就保留了插入顺序）。




# 二叉树遍历（https://blog.csdn.net/My_Jobs/article/details/43451187

# 平衡二叉树、B-tree、B+tree、B*树 （https://zhuanlan.zhihu.com/p/27700617
## 平衡二叉树
### 特点
平衡二叉树是采用二分法思维把数据按规则组装成一个树形结构的数据，用这个树形结构的数据减少无关数据的检索，大大的提升了数据检索的速度；平衡二叉树的数据结构组装过程有以下规则：

（1）非叶子节点只能允许最多两个子节点存在。

（2）每一个非叶子节点数据分布规则为左边的子节点小当前节点的值，右边的子节点大于当前节点的值(这里值是基于自己的算法规则而定的，比如hash值)；

平衡树的层级结构：因为平衡二叉树查询性能和树的层级（h高度）成反比，h值越小查询越快、为了保证树的结构左右两端数据大致平衡降低二叉树的查询难度一般会采用一种算法机制实现节点数据结构的平衡，实现了这种算法的有比如Treap、红黑树，使用平衡二叉树能保证数据的左右两边的节点层级相差不会大于1，通过这样避免树形结构由于删除增加变成线性链表影响查询效率，保证数据平衡的情况下查找数据的速度近于二分法查找。

## B-tree
B树和平衡二叉树稍有不同的是B树属于多叉树又名平衡多路查找树（查找路径不只两个）。
### 规则
（1）排序方式：所有节点关键字是按递增次序排列，并遵循左小右大原则；

（2）子节点数：非叶节点的子节点数>1，且<=M ，且M>=2，空树除外（注：M阶代表一个树节点最多有多少个查找路径，M=M路,当M=2则是2叉树,M=3则是3叉）；

（3）关键字数：枝节点的关键字数量大于等于ceil(m/2)-1个且小于等于M-1个（注：ceil()是个朝正无穷方向取整的函数 如ceil(1.1)结果为2);

（4）所有叶子节点均在同一层、叶子节点除了包含了关键字和关键字记录的指针外也有指向其子节点的指针只不过其指针地址都为null对应下图最后一层节点的空格子; 

### 特点
B树相对于平衡二叉树的不同是，每个节点包含的关键字增多了，特别是在B树应用到数据库中的时候，数据库充分利用了磁盘块的原理（磁盘数据存储是采用块的形式存储的，每个块的大小为4K，每次IO进行数据读取时，同一个磁盘块的数据可以一次性读取出来）把节点大小限制和充分使用在磁盘快大小范围；把树的节点关键字增多后树的层级比原来的二叉树少了，减少数据查找的次数和复杂度;

## B+tree
B+树是B树的一个升级版，相对于B树来说B+树更充分的利用了节点的空间，让查询速度更加稳定，其速度完全接近于二分法查找.
### 规则
（1）B+跟B树不同，B+树的非叶子节点不保存关键字记录的指针，只进行数据索引，这样使得B+树每个非叶子节点所能保存的关键字大大增加；

（2）B+树叶子节点保存了父节点的所有关键字记录的指针，所有数据地址必须要到叶子节点才能获取到。所以每次数据查询的次数都一样；

（3）B+树叶子节点的关键字从小到大有序排列，左边结尾数据都会保存右边节点开始数据的指针。

### 特点
1、B+树的层级更少：相较于B树B+每个非叶子节点存储的关键字数更多，树的层级更少所以查询数据更快；

2、B+树查询速度更稳定：B+所有关键字数据地址都存在叶子节点上，所以每次查找的次数都相同所以查询速度要比B树更稳定;

3、B+树天然具备排序功能：B+树所有的叶子节点数据构成了一个有序链表，在查询大小区间的数据时候更方便，数据紧密性很高，缓存的命中率也会比B树高。

4、B+树全节点遍历更快：B+树遍历整棵树只需要遍历所有的叶子节点即可，，而不需要像B树一样需要对每一层进行遍历，这有利于数据库做全表扫描。

B树相对于B+树的优点是，如果经常访问的数据离根节点很近，而B树的非叶子节点本身存有关键字其数据的地址，所以这种数据检索的时候会要比B+树快。

##  B*tree
### 规则

B*树是B+树的变种，相对于B+树他们的不同之处如下：

（1）首先是关键字个数限制问题，B+树初始化的关键字初始化个数是ceil(m/2)，b*树的初始化个数为（ceil(2/3*m)）

（2）B+树节点满时就会分裂，而B*树节点满时会检查兄弟节点是否满（因为每个节点都有指向兄弟的指针），如果兄弟节点未满则向兄弟节点转移关键字，如果兄弟节点已满，则从当前节点和兄弟节点各拿出1/3的数据创建一个新的节点出来；

### 特点
在B+树的基础上因其初始化的容量变大，使得节点空间使用率更高，而又存有兄弟节点的指针，可以向兄弟节点转移关键字的特性使得B*树额分解次数变得更少。


# 二叉搜索树，红黑树(https://blog.csdn.net/u012124438/article/details/78200189
红黑树是平衡二叉查找树的一种。

## 二叉搜索树（BST）
二叉查找树（Binary Search Tree，简称BST）是一棵二叉树，它的左子节点的值比父节点的值要小，右节点的值要比父节点的值大。它的高度决定了它的查找效率。

在理想的情况下，二叉查找树增删查改的时间复杂度为O(logN)（其中N为节点数），最坏的情况下为O(N)。当它的高度为logN+1时，我们就说二叉查找树是平衡的。

## 红黑树
红黑树(Red-Black Tree，简称R-B Tree)，它一种特殊的二叉查找树。 
红黑树是特殊的二叉查找树，意味着它满足二叉查找树的特征：任意一个节点所包含的键值，大于等于左孩子的键值，小于等于右孩子的键值。 
除了具备该特性之外，红黑树还包括许多额外的信息。

红黑树的每个节点上都有存储位表示节点的颜色，颜色是红(Red)或黑(Black)。

红黑树的特性: 
(1) 每个节点或者是黑色，或者是红色。 
(2) 根节点是黑色。 
(3) 每个叶子节点是黑色。 [注意：这里叶子节点，是指为空的叶子节点！] 
(4) 如果一个节点是红色的，则它的子节点必须是黑色的。 
(5) 从一个节点到该节点的子孙节点的所有路径上包含相同数目的黑节点。

关于它的特性，需要注意的是： 
第一，特性(3)中的叶子节点，是只为空(NIL或null)的节点。 
第二，特性(5)，确保没有一条路径会比其他路径长出俩倍。因而，红黑树是相对是接近平衡的二叉树。

# int和Integer
## 区别
1、Integer是int的包装类，int则是java的一种基本数据类型；

2、Integer变量必须实例化后才能使用，而int变量不需要；

3、Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值；

4、Integer的默认值是null，int的默认值是0。

## 比较
1、由于Integer变量实际上是对一个Integer对象的引用，所以两个通过new生成的Integer变量永远是不相等的（因为new生成的是两个对象，其内存地址不同）。

2、Integer变量和int变量比较时，只要两个变量的值是向等的，则结果为true（因为包装类Integer和基本数据类型int比较时，java会自动拆包装为int，然后进行比较，实际上就变为两个int变量的比较）

3、非new生成的Integer变量和new Integer()生成的变量比较时，结果为false。（因为非new生成的Integer变量指向的是java常量池中的对象，而new Integer()生成的变量指向堆中新建的对象，两者在内存中的地址不同）

4、对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则比较结果为false。

# Java Exception异常的续程次结构（https://blog.csdn.net/renfufei/article/details/16344847
## Error和Exception的联系
继承结构：Error和Exception都是继承于Throwable，RuntimeException继承自Exception。

Error和RuntimeException及其子类称为未检查异常（Unchecked exception），其它异常成为受检查异常（Checked Exception）。

## Error和Exception的区别
Error类一般是指与虚拟机相关的问题，如系统崩溃，虚拟机错误，内存空间不足，方法调用栈溢出等。如java.lang.StackOverFlowError和Java.lang.OutOfMemoryError。对于这类错误，Java编译器不去检查他们。对于这类错误的导致的应用程序中断，仅靠程序本身无法恢复和预防，遇到这样的错误，建议让程序终止。

Exception类表示程序可以处理的异常，可以捕获且可能恢复。遇到这类异常，应该尽可能处理异常，使程序恢复运行，而不应该随意终止异常。

## 运行时异常（Runtime Exception）和受检查的异常(Checked Exception )。
RuntimeException：其特点是Java编译器不去检查它，也就是说，当程序中可能出现这类异常时，即使没有用try……catch捕获，也没有用throws抛出，还是会编译通过，如除数为零的ArithmeticException、错误的类型转换、数组越界访问和试图访问空指针等。处理RuntimeException的原则是：如果出现RuntimeException，那么一定是程序员的错误。

受检查的异常（IOException等）：这类异常如果没有try……catch也没有throws抛出，编译是通不过的。这类异常一般是外部错误，例如文件找不到、试图从文件尾后读取数据等，这并不是程序本身的错误，而是在应用环境中出现的外部错误。

### 常见Runtime Exception
ArrayStoreException                试图将错误类型的对象存储到一个对象数组时抛出的异常

ClassCastException                试图将对象强制转换为不是实例的子类时，抛出该异常

IllegalArgumentException         抛出的异常表明向方法传递了一个不合法或不正确的参数

IndexOutOfBoundsException   指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出

NoSuchElementException       表明枚举中没有更多的元素

NullPointerException                当应用程序试图在需要对象的地方使用 null 时，抛出该异常


## throw 和 throws两个关键字有什么不同
throw 是用来抛出任意异常的，你可以抛出任意 Throwable，包括自定义的异常类对象；throws总是出现在一个函数头中，用来标明该成员函数可能抛出的各种异常。如果方法抛出了异常，那么调用这个方法的时候就需要处理这个异常。

## try-catch-finally-return执行顺序
1、不管是否有异常产生，finally块中代码都会执行；

2、当try和catch中有return语句时，finally块仍然会执行；

3、finally是在return后面的表达式运算后执行的，所以函数返回值是在finally执行前确定的。无论finally中的代码怎么样，返回的值都不会改变，仍然是之前return语句中保存的值；

4、finally中最好不要包含return，否则程序会提前退出，返回值不是try或catch中保存的返回值。


# 线程、进程、程序
线程与进程相似，但线程是一个比进程更小的执行单位。一个进程在其执行的过程中可以产生多个线程。与进程不同的是同类的多个线程共享同一块内存空间和一组系统资源，所以系统在产生一个线程，或是在各个线程之间作切换工作时，负担要比进程小得多，也正因为如此，线程也被称为轻量级进程。

程序是含有指令和数据的文件，被存储在磁盘或其他的数据存储设备中，也就是说程序是静态的代码。

进程是程序的一次执行过程，是系统运行程序的基本单位，因此进程是动态的。系统运行一个程序即是一个进程从创建，运行到消亡的过程。简单来说，一个进程就是一个执行中的程序，它在计算机中一个指令接着一个指令地执行着，同时，每个进程还占有某些系统资源如CPU时间，内存空间，文件，文件，输入输出设备的使用权等等。换句话说，当程序在执行时，将会被操作系统载入内存中。 线程是进程划分成的更小的运行单位。线程和进程最大的不同在于基本上各进程是独立的，而各线程则不一定，因为同一进程中的线程极有可能会相互影响。从另一角度来说，进程属于操作系统的范畴，主要是同一段时间内，可以同时执行一个以上的程序，而线程则是在同一程序内几乎同时执行一个以上的程序段。

## 进程通信方式
管道（pipe）：管道是一种半双工的通信方式，数据只能单向流动，而且只能在具有血缘关系的进程间使用。进程的血缘关系通常指父子进程关系。管道分为pipe（无名管道）和fifo（命名管道）两种，有名管道也是半双工的通信方式，但是它允许无亲缘关系进程间通信。

信号量（semophore）：信号量是一个计数器，可以用来控制多个进程对共享资源的访问。它通常作为一种锁机制，防止某进程正在访问共享资源时，其他进程也访问该资源。因此，主要作为进程间以及同一进程内不同线程之间的同步手段。

消息队列（message queue）：消息队列是由消息组成的链表，存放在内核中 并由消息队列标识符标识。消息队列克服了信号传递信息少，管道只能承载无格式字节流以及缓冲区大小受限等缺点。消息队列与管道通信相比，其优势是对每个消息指定特定的消息类型，接收的时候不需要按照队列次序，而是可以根据自定义条件接收特定类型的消息。

信号（signal）：信号是一种比较复杂的通信方式，用于通知接收进程某一事件已经发生。
共享内存（shared memory）：共享内存就是映射一段能被其他进程所访问的内存，这段共享内存由一个进程创建，但多个进程都可以访问，共享内存是最快的IPC方式，它是针对其他进程间的通信方式运行效率低而专门设计的。它往往与其他通信机制，如信号量配合使用，来实现进程间的同步和通信。

套接字（socket）：socket，即套接字是一种通信机制，凭借这种机制，客户/服务器（即要进行通信的进程）系统的开发工作既可以在本地单机上进行，也可以跨网络进行。也就是说它可以让不在同一台计算机但通过网络连接计算机上的进程进行通信。也因为这样，套接字明确地将客户端和服务器区分开来。

## 创建线程的方式（https://blog.csdn.net/longshengguoji/article/details/41126119
### 继承Thread类创建线程类

（1）定义Thread类的子类，并重写该类的run方法，该run方法的方法体就代表了线程要完成的任务。因此把run()方法称为执行体。

（2）创建Thread子类的实例，即创建了线程对象。

（3）调用线程对象的start()方法来启动该线程。

### 通过Runnable接口创建线程类

（1）定义runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程执行体。

（2）创建 Runnable实现类的实例，并依此实例作为Thread的target来创建Thread对象，该Thread对象才是真正的线程对象。

（3）调用线程对象的start()方法来启动该线程。

### 通过Callable和Future创建线程

（1）创建Callable接口的实现类，并实现call()方法，该call()方法将作为线程执行体，并且有返回值。

（2）创建Callable实现类的实例，使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call()方法的返回值。

（3）使用FutureTask对象作为Thread对象的target创建并启动新线程。

（4）调用FutureTask对象的get()方法来获得子线程执行结束后的返回值


## 线程通信方式
1、锁机制

互斥锁：提供了以排它方式阻止数据结构被并发修改的方法。
读写锁：允许多个线程同时读共享数据，而对写操作互斥。
条件变量：可以以原子的方式阻塞进程，直到某个特定条件为真为止。对条件测试是在互斥锁的保护下进行的。条件变量始终与互斥锁一起使用。

2、信号量机制：包括无名线程信号量与有名线程信号量

3、信号机制：类似于进程间的信号处理。

线程间通信的主要目的是用于线程同步，所以线程没有象进程通信中用于数据交换的通信机制。

## 线程状态
线程创建之后它将处于 NEW（新建） 状态，调用 start() 方法后开始运行，线程这时候处于 READY（可运行） 状态。可运行状态的线程获得了 cpu 时间片（timeslice）后就处于 RUNNING（运行） 状态。当线程执行 wait()方法之后，线程进入 **WAITING（等待）**状态。进入等待状态的线程需要依靠其他线程的通知才能够返回到运行状态，而 TIME_WAITING(超时等待) 状态相当于在等待状态的基础上增加了超时限制，比如通过 sleep（long millis）方法或 wait（long millis）方法可以将 Java 线程置于 TIMED WAITING 状态。当超时时间到达后 Java 线程将会返回到 RUNNABLE 状态。当线程调用同步方法时，在没有获取到锁的情况下，线程将会进入到 BLOCKED（阻塞） 状态。线程在执行 Runnable 的run()方法之后将会进入到 TERMINATED（终止） 状态。

# 守护线程
作用是为其他线程的运行提供服务，比如说GC线程。其实User Thread线程和Daemon Thread守护线程本质上来说去没啥区别的，唯一的区别之处就在虚拟机的离开：如果User Thread全部撤离，那么Daemon Thread也就没啥线程好服务的了，所以虚拟机也就退出了。
守护线程并非虚拟机内部可以提供，用户也可以自行的设定守护线程，方法：public final void setDaemon(boolean on) ；但是有几点需要注意：

1）、thread.setDaemon(true)
必须在thread.start()之前设置，否则会跑出一个IllegalThreadStateException异常。你不能把正在运行的常规线程设置为守护线程。  （备注：这点与守护进程有着明显的区别，守护进程是创建后，让进程摆脱原会话的控制+让进程摆脱原进程组的控制+让进程摆脱原控制终端的控制；所以说寄托于虚拟机的语言机制跟系统级语言有着本质上面的区别）

2）、 在Daemon线程中产生的新线程也是Daemon的。  （这一点又是有着本质的区别了：守护进程fork()出来的子进程不再是守护进程，尽管它把父进程的进程相关信息复制过去了，但是子进程的进程的父进程不是init进程，所谓的守护进程本质上说就是“父进程挂掉，init收养，然后文件0,1,2都是/dev/null，当前目录到/”）

3）、不是所有的应用都可以分配给Daemon线程来进行服务，比如读写操作或者计算逻辑。因为在Daemon Thread还没来的及进行操作时，虚拟机可能已经退出了。

# ThreadLocal（https://droidyue.com/blog/2016/03/13/learning-threadlocal-in-java/
ThreadLocal是一个关于创建线程局部变量的类。通常情况下，我们创建的变量是可以被任何一个线程访问并修改的。而使用ThreadLocal创建的变量只能被当前线程访问，其他线程则无法访问和修改。适用于每个线程需要自己独立的实例且该实例需要在多个方法中被使用，也即变量在线程间隔离而在方法或类间共享的场景。

# 线程死锁
多个线程同时被阻塞，它们中的一个或者全部都在等待某个资源被释放。由于线程被无限期地阻塞，因此程序不可能正常终止。

## 产生死锁必须具备以下四个条件：

互斥条件：该资源任意一个时刻只由一个线程占用。

请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。

不剥夺条件:线程已获得的资源在末使用完之前不能被其他线程强行剥夺，只有自己使用完毕后才释放资源。

循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

## 避免死锁：

### 破坏互斥条件

这个条件我们没有办法破坏，因为我们用锁本来就是想让他们互斥的（临界资源需要互斥访问）。

### 破坏请求与保持条件

一次性申请所有的资源。

### 破坏不剥夺条件

占用部分资源的线程进一步申请其他资源时，如果申请不到，可以主动释放它占有的资源。

### 破坏循环等待条件

靠按序申请资源来预防。按某一顺序申请资源，释放资源则反序释放。破坏循环等待条件。

# sleep() 和 wait()
两者最主要的区别在于：sleep 方法没有释放锁，而 wait 方法释放了锁 。

两者都可以暂停线程的执行。

Wait 通常被用于线程间交互/通信，sleep 通常被用于暂停执行。

wait() 方法被调用后，线程不会自动苏醒，需要别的线程调用同一个对象上的 notify() 或者 notifyAll() 方法。sleep() 方法执行完成后，线程会自动苏醒。或者可以使用wait(long timeout)超时后线程会自动苏醒。

# wait()实现原理
1、将当前线程封装成ObjectWaiter对象node

2、通过ObjectMonitor::AddWaiter方法将node添加到_WaitSet列表中

3、通过ObjectMonitor::exit方法释放当前的ObjectMonitor对象，这样其它竞争线程就可以获取该ObjectMonitor对象

4、最终底层的park方法会挂起线程

# notify（）实现
1、如果当前_WaitSet为空，即没有正在等待的线程，则直接返回；
2、通过ObjectMonitor::DequeueWaiter方法，获取_WaitSet列表中的第一个ObjectWaiter节点，实现也很简单。在jdk的notify方法注释是随机唤醒一个线程，其实是第一个ObjectWaiter节点。
3、根据不同的策略，将取出来的ObjectWaiter节点，加入到_EntryList或则通过Atomic::cmpxchg_ptr指令进行自旋操作cxq


# 为什么我们调用 start() 方法时会执行 run() 方法，为什么我们不能直接调用 run() 方法？
new 一个 Thread，线程进入了新建状态;调用 start() 方法，会启动一个线程并使线程进入了就绪状态，当分配到时间片后就可以开始运行了。 start() 会执行线程的相应准备工作，然后自动执行 run() 方法的内容，这是真正的多线程工作。 而直接执行 run() 方法，会把 run 方法当成一个 main 线程下的普通方法去执行，并不会在某个线程中执行它，所以这并不是多线程工作。

总结： 调用 start 方法方可启动线程并使线程进入就绪状态，而 run 方法只是 thread 的一个普通方法调用，还是在主线程里执行。

# synchronized
synchronized关键字解决的是多个线程之间访问资源的同步性，synchronized关键字可以保证被它修饰的方法或者代码块在任意时刻只能有一个线程执行。

## 使用方式
修饰实例方法: 作用于当前对象实例加锁，进入同步代码前要获得当前对象实例的锁

修饰静态方法: :也就是给当前类加锁，会作用于类的所有对象实例，因为静态成员不属于任何一个实例对象，是类成员（ static 表明这是该类的一个静态资源，不管new了多少个对象，只有一份）。所以如果一个线程A调用一个实例对象的非静态 synchronized 方法，而线程B需要调用这个实例对象所属类的静态 synchronized 方法，是允许的，不会发生互斥现象，因为访问静态 synchronized 方法占用的锁是当前类的锁，而访问非静态 synchronized 方法占用的锁是当前实例对象锁。

修饰代码块: 指定加锁对象，对给定对象加锁，进入同步代码库前要获得给定对象的锁。

总结： synchronized 关键字加到 static 静态方法和 synchronized(class)代码块上都是是给 Class 类上锁。synchronized 关键字加到实例方法上是给对象实例上锁。尽量不要使用 synchronized(String a) 因为JVM中，字符串常量池具有缓存功能！

## 双重校验锁实现对象单例（线程安全 懒汉式）

	public class Singleton {

	    private volatile static Singleton uniqueInstance;

	    private Singleton() {
	    }

	    public static Singleton getUniqueInstance() {
	       //先判断对象是否已经实例过，没有实例化过才进入加锁代码
	        if (uniqueInstance == null) {
	            //类对象加锁
	            synchronized (Singleton.class) {
	                if (uniqueInstance == null) {
	                    uniqueInstance = new Singleton();
	                }
	            }
	        }
	        return uniqueInstance;
	    }
	}

## 单例模式 （饿汉式）

	public class EagerSingleton {  
	        // jvm保证在任何线程访问uniqueInstance静态变量之前一定先创建了此实例  
	        private static EagerSingleton uniqueInstance = new EagerSingleton();  
	  
	        // 私有的默认构造子，保证外界无法直接实例化  
	        private EagerSingleton() {  
	        }  
	  
	        // 提供全局访问点获取唯一的实例  
	        public static EagerSingleton getInstance() {  
	                return uniqueInstance;  
	        }  
	}

## 登记事单例
	public class Dengjishi {  
	    private static Map<String,Dengjishi> map = new HashMap<String,Dengjishi>();  
	    static{  
	    	Dengjishi single = new Dengjishi();  
	        map.put(single.getClass().getName(), single);  
	        
	        
	    }  
	    //保护的默认构造子  
	    protected Dengjishi(){
	    	System.out.println("-----实例对象被创建-----");
	    }  
	    //静态工厂方法,返还此类惟一的实例  
	    public static Dengjishi getInstance(String name) {  
	        if(name == null) {  
	            name = Dengjishi.class.getName();  
	            System.out.println("name == null"+"--->name="+name);  
	        }  
	        if(map.get(name) == null) {  
	            try {  
	                map.put(name, (Dengjishi) Class.forName(name).newInstance());  
	            } catch (Exception e) {  
	                e.printStackTrace();  
	            }
	        }  
	        return map.get(name);  
	    }     
	     
	}


## 底层实现
synchronized 同步语句块的实现使用的是 monitorenter 和 monitorexit 指令，其中 monitorenter 指令指向同步代码块的开始位置，monitorexit 指令则指明同步代码块的结束位置。 当执行 monitorenter 指令时，线程试图获取锁也就是获取 monitor(monitor对象存在于每个Java对象的对象头中，synchronized 锁便是通过这种方式获取锁的，也是为什么Java中任意对象可以作为锁的原因) 的持有权。当计数器为0则可以成功获取，获取后将锁计数器设为1也就是加1。相应的在执行 monitorexit 指令后，将锁计数器设为0，表明锁被释放。如果获取对象锁失败，那当前线程就要阻塞等待，直到锁被另外一个线程释放为止。

## synchronized和ReentrantLock 的区别
① 两者都是可重入锁

两者都是可重入锁。“可重入锁”概念是：自己可以再次获取自己的内部锁。比如一个线程获得了某个对象的锁，此时这个对象锁还没有释放，当其再次想要获取这个对象的锁的时候还是可以获取的，如果不可锁重入的话，就会造成死锁。同一个线程每次获取锁，锁的计数器都自增1，所以要等到锁的计数器下降为0时才能释放锁。

② synchronized 依赖于 JVM 而 ReentrantLock 依赖于 API

synchronized 是依赖于 JVM 实现的，前面我们也讲到了 虚拟机团队在 JDK1.6 为 synchronized 关键字进行了很多优化，但是这些优化都是在虚拟机层面实现的，并没有直接暴露给我们。ReentrantLock 是 JDK 层面实现的（也就是 API 层面，需要 lock() 和 unlock() 方法配合 try/finally 语句块来完成），所以我们可以通过查看它的源代码，来看它是如何实现的。

③ ReentrantLock 比 synchronized 增加了一些高级功能

相比synchronized，ReentrantLock增加了一些高级功能。主要来说主要有三点：①等待可中断；②可实现公平锁；③可实现选择性通知（锁可以绑定多个条件）

ReentrantLock提供了一种能够中断等待锁的线程的机制，通过lock.lockInterruptibly()来实现这个机制。也就是说正在等待的线程可以选择放弃等待，改为处理其他事情。
ReentrantLock可以指定是公平锁还是非公平锁。而synchronized只能是非公平锁。所谓的公平锁就是先等待的线程先获得锁。 ReentrantLock默认情况是非公平的，可以通过 ReentrantLock类的ReentrantLock(boolean fair)构造方法来制定是否是公平的。
synchronized关键字与wait()和notify()/notifyAll()方法相结合可以实现等待/通知机制，ReentrantLock类当然也可以实现，但是需要借助于Condition接口与newCondition() 方法。Condition是JDK1.5之后才有的，它具有很好的灵活性，比如可以实现多路通知功能也就是在一个Lock对象中可以创建多个Condition实例（即对象监视器），线程对象可以注册在指定的Condition中，从而可以有选择性的进行线程通知，在调度线程上更加灵活。 在使用notify()/notifyAll()方法进行通知时，被通知的线程是由 JVM 选择的，用ReentrantLock类结合Condition实例可以实现“选择性通知” ，这个功能非常重要，而且是Condition接口默认提供的。而synchronized关键字就相当于整个Lock对象中只有一个Condition实例，所有的线程都注册在它一个身上。如果执行notifyAll()方法的话就会通知所有处于等待状态的线程这样会造成很大的效率问题，而Condition实例的signalAll()方法 只会唤醒注册在该Condition实例中的所有等待线程。
如果你想使用上述功能，那么选择ReentrantLock是一个不错的选择。

④ 性能已不是选择标准

# 线程池
## 好处
降低资源消耗。 通过重复利用已创建的线程降低线程创建和销毁造成的消耗。

提高响应速度。 当任务到达时，任务可以不需要的等到线程创建就能立即执行。

提高线程的可管理性。 
线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控。

## 风险
虽然线程池是构建多线程应用程序的强大机制，但使用它并不是没有风险的。用线程池构建的应用程序容易遭受所有并发风险，诸如同步错误和死锁，它还容易遭受特定于线程池的少数其它风险，诸如与池有关的死锁、资源不足和线程泄漏。

## 线程池状态
线程池有四种状态，分别为RUNNING、SHURDOWN、STOP、TERMINATED。

 线程池创建后处于RUNNING状态。

 调用shutdown后处于SHUTDOWN状态，线程池不能接受新的任务，会等待缓冲队列的任务完成。

 调用shutdownNow后处于STOP状态，线程池不能接受新的任务，并尝试终止正在执行的任务。

 当线程池处于SHUTDOWN或STOP状态，并且所有工作线程已经销毁，任务缓存队列已经清空或执行结束后，线程池被设置为TERMINATED状态。

## 线程池原理
预先启动一些线程，线程无限循环从任务队列中获取一个任务进行执行，直到线程池被关闭。如果某个线程因为执行某个任务发生异常而终止，那么重新创建一个新的线程而已，如此反复。

## 处理流程
1、判断线程池里的核心线程是否都在执行任务，如果不是（核心线程空闲或者还有核心线程没有被创建）则创建一个新的工作线程来执行任务。如果核心线程都在执行任务，则进入下个流程。

2、线程池判断工作队列是否已满，如果工作队列没有满，则将新提交的任务存储在这个工作队列里。如果工作队列满了，则进入下个流程。

3、判断线程池里的线程是否都处于工作状态，如果没有，则创建一个新的工作线程来执行任务。如果已经满了，则交给饱和策略来处理这个任务。

## Java线程池及使用场景
### FixedThreadPool
该方法返回一个固定线程数量的线程池。该线程池中的线程数量始终不变。当有一个新的任务提交时，线程池中若有空闲线程，则立即执行。若没有，则新的任务会被暂存在一个任务队列中，待有线程空闲时，便处理在任务队列中的任务。适用于为了满足资源管理需求，而需要限制当前线程数量的应用场景。它适用于负载比较重的服务器。

### SingleThreadExecutor
方法返回一个只有一个线程的线程池。若多余一个任务被提交到该线程池，任务会被保存在一个任务队列中，待线程空闲，按先入先出的顺序执行队列中的任务。适用于需要保证顺序地执行各个任务并且在任意时间点，不会有多个线程是活动的应用场景。

### CachedThreadPool
该方法返回一个可根据实际情况调整线程数量的线程池。线程池的线程数量不确定，但若有空闲线程可以复用，则会优先使用可复用的线程。若所有线程均在工作，又有新的任务提交，则会创建新的线程处理任务。所有线程在当前任务执行完毕后，将返回线程池进行复用。适用于执行很多的短期异步任务的小程序，或者是负载较轻的服务器；

### ScheduledThreadPoolExecutor
主要用来在给定的延迟后运行任务，或者定期执行任务。ScheduledThreadPoolExecutor又分为：ScheduledThreadPoolExecutor（包含多个线程）和SingleThreadScheduledExecutor （只包含一个线程）两种。ScheduledThreadPoolExecutor： 适用于需要多个后台执行周期任务，同时为了满足资源管理需求而需要限制后台线程的数量的应用场景。
SingleThreadScheduledExecutor： 适用于需要单个后台线程执行周期任务，同时保证顺序地执行各个任务的应用场景。

## ThreadPoolExecutor
### 参数
1，corePoolSize：表示核心线程池的大小。当提交一个任务时，如果当前核心线程池的线程个数没有达到corePoolSize，则会创建新的线程来执行所提交的任务，即使当前核心线程池有空闲的线程。如果当前核心线程池的线程个数已经达到了corePoolSize，则不再重新创建线程。如果调用了prestartCoreThread()或者 prestartAllCoreThreads()，线程池创建的时候所有的核心线程都会被创建并且启动。

2，maximumPoolSize：表示线程池能创建线程的最大个数。如果当阻塞队列已满时，并且当前线程池线程个数没有超过maximumPoolSize的话，就会创建新的线程来执行任务。

3，keepAliveTime：空闲线程存活时间。如果当前线程池的线程个数已经超过了corePoolSize，并且线程空闲时间超过了keepAliveTime的话，就会将这些空闲线程销毁，这样可以尽可能降低系统资源消耗。

4，unit：时间单位。为keepAliveTime指定时间单位。

5， workQueue：阻塞队列。用于保存任务的阻塞队列，关于阻塞队列可以看这篇文章。可以使用ArrayBlockingQueue, LinkedBlockingQueue, SynchronousQueue, PriorityBlockingQueue。

6， threadFactory：创建线程的工程类。可以通过指定线程工厂为每个创建出来的线程设置更有意义的名字，如果出现并发问题，也方便查找问题原因。

7，handler：饱和策略。当线程池的阻塞队列已满和指定的线程都已经开启，说明当前线程池已经处于饱和状态了，那么就需要采用一种策略来处理这种情况。采用的策略有这几种：
	AbortPolicy： 直接拒绝所提交的任务，并抛出RejectedExecutionException异常；

	CallerRunsPolicy：只用调用者所在的线程来执行任务；

	DiscardPolicy：不处理直接丢弃掉任务；

	DiscardOldestPolicy：丢弃掉阻塞队列中存放时间最久的任务，执行当前任务

### 实现（http://dockone.io/article/8284

## 线程池的四种实现方式
ExecutorService是线程池接口。它定义了4中线程池：

### newCachedThreadPool：
底层：返回ThreadPoolExecutor实例，corePoolSize为0；maximumPoolSize为Integer.MAX_VALUE；keepAliveTime为60L；unit为TimeUnit.SECONDS；workQueue为SynchronousQueue(同步队列)
通俗：当有新任务到来，则插入到SynchronousQueue中，由于SynchronousQueue是同步队列，因此会在池中寻找可用线程来执行，若有可以线程则执行，若没有可用线程则创建一个线程来执行该任务；若池中线程空闲时间超过指定大小，则该线程会被销毁。
适用：执行很多短期异步的小程序或者负载较轻的服务器

### newFixedThreadPool：
底层：返回ThreadPoolExecutor实例，接收参数为所设定线程数量nThread，corePoolSize为nThread，maximumPoolSize为nThread；keepAliveTime为0L(不限时)；unit为：TimeUnit.MILLISECONDS；WorkQueue为：new LinkedBlockingQueue<Runnable>() 无界阻塞队列
通俗：创建可容纳固定数量线程的池子，每隔线程的存活时间是无限的，当池子满了就不在添加线程了；如果池中的所有线程均在繁忙状态，对于新任务会进入阻塞队列中(无界的阻塞队列)，但是，在线程池空闲时，即线程池中没有可运行任务时，它不会释放工作线程，还会占用一定的系统资源。
适用：执行长期的任务，性能好很多

### newSingleThreadExecutor:
底层：FinalizableDelegatedExecutorService包装的ThreadPoolExecutor实例，corePoolSize为1；maximumPoolSize为1；keepAliveTime为0L；unit为：TimeUnit.MILLISECONDS；workQueue为：new LinkedBlockingQueue<Runnable>() 无界阻塞队列
通俗：创建只有一个线程的线程池，且线程的存活时间是无限的；当该线程正繁忙时，对于新任务会进入阻塞队列中(无界的阻塞队列)
适用：一个任务一个任务执行的场景

### NewScheduledThreadPool:

底层：创建ScheduledThreadPoolExecutor实例，corePoolSize为传递来的参数，maximumPoolSize为Integer.MAX_VALUE；keepAliveTime为0；unit为：TimeUnit.NANOSECONDS；workQueue为：new DelayedWorkQueue() 一个按超时时间升序排序的队列
通俗：创建一个固定大小的线程池，线程池内线程存活时间无限制，线程池可以支持定时及周期性任务执行，如果所有线程均处于繁忙状态，对于新任务会进入DelayedWorkQueue队列中，这是一种按照超时时间排序的队列结构
适用：周期性执行任务的场景

# 悲观锁与乐观锁
## 悲观锁
总是假设最坏的情况，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻塞直到它拿到锁（共享资源每次只给一个线程使用，其它线程阻塞，用完后再把资源转让给其它线程）。传统的关系型数据库里边就用到了很多这种锁机制，比如行锁，表锁等，读锁，写锁等，都是在做操作之前先上锁。Java中synchronized和ReentrantLock等独占锁就是悲观锁思想的实现。

## 乐观锁
总是假设最好的情况，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号机制和CAS算法实现。乐观锁适用于多读的应用类型，这样可以提高吞吐量，像数据库提供的类似于write_condition机制，其实都是提供的乐观锁。在Java中java.util.concurrent.atomic包下面的原子变量类就是使用了乐观锁的一种实现方式CAS实现的。

### 实现方式
#### 版本号机制
一般是在数据表中加上一个数据版本号version字段，表示数据被修改的次数，当数据被修改时，version值会加一。当线程A要更新数据值时，在读取数据的同时也会读取version值，在提交更新时，若刚才读取到的version值为当前数据库中的version值相等时才更新，否则重试更新操作，直到更新成功。

#### CAS算法：
即compare and swap（比较与交换），是一种有名的无锁算法。无锁编程，即不使用锁的情况下实现多线程之间的变量同步，也就是在没有线程被阻塞的情况下实现变量的同步，所以也叫非阻塞同步（Non-blocking Synchronization）。CAS算法涉及到三个操作数

需要读写的内存值 V
进行比较的值 A
拟写入的新值 B
当且仅当 V 的值等于A时，CAS通过原子方式用新值B来更新V的值，否则不会执行任何操作（比较和替换是一个原子操作）。一般情况下是一个自旋操作，即不断的重试。

## 使用场景
从上面对两种锁的介绍，我们知道两种锁各有优缺点，不可认为一种好于另一种，像乐观锁适用于写比较少的情况下（多读场景），即冲突真的很少发生的时候，这样可以省去了锁的开销，加大了系统的整个吞吐量。但如果是多写的情况，一般会经常产生冲突，这就会导致上层应用会不断的进行retry，这样反倒是降低了性能，所以一般多写的场景下用悲观锁就比较合适。

# JVM(https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/jvm/Java%E5%86%85%E5%AD%98%E5%8C%BA%E5%9F%9F.md
## Java 内存区域（运行时数据区）

### 线程私有的：
程序计数器
虚拟机栈
本地方法栈

### 线程共享的：
堆
方法区
直接内存 (非运行时数据区的一部分)

### 堆
Java 虚拟机所管理的内存中最大的一块，Java 堆是所有线程共享的一块内存区域，在虚拟机启动时创建。此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例以及数组都在这里分配内存。

Java 堆是垃圾收集器管理的主要区域，因此也被称作GC 堆（Garbage Collected Heap）.从垃圾回收的角度，由于现在收集器基本都采用分代垃圾收集算法，所以 Java 堆还可以细分为：新生代和老年代：再细致一点有：Eden 空间、From Survivor、To Survivor 空间等。进一步划分的目的是更好地回收内存，或者更快地分配内存。eden 区、s0 区、s1 区都属于新生代，tentired 区属于老年代。大部分情况，对象都会首先在 Eden 区域分配，在一次新生代垃圾回收后，如果对象还存活，则会进入 s0 或者 s1，并且对象的年龄还会加 1(Eden 区->Survivor 区后对象的初始年龄变为 1)，当它的年龄增加到一定程度（默认为 15 岁），就会被晋升到老年代中。对象晋升到老年代的年龄阈值，可以通过参数 -XX:MaxTenuringThreshold 来设置。

### 方法区（永久代）
方法区与 Java 堆一样，是各个线程共享的内存区域，它用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。虽然 Java 虚拟机规范把方法区描述为堆的一个逻辑部分，但是它却有一个别名叫做 Non-Heap（非堆），目的应该是与 Java 堆区分开来。

### 为什么要将永久代 (PermGen) 替换为元空间 (MetaSpace) （java 8）
整个永久代有一个 JVM 本身设置固定大小上线，无法进行调整，而元空间使用的是直接内存，受本机可用内存的限制，并且永远不会得到 java.lang.OutOfMemoryError。你可以使用 -XX：MaxMetaspaceSize 标志设置最大元空间大小，默认值为 unlimited，这意味着它只受系统内存的限制。-XX：MetaspaceSize 调整标志定义元空间的初始大小如果未指定此标志，则 Metaspace 将根据运行时的应用程序需求动态地重新调整大小。

### 运行时常量池
运行时常量池是方法区的一部分。Class 文件中除了有类的版本、字段、方法、接口等描述信息外，还有常量池信息（用于存放编译期生成的各种字面量和符号引用）

既然运行时常量池时方法区的一部分，自然受到方法区内存的限制，当常量池无法再申请到内存时会抛出 OutOfMemoryError 异常。

JDK1.7 及之后版本的 JVM 已经将运行时常量池从方法区中移了出来，在 Java 堆（Heap）中开辟了一块区域存放运行时常量池。

## 内存溢出（outofmemory）
内存溢出是指应用系统中存在无法回收的内存或使用的内存过多，最终使得程序运行要用到的内存大于虚拟机能提供的最大内存。

引起内存溢出的原因有很多种，常见的有以下几种：

　　1.内存中加载的数据量过于庞大，如一次从数据库取出过多数据；

　　2.集合类中有对对象的引用，使用完后未清空，使得JVM不能回收；

　　3.代码中存在死循环或循环产生过多重复的对象实体；

　　4.使用的第三方软件中的BUG；

　　5.启动参数内存值设定的过小；

内存溢出的解决方案：

第一步，修改JVM启动参数，直接增加内存。(-Xms，-Xmx参数一定不要忘记加。)

第二步，检查错误日志，查看“OutOfMemory”错误前是否有其它异常或错误。

第三步，对代码进行走查和分析，找出可能发生内存溢出的位置。

重点排查以下几点：

1.检查对数据库查询中，是否有一次获得全部数据的查询。一般来说，如果一次取十万条记录到内存，就可能引起内存溢出。这个问题比较隐蔽，在上线前，数据库中数据较少，不容易出问题，上线后，数据库中数据多了，一次查询就有可能引起内存溢出。因此对于数据库查询尽量采用分页的方式查询。

2.检查代码中是否有死循环或递归调用。

3.检查是否有大循环重复产生新对象实体。

4.检查对数据库查询中，是否有一次获得全部数据的查询。一般来说，如果一次取十万条记录到内存，就可能引起内存溢出。这个问题比较隐蔽，在上线前，数据库中数据较少，不容易出问题，上线后，数据库中数据多了，一次查询就有可能引起内存溢出。因此对于数据库查询尽量采用分页的方式查询。

5.检查List、MAP等集合对象是否有使用完后，未清除的问题。List、MAP等集合对象会始终存有对对象的引用，使得这些对象不能被GC回收。

第四步，使用内存查看工具动态查看内存使用情况。

## 类加载过程（https://github.com/Simon9637/JavaGuide/blob/master/docs/java/jvm/%E7%B1%BB%E5%8A%A0%E8%BD%BD%E8%BF%87%E7%A8%8B.md）

## 对象创建过程
### Step1:类加载检查
虚拟机遇到一条 new 指令时，首先将去检查这个指令的参数是否能在常量池中定位到这个类的符号引用，并且检查这个符号引用代表的类是否已被加载过、解析和初始化过。如果没有，那必须先执行相应的类加载过程。

### Step2:分配内存
在类加载检查通过后，接下来虚拟机将为新生对象分配内存。对象所需的内存大小在类加载完成后便可确定，为对象分配空间的任务等同于把一块确定大小的内存从 Java 堆中划分出来。分配方式有 “指针碰撞” 和 “空闲列表” 两种，选择那种分配方式由 Java 堆是否规整决定，而 Java 堆是否规整又由所采用的垃圾收集器是否带有压缩整理功能决定。

### Step3:初始化零值
内存分配完成后，虚拟机需要将分配到的内存空间都初始化为零值（不包括对象头），这一步操作保证了对象的实例字段在 Java 代码中可以不赋初始值就直接使用，程序能访问到这些字段的数据类型所对应的零值。

### Step4:设置对象头
初始化零值完成之后，虚拟机要对对象进行必要的设置，例如这个对象是那个类的实例、如何才能找到类的元数据信息、对象的哈希码、对象的 GC 分代年龄等信息。 这些信息存放在对象头中。 另外，根据虚拟机当前运行状态的不同，如是否启用偏向锁等，对象头会有不同的设置方式。

### Step5:执行 init 方法
在上面工作都完成之后，从虚拟机的视角来看，一个新的对象已经产生了，但从 Java 程序的视角来看，对象创建才刚开始，<init> 方法还没有执行，所有的字段都还为零。所以一般来说，执行 new 指令之后会接着执行 <init> 方法，把对象按照程序员的意愿进行初始化，这样一个真正可用的对象才算完全产生出来。

### String s1 = new String("abc");这句话创建了几个字符串对象？
将创建 1 或 2 个字符串。如果池中已存在字符串文字“abc”，则池中只会创建一个字符串“s1”。如果池中没有字符串文字“abc”，那么它将首先在池中创建，然后在堆空间中创建，因此将创建总共 2 个字符串对象。

## 双亲委派模型
每一个类都有一个对应它的类加载器。系统中的 ClassLoder 在协同工作的时候会默认使用 双亲委派模型 。即在类加载的时候，系统会首先判断当前类是否被加载过。已经被加载的类会直接返回，否则才会尝试加载。加载的时候，首先会把该请求委派该父类加载器的 loadClass() 处理，因此所有的请求最终都应该传送到顶层的启动类加载器 BootstrapClassLoader 中。当父类加载器无法处理时，才由自己来处理。当父类加载器为null时，会使用启动类加载器 BootstrapClassLoader 作为父类加载器。

### 双亲委派模型的好处
双亲委派模型保证了Java程序的稳定运行，可以避免类的重复加载（JVM 区分不同类的方式不仅仅根据类名，相同的类文件被不同的类加载器加载产生的是两个不同的类），也保证了 Java 的核心 API 不被篡改。如果没有使用双亲委派模型，而是每个类加载器加载自己的话就会出现一些问题，比如我们编写一个称为 java.lang.Object 类的话，那么程序运行的时候，系统就会出现多个不同的 Object 类。

## 启动参数
-vmargs：用来说明后面的就是JVM的参数了

-Xms：JVM初始分配的堆内存

-Xmx：JVM最大允许分配的堆内存，按需分配

-XX:PermSize：JVM初始分配的非堆内存

-XX:MaxPermSize：JVM最大允许分配的非堆内存，按需分配

### 调优
#### 堆内存：

JVM留给开发者用的内存。一般存放对象以及数组。

JVM初始分配的堆内存由-Xms指定，默认是物理内存的1/64；JVM最大分配的堆内存由-Xmx指定，默认是物理内存的1/4。

空余堆内存小于40%时，JVM就会增大堆内存直到-Xmx的最大限制；空余堆内存大于70%时，JVM会减少堆内存直到-Xms的最小限制。因此服务器一般设置-Xms、-Xmx相等以避免在每次GC后调整堆内存的大小。

如果-Xmx不指定或者指定偏小，应用可能会导致java.lang.OutOfMemory错误，此错误来自JVM，不是Throwable的，无法用try...catch捕捉。

#### 非堆内存： 

JVM留给自己用的内存。方法区、JVM内部处理或优化所需的内存(如JIT编译后的代码缓存)、每个类结构(如运行时常数池、字段和方法数据)以及方法和构造方法的代码都在非堆内存中。

JVM初始分配的非堆内存由-XX:PermSize指定，默认是物理内存的1/64；JVM最大分配的非堆内存由-XX:MaxPermSize指定，默认是物理内存的1/4。（还有一说：MaxPermSize缺省值和-server -client选项相关，-server选项下默认MaxPermSize为64m，-client选项下默认MaxPermSize为32m）

-XX:MaxPermSize设置过小会导致java.lang.OutOfMemoryError: PermGen space，原因如下：

PermGen space用于存放Class和Meta的信息，GC不会对PermGen space进行处理，所以如果Load很多Class的话，就会出现上述Error。这种Error在web服务器对JSP进行pre compile的时候比较常见


# JVM垃圾回收
## 对象已经死亡(不可用)?
### 引用计数法
给对象中添加一个引用计数器，每当有一个地方引用它，计数器就加 1；当引用失效，计数器就减 1；任何时候计数器为 0 的对象就是不可能再被使用的。
这个方法实现简单，效率高，但是目前主流的虚拟机中并没有选择这个算法来管理内存，其最主要的原因是它很难解决对象之间相互循环引用的问题。

### 可达性分析算法
这个算法的基本思想就是通过一系列的称为 “GC Roots” 的对象作为起点，从这些节点开始向下搜索，节点所走过的路径称为引用链，当一个对象到 GC Roots 没有任何引用链相连的话，则证明此对象是不可用的。

即使在可达性分析法中不可达的对象，也并非是“非死不可”的，这时候它们暂时处于“缓刑阶段”，要真正宣告一个对象死亡，至少要经历两次标记过程；可达性分析法中不可达的对象被第一次标记并且进行一次筛选，筛选的条件是此对象是否有必要执行 finalize 方法。当对象没有覆盖 finalize 方法，或 finalize 方法已经被虚拟机调用过时，虚拟机将这两种情况视为没有必要执行。被判定为需要执行的对象将会被放在一个队列中进行第二次标记，除非这个对象与引用链上的任何一个对象建立关联，否则就会被真的回收。

## 垃圾收集算法
### 标记-清除算法
该算法分为“标记”和“清除”阶段：首先标记出所有需要回收的对象，在标记完成后统一回收所有被标记的对象。它是最基础的收集算法，后续的算法都是对其不足进行改进得到。这种垃圾收集算法会带来两个明显的问题：效率问题，空间问题（标记清除后会产生大量不连续的碎片）。

### 复制算法
为了解决效率问题，“复制”收集算法出现了。它可以将内存分为大小相同的两块，每次使用其中的一块。当这一块的内存使用完后，就将还存活的对象复制到另一块去，然后再把使用的空间一次清理掉。这样就使每次的内存回收都是对内存区间的一半进行回收。

### 标记-整理算法
标记过程仍然与“标记-清除”算法一样，但后续步骤不是直接对可回收对象回收，而是让所有存活的对象向一端移动，然后直接清理掉端边界以外的内存。

### 分代收集算法
当前虚拟机的垃圾收集都采用分代收集算法，这种算法没有什么新的思想，只是根据对象存活周期的不同将内存分为几块。一般将 java 堆分为新生代和老年代，这样我们就可以根据各个年代的特点选择合适的垃圾收集算法。

比如在新生代中，每次收集都会有大量对象死去，所以可以选择复制算法，只需要付出少量对象的复制成本就可以完成每次垃圾收集。而老年代的对象存活几率是比较高的，而且没有额外的空间对它进行分配担保，所以我们必须选择“标记-清除”或“标记-整理”算法进行垃圾收集。

### G1 收集器
G1 (Garbage-First) 是一款面向服务器的垃圾收集器,主要针对配备多颗处理器及大容量内存的机器. 以极高概率满足 GC 停顿时间要求的同时,还具备高吞吐量性能特征.

被视为 JDK1.7 中 HotSpot 虚拟机的一个重要进化特征。它具备一下特点：

并行与并发：G1 能充分利用 CPU、多核环境下的硬件优势，使用多个 CPU（CPU 或者 CPU 核心）来缩短 Stop-The-World 停顿时间。部分其他收集器原本需要停顿 Java 线程执行的 GC 动作，G1 收集器仍然可以通过并发的方式让 java 程序继续执行。

分代收集：虽然 G1 可以不需要其他收集器配合就能独立管理整个 GC 堆，但是还是保留了分代的概念。

空间整合：与 CMS 的“标记--清理”算法不同，G1 从整体来看是基于“标记整理”算法实现的收集器；从局部上来看是基于“复制”算法实现的。

可预测的停顿：这是 G1 相对于 CMS 的另一个大优势，降低停顿时间是 G1 和 CMS 共同的关注点，但 G1 除了追求低停顿外，还能建立可预测的停顿时间模型，能让使用者明确指定在一个长度为 M 毫秒的时间片段内。

G1 收集器的运作大致分为以下几个步骤：初始标记，并发标记，，最终标记，筛选回收。
G1 收集器在后台维护了一个优先列表，每次根据允许的收集时间，优先选择回收价值最大的 Region(这也就是它的名字 Garbage-First 的由来)。这种使用 Region 划分内存空间以及有优先级的区域回收方式，保证了 GF 收集器在有限时间内可以尽可能高的收集效率（把内存化整为零）。

### CMS垃圾收集器（https://juejin.im/post/5c7262a15188252f30484351
CMS一款并发、使用标记-清除算法的gc，是老年代垃圾收集器，在收集过程中可以与用户线程并发操作。它可以与Serial收集器和Parallel New收集器搭配使用。CMS牺牲了系统的吞吐量来追求收集速度，适合追求垃圾收集速度的服务器上。可以通过JVM启动参数：-XX:+UseConcMarkSweepGC来开启CMS。

### YGC 和 FGC
1.YGC和FGC是什么 

   YGC ：对新生代堆进行gc。频率比较高，因为大部分对象的存活寿命较短，在新生代里被回收。性能耗费较小。

   FGC ：全堆范围的gc。默认堆空间使用到达80%(可调整)的时候会触发fgc。以我们生产环境为例，一般比较少会触发fgc，有时10天或一周左右会有一次。

2.什么时候执行YGC和FGC

   a.edn空间不足,执行 young gc

   b.old空间不足，perm空间不足，调用方法System.gc() ，ygc时的悲观策略, dump live的内存信息时(jmap –dump:live)，都会执行full gc

## heap buffer和direct buffer有什么区别
首先解释一下两者的区别：

heap buffer这种缓冲区是分配在堆上面的，直接由Java虚拟机负责垃圾回收，可以直接想象成一个字节数组的包装类。

direct buffer则是通过JNI在Java的虚拟机外的内存中分配了一块缓冲区(所以即使在运行时通过-Xmx指定了Java虚拟机的最大堆内存，还是可以实例化超出该大小的Direct ByteBuffer),该块并不直接由Java虚拟机负责垃圾回收收集，但是在direct buffer包装类被回收时，会通过Java Reference机制来释放该内存块。(但Direct Buffer的JAVA对象是归GC管理的，只要GC回收了它的JAVA对象，操作系统才会释放Direct Buffer所申请的空间)

两者各有优劣势:direct buffer对比 heap buffer:

劣势：创建和释放Direct Buffer的代价比Heap Buffer得要高；

优势：当我们把一个Direct Buffer写入Channel的时候，就好比是“内核缓冲区”的内容直接写入了Channel，这样显然快了，减少了数据拷贝（因为我们平时的read/write都是需要在I/O设备与应用程序空间之间的“内核缓冲区”中转一下的）。而当我们把一个Heap Buffer写入Channel的时候，实际上底层实现会先构建一个临时的Direct Buffer，然后把Heap Buffer的内容复制到这个临时的Direct Buffer上，再把这个Direct Buffer写出去。当然，如果我们多次调用write方法，把一个Heap Buffer写入Channel，底层实现可以重复使用临时的Direct Buffer，这样不至于因为频繁地创建和销毁Direct Buffer影响性能。

结论：Direct Buffer创建和销毁的代价很高，所以要用在尽可能重用的地方。 比如周期长传输文件大采用direct buffer，不然一般情况下就直接用heap buffer 就好。

# 网络
## TCP 三次握手和四次挥手
### 三次握手
首先Client端发送连接请求报文，Server段接受连接后回复ACK报文，并为这次连接分配资源。Client端接收到ACK报文后也向Server段发生ACK报文，并分配资源，这样TCP连接就建立了。

### 过程
客户端–发送带有 SYN 标志的数据包–一次握手–服务端

服务端–发送带有 SYN/ACK 标志的数据包–二次握手–客户端

客户端–发送带有带有 ACK 标志的数据包–三次握手–服务端

#### 为什么要三次握手
三次握手的目的是建立可靠的通信信道，说到通讯，简单来说就是数据的发送与接收，而三次握手最主要的目的就是双方确认自己与对方的发送与接收是正常的。

第一次握手：Client 什么都不能确认；Server 确认了对方发送正常，自己接收正常

第二次握手：Client 确认了：自己发送、接收正常，对方发送、接收正常；Server 确认了：对方发送正常，自己接收正常

第三次握手：Client 确认了：自己发送、接收正常，对方发送、接收正常；Server 确认了：自己发送、接收正常，对方发送、接收正常

所以三次握手就能确认双发收发功能都正常，缺一不可。

#### 为什么要传回 SYN， 传了 SYN,为啥还要传 ACK？
接收端传回发送端所发送的 SYN 是为了告诉发送端，我接收到的信息确实就是你所发送的信号了。双方通信无误必须是两者互相发送信息都无误。传了 SYN，证明发送方到接收方的通道没有问题，但是接收方到发送方的通道还需要 ACK 信号来进行验证。

### 四次挥手
假设Client端发起中断连接请求，也就是发送FIN报文。Server端接到FIN报文后，意思是说"我Client端没有数据要发给你了"，但是如果你还有数据没有发送完成，则不必急着关闭Socket，可以继续发送数据。所以你先发送ACK，"告诉Client端，你的请求我收到了，但是我还没准备好，请继续你等我的消息"。这个时候Client端就进入FIN_WAIT状态，继续等待Server端的FIN报文。当Server端确定数据已发送完成，则向Client端发送FIN报文，"告诉Client端，好了，我这边数据发完了，准备好关闭连接了"。Client端收到FIN报文后，"就知道可以关闭连接了，但是他还是不相信网络，怕Server端不知道要关闭，所以发送ACK后进入TIME_WAIT状态，如果Server端没有收到ACK则可以重传。“，Server端收到ACK后，"就知道可以断开连接了"。Client端等待了2MSL后依然没有收到回复，则证明Server端已正常关闭，那好，我Client端也可以关闭连接了。Ok，TCP连接就这样关闭了！

### 过程
客户端-发送一个 FIN，用来关闭客户端到服务器的数据传送

服务器-收到这个 FIN，它发回一 个 ACK，确认序号为收到的序号加1 。和 SYN 一样，一个 FIN 将占用一个序号

服务器-关闭与客户端的连接，发送一个FIN给客户端

客户端-发回 ACK 报文确认，并将确认序号设置为收到序号加1

### 为什么连接的时候是三次握手，关闭的时候却是四次握手？
因为当Server端收到Client端的SYN连接请求报文后，可以直接发送SYN+ACK报文。其中ACK报文是用来应答的，SYN报文是用来同步的。但是关闭连接时，当Server端收到FIN报文时，很可能并不会立即关闭SOCKET，所以只能先回复一个ACK报文，告诉Client端，"你发的FIN报文我收到了"。只有等到我Server端所有的报文都发送完了，我才能发送FIN报文，因此不能一起发送。故需要四步握手。

### 为什么TIME_WAIT状态需要经过2MSL(最大报文段生存时间)才能返回到CLOSE状态？
虽然按道理，四个报文都发送完毕，我们可以直接进入CLOSE状态了，但是我们必须假象网络是不可靠的，有可以最后一个ACK丢失。所以TIME_WAIT状态就是用来重发可能丢失的ACK报文。

## 从输入url到页面加载发生了什么？使用了哪些协议
### 过程
DNS解析，TCP连接，发送HTTP请求，服务器处理请求并返回HTTP报文，浏览器解析渲染页面，连接结束

### 协议：
1，DNS：获取域名对应iP;
2，TCP：与服务器建立tcp连接；
3，IP：建立tcp连接时需要传输数据，传送数据在网络层使用ip协议；
4，OPSF：ip数据包在路由器之间，路由选择使用OPSF协议；
5，ARP：路由器与服务器进行通信时，需要将IP地址转换为MAC地址，使用ARF协议；
6，HTTP：在tcp建立完成后，使用http访问网页

## 常用状态码
1XX 信息性状态码 接受的请求正在处理
2XX 成功状态码   请求正在处理完毕
3XX 重定向状态码 需要进行附加操作以完成请求
4XX 客户端错误   服务器无法正常处理请求
5XX 服务端错误   服务器处理请求出错

## HTTP协议与TCP/IP协议的关系
HTTP的长连接和短连接本质上是TCP长连接和短连接。HTTP属于应用层协议，在传输层使用TCP协议，在网络层使用IP协议。 IP协议主要解决网络路由和寻址问题，TCP协议主要解决如何在IP层之上可靠地传递数据包，使得网络上接收端收到发送端所发出的所有包，并且顺序与发送顺序一致。TCP协议是可靠的、面向连接的。

## HTTP协议是无状态的
HTTP协议是无状态的，指的是协议对于事务处理没有记忆能力，服务器不知道客户端是什么状态。也就是说，打开一个服务器上的网页和上一次打开这个服务器上的网页之间没有任何联系。HTTP是一个无状态的面向连接的协议，无状态不代表HTTP不能保持TCP连接，更不能代表HTTP使用的是UDP协议（无连接）。

### HTTP是不保存状态的协议,如何保存用户状态
HTTP 是一种不保存状态，即无状态（stateless）协议。也就是说 HTTP 协议自身不对请求和响应之间的通信状态进行保存。那么我们保存用户状态呢？Session 机制的存在就是为了解决这个问题，Session 的主要作用就是通过服务端记录用户的状态。典型的场景是购物车，当你要添加商品到购物车的时候，系统不知道是哪个用户操作的，因为 HTTP 协议是无状态的。服务端给特定的用户创建特定的 Session 之后就可以标识这个用户并且跟踪这个用户了（一般情况下，服务器会在一定时间内保存这个 Session，过了时间限制，就会销毁这个Session）。

在服务端保存 Session 的方法很多，最常用的就是内存和数据库(比如是使用内存数据库redis保存)。既然 Session 存放在服务器端，那么我们如何实现 Session 跟踪呢？大部分情况下，我们都是通过在 Cookie 中附加一个 Session ID 来方式来跟踪。

## Cookie 与Session
Cookie 和 Session都是用来跟踪浏览器用户身份的会话方式，但是两者的应用场景不太一样。

Cookie 一般用来保存用户信息 比如①我们在 Cookie 中保存已经登录过得用户信息，下次访问网站的时候页面可以自动帮你登录的一些基本信息给填了；②一般的网站都会有保持登录也就是说下次你再访问网站的时候就不需要重新登录了，这是因为用户登录的时候我们可以存放了一个 Token 在 Cookie 中，下次登录的时候只需要根据 Token 值来查找用户即可(为了安全考虑，重新登录一般要将 Token 重写)；③登录一次网站后访问网站其他页面不需要重新登录。

Session 的主要作用就是通过服务端记录用户的状态。 典型的场景是购物车，当你要添加商品到购物车的时候，系统不知道是哪个用户操作的，因为 HTTP 协议是无状态的。服务端给特定的用户创建特定的 Session 之后就可以标识这个用户并且跟踪这个用户了。

Cookie 数据保存在客户端(浏览器端)，Session 数据保存在服务器端。

Cookie 存储在客户端中，而Session存储在服务器上，相对来说 Session 安全性更高。如果使用 Cookie 的一些敏感信息不要写入 Cookie 中，最好能将 Cookie 信息加密然后使用到的时候再去服务器端解密。

## 短连接，长连接
在HTTP/1.0中默认使用短连接。也就是说，客户端和服务器每进行一次HTTP操作，就建立一次连接，任务结束就中断连接。当客户端浏览器访问的某个HTML或其他类型的Web页中包含有其他的Web资源（如JavaScript文件、图像文件、CSS文件等），每遇到这样一个Web资源，浏览器就会重新建立一个HTTP会话。而从HTTP/1.1起，默认使用长连接，用以保持连接特性。使用长连接的HTTP协议，会在响应头加入这行代码：
Connection:keep-alive
在使用长连接的情况下，当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，客户端再次访问这个服务器时，会继续使用这一条已经建立的连接。Keep-Alive不会永久保持连接，它有一个保持时间，可以在不同的服务器软件（如Apache）中设定这个时间。实现长连接需要客户端和服务端都支持长连接。

## HTTP 1.0 1.1区别
长连接 : 在HTTP/1.0中，默认使用的是短连接，也就是说每次请求都要重新建立一次连接。HTTP 是基于TCP/IP协议的,每一次建立或者断开连接都需要三次握手四次挥手的开销，如果每次请求都要这样的话，开销会比较大。因此最好能维持一个长连接，可以用个长连接来发多个请求。HTTP 1.1起，默认使用长连接 ,默认开启Connection： keep-alive。 HTTP/1.1的持续连接有非流水线方式和流水线方式 。流水线方式是客户在收到HTTP的响应报文之前就能接着发送新的请求报文。与之相对应的非流水线方式是客户在收到前一个响应后才能发送下一个请求。

错误状态响应码 :在HTTP1.1中新增了24个错误状态响应码，如409（Conflict）表示请求的资源与资源的当前状态发生冲突；410（Gone）表示服务器上的某个资源被永久性的删除。

缓存处理 :在HTTP1.0中主要使用header里的If-Modified-Since,Expires来做为缓存判断的标准，HTTP1.1则引入了更多的缓存控制策略例如Entity tag，If-Unmodified-Since, If-Match, If-None-Match等更多可供选择的缓存头来控制缓存策略。

带宽优化及网络连接的使用 :HTTP1.0中，存在一些浪费带宽的现象，例如客户端只是需要某个对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能，HTTP1.1则在请求头引入了range头域，它允许只请求资源的某个部分，即返回码是206（Partial Content），这样就方便了开发者自由的选择以便于充分利用带宽和连接。

## HTTP 和 HTTPS 的区别
端口 ：HTTP的URL由“http://”起始且默认使用端口80，而HTTPS的URL由“https://”起始且默认使用端口443。

安全性和资源消耗： HTTP协议运行在TCP之上，所有传输的内容都是明文，客户端和服务器端都无法验证对方的身份。HTTPS是运行在SSL/TLS之上的HTTP协议，SSL/TLS 运行在TCP之上。所有传输的内容都经过加密，加密采用对称加密，但对称加密的密钥用服务器方的证书进行了非对称加密。所以说，HTTP 安全性没有 HTTPS高，但是 HTTPS 比HTTP耗费更多服务器资源。
对称加密：密钥只有一个，加密解密为同一个密码，且加解密速度快，典型的对称加密算法有DES、AES等；
非对称加密：密钥成对出现（且根据公钥无法推知私钥，根据私钥也无法推知公钥），加密解密使用不同密钥（公钥加密需要私钥解密，私钥加密需要公钥解密），相对对称加密速度较慢，典型的非对称加密算法有RSA、DSA等。

## REST模式：POST，GET，PUT，DELETE，PATCH的含义与区别
1. 根据HTTP规范，GET用于信息获取，而且是安全的和幂等的

GET请求是安全的。所谓安全是指不管进行多少次操作，资源的状态都不会改变。该请求就像数据库的select操作一样，只是用来查询一下数据，不会修改、增加数据，不会影响资源的内容，即该请求不会产生副作用。无论进行多少次操作，结果都是一样的。

2. 根据HTTP规范，POST一般用于创建数据，不是安全和幂等的

POST请求既不是安全的，也不是幂等的，比如常见的POST重复加载问题：当我们多次发出同样的POST请求后，其结果是创建出了若干的资源。

3. PUT一般用于创建或完整更新数据，而且是安全和幂等的

PUT请求是向服务器端发送数据的，从而改变信息，该请求就像数据库的update操作一样，用来修改完整的数据内容，但是不会增加数据的种类等，也就是说无论进行多少次PUT操作，其结果并没有不同。

4. DELETE一般用于删除数据，而且是安全和幂等的

DELETE请求顾名思义，就是用来删除某一个资源的，该请求就像数据库的delete操作，无论进行多少次DELETE操作，其结果并没有不同。

5. PATCH一般用于更新部分数据，不是安全和幂等的

PATCH请求是对PUT请求的补充，一般用来对已知资源部分更新，是后来新出的标准，GitHub Api也开始使用。

## 转发(Forward)和重定向(Redirect)的区别
转发是服务器行为，重定向是客户端行为。

转发（Forword） 通过RequestDispatcher对象的forward（HttpServletRequest request,HttpServletResponse response）方法实现的。RequestDispatcher 可以通过HttpServletRequest 的 getRequestDispatcher()方法获得。例如下面的代码就是跳转到 login_success.jsp 页面。

request.getRequestDispatcher("login_success.jsp").forward(request, response);
重定向（Redirect） 是利用服务器返回的状态码来实现的。客户端浏览器请求服务器的时候，服务器会返回一个状态码。服务器通过HttpServletRequestResponse的setStatus(int status)方法设置状态码。如果服务器返回301或者302，则浏览器会到新的网址重新请求该资源。

从地址栏显示来说：forward是服务器请求资源，服务器直接访问目标地址的URL，把那个URL的响应内容读取过来，然后把这些内容再发给浏览器。浏览器根本不知道服务器发送的内容从哪里来的，所以它的地址栏还是原来的地址。redirect是服务端根据逻辑，发送一个状态码，告诉浏览器重新去请求那个地址。所以地址栏显示的是新的URL。
从数据共享来说：forward：转发页面和转发到的页面可以共享request里面的数据。redirect：不能共享数据。
从运用地方来说：forward：一般用于用户登陆的时候，根据角色转发到相应的模块。redirect：一般用于用户注销登陆时返回主页面和跳转到其它的网站等。
从效率来说：forward：高。redirect：低。

##  IP地址与MAC地址的区别
IP地址是指互联网协议地址（Internet Protocol Address）IP Address的缩写。IP地址是IP协议提供的一种统一的地址格式，它为互联网上的每一个网络和每一台主机分配一个逻辑地址，以此来屏蔽物理地址的差异。

MAC 地址又称为物理地址、硬件地址，用来定义网络设备的位置。网卡的物理地址通常是由网卡生产厂家写入网卡的，具有全球唯一性。MAC地址用于在网络中唯一标示一个网卡，一台电脑会有一或多个网卡，每个网卡都需要有一个唯一的MAC地址。

## TCP 和 UDP区别
### UDP（User Data Protocol，用户数据报协议）
1，是一个非连接的协议，传输数据之前源端和终端不建立连接，当它想传送时就简单地去抓取来自应用程序的数据，并尽可能快地把它扔到网络上。在发送端，UDP传送数据的速度仅仅是受应用程序生成数据的速度、计算机的能力和传输带宽的限制；在接收端，UDP把每个消息段放在队列中，应用程序每次从队列中读一个消息段。

（2） 由于传输数据不建立连接，因此也就不需要维护连接状态，包括收发状态等，因此一台服务机可同时向多个客户机传输相同的消息。

（3） UDP信息包的标题很短，只有8个字节，相对于TCP的20个字节信息包的额外开销很小。

（4） 吞吐量不受拥挤控制算法的调节，只受应用软件生成数据的速率、传输带宽、源端和终端主机性能的限制。

（5）UDP使用尽最大努力交付，即不保证可靠交付，因此主机不需要维持复杂的链接状态表（这里面有许多参数）。

（6）UDP是面向报文的。发送方的UDP对应用程序交下来的报文，在添加首部后就向下交付给IP层。既不拆分，也不合并，而是保留这些报文的边界，因此，应用程序需要选择合适的报文大小。

### 区别
UDP 在传送数据之前不需要先建立连接，远地主机在收到 UDP 报文后，不需要给出任何确认。虽然 UDP 不提供可靠交付，但在某些情况下 UDP 确是一种最有效的工作方式（一般用于即时通信），比如： QQ 语音、 QQ 视频 、直播等等

TCP 提供面向连接的服务。在传送数据之前必须先建立连接，数据传送结束后要释放连接。 TCP 不提供广播或多播服务。由于 TCP 要提供可靠的，面向连接的传输服务（TCP的可靠体现在TCP在传递数据之前，会有三次握手来建立连接，而且在数据传递时，有确认、窗口、重传、拥塞控制机制，在数据传完后，还会断开连接用来节约系统资源），这一难以避免增加了许多开销，如确认，流量控制，计时器以及连接管理等。这不仅使协议数据单元的首部增大很多，还要占用许多处理机资源。TCP 一般用于文件传输、发送和接收邮件、远程登录等场景。

## TCP 协议如何保证可靠传输
1，应用数据被分割成 TCP 认为最适合发送的数据块。

2，TCP 给发送的每一个包进行编号，接收方对数据包进行排序，把有序数据传送给应用层。

3，校验和： TCP 将保持它首部和数据的检验和。这是一个端到端的检验和，目的是检测数据在传输过程中的任何变化。如果收到段的检验和有差错，TCP 将丢弃这个报文段和不确认收到此报文段。

4，TCP 的接收端会丢弃重复的数据。

5，流量控制： TCP 连接的每一方都有固定大小的缓冲空间，TCP的接收端只允许发送端发送接收端缓冲区能接纳的数据。当接收方来不及处理发送方的数据，能提示发送方降低发送的速率，防止包丢失。TCP 使用的流量控制协议是可变大小的滑动窗口协议。 （TCP 利用滑动窗口实现流量控制）

6，拥塞控制： 当网络拥塞时，减少数据的发送。

7， ARQ协议： 也是为了实现可靠传输的，它的基本原理就是每发完一个分组就停止发送，等待对方确认。在收到确认后再发下一个分组。

8，超时重传： 当 TCP 发出一个段后，它启动一个定时器，等待目的端确认收到这个报文段。如果不能及时收到一个确认，将重发这个报文段。

## ARQ协议
自动重传请求（Automatic Repeat-reQuest，ARQ）是OSI模型中数据链路层和传输层的错误纠正协议之一。它通过使用确认和超时这两个机制，在不可靠服务的基础上实现可靠的信息传输。如果发送方在发送后一段时间之内没有收到确认帧，它通常会重新发送。ARQ包括停止等待ARQ协议和连续ARQ协议。

停止等待ARQ协议
停止等待协议是为了实现可靠传输的，它的基本原理就是每发完一个分组就停止发送，等待对方确认（回复ACK）。如果过了一段时间（超时时间后），还是没有收到 ACK 确认，说明没有发送成功，需要重新发送，直到收到确认后再发下一个分组；
在停止等待协议中，若接收方收到重复分组，就丢弃该分组，但同时还要发送确认；
优点： 简单

缺点： 信道利用率低，等待时间长

1) 无差错情况:

发送方发送分组,接收方在规定时间内收到,并且回复确认.发送方再次发送。

2) 出现差错情况（超时重传）:

停止等待协议中超时重传是指只要超过一段时间仍然没有收到确认，就重传前面发送过的分组（认为刚才发送过的分组丢失了）。因此每发送完一个分组需要设置一个超时计时器，其重传时间应比数据在分组传输的平均往返时间更长一些。这种自动重传方式常称为 自动重传请求 ARQ 。另外在停止等待协议中若收到重复分组，就丢弃该分组，但同时还要发送确认。连续 ARQ 协议 可提高信道利用率。发送维持一个发送窗口，凡位于发送窗口内的分组可连续发送出去，而不需要等待对方确认。接收方一般采用累积确认，对按序到达的最后一个分组发送确认，表明到这个分组位置的所有分组都已经正确收到了。

3) 确认丢失和确认迟到

确认丢失 ：确认消息在传输过程丢失。当A发送M1消息，B收到后，B向A发送了一个M1确认消息，但却在传输过程中丢失。而A并不知道，在超时计时过后，A重传M1消息，B再次收到该消息后采取以下两点措施：1. 丢弃这个重复的M1消息，不向上层交付。 2. 向A发送确认消息。（不会认为已经发送过了，就不再发送。A能重传，就证明B的确认消息丢失）。
确认迟到 ：确认消息在传输过程中迟到。A发送M1消息，B收到并发送确认。在超时时间内没有收到确认消息，A重传M1消息，B仍然收到并继续发送确认消息（B收到了2份M1）。此时A收到了B第二次发送的确认消息。接着发送其他数据。过了一会，A收到了B第一次发送的对M1的确认消息（A也收到了2份确认消息）。处理如下：1. A收到重复的确认后，直接丢弃。2. B收到重复的M1后，也直接丢弃重复的M1。
连续ARQ协议
连续 ARQ 协议可提高信道利用率。发送方维持一个发送窗口，凡位于发送窗口内的分组可以连续发送出去，而不需要等待对方确认。接收方一般采用累计确认，对按序到达的最后一个分组发送确认，表明到这个分组为止的所有分组都已经正确收到了。

优点： 信道利用率高，容易实现，即使确认丢失，也不必重传。

缺点： 不能向发送方反映出接收方已经正确收到的所有分组的信息。 比如：发送方发送了 5条 消息，中间第三条丢失（3号），这时接收方只能对前两个发送确认。发送方无法知道后三个分组的下落，而只好把后三个全部重传一次。这也叫 Go-Back-N（回退 N），表示需要退回来重传已经发送过的 N 个消息。

## TCP粘包，拆包
假设客户端分别发送了两个数据包D1和D2给服务端，由于服务端一次读取到的字节数是不确定的，故可能存在以下4种情况。

（1）服务端分两次读取到了两个独立的数据包，分别是D1和D2，没有粘包和拆包；

（2）服务端一次接收到了两个数据包，D1和D2粘合在一起，被称为TCP粘包；

（3）服务端分两次读取到了两个数据包，第一次读取到了完整的D1包和D2包的部分内容，第二次读取到了D2包的剩余内容，这被称为TCP拆包；

（4）服务端分两次读取到了两个数据包，第一次读取到了D1包的部分内容D1_1，第二次读取到了D1包的剩余内容D1_2和D2包的整包。

如果此时服务端TCP接收滑窗非常小，而数据包D1和D2比较大，很有可能会发生第五种可能，即服务端分多次才能将D1和D2包接收完全，期间发生多次拆包。

### 粘包问题的解决策略
由于底层的TCP无法理解上层的业务数据，所以在底层是无法保证数据包不被拆分和重组的，这个问题只能通过上层的应用协议栈设计来解决，根据业界的主流协议的解决方案，可以归纳如下。

（1）消息定长，例如每个报文的大小为固定长度200字节，如果不够，空位补空格；

（2）在包尾增加回车换行符进行分割，例如FTP协议；

（3）将消息分为消息头和消息体，消息头中包含表示消息总长度（或者消息体长度）的字段，通常设计思路为消息头的第一个字段使用int32来表示消息的总长度；

（4）更复杂的应用层协议。

## 各种协议与HTTP协议之间的关系
### 客户端：
HTTP协议的职责：生成对目标服务器的HTTP请求报文；
TCP协议的职责：为了方便通信，将http报文按序号分割成报文段，将每个报文段可靠的传送给对方

### 路由器
IP协议的职责：搜索对方的地址，一边中转一边传输

### 服务器端
TCP协议的职责：从对方接受报文段并按序号重组
HTTP协议的职责：对请求的内容进行处理；



# Mysql
## 存储引擎(MyISAM和InnoDB)
MyISAM是MySQL的默认数据库引擎（5.5版之前）。虽然性能极佳，而且提供了大量的特性，包括全文索引、压缩、空间函数等，但MyISAM不支持事务和行级锁，而且最大的缺陷就是崩溃后无法安全恢复。不过，5.5版本之后，MySQL引入了InnoDB（事务性数据库引擎），MySQL 5.5版本后默认的存储引擎为InnoDB。

大多数时候我们使用的都是 InnoDB 存储引擎，但是在某些情况下使用 MyISAM 也是合适的比如读密集的情况下。（如果你不介意 MyISAM 崩溃回复问题的话）。

### 两者的对比：
是否支持行级锁 : MyISAM 只有表级锁(table-level locking)，而InnoDB 支持行级锁(row-level locking)和表级锁,默认为行级锁。

是否支持事务和崩溃后的安全恢复： MyISAM 强调的是性能，每次查询具有原子性,其执行数度比InnoDB类型更快，但是不提供事务支持。但是InnoDB 提供事务支持事务，外部键等高级数据库功能。 具有事务(commit)、回滚(rollback)和崩溃修复能力(crash recovery capabilities)的事务安全(transaction-safe (ACID compliant))型表。

是否支持外键： MyISAM不支持，而InnoDB支持。

是否支持MVCC(多版本并发控制) ：仅 InnoDB 支持。应对高并发事务, MVCC比单纯的加锁更高效;MVCC只在 READ COMMITTED 和 REPEATABLE READ 
两个隔离级别下工作;MVCC可以使用 乐观(optimistic)锁 和 悲观(pessimistic)锁来实现;各数据库中MVCC实现并不统一。

索引实现方式不同：见下方

## 索引
MySQL索引使用的数据结构主要有BTree索引 和 哈希索引 。对于哈希索引来说，底层的数据结构就是哈希表，因此在绝大多数需求为单条记录查询的时候，可以选择哈希索引，查询性能最快；其余大部分场景，建议选择BTree索引。

MySQL的BTree索引使用的是B树中的B+Tree，但对于主要的两种存储引擎的实现方式是不同的。

MyISAM: B+Tree叶节点的data域存放的是数据记录的地址。在索引检索的时候，首先按照B+Tree搜索算法搜索索引，如果指定的Key存在，则取出其 data 域的值，然后以 data 域的值为地址读取相应的数据记录。这被称为“非聚簇索引”。

InnoDB: 其数据文件本身就是索引文件。相比MyISAM，索引文件和数据文件是分离的，其表数据文件本身就是按B+Tree组织的一个索引结构，树的叶节点data域保存了完整的数据记录。这个索引的key是数据表的主键，因此InnoDB表数据文件本身就是主索引。这被称为“聚簇索引（或聚集索引）”。而其余的索引都作为辅助索引，辅助索引的data域存储相应记录主键的值而不是地址，这也是和MyISAM不同的地方。在根据主索引搜索时，直接找到key所在的节点即可取出数据；在根据辅助索引查找时，则需要先取出主键的值，再走一遍主索引。 因此，在设计表的时候，不建议使用过长的字段作为主键，也不建议使用非单调的字段作为主键，这样会造成主索引频繁分裂。

### BTree索引类型
#### 普通索引
这是最基本的索引类型，而且它没有唯一性之类的限制。普通索引可以通过以下几种方式创建：

（1）创建索引: CREATE INDEX 索引名 ON 表名(列名1，列名2,...);

（2）修改表: ALTER TABLE 表名ADD INDEX 索引名 (列名1，列名2,...);

（3）创建表时指定索引：CREATE TABLE 表名 ( [...], INDEX 索引名 (列名1，列名 2,...) );

#### UNIQUE索引
表示唯一的，不允许重复的索引，如果该字段信息保证不会重复例如身份证号用作索引时，可设置为unique：

（1）创建索引：CREATE UNIQUE INDEX 索引名 ON 表名(列的列表);

（2）修改表：ALTER TABLE 表名ADD UNIQUE 索引名 (列的列表);

（3）创建表时指定索引：CREATE TABLE 表名( [...], UNIQUE 索引名 (列的列表) );

#### 主键：PRIMARY KEY索引
主键是一种唯一性索引，但它必须指定为“PRIMARY KEY”。

（1）主键一般在创建表的时候指定：“CREATE TABLE 表名( [...], PRIMARY KEY (列的列表) ); ”。

（2）但是，我们也可以通过修改表的方式加入主键：“ALTER TABLE 表名ADD PRIMARY KEY (列的列表); ”。

每个表只能有一个主键。 （主键相当于聚合索引，是查找最快的索引）

注：不能用CREATE INDEX语句创建PRIMARY KEY索引

### 索引优化
1，索引不会包含有NULL值的列：只要列中包含有NULL值，都将不会被包含在索引中，组合索引中只要有一列有NULL值，那么这一列对于此条组合索引就是无效的。所以我们在数据库设计时，不要让索引字段的默认值为NULL。

2，使用短索引：假设，如果有一个数据类型为CHAR(255)的列，在前10个或20个字符内，绝大部分数据的值是唯一的，那么就不要对整个列进行索引。短索引不仅可以提高查询速度而且可以节省I/O操作。

3，索引列排序：MySQL查询只使用一个索引，因此如果WHERE子句中已经使用了索引的话，那么ORDER BY中的列是不会使用索引的。因此数据库默认排序可以符合要求的情况下，不要使用排序操作；尽量不要包含多个列的排序，如果需要，最好给这些列也创建组合索引。

4，LIKE语句操作：一般情况下，不建议使用LIKE操作；如果非使用不可，如何使用也是一个研究的课题。LIKE "%aaaaa%"不会使用索引，但是LIKE "aaa%"却可以使用索引。

5，不要在索引列上进行运算：在建立索引的原则中，提到了索引列不能进行运算，这里就不再赘述了。


### 为什么要使用索引？

1，通过创建唯一性索引，可以保证数据库表中每一行数据的唯一性。
2，可以大大加快数据的检索速度（大大减少的检索的数据量）, 这也是创建索引的最主要的原因。
3，帮助服务器避免排序和临时表
4，将随机IO变为顺序IO
5，可以加速表和表之间的连接，特别是在实现数据的参考完整性方面特别有意义。

### 为什么不对表中的每一个列创建一个索引呢？

当对表中的数据进行增加、删除和修改的时候，索引也要动态的维护，这样就降低了数据的维护速度。
索引需要占物理空间，除了数据表占数据空间之外，每一个索引还要占一定的物理空间，如果要建立聚簇索引，那么需要的空间就会更大。
创建索引和维护索引要耗费时间，这种时间随着数据量的增加而增加。

### 索引是如何提高查询速度的？

将无序的数据变成相对有序的数据（就像查目录一样）

### 索引的注意事项

避免 where 子句中对字段施加函数，这会造成无法命中索引。
在使用InnoDB时使用与业务无关的自增主键作为主键，即使用逻辑主键，而不要使用业务主键。
将打算加索引的列设置为 NOT NULL ，否则将导致引擎放弃使用索引而进行全表扫描
删除长期未使用的索引，不用的索引的存在会造成不必要的性能损耗 MySQL 5.7 可以通过查询 sys 库的 schema_unused_indexes 视图来查询哪些索引从未被使用
在使用 limit offset 查询缓慢时，可以借助索引来提高性能

## 事务
### 特性（ACID）
原子性： 事务是最小的执行单位，不允许分割。事务的原子性确保动作要么全部完成，要么完全不起作用；

一致性： 执行事务前后，数据保持一致，多个事务对同一个数据读取的结果是相同的；

隔离性： 并发访问数据库时，一个用户的事务不被其他事务所干扰，各并发事务之间数据库是独立的；

持久性： 一个事务被提交之后。它对数据库中数据的改变是持久的，即使数据库发生故障也不应该对其有任何影响。

### 事务的ACID是通过InnoDB日志和锁来保证。
事务的隔离性是通过数据库锁的机制实现的，持久性通过redo log（重做日志）来实现，原子性和一致性通过Undo log来实现。UndoLog的原理很简单，为了满足事务的原子性，在操作任何数据之前，首先将数据备份到一个地方（这个存储数据备份的地方称为UndoLog）。然后进行数据的修改。如果出现了错误或者用户执行了ROLLBACK语句，系统可以利用Undo Log中的备份将数据恢复到事务开始之前的状态。
和Undo Log相反，RedoLog记录的是新数据的备份。在事务提交前，只要将RedoLog持久化即可，不需要将数据持久化。当系统崩溃时，虽然数据没有持久化，但是RedoLog已经持久化。系统可以根据RedoLog的内容，将所有数据恢复到最新的状态。

### 并发事务带来哪些问题
脏读（Dirty read）: 当一个事务正在访问数据并且对数据进行了修改，而这种修改还没有提交到数据库中，这时另外一个事务也访问了这个数据，然后使用了这个数据。因为这个数据是还没有提交的数据，那么另外一个事务读到的这个数据是“脏数据”，依据“脏数据”所做的操作可能是不正确的。

丢失修改（Lost to modify）: 指在一个事务读取一个数据时，另外一个事务也访问了该数据，那么在第一个事务中修改了这个数据后，第二个事务也修改了这个数据。这样第一个事务内的修改结果就被丢失，因此称为丢失修改。	例如：事务1读取某表中的数据A=20，事务2也读取A=20，事务1修改A=A-1，事务2也修改A=A-1，最终结果A=19，事务1的修改被丢失。

不可重复读（Unrepeatableread）: 指在一个事务内多次读同一数据。在这个事务还没有结束时，另一个事务也访问该数据。那么，在第一个事务中的两次读数据之间，由于第二个事务的修改导致第一个事务两次读取的数据可能不太一样。这就发生了在一个事务内两次读到的数据是不一样的情况，因此称为不可重复读。

幻读（Phantom read）: 幻读与不可重复读类似。它发生在一个事务（T1）读取了几行数据，接着另一个并发事务（T2）插入了一些数据时。在随后的查询中，第一个事务（T1）就会发现多了一些原本不存在的记录，就好像发生了幻觉一样，所以称为幻读。

#### 不可重复读和幻读区别
不可重复读的重点是修改比如多次读取一条记录发现其中某些列的值被修改，幻读的重点在于新增或者删除比如多次读取一条记录发现记录增多或减少了。

### 隔离级别
READ-UNCOMMITTED(读取未提交)： 最低的隔离级别，允许读取尚未提交的数据变更，可能会导致脏读、不可重复读或幻读。

READ-COMMITTED(读取已提交)： 允许读取并发事务已经提交的数据，可以阻止脏读，但是幻读或不可重复读仍有可能发生。

REPEATABLE-READ(可重复读)：对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，可以阻止脏读和不可重复读，但幻读仍有可能发生。

SERIALIZABLE(可串行化)： 最高的隔离级别，完全服从ACID的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，该级别可以防止脏读、不可重复读以及幻读。

MySQL InnoDB 存储引擎的默认支持的隔离级别是 REPEATABLE-READ（可重读）。

### 分布式事务
分布式事务就是指事务的参与者、支持事务的服务器、资源服务器以及事务管理器分别位于不同的分布式系统的不同节点之上。简单的说，就是一次大的操作由不同的小操作组成，这些小的操作分布在不同的服务器上，且属于不同的应用，分布式事务需要保证这些小操作要么全部成功，要么全部失败。本质上来说，分布式事务就是为了保证不同数据库的数据一致性。

#### 产生原因
一个是service产生多个节点，另一个是resource产生多个节点。

##### service多个节点
随着互联网快速发展，微服务，SOA等服务架构模式正在被大规模的使用，举个简单的例子，一个公司之内，用户的资产可能分为好多个部分，比如余额，积分，优惠券等等。在公司内部有可能积分功能由一个微服务团队维护，优惠券又是另外的团队维护，这样的话就无法保证积分扣减了之后，优惠券能否扣减成功。

##### resource多个节点
同样的，互联网发展得太快了，我们的Mysql一般来说装千万级的数据就得进行分库分表，对于一个支付宝的转账业务来说，你给的朋友转钱，有可能你的数据库是在北京，而你的朋友的钱是存在上海，所以我们依然无法保证他们能同时成功。

#### 基础
##### CAP
CAP定理，又被叫作布鲁尔定理。对于设计分布式系统来说(不仅仅是分布式事务)的架构师来说，CAP就是你的入门理论。

C (一致性):对某个指定的客户端来说，读操作能返回最新的写操作。对于数据分布在不同节点上的数据上来说，如果在某个节点更新了数据，那么在其他节点如果都能读取到这个最新的数据，那么就称为强一致，如果有某个节点没有读取到，那就是分布式不一致。

A (可用性)：非故障的节点在合理的时间内返回合理的响应(不是错误和超时的响应)。可用性的两个关键一个是合理的时间，一个是合理的响应。合理的时间指的是请求不能无限被阻塞，应该在合理的时间给出返回。合理的响应指的是系统应该明确返回结果并且结果是正确的，这里的正确指的是比如应该返回50，而不是返回40。

P (分区容错性):当出现网络分区后，系统能够继续工作。打个比方，这里个集群有多台机器，有台机器网络出现了问题，但是这个集群仍然可以正常工作。

熟悉CAP的人都知道，三者不能共有，如果感兴趣可以搜索CAP的证明，在分布式系统中，网络无法100%可靠，分区其实是一个必然现象，如果我们选择了CA而放弃了P，那么当发生分区现象时，为了保证一致性，这个时候必须拒绝请求，但是A又不允许，所以分布式系统理论上不可能选择CA架构，只能选择CP或者AP架构。

对于CP来说，放弃可用性，追求一致性和分区容错性，我们的zookeeper其实就是追求的强一致。
对于AP来说，放弃一致性(这里说的一致性是强一致性)，追求分区容错性和可用性，这是很多分布式系统设计时的选择，后面的BASE也是根据AP来扩展。
顺便一提，CAP理论中是忽略网络延迟，也就是当事务提交时，从节点A复制到节点B，但是在现实中这个是明显不可能的，所以总会有一定的时间是不一致。同时CAP中选择两个，比如你选择了CP，并不是叫你放弃A。因为P出现的概率实在是太小了，大部分的时间你仍然需要保证CA。就算分区出现了你也要为后来的A做准备，比如通过一些日志的手段，是其他机器回复至可用。

#### 解决方案（https://juejin.im/post/5b5a0bf9f265da0f6523913b#heading-4

## 表级锁和行级锁对比：
表级锁： MySQL中锁定 粒度最大 的一种锁，对当前操作的整张表加锁，实现简单，资源消耗也比较少，加锁快，不会出现死锁。其锁定粒度最大，触发锁冲突的概率最高，并发度最低，MyISAM和 InnoDB引擎都支持表级锁。

行级锁： MySQL中锁定 粒度最小 的一种锁，只针对当前操作的行进行加锁。 行级锁能大大减少数据库操作的冲突。其加锁粒度最小，并发度高，但加锁的开销也最大，加锁慢，会出现死锁。

## 大表优化
当MySQL单表记录数过大时，数据库的CRUD性能会明显下降，一些常见的优化措施如下：

1. 限定数据的范围

务必禁止不带任何限制数据范围条件的查询语句。比如：我们当用户在查询订单历史的时候，我们可以控制在一个月的范围内；

2. 读/写分离

经典的数据库拆分方案，主库负责写，从库负责读；

3. 垂直分区

根据数据库里面数据表的相关性进行拆分。 例如，用户表中既有用户的登录信息又有用户的基本信息，可以将用户表拆分成两个单独的表，甚至放到单独的库做分库。

简单来说垂直拆分是指数据表列的拆分，把一张列比较多的表拆分为多张表。

垂直拆分的优点： 可以使得列数据变小，在查询时减少读取的Block数，减少I/O次数。此外，垂直分区可以简化表的结构，易于维护。

垂直拆分的缺点： 主键会出现冗余，需要管理冗余列，并会引起Join操作，可以通过在应用层进行Join来解决。此外，垂直分区会让事务变得更加复杂；

4. 水平分区

保持数据表结构不变，通过某种策略存储数据分片。这样每一片数据分散到不同的表或者库中，达到了分布式的目的。 水平拆分可以支撑非常大的数据量。
水平拆分是指数据表行的拆分，表的行数超过200万行时，就会变慢，这时可以把一张的表的数据拆成多张表来存放。水平拆分可以支持非常大的数据量。需要注意的一点是：分表仅仅是解决了单一表数据过大的问题，但由于表的数据还是在同一台机器上，其实对于提升MySQL并发能力没有什么意义，所以 水平拆分最好分库 。

水平拆分能够 支持非常大的数据量存储，应用端改造也少，但 分片事务难以解决 ，跨节点Join性能较差，逻辑复杂。

## sql语句执行顺序（select为例）
1、 FROM：对FROM子句中的前两个表执行笛卡尔积(交叉联接)，生成虚拟表VT1。

2、 ON：对VT1应用ON筛选器，只有那些使为真才被插入到TV2。

3、 OUTER (JOIN):如果指定了OUTER JOIN(相对于CROSS JOIN或INNER JOIN)，保留表中未找到匹配的行将作为外部行添加到VT2，生成TV3。如果FROM子句包含两个以上的表，则对上一个联接生成的结果表和下一个表重复执行步骤1到步骤3，直到处理完所有的表位置。

4、 WHERE：对TV3应用WHERE筛选器，只有使为true的行才插入TV4。

5、 GROUP BY：按GROUP BY子句中的列列表对TV4中的行进行分组，生成TV5。

6、 CUTE|ROLLUP：把超组插入VT5，生成VT6。

7、 HAVING：对VT6应用HAVING筛选器，只有使为true的组插入到VT7。

8、 SELECT：处理SELECT列表，产生VT8。

9、 DISTINCT：将重复的行从VT8中删除，产品VT9。

10、ORDER BY：将VT9中的行按ORDER BY子句中的列列表顺序，生成一个游标(VC10)。

11、TOP：从VC10的开始处选择指定数量或比例的行，生成表TV11，并返回给调用者。

## sql注入及预防
### 注入
1.数字注入

在浏览器地址栏输入：learn.me/sql/article.php?id=1，这是一个get型接口，发送这个请求相当于调用一个查询语句：

$sql = "SELECT * FROM article WHERE id =",$id
正常情况下，应该返回一个id=1的文章信息。那么，如果在浏览器地址栏输入：learn.me/sql/article.php?id=-1 OR 1 =1，这就是一个SQL注入攻击了，可能会返回所有文章的相关信息


2.字符串注入

有这样一个用户登录场景：登录界面包括用户名和密码输入框，以及提交按钮。输入用户名和密码，提交。

这是一个post请求，登录时调用接口learn.me/sql/login.html，首先连接数据库，然后后台对post请求参数中携带的用户名、密码进行参数校验，即sql的查询过程。假设正确的用户名和密码为user和pwd123，输入正确的用户名和密码、提交，相当于调用了以下的SQL语句：

SELECT * FROM user WHERE username = 'user' ADN password = 'pwd123'
由于用户名和密码都是字符串，SQL注入方法即把参数携带的数据变成mysql中注释的字符串。mysql中有2种注释的方法：

1）'#'：'#'后所有的字符串都会被当成注释来处理

用户名输入：user'#（单引号闭合user左边的单引号），密码随意输入，如：111，然后点击提交按钮。等价于SQL语句：

SELECT * FROM user WHERE username = 'user'#'ADN password = '111'
'#'后面都被注释掉了，相当于：

SELECT * FROM user WHERE username = 'user' 
2）'-- ' （--后面有个空格）：'-- '后面的字符串都会被当成注释来处理

用户名输入：user'-- （注意--后面有个空格，单引号闭合user左边的单引号），密码随意输入，如：111，然后点击提交按钮。等价于SQL语句：

SELECT * FROM user WHERE username = 'user'-- 'AND password = '111'
SELECT * FROM user WHERE username = 'user'-- 'AND password = '1111'
'-- '后面都被注释掉了，相当于：

SELECT * FROM user WHERE username = 'user'
因此，以上两种情况可能输入一个错误的密码或者不输入密码就可登录用户名为'user'的账号，这是十分危险的事情。


### 预防
1）严格检查输入变量的类型和格式

对于整数参数，加判断条件：不能为空、参数类型必须为数字

对于字符串参数，可以使用正则表达式进行过滤：如：必须为[0-9a-zA-Z]范围内的字符串

2）过滤和转义特殊字符

在username这个变量前进行转义，对'、"、\等特殊字符进行转义，如：php中的addslashes()函数对username参数进行转义

3）利用mysql的预编译机制

把sql语句的模板（变量采用占位符进行占位）发送给mysql服务器，mysql服务器对sql语句的模板进行编译，编译之后根据语句的优化分析对相应的索引进行优化，在最终绑定参数时把相应的参数传送给mysql服务器，直接进行执行，节省了sql查询时间，以及mysql服务器的资源，达到一次编译、多次执行的目的，除此之外，还可以防止SQL注入。具体是怎样防止SQL注入的呢？实际上当将绑定的参数传到mysql服务器，mysql服务器对参数进行编译，即填充到相应的占位符的过程中，做了转义操作。


# redis 
## memcached 的区别
redis支持更丰富的数据类型（支持更复杂的应用场景）：Redis不仅仅支持简单的k/v类型的数据，同时还提供list，set，zset，hash等数据结构的存储。memcache支持简单的数据类型，String。

Redis支持数据的持久化，可以将内存中的数据保持在磁盘中，重启的时候可以再次加载进行使用,而Memecache把数据全部存在内存之中。

集群模式：memcached没有原生的集群模式，需要依靠客户端来实现往集群中分片写入数据；但是 redis 目前是原生支持 cluster 模式的.
Memcached是多线程，非阻塞IO复用的网络模型；Redis使用单线程的多路 IO 复用模型。

## 常见数据结构以及使用场景分析（实现：https://www.cnblogs.com/binyue/p/5342281.html）
### 1.String
常用命令: set,get,decr,incr,mget 等。

String数据结构是简单的key-value类型，value其实不仅可以是String，也可以是数字。 常规key-value缓存应用； 常规计数：微博数，粉丝数等。

### 2.Hash
常用命令： hget,hset,hgetall 等。

hash 是一个 string 类型的 field 和 value 的映射表，hash 特别适合用于存储对象，后续操作的时候，你可以直接仅仅修改这个对象中的某个字段的值。

### 3.List
常用命令: lpush,rpush,lpop,rpop,lrange等

list 就是链表，Redis list 的应用场景非常多，也是Redis最重要的数据结构之一，比如微博的关注列表，粉丝列表，消息列表等功能都可以用Redis的 list 结构来实现。

Redis list 的实现为一个双向链表，即可以支持反向查找和遍历，更方便操作，不过带来了部分额外的内存开销。

另外可以通过 lrange 命令，就是从某个元素开始读取多少个元素，可以基于 list 实现分页查询，这个很棒的一个功能，基于 redis 实现简单的高性能分页，可以做类似微博那种下拉不断分页的东西（一页一页的往下走），性能高。

### 4.Set
常用命令： sadd,spop,smembers,sunion 等

set 对外提供的功能与list类似是一个列表的功能，特殊之处在于 set 是可以自动排重的。

当你需要存储一个列表数据，又不希望出现重复数据时，set是一个很好的选择，并且set提供了判断某个成员是否在一个set集合内的重要接口，这个也是list所不能提供的。可以基于 set 轻易实现交集、并集、差集的操作。

### 5.Sorted Set
常用命令： zadd,zrange,zrem,zcard等

和set相比，sorted set增加了一个权重参数score，使得集合中的元素能够按score进行有序排列。

举例： 在直播系统中，实时排行信息包含直播间在线用户列表，各种礼物排行榜，弹幕消息（可以理解为按消息维度的消息排行榜）等信息，适合使用 Redis 中的 Sorted Set 结构进行存储。

### 6.Zset(https://www.daxiaju.club/2019/06/28/Redis-Zset-%E5%AE%9E%E7%8E%B0%E5%8E%9F%E7%90%86/)

## redis 持久化机制(怎么保证 redis 挂掉之后再重启数据可以进行恢复)
Redis不同于Memcached的很重一点就是，Redis支持持久化，而且支持两种不同的持久化操作。Redis的一种持久化方式叫快照（snapshotting，RDB），另一种方式是只追加文件（append-only file,AOF）。

### 快照（snapshotting）持久化（RDB）

Redis可以通过创建快照来获得存储在内存里面的数据在某个时间点上的副本。Redis创建快照之后，可以对快照进行备份，可以将快照复制到其他服务器从而创建具有相同数据的服务器副本（Redis主从结构，主要用来提高Redis性能），还可以将快照留在原地以便重启服务器的时候使用。

快照持久化是Redis默认采用的持久化方式。

### AOF（append-only file）持久化

与快照持久化相比，AOF持久化 的实时性更好，因此已成为主流的持久化方案。默认情况下Redis没有开启AOF（append only file）方式的持久化，可以通过appendonly参数开启：

appendonly yes
开启AOF持久化后每执行一条会更改Redis中的数据的命令，Redis就会将该命令写入硬盘中的AOF文件。

### 持久化实现（https://juejin.im/post/5b70dfcf518825610f1f5c16）

## redis 事务
Redis 通过 MULTI、EXEC、WATCH 等命令来实现事务(transaction)功能。事务提供了一种将多个命令请求打包，然后一次性、按顺序地执行多个命令的机制，并且在事务执行期间，服务器不会中断事务而改去执行其他客户端的命令请求，它会将事务中的所有命令都执行完毕，然后才去处理其他客户端的命令请求。

在传统的关系式数据库中，常常用 ACID 性质来检验事务功能的可靠性和安全性。在 Redis 中，事务总是具有原子性（Atomicity）、一致性（Consistency）和隔离性（Isolation），并且当 Redis 运行在某种特定的持久化模式下时，事务也具有持久性（Durability）。

## 缓存雪崩

简介：缓存同一时间大面积的失效，所以，后面的请求都会落到数据库上，造成数据库短时间内承受大量请求而崩掉。

解决办法：

事前：尽量保证整个 redis 集群的高可用性，发现机器宕机尽快补上。选择合适的内存淘汰策略。
事中：本地ehcache缓存 + hystrix限流&降级，避免MySQL崩掉。
事后：利用 redis 持久化机制保存的数据尽快恢复缓存。

## 缓存穿透

简介：一般是黑客故意去请求缓存中不存在的数据，导致所有的请求都落到数据库上，造成数据库短时间内承受大量请求而崩掉。

解决办法： 有很多种方法可以有效地解决缓存穿透问题，最常见的则是采用布隆过滤器，将所有可能存在的数据哈希到一个足够大的bitmap中，一个一定不存在的数据会被 这个bitmap拦截掉，从而避免了对底层存储系统的查询压力。另外也有一个更为简单粗暴的方法（我们采用的就是这种），如果一个查询返回的数据为空（不管是数 据不存在，还是系统故障），我们仍然把这个空结果进行缓存，但它的过期时间会很短，最长不超过五分钟。

## 如何解决 Redis 的并发竞争 Key 问题
所谓 Redis 的并发竞争 Key 的问题也就是多个系统同时对一个 key 进行操作，但是最后执行的顺序和我们期望的顺序不同，这样也就导致了结果的不同！

推荐一种方案：分布式锁（zookeeper 和 redis 都可以实现分布式锁）。（如果不存在 Redis 的并发竞争 Key 问题，不要使用分布式锁，这样会影响性能）

基于zookeeper临时有序节点可以实现的分布式锁。大致思想为：每个客户端对某个方法加锁时，在zookeeper上的与该方法对应的指定节点的目录下，生成一个唯一的瞬时有序节点。 判断是否获取锁的方式很简单，只需要判断有序节点中序号最小的一个。 当释放锁的时候，只需将这个瞬时节点删除即可。同时，其可以避免服务宕机导致的锁无法释放，而产生的死锁问题。完成业务流程后，删除对应的子节点释放锁。

在实践中，当然是从以可靠性为主。所以首推Zookeeper。

## 如何保证缓存与数据库双写时的数据一致性?
你只要用缓存，就可能会涉及到缓存与数据库双存储双写，你只要是双写，就一定会有数据一致性的问题，那么你如何解决一致性问题？

一般来说，就是如果你的系统不是严格要求缓存+数据库必须一致性的话，缓存可以稍微的跟数据库偶尔有不一致的情况，最好不要做这个方案，读请求和写请求串行化，串到一个内存队列里去，这样就可以保证一定不会出现不一致的情况

串行化之后，就会导致系统的吞吐量会大幅度的降低，用比正常情况下多几倍的机器去支撑线上的一个请求。

# Spring
## Spring 框架
Spring 是一种轻量级开发框架，旨在提高开发人员的开发效率以及系统的可维护性。Spring 官网：https://spring.io/。

我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发。这些模块是：核心容器、数据访问/集成,、Web、AOP（面向切面编程）、工具、消息和测试模块。比如：Core Container 中的 Core 组件是Spring 所有组件的核心，Beans 组件和 Context 组件是实现IOC和依赖注入的基础，AOP组件用来实现面向切面编程。

Spring 官网列出的 Spring 的 6 个特征:

核心技术 ：依赖注入(DI)，AOP，事件(events)，资源，i18n，验证，数据绑定，类型转换，SpEL。
测试 ：模拟对象，TestContext框架，Spring MVC 测试，WebTestClient。
数据访问 ：事务，DAO支持，JDBC，ORM，编组XML。
Web支持 : Spring MVC和Spring WebFlux Web框架。
集成 ：远程处理，JMS，JCA，JMX，电子邮件，任务，调度，缓存。
语言 ：Kotlin，Groovy，动态语言。

## Spring模块
Spring Core： 基础,可以说 Spring 其他所有的功能都需要依赖于该类库。主要提供 IoC 依赖注入功能。

Spring Aspects ： 该模块为与AspectJ的集成提供支持。

Spring AOP ：提供了面向切面的编程实现。

Spring JDBC : Java数据库连接。

Spring JMS ：Java消息服务。

Spring ORM : 用于支持Hibernate等ORM工具。

Spring Web : 为创建Web应用程序提供支持。

Spring Test : 提供了对 JUnit 和 TestNG 测试的支持。

## 设计模式
工厂设计模式 : Spring使用工厂模式通过 BeanFactory、ApplicationContext 创建 bean 对象。

代理设计模式 : Spring AOP 功能的实现。

单例设计模式 : Spring 中的 Bean 默认都是单例的。

模板方法模式 : Spring 中 jdbcTemplate、hibernateTemplate 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。

包装器设计模式 : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。

观察者模式: Spring 事件驱动模型就是观察者模式很经典的一个应用。

适配器模式 :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配Controller。


## IoC 和 AOP
### IoC
初始化过程：XML(读取)--> Resource(解析) --> BeanDefinition(注册) --> BeanFactory

IoC（Inverse of Control:控制反转）是一种设计思想，将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。IoC 容器是 Spring 用来实现 IoC 的载体， IoC 容器实际上就是个Map（key，value）,Map 中存放的是各种对象。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。 在实际项目中一个 Service 类可能有几百甚至上千个类作为它的底层，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IoC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。

### AOP
AOP(Aspect-Oriented Programming:面向切面编程)能够将那些与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可拓展性和可维护性。

Spring AOP就是基于动态代理的，如果要代理的对象，实现了某个接口，那么Spring AOP会使用JDK Proxy，去创建代理对象;而对于没有实现接口的对象，Spring AOP会使用Cglib ，这时候Spring AOP会使用 Cglib 生成一个被代理对象的子类来作为代理

#### JDK和CGLIB动态代理区别（https://blog.csdn.net/yhl_jxy/article/details/80635012
1、JDK动态代理
利用拦截器(拦截器必须实现InvocationHanlder)加上反射机制生成一个实现代理接口的匿名类，

在调用具体方法前调用InvokeHandler来处理。

2、CGLIB动态代理
利用ASM开源包，对代理对象类的class文件加载进来，通过修改其字节码生成子类来处理。


#### Spring AOP 和 AspectJ AOP 有什么区别？
Spring AOP 属于运行时增强，而 AspectJ 是编译时增强。 Spring AOP 基于代理(Proxying)，而 AspectJ 基于字节码操作(Bytecode Manipulation)。

Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。AspectJ 相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单，

如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比Spring AOP 快很多。

## bean 的作用域
### singleton : 
唯一 bean 实例，Spring 中的 bean 默认都是单例的。当一个 bean 的作用域为 singleton，那么Spring IoC容器中只会存在一个共享的 bean 实例，并且所有对 bean 的请求，只要 id 与该 bean 定义相匹配，则只会返回bean的同一实例。 singleton 是单例类型(对应于单例模式)，就是在创建起容器时就同时自动创建了一个bean的对象，不管你是否使用，但我们可以指定Bean节点的 lazy-init=”true” 来延迟初始化bean，这时候，只有在第一次获取bean时才会初始化bean，即第一次请求该bean时才初始化。 每次获取到的对象都是同一个对象。注意，singleton 作用域是Spring中的缺省作用域。

Spring 容器可以管理 singleton 作用域下 bean 的生命周期，在此作用域下，Spring 能够精确地知道bean何时被创建，何时初始化完成，以及何时被销毁。而对于 prototype 作用域的bean，Spring只负责创建，当容器创建了 bean 的实例后，bean 的实例就交给了客户端的代码管理，Spring容器将不再跟踪其生命周期，并且不会管理那些被配置成prototype作用域的bean的生命周期。

### prototype : 
每次请求都会创建一个新的 bean 实例。当一个bean的作用域为 prototype，表示一个 bean 定义对应多个对象实例。 prototype 作用域的 bean 会导致在每次对该 bean 请求（将其注入到另一个 bean 中，或者以程序的方式调用容器的 getBean() 方法**）时都会创建一个新的 bean 实例。prototype 是原型类型，它在我们创建容器的时候并没有实例化，而是当我们获取bean的时候才会去创建一个对象，而且我们每次获取到的对象都不是同一个对象。根据经验，对有状态的 bean 应该使用 prototype 作用域，而对无状态的 bean 则应该使用 singleton 作用域。

如果 bean 的 scope 设为prototype时，当容器关闭时，destroy 方法不会被调用。对于 prototype 作用域的 bean，有一点非常重要，那就是 Spring不能对一个 prototype bean 的整个生命周期负责：容器在初始化、配置、装饰或者是装配完一个prototype实例后，将它交给客户端，随后就对该prototype实例不闻不问了。 不管何种作用域，容器都会调用所有对象的初始化生命周期回调方法。但对prototype而言，任何配置好的析构生命周期回调方法都将不会被调用。清除prototype作用域的对象并释放任何prototype bean所持有的昂贵资源，都是客户端代码的职责（让Spring容器释放被prototype作用域bean占用资源的一种可行方式是，通过使用bean的后置处理器，该处理器持有要被清除的bean的引用）。谈及prototype作用域的bean时，在某些方面你可以将Spring容器的角色看作是Java new操作的替代者，任何迟于该时间点的生命周期事宜都得交由客户端来处理。

### request : 
每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有效， 当请求结束后，该对象的生命周期即告结束。

### session : 
每一次HTTP请求都会产生一个新的 bean，该bean仅在当前 HTTP session 内有效。session只适用于Web程序，session 作用域表示该针对每一次 HTTP 请求都会产生一个新的 bean，同时该 bean 仅在当前 HTTP session 内有效.与request作用域一样，可以根据需要放心的更改所创建实例的内部状态，而别的 HTTP session 中根据 userPreferences 创建的实例，将不会看到这些特定于某个 HTTP session 的状态变化。当HTTP session最终被废弃的时候，在该HTTP session作用域内的bean也会被废弃掉。

global-session： 全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring5已经没有了。Portlet是能够生成语义代码(例如：HTML)片段的小型Java Web插件。它们基于portlet容器，可以像servlet一样处理HTTP请求。但是，与 servlet 不同，每个 portlet 都有不同的会话

## bean的生命周期（https://www.cnblogs.com/zrtqsk/p/3735273.html
Bean容器找到配置文件中 Spring Bean 的定义。

Bean容器利用Java Reflection API创建一个Bean的实例。

如果涉及到一些属性值 利用set方法设置一些属性值。

如果Bean实现了BeanNameAware接口，调用setBeanName()方法，传入Bean的名字。

如果Bean实现了BeanClassLoaderAware接口，调用setBeanClassLoader()方法，传入ClassLoader对象的实例。

如果Bean实现了BeanFactoryAware接口，调用setBeanClassLoader()方法，传入ClassLoader对象的实例。

与上面的类似，如果实现了其他*Aware接口，就调用相应的方法。

如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行postProcessBeforeInitialization()方法

如果Bean实现了InitializingBean接口，执行afterPropertiesSet()方法。

如果Bean在配置文件中的定义包含init-method属性，执行指定的方法。

如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行postProcessAfterInitialization()方法

当要销毁Bean的时候，如果Bean实现了DisposableBean接口，执行destroy()方法。

当要销毁Bean的时候，如果Bean在配置文件中的定义包含destroy-method属性，执行指定的方法。

## Spring MVC
MVC 是一种设计模式,Spring MVC 是一款很优秀的 MVC 框架。Spring MVC 可以帮助我们进行更简洁的Web层的开发，并且它天生与 Spring 框架集成。Spring MVC 下我们一般把后端项目分为 Service层（处理业务）、Dao层（数据库操作）、Entity层（实体类）、Controller层(控制层，返回数据给前台页面)。

### 原理（过程）
客户端（浏览器）发送请求，直接请求到 DispatcherServlet。

DispatcherServlet 根据请求信息调用 HandlerMapping，解析请求对应的 Handler。

解析到对应的 Handler（也就是我们平常说的 Controller 控制器）后，开始由 HandlerAdapter 适配器处理。

HandlerAdapter 会根据 Handler 来调用真正的处理器开处理请求，并处理相应的业务逻辑。

处理器处理完业务后，会返回一个 ModelAndView 对象，Model 是返回的数据对象，View 是个逻辑上的 View。

ViewResolver 会根据逻辑 View 查找实际的 View。

DispaterServlet 把返回的 Model 传给 View（视图渲染）。

把 View 返回给请求者（浏览器）



## Spring事务
1，编程式事务，在代码中硬编码。(不推荐使用)

2，声明式事务，在配置文件中配置（推荐使用）
声明式事务又分为两种：基于XML的声明式事务，基于注解的声明式事务

### Spring 事务中的隔离级别
TransactionDefinition.ISOLATION_DEFAULT: 使用后端数据库默认的隔离级别，Mysql 默认采用的 REPEATABLE_READ隔离级别 Oracle 默认采用的 READ_COMMITTED隔离级别.

TransactionDefinition.ISOLATION_READ_UNCOMMITTED: 最低的隔离级别，允许读取尚未提交的数据变更，可能会导致脏读、幻读或不可重复读

TransactionDefinition.ISOLATION_READ_COMMITTED: 允许读取并发事务已经提交的数据，可以阻止脏读，但是幻读或不可重复读仍有可能发生

TransactionDefinition.ISOLATION_REPEATABLE_READ: 对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，可以阻止脏读和不可重复读，但幻读仍有可能发生。

TransactionDefinition.ISOLATION_SERIALIZABLE: 最高的隔离级别，完全服从ACID的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，该级别可以防止脏读、不可重复读以及幻读。但是这将严重影响程序的性能。通常情况下也不会用到该级别。

### Spring 事务中哪几种事务传播行为
#### 支持当前事务的情况：

TransactionDefinition.PROPAGATION_REQUIRED： 如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。

TransactionDefinition.PROPAGATION_SUPPORTS： 如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务的方式继续运行。

TransactionDefinition.PROPAGATION_MANDATORY： 如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。（mandatory：强制性）

#### 不支持当前事务的情况：

TransactionDefinition.PROPAGATION_REQUIRES_NEW： 创建一个新的事务，如果当前存在事务，则把当前事务挂起。

TransactionDefinition.PROPAGATION_NOT_SUPPORTED： 以非事务方式运行，如果当前存在事务，则把当前事务挂起。

TransactionDefinition.PROPAGATION_NEVER： 以非事务方式运行，如果当前存在事务，则抛出异常。

#### 其他情况：

TransactionDefinition.PROPAGATION_NESTED： 如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；如果当前没有事务，则该取值等价于TransactionDefinition.PROPAGATION_REQUIRED。

## @Component 和 @Bean 的区别是什么？
1，作用对象不同: @Component 注解作用于类，而@Bean注解作用于方法。

2，@Component通常是通过类路径扫描来自动侦测以及自动装配到Spring容器中（我们可以使用 @ComponentScan 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。@Bean 注解通常是我们在标有该注解的方法中定义产生这个 bean,@Bean告诉了Spring这是某个类的示例，当我需要用它的时候还给我。

3，@Bean 注解比 Component 注解的自定义性更强，而且很多地方我们只能通过 @Bean 注解来注册bean。比如当我们引用第三方库中的类需要装配到 Spring容器时，则只能通过 @Bean来实现。

## 将一个类声明为Spring的 bean 的注解有哪些?
我们一般使用 @Autowired 注解自动装配 bean，要想把类标识成可用于 @Autowired 注解自动装配的 bean 的类,采用以下注解可实现：

@Component ：通用的注解，可标注任意类为 Spring 组件。如果一个Bean不知道属于哪个层，可以使用@Component 注解标注。

@Repository : 对应持久层即 Dao 层，主要用于数据库相关操作。

@Service : 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao层。

@Controller : 对应 Spring MVC 控制层，主要用户接受用户请求并调用 Service 层返回数据给前端页面。

# 消息队列
## 应用场景/使用消息队列的好处
### 通过异步处理提高系统性能
在不使用消息队列服务器的时候，用户的请求数据直接写入数据库，在高并发的情况下数据库压力剧增，使得响应速度变慢。但是在使用消息队列之后，用户的请求数据发送给消息队列之后立即 返回，再由消息队列的消费者进程从消息队列中获取数据，异步写入数据库。由于消息队列服务器处理速度快于数据库（消息队列也比数据库有更好的伸缩性），因此响应速度得到大幅改善。

消息队列具有很好的削峰作用的功能——即通过异步处理，将短时间高并发产生的事务消息存储在消息队列中，从而削平高峰期的并发事务。 举例：在电子商务一些秒杀、促销活动中，合理使用消息队列可以有效抵御促销活动刚开始大量订单涌入对系统的冲击。

### 降低系统耦合性
 消息队列使利用发布-订阅模式工作，消息发送者（生产者）发布消息，一个或多个消息接受者（消费者）订阅消息。 消息发送者（生产者）和消息接受者（消费者）之间没有直接耦合，消息发送者将消息发送至分布式消息队列即结束对消息的处理，消息接受者从分布式消息队列获取该消息后进行后续处理，并不需要知道该消息从何而来。对新增业务，只要对该类消息感兴趣，即可订阅该消息，对原有系统和业务没有任何影响，从而实现网站业务的可扩展性设计。

## 使用消息队列会带来什么问题
 系统可用性降低： 系统可用性在某种程度上降低，为什么这样说呢？在加入MQ之前，你不用考虑消息丢失或者说MQ挂掉等等的情况，但是，引入MQ之后你就需要去考虑了！

系统复杂性提高： 加入MQ之后，你需要保证消息没有被重复消费、处理消息丢失的情况、保证消息传递的顺序性等等问题！

一致性问题：消息队列可以实现异步，消息队列带来的异步确实可以提高系统响应速度。但是，万一消息的真正消费者并没有正确消费消息怎么办？这样就会导致数据不一致的情况了!

## mq积压
先修复 consumer 的问题，确保其恢复消费速度，然后将现有 consumer 都停掉。
新建一个 topic，partition 是原来的 10 倍，临时建立好原先 10 倍的 queue 数量。
然后写一个临时的分发数据的 consumer 程序，这个程序部署上去消费积压的数据，消费之后不做耗时的处理，直接均匀轮询写入临时建立好的 10 倍数量的 queue。
接着临时征用 10 倍的机器来部署 consumer，每一批 consumer 消费一个临时 queue 的数据。这种做法相当于是临时将 queue 资源和 consumer 资源扩大 10 倍，以正常的 10 倍速度来消费数据。
等快速消费完积压数据之后，得恢复原先部署的架构，重新用原先的 consumer 机器来消费消息。

## mq过期
假设你用的是 RabbitMQ，RabbtiMQ 是可以设置过期时间的，也就是 TTL。如果消息在 queue 中积压超过一定的时间就会被 RabbitMQ 给清理掉，这个数据就没了。那这就是第二个坑了。这就不是说数据会大量积压在 mq 里，而是大量的数据会直接搞丢。

这个情况下，就不是说要增加 consumer 消费积压的消息，因为实际上没啥积压，而是丢了大量的消息。我们可以采取一个方案，就是批量重导，这个我们之前线上也有类似的场景干过。就是大量积压的时候，我们当时就直接丢弃数据了，然后等过了高峰期以后，比如大家一起喝咖啡熬夜到晚上12点以后，用户都睡觉了。这个时候我们就开始写程序，将丢失的那批数据，写个临时程序，一点一点的查出来，然后重新灌入 mq 里面去，把白天丢的数据给他补回来。也只能是这样了。

假设 1 万个订单积压在 mq 里面，没有处理，其中 1000 个订单都丢了，你只能手动写程序把那 1000 个订单给查出来，手动发到 mq 里去再补一次。

## 高可用
### rabbitmq的高可用模式：镜像集群模式
跟普通集群模式不一样的是，你创建的queue，无论元数据还是queue里的消息都会存在于多个实例上，然后每次你写消息到queue的时候，都会自动把消息到多个实例的queue里进行消息同步。这样的话，好处在于，你任何一个机器宕机了，没事儿，别的机器都可以用。坏处在于，第一，这个性能开销也太大了吧，消息同步所有机器，导致网络带宽压力和消耗很重！第二，这么玩儿，就没有扩展性可言了，如果某个queue负载很重，你加机器，新增的机器也包含了这个queue的所有数据，并没有办法线性扩展你的queue那么怎么开启这个镜像集群模式呢？我这里简单说一下，避免面试人家问你你不知道，其实很简单rabbitmq有很好的管理控制台，就是在后台新增一个策略，这个策略是镜像集群模式的策略，指定的时候可以要求数据同步到所有节点的，也可以要求就同步到指定数量的节点，然后你再次创建queue的时候，应用这个策略，就会自动将数据同步到其他的节点上去了。

### kafka的高可用性
kafka一个最基本的架构认识：多个broker组成，每个broker是一个节点；你创建一个topic，这个topic可以划分为多个partition，每个partition可以存在于不同的broker上，每个partition就放一部分数据。这就是天然的分布式消息队列，就是说一个topic的数据，是分散放在多个机器上的，每个机器就放一部分数据。

实际上rabbitmq之类的，并不是分布式消息队列，他就是传统的消息队列，只不过提供了一些集群、HA的机制而已，因为无论怎么玩儿，rabbitmq一个queue的数据都是放在一个节点里的，镜像集群下，也是每个节点都放这个queue的完整数据。

kafka 0.8以后，提供了HA机制，就是replica副本机制。每个partition的数据都会同步到其他机器上，形成自己的多个replica副本。然后所有replica会选举一个leader出来，那么生产和消费都跟这个leader打交道，然后其他replica就是follower。写的时候，leader会负责把数据同步到所有follower上去，读的时候就直接读leader上数据即可。只能读写leader？很简单，要是你可以随意读写每个follower，那么就要care数据一致性的问题，系统复杂度太高，很容易出问题。kafka会均匀的将一个partition的所有replica分布在不同的机器上，这样才可以提高容错性。

这么搞，就有所谓的高可用性了，因为如果某个broker宕机了，没事儿，那个broker上面的partition在其他机器上都有副本的，如果这上面有某个partition的leader，那么此时会重新选举一个新的leader出来，大家继续读写那个新的leader即可。这就有所谓的高可用性了。写数据的时候，生产者就写leader，然后leader将数据落地写本地磁盘，接着其他follower自己主动从leader来pull数据。一旦所有follower同步好数据了，就会发送ack给leader，leader收到所有follower的ack之后，就会返回写成功的消息给生产者。（当然，这只是其中一种模式，还可以适当调整这个行为）消费的时候，只会从leader去读，但是只有一个消息已经被所有follower都同步成功返回ack的时候，这个消息才会被消费者读到。


## RabbitMQ 简介
RabbitMQ 是采用 Erlang 语言实现 AMQP(Advanced Message Queuing Protocol，高级消息队列协议）的消息中间件，它最初起源于金融系统，用于在分布式系统中存储转发消息。

RabbitMQ 发展到今天，被越来越多的人认可，这和它在易用性、扩展性、可靠性和高可用性等方面的卓著表现是分不开的。RabbitMQ 的具体特点可以概括为以下几点：

可靠性： RabbitMQ使用一些机制来保证消息的可靠性，如持久化、传输确认及发布确认等。

灵活的路由： 在消息进入队列之前，通过交换器来路由消息。对于典型的路由功能，RabbitMQ 己经提供了一些内置的交换器来实现。针对更复杂的路由功能，可以将多个交换器绑定在一起，也可以通过插件机制来实现自己的交换器。

扩展性： 多个RabbitMQ节点可以组成一个集群，也可以根据实际业务情况动态地扩展集群中节点。

高可用性： 队列可以在集群中的机器上设置镜像，使得在部分节点出现问题的情况下队列仍然可用。

支持多种协议： RabbitMQ 除了原生支持 AMQP 协议，还支持 STOMP、MQTT 等多种消息中间件协议。

多语言客户端： RabbitMQ几乎支持所有常用语言，比如 Java、Python、Ruby、PHP、C#、JavaScript等。

易用的管理界面： RabbitMQ提供了一个易用的用户界面，使得用户可以监控和管理消息、集群中的节点等。在安装 RabbitMQ 的时候会介绍到，安装好 RabbitMQ 就自带管理界面。

插件机制： RabbitMQ 提供了许多插件，以实现从多方面进行扩展，当然也可以编写自己的插件。

### RabbitMQ 会始终记录以下四种类型的内部元数据：

队列元数据：包括队列名称和它们的属性，比如是否可持久化，是否自动删除。

交换器元数据：交换器名称、类型、属性。

绑定元数据：内部是一张表格记录如何将消息路由到队列。

vhost 元数据：为 vhost 内部的队列、交换器、绑定提供命名空间和安全属性。

### 队列模式(https://www.rabbitmq.com/getstarted.html
1，简单队列模式：一个生产者对应一个消费者。

2，work模式：一个生产者对应多个消费者，但是只能有一个消费者获得消息。应用场景：效率高的消费者消费消息多。可以用来进行负载均衡。

3，发布订阅模式：一个消费者将消息首先发送到交换器，交换器绑定到多个队列，然后被监听该队列的消费者所接收并消费。应用场景：比如一个商城系统需要在管理员上传商品新的图片时，前台系统必须更新图片，日志系统必须记录相应的日志，那么就可以将两个队列绑定到图片上传交换器上，一个用于前台系统更新图片，另一个用于日志系统记录日志。


4，路由模式：生产者将消息发送到direct交换器，在绑定队列和交换器的时候有一个路由key，生产者发送的消息会指定一个路由key，那么消息只会发送到相应key相同的队列，接着监听该队列的消费者消费消息。也就是让消费者有选择性的接收消息。应用场景：利用消费者能够有选择性的接收消息的特性，比如我们商城系统的后台管理系统对于商品进行修改、删除、新增操作都需要更新前台系统的界面展示，而查询操作确不需要，那么这两个队列分开接收消息就比较好。

5，主题模式：路由模式是根据路由key进行完整的匹配（完全相等才发送消息），这里的通配符模式通俗的来讲就是模糊匹配。

6,RPC


## AMQP核心概念
### Producer(生产者) 和 Consumer(消费者)
Producer(生产者) :生产消息的一方（邮件投递者）
Consumer(消费者) :消费消息的一方（邮件收件人）
消息一般由 2 部分组成：消息头（或者说是标签 Label）和 消息体。消息体也可以称为 payLoad ,消息体是不透明的，而消息头则由一系列的可选属性组成，这些属性包括 routing-key（路由键）、priority（相对于其他消息的优先权）、delivery-mode（指出该消息可能需要持久性存储）等。生产者把消息交由 MQ 后，MQ 会根据消息头把消息发送给感兴趣的 Consumer(消费者)。

### Exchange(交换器)
在 MQ 中，消息并不是直接被投递到 Queue(消息队列) 中的，中间还必须经过 Exchange(交换器) 这一层，Exchange(交换器) 会把我们的消息分配到对应的 Queue(消息队列) 中。

Exchange(交换器) 用来接收生产者发送的消息并将这些消息路由给服务器中的队列中，如果路由不到，或许会返回给 Producer(生产者) ，或许会被直接丢弃掉 。这里可以将RabbitMQ中的交换器看作一个简单的实体。

RabbitMQ 的 Exchange(交换器) 有4种类型，不同的类型对应着不同的路由策略：direct(默认)，fanout, topic, 和 headers，不同类型的Exchange转发消息的策略有所区别。

生产者将消息发送给交换器时，需要一个RoutingKey,当 BindingKey 和 RoutingKey 相匹配时，消息会被路由到对应的队列中。在绑定多个队列到同一个交换器的时候，这些绑定允许使用相同的 BindingKey。BindingKey 并不是在所有的情况下都生效，它依赖于交换器类型，比如fanout类型的交换器就会无视，而是将消息路由到所有绑定到该交换器的队列中。

### Queue(消息队列)
Queue(消息队列) 用来保存消息直到发送给消费者。它是消息的容器，也是消息的终点。一个消息可投入一个或多个队列。消息一直在队列里面，等待消费者连接到这个队列将其取走。

MQ 中消息只能存储在 队列 中，这一点和 Kafka 这种消息中间件相反。Kafka 将消息存储在 topic（主题） 这个逻辑层面，而相对应的队列逻辑只是topic实际存储文件中的位移标识。 RabbitMQ 的生产者生产消息并最终投递到队列中，消费者可以从队列中获取消息并消费。

多个消费者可以订阅同一个队列，这时队列中的消息会被平均分摊（Round-Robin，即轮询）给多个消费者进行处理，而不是每个消费者都收到所有的消息并处理，这样避免的消息被重复消费。

MQ 不支持队列层面的广播消费,如果有广播消费的需求，需要在其上进行二次开发,这样会很麻烦，不建议这样做。

### Broker（消息中间件的服务节点）
接受客户端的连接，实现AMQP实体服务。对于 RabbitMQ 来说，一个 RabbitMQ Broker 可以简单地看作一个 RabbitMQ 服务节点，或者RabbitMQ服务实例。大多数情况下也可以将一个 RabbitMQ Broker 看作一台 RabbitMQ 服务器。

### vhost
虚拟地址（一般用于隔离项目），用于进行逻辑隔离，最上层的消息路由。一个Virtual Host里面可以有若干个Exchange和Queue，同一个Virtual Host里面不能有相同名称的Exchange或Queue。一个 broker 里可以开设多个 vhost，用作不同用户的权限分离。

### Connection：
应用程序与Broker的网络连接。Producer 和 Consumer 通过 TCP 连接到MQ。断开连接的操作只会在client端进行，Broker不会断开连接，除非出现网络故障或broker服务出现问题。

### Channel：
网络信道，几乎所有的操作都在Channel中进行，Channel是进行消息读写的通道。客户端可以建立多个Channel，每个Channel代表一个会话任务。它建立在上述的 TCP 连接中，数据流动都是在 Channel 中进行的。如果客户端每次和Broker通信都需要建议一条连接，在并大量连接并发的情况下建立TCP Connection的开销将是巨大的，效率也较低。于是，
AMQP引入了channel的概念，channel是connection之上应用层建立的逻辑连接，Broker在实现中可创建单独的thread/协程来实现channel的并发，AMQP method
包含了channel id帮助客户端和message broker识别channel，所以channel之间是完全隔离的。Channel作为轻量级的Connection极大减少了操作系统建立
TCP connection的开销。

### Exchange Types(交换器类型)
#### fanout
fanout 类型的Exchange路由规则非常简单，它会把所有发送到该Exchange的消息路由到所有与它绑定的Queue中，不需要做任何判断操作，所以 fanout 类型是所有的交换机类型里面速度最快的。fanout 类型常用来广播消息。

#### direct
direct 类型的Exchange路由规则也很简单，它会把消息路由到那些 Bindingkey 与 RoutingKey 完全匹配的 Queue 中。
direct 类型常用在处理有优先级的任务，根据任务的优先级把消息发送到对应的队列，这样可以指派更多的资源去处理高优先级的队列。

#### topic
前面讲到direct类型的交换器路由规则是完全匹配 BindingKey 和 RoutingKey ，但是这种严格的匹配方式在很多情况下不能满足实际业务的需求。topic类型的交换器在匹配规则上进行了扩展，它与 direct 类型的交换器相似，也是将消息路由到 BindingKey 和 RoutingKey 相匹配的队列中，但这里的匹配规则有些不同，它约定：

RoutingKey 为一个点号“．”分隔的字符串（被点号“．”分隔开的每一段独立的字符串称为一个单词），如 “com.rabbitmq.client”、“java.util.concurrent”、“com.hidden.client”;
BindingKey 和 RoutingKey 一样也是点号“．”分隔的字符串；
BindingKey 中可以存在两种特殊字符串“*”和“#”，用于做模糊匹配，其中“.”用于匹配一个单词，“#”用于匹配多个单词(可以是零个)。

#### headers(不推荐)
headers 类型的交换器不依赖于路由键的匹配规则来路由消息，而是根据发送的消息内容中的 headers 属性进行匹配。在绑定队列和交换器时制定一组键值对，当发送消息到交换器时，RabbitMQ会获取到该消息的 headers（也是一个键值对的形式)'对比其中的键值对是否完全匹配队列和交换器绑定时指定的键值对，如果完全匹配则消息会路由到该队列，否则不会路由到该队列。headers 类型的交换器性能会很差，而且也不实用，基本上不会看到它的存在。

## 消息如何流转
生产者发送消息到RabbitMQ（指定某个Exchange和Routing key）；
Message发送到某个Exchange；
根据路由规则，Exchange将消息发送到某一个或几个Message Queue；
由监听相应Message Queue的消费者处理消息。

## Confirm消息确认实现
消息确认，是指生产者投递消息后，如果Broker收到消息，则会给生产者一个应答。生产者收到应答，来确认消息是否正常的发送到Broker。

如何实现Confirm确认消息
在channel上开启确认模式：channel.confirmSelect()
在channel上添加监听：addConfirmListener，监听成功和失败的返回结果，根据具体的结果对消息进行重新发送、或记录日志等后续处理
重写addConfirmListener两个方法，handleNack 失败处理和handleAck成功处理

### 原理
生产者将信道设置成confirm模式，一旦信道进入confirm模式，所有在该信道上面发布的消息都会被指派一个唯一的ID(从1开始)，一旦消息被投递到所有匹配的队列之后，broker就会发送一个确认给生产者（包含消息的唯一ID）,这就使得生产者知道消息已经正确到达目的队列了，如果消息和队列是可持久化的，那么确认消息会将消息写入磁盘之后发出，broker回传给生产者的确认消息中deliver-tag域包含了确认消息的序列号，此外broker也可以设置basic.ack的multiple域，表示到这个序列号之前的所有消息都已经得到了处理。

confirm模式最大的好处在于他是异步的，一旦发布一条消息，生产者应用程序就可以在等信道返回确认的同时继续发送下一条消息，当消息最终得到确认之后，生产者应用便可以通过回调方法来处理该确认消息，如果RabbitMQ因为自身内部错误导致消息丢失，就会发送一条nack消息，生产者应用程序同样可以在回调方法中处理该nack消息。

在channel 被设置成 confirm 模式之后，所有被 publish 的后续消息都将被 confirm（即 ack） 或者被nack一次。但是没有对消息被 confirm 的快慢做任何保证，并且同一条消息不会既被 confirm又被nack 。


## 消息可靠性（不丢失）
1. Publishing可靠性，生产者设置confirm服务端确认机制，确认服务端成功接收到生产者消息。 

2. 消息Routing可靠性，生产者设置Publish mandatory，确认消息路由到queue。

3. Consuming可靠性，消费者设置手工Ack，服务端在收到消息Ack后才清除本地消息。

# RockerMQ
## 消息丢失的问题
当你系统需要保证百分百消息不丢失，你可以使用生产者每发送一个消息，Broker 同步返回一个消息发送成功的反馈消息
即每发送一个消息，同步落盘后才返回生产者消息发送成功，这样只要生产者得到了消息发送生成的返回，事后除了硬盘损坏，都可以保证不会消息丢失
但是这同时引入了一个问题，同步落盘怎么才能快？

## 同步落盘怎么才能快
使用 FileChannel + Direct Buffer 池，使用堆外内存，加快内存拷贝
使用数据和索引分离，当消息需要写入时，使用 commitlog 文件顺序写，当需要定位某个消息时，查询index 文件来定位，从而减少文件IO随机读写的性能损耗

## 定时消息的实现
实际 RocketMQ 没有实现任意精度的定时消息，它只支持某些特定的时间精度的定时消息

实现定时消息的原理是：创建特定时间精度的 MessageQueue，例如生产者需要定时1s之后被消费者消费，你只需要将此消息发送到特定的 Topic，例如：MessageQueue-1 表示这个 MessageQueue 里面的消息都会延迟一秒被消费，然后 Broker 会在 1s 后发送到消费者消费此消息，使用 newSingleThreadScheduledExecutor 实现

## 顺序消息的实现
与定时消息同原理，生产者生产消息时指定特定的 MessageQueue ，消费者消费消息时，消费特定的 MessageQueue，其实单机版的消息中心在一个 MessageQueue 就天然支持了顺序消息
注意：同一个 MessageQueue 保证里面的消息是顺序消费的前提是：消费者是串行的消费该 MessageQueue，因为就算 MessageQueue 是顺序的，但是当并行消费时，还是会有顺序问题，但是串行消费也同时引入了两个问题：
引入锁来实现串行;
前一个消费阻塞时后面都会被阻塞

## 消息重复发送的避免
RocketMQ 会出现消息重复发送的问题，因为在网络延迟的情况下，这种问题不可避免的发生，如果非要实现消息不可重复发送，那基本太难，因为网络环境无法预知，还会使程序复杂度加大，因此默认允许消息重复发送;

RocketMQ 让使用者在消费者端去解决该问题，即需要消费者端在消费消息时支持幂等性的去消费消息

最简单的解决方案是每条消费记录有个消费状态字段，根据这个消费状态字段来是否消费或者使用一个集中式的表，来存储所有消息的消费状态，从而避免重复消费
具体实现可以查询关于消息幂等消费的解决方案

### 幂等性概念及业界主流解决方案
#### 概念
可以参考数据库乐观锁机制，比如执行一条更新库存的 SQL 语句，在并发场景，为了性能和数据可靠性，会在更新时加上查询时的版本，并且更新这个版本信息。可能你要对一个事情进行操作，这个操作可能会执行成百上千次，但是操作结果都是相同的，这就是幂等性。

#### 解决方案：
1，唯一 ID 

解决方案 ：根据 ID 进行分库分表，对 id 进行算法路由，落到一个具体的数据库，然后当这个 id 第二次来又会落到这个数据库，这时候就像我单库时的查重一样了。利用算法路由把单库的幂等变成多库的幂等，分摊数据流量压力，提高性能。

2，利用 redis 的原子性去实现

使用 redis 的原子性去实现需要考虑两个点：
一是  是否 要进行数据落库，如果落库的话，关键解决的问题是数据库和缓存如何做到原子性？
数据库与缓存进行同步肯定要进行写操作，到底先写 redis 还是先写数据库，这是个问题，涉及到缓存更新与淘汰的问题
二是如果不落库，那么都存储到缓存中，如何设置定时同步的策略？
不入库的话，可以使用双重缓存等策略，保障一个消息副本，具体同步可以使用类似 databus 这种同步工具。



# 几款MQ对比：
## rabbitMQ
基于erlang开发

是采用Erlang语言实现的AMQP协议的消息中间件，最初起源于金融系统，用于在分布式系统中存储转发消息。RabbitMQ发展到今天，被越来越多的人认可，这和它在可靠性、可用性、扩展性、功能丰富等方面的卓越表现是分不开的。

优点：

由于erlang语言的特性，mq性能较好，高并发；
健壮、稳定、易用、跨平台、支持多种语言、文档齐全；
有消息确认机制和持久化机制，可靠性高；
高度可定制的路由；
管理界面较丰富，在互联网公司也有较大规模的应用；
社区活跃度高；

缺点：

尽管结合erlang语言本身的并发优势，性能较好，但是不利于做二次开发和维护；
实现了代理架构，意味着消息在发送到客户端之前可以在中央节点上排队。此特性使得RabbitMQ易于使用和部署，但是使得其运行速度较慢，因为中央节点增加了延迟，消息封装后也比较大；
需要学习比较复杂的接口和协议，学习和维护成本较高；

## activeMQ
基于java开发

是Apache出品的、采用Java语言编写的完全基于JMS1.1规范的面向消息的中间件，为应用程序提供高效的、可扩展的、稳定的和安全的企业级消息通信。不过由于历史原因包袱太重，目前市场份额没有后面三种消息中间件多，其最新架构被命名为Apollo,(京东的消息中间件就是基于activeMQ开发的)
优点：

跨平台(JAVA编写与平台无关有，ActiveMQ几乎可以运行在任何的JVM上)

可以用JDBC：可以将数据持久化到数据库

支持JMS ：支持JMS的统一接口;

支持自动重连；

有安全机制：支持基于shiro，jaas等多种安全配置机制，可以对Queue/Topic进行认证和授权

监控完善：拥有完善的监控，包括Web Console，JMX，Shell命令行，Jolokia的REST API；

界面友善：提供的Web Console可以满足大部分情况，还有很多第三方的组件可以使用，如hawtio；

缺点：

社区活跃度不及RabbitMQ高；
会出莫名其妙的问题，会丢失消息；
不适合用于上千个队列的应用场景；

## rocketMQ
基于java开发（阿里消息中间件）

是阿里开源的消息中间件，目前已经捐献个Apache基金会，它是由Java语言开发的，具备高吞吐量、高可用性、适合大规模分布式系统应用等特点，经历过双11的洗礼，实力不容小觑。
优点：

单机支持 1 万以上持久化队列
RocketMQ 的所有消息都是持久化的，先写入系统 pagecache(页高速缓冲存储器)，然后刷盘，可以保证内存与磁盘都有一份数据，访问时，直接从内存读取。
模型简单，接口易用（JMS 的接口很多场合并不太实用）
性能非常好，可以大量堆积消息在broker(集群中包含一个或多个服务器，这些服务器被称为broker)中；
支持多种消费，包括集群消费、广播消费等。
各个环节分布式扩展设计，主从HA(高可用性集群)；
开发度较活跃，版本更新很快。

缺点：

支持的客户端语言不多，目前是java及c++，其中c++不成熟；
RocketMQ社区关注度及成熟度也不及前两者；
没有web管理界面，提供了一个CLI(命令行界面)管理工具带来查询、管理和诊断各种问题；
没有在 mq 核心中去实现JMS等接口；

### pull和push
在rocketmq里，consumer被分为2类：MQPullConsumer和MQPushConsumer，其实本质都是拉模式（pull），即consumer轮询从broker拉取消息。

区别是：

push方式里，consumer把轮询过程封装了，并注册MessageListener监听器，取到消息后，唤醒MessageListener的consumeMessage()来消费，对用户而言，感觉消息是被推送过来的。

pull方式里，取消息的过程需要用户自己写，首先通过打算消费的Topic拿到MessageQueue的集合，遍历MessageQueue集合，然后针对每个MessageQueue批量取消息，一次取完后，记录该队列下一次要取的开始offset，直到取完了，再换另一个MessageQueue。

## kafka/jafka
基于Scala和Java开发

起初是由LinkedIn公司采用Scala语言开发的一个分布式、多分区、多副本且基于zookeeper协调的分布式消息系统，现已捐献给Apache基金会。它是一种高吞吐量的分布式发布订阅消息系统，以可水平扩展和高吞吐率而被广泛使用。目前越来越多的开源分布式处理系统如Cloudera、Apache Storm、Spark、Flink等都支持与Kafka集成。
优点：

客户端语言丰富，支持java、.net、php、ruby、python、go等多种语言；
性能卓越，单机写入TPS约在百万条/秒，消息大小10个字节；
提供完全分布式架构, 并有replica机制, 拥有较高的可用性和可靠性, 理论上支持消息无限堆积；
支持批量操作；
消费者采用Pull方式获取消息, 消息有序, 通过控制能够保证所有消息被消费且仅被消费一次;
有优秀的第三方Kafka Web管理界面Kafka-Manager；
在日志领域比较成熟，被多家公司和多个开源项目使用；

Jafka 是在 Kafka 之上孵化而来的，即 Kafka 的一个升级版。具有以下特性：快速持久化，可以在 O(1) 的系统开销下进行消息持久化；高吞吐，在一台普通的服务器上既可以达到 10W/s 的吞吐速率；完全的分布式系统，Broker、Producer、Consumer 都原生自动支持分布式，自动实现负载均衡；支持 Hadoop 数据并行加载，对于像 Hadoop 的一样的日志数据和离线分析系统，但又要求实时处理的限制，这是一个可行的解决方案。Kafka 通过 Hadoop 的并行加载机制统一了在线和离线的消息处理。Apache Kafka 相对于 ActiveMQ 是一个非常轻量级的消息系统，除了性能非常好之外，还是一个工作良好的分布式系统。

缺点：

Kafka单机超过64个队列/分区，Load会发生明显的飙高现象，队列越多，load越高，发送消息响应时间变长
使用短轮询方式，实时性取决于轮询间隔时间；
消费失败不支持重试；
支持消息顺序，但是一台代理宕机后，就会产生消息乱序；
社区更新较慢；

### 架构
Broker： Kafka 集群包含一个或多个服务器，这种服务器被称为 broker

Topic：每条发布到 Kafka 集群的消息都有一个类别，这个类别被称为 Topic。（物理上不同 Topic 的消息分开存储，逻辑上一个 Topic 的消息虽然保存于一个或多个 broker 上但用户只需指定消息的 Topic 即可生产或消费数据而不必关心数据存于何处）

Partition：Parition 是物理上的概念，每个 Topic 包含一个或多个 Partition.

Producer：负责发布消息到 Kafka broker，Producer 使用 push 模式将消息发布到 broker

Consumer：消息消费者，使用 pull 模式从 broker 订阅并消费消息，

Consumer Group：每个 Consumer 属于一个特定的 Consumer Group（可为每个 Consumer 指定 group name，若不指定 group name 则属于默认的 group）。

一个典型的 Kafka 集群中包含若干 Producer（可以是 web 前端产生的 Page View，或者是服务器日志，系统 CPU、Memory 等），若干 broker（Kafka 支持水平扩展，一般 broker 数量越多，集群吞吐率越高），若干 Consumer Group，以及一个 Zookeeper 集群。Kafka 通过 Zookeeper 管理集群配置，选举 leader，以及在 Consumer Group 发生变化时进行 rebalance。Producer 使用 push 模式将消息发布到 broker，Consumer 使用 pull 模式从 broker 订阅并消费消息。

#### Producer 消息路由
Producer 发送消息到 broker 时，会根据 Paritition 机制选择将其存储到哪一个 Partition。如果 Partition 机制设置合理，所有消息可以均匀分布到不同的 Partition 里，这样就实现了负载均衡。如果一个 Topic 对应一个文件，那这个文件所在的机器 I/O 将会成为这个 Topic 的性能瓶颈，而有了 Partition 后，不同的消息可以并行写入不同 broker 的不同 Partition 里，极大的提高了吞吐率。可以在 $KAFKA_HOME/config/server.properties 中通过配置项 num.partitions 来指定新建 Topic 的默认 Partition 数量，也可在创建 Topic 时通过参数指定，同时也可以在 Topic 创建之后通过 Kafka 提供的工具修改。

在发送一条消息时，可以指定这条消息的 key，Producer 根据这个 key 和 Partition 机制来判断应该将这条消息发送到哪个 Parition。Paritition 机制可以通过指定 Producer 的 paritition. class 这一参数来指定，该 class 必须实现 kafka.producer.Partitioner 接口。本例中如果 key 可以被解析为整数则将对应的整数与 Partition 总数取余，该消息会被发送到该数对应的 Partition。（每个 Parition 都会有个序号, 序号从 0 开始）

#### 消息保留与消费
对于传统的 message queue 而言，一般会删除已经被消费的消息，而 Kafka 集群会保留所有的消息，无论其被消费与否。当然，因为磁盘限制，不可能永久保留所有数据（实际上也没必要），因此 Kafka 提供两种策略删除旧数据。一是基于时间，二是基于 Partition 文件大小。

因为 Kafka 读取特定消息的时间复杂度为 O(1)，即与文件大小无关，所以这里删除过期文件与提高 Kafka 性能无关。选择怎样的删除策略只与磁盘以及具体的需求有关。另外，Kafka 会为每一个 Consumer Group 保留一些 metadata 信息——当前消费的消息的 position，也即 offset。这个 offset 由 Consumer 控制。正常情况下 Consumer 会在消费完一条消息后递增该 offset。当然，Consumer 也可将 offset 设成一个较小的值，重新消费一些消息。因为 offet 由 Consumer 控制，所以 Kafka broker 是无状态的，它不需要标记哪些消息被哪些消费过，也不需要通过 broker 去保证同一个 Consumer Group 只有一个 Consumer 能消费某一条消息，因此也就不需要锁机制，这也为 Kafka 的高吞吐率提供了有力保障。

#### Consumer Group
同一 Topic 的一条消息只能被同一个 Consumer Group 内的一个 Consumer 消费，但多个 Consumer Group 可同时消费这一消息。这是 Kafka 用来实现一个 Topic 消息的广播（发给所有的 Consumer）和单播（发给某一个 Consumer）的手段。一个 Topic 可以对应多个 Consumer Group。如果需要实现广播，只要每个 Consumer 有一个独立的 Group 就可以了。要实现单播只要所有的 Consumer 在同一个 Group 里。用 Consumer Group 还可以将 Consumer 进行自由的分组而不需要多次发送消息到不同的 Topic。

#### ack
Kafka producer有三种ack机制  初始化producer时在config中进行配置

0 

意味着producer不等待broker同步完成的确认，继续发送下一条(批)信息

提供了最低的延迟。但是最弱的持久性，当服务器发生故障时，就很可能发生数据丢失。例如leader已经死亡，producer不知情，还会继续发送消息broker接收不到数据就会数据丢失

1

意味着producer要等待leader成功收到数据并得到确认，才发送下一条message。此选项提供了较好的持久性较低的延迟性。

Partition的Leader死亡，follwer尚未复制，数据就会丢失

 

-1

意味着producer得到follwer确认，才发送下一条数据

持久性最好，延时性最差

# MRC
MRC是跨机房消息同步组件(Message Replication Center)，用于跨机房间的以队列为单位的消息同步，支持单向与双向同步，以满足业务方在单个机房消费多机房全量消息的需求。



注：经过 MRC 的消息会被 MRC 在消息头中添加一个  MRC_EZONE 的 header，用以指明该消息的原发地是哪个 ezone。业务方的消费者可以从消息头中取出该 MRC_EZONE 的值，可能的值为：alta1, altb1, altc1, xg1, wg1, zb1.

原理：
源端机房新建 queue (mrc_test_queue)，这个 queue 的 bindings 与本机房 test_queue 原先的 bindings 一致，所以 queue (mrc_test_queue) 只会接收到本机房原本应该接收到的消息，而不会接收到对端机房发来的消息。
目的机房新增 test_queue 对应的 exchange (mrc_test_queue)，这个 exchange 会接收来自源端机房发来的消息，并且会绑定到本机房的queue (test_queue)，这样目的机房的 queue (test_queue) 就会接收到来自源端机房的消息。
部署在源端机房的 MRC 作为消费者消费本机房 queue (mrc_test_queue) 上的消息，作为生产者发送消息到目的端的 exchange (mrc_test_queue)，由目的端的 exchange (mrc_test_queue) 路由消息到目的机房的 queue (test_queue)。

# 大型网站系统架构常见问题
## 设计高可用系统的常用手段
1，降级： 服务降级是当服务器压力剧增的情况下，根据当前业务情况及流量对一些服务和页面有策略的降级，以此释放服务器资源以保证核心任务的正常运行。降级往往会指定不同的级别，面临不同的异常等级执行不同的处理。根据服务方式：可以拒接服务，可以延迟服务，也有时候可以随机服务。根据服务范围：可以砍掉某个功能，也可以砍掉某些模块。总之服务降级需要根据不同的业务需求采用不同的降级策略。主要的目的就是服务虽然有损但是总比没有好；

2，限流： 防止恶意请求流量、恶意攻击，或者防止流量超出系统峰值；

3，缓存： 避免大量请求直接落到数据库，将数据库击垮；

4，超时和重试机制： 避免请求堆积造成雪崩；

5，回滚机制： 快速修复错误版本。

## Nginx
Nginx是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器。 Nginx 主要提供反向代理、负载均衡、动静分离(静态资源服务)等服务。

### 反向代理
谈到反向代理，就不得不提一下正向代理。无论是正向代理，还是反向代理，说到底，就是代理模式的衍生版本罢了

正向代理：某些情况下，代理我们用户去访问服务器，需要用户手动的设置代理服务器的ip和端口号。正向代理比较常见的一个例子就是 VPN 了。

反向代理： 是用来代理服务器的，代理我们要访问的目标服务器。代理服务器接受请求，然后将请求转发给内部网络的服务器，并将从服务器上得到的结果返回给客户端，此时代理服务器对外就表现为一个服务器。

### 负载均衡
在高并发情况下需要使用，其原理就是将并发请求分摊到多个服务器执行，减轻每台服务器的压力，多台服务器(集群)共同完成工作任务，从而提高了数据的吞吐量。

Nginx支持的weight轮询（默认）、ip_hash、fair、url_hash这四种负载均衡调度算法，感兴趣的可以自行查阅。

负载均衡相比于反向代理更侧重的是将请求分担到多台服务器上去，所以谈论负载均衡只有在提供某服务的服务器大于两台时才有意义。

### 动静分离
动静分离是让动态网站里的动态网页根据一定规则把不变的资源和经常变的资源区分开来，动静资源做好了拆分以后，我们就可以根据静态资源的特点将其做缓存操作，这就是网站静态化处理的核心思路。

###  为什么要用 Nginx?
如果面试官问你这个问题，就一定想看你知道 Nginx 服务器的一些优点吗。

Nginx 有以下5个优点：

高并发、高性能（这是其他web服务器不具有的）
可扩展性好（模块化设计，第三方插件生态圈丰富）
高可靠性（可以在服务器行持续不间断的运行数年）
热部署（这个功能对于 Nginx 来说特别重要，热部署指可以在不停止 Nginx服务的情况下升级 Nginx）
BSD许可证（意味着我们可以将源代码下载下来进行修改然后使用自己的版本）

# ZK
##  概览
ZooKeeper 是一个开源的分布式协调服务。ZooKeeper 的设计目标是将那些复杂且容易出错的分布式一致性服务封装起来，构成一个高效可靠的原语集，并以一系列简单易用的接口提供给用户使用。

原语： 操作系统或计算机网络用语范畴。是由若干条指令组成的，用于完成一定功能的一个过程。具有不可分割性·即原语的执行必须是连续的，在执行过程中不允许被中断。

ZooKeeper 是一个典型的分布式数据一致性解决方案，分布式应用程序可以基于 ZooKeeper 实现诸如数据发布/订阅、负载均衡、命名服务、分布式协调/通知、集群管理、Master 选举、分布式锁和分布式队列等功能。

Zookeeper 一个最常用的使用场景就是用于担任服务生产者和服务消费者的注册中心(提供发布订阅服务)。 服务生产者将自己提供的服务注册到Zookeeper中心，服务的消费者在进行服务调用的时候先到Zookeeper中查找服务，获取到服务生产者的详细信息之后，再去调用服务生产者的内容与数据。
## 为什么最好使用奇数台服务器构成 ZooKeeper 集群？

所谓的zookeeper容错是指，当宕掉几个zookeeper服务器之后，剩下的个数必须大于宕掉的个数的话整个zookeeper才依然可用。假如我们的集群中有n台zookeeper服务器，那么也就是剩下的服务数必须大于n/2。先说一下结论，2n和2n-1的容忍度是一样的，都是n-1，大家可以先自己仔细想一想，这应该是一个很简单的数学问题了。 比如假如我们有3台，那么最大允许宕掉1台zookeeper服务器，如果我们有4台的的时候也同样只允许宕掉1台。 假如我们有5台，那么最大允许宕掉2台zookeeper服务器，如果我们有6台的的时候也同样只允许宕掉2台。

综上，何必增加那一个不必要的zookeeper呢？

## 重要概念总结
ZooKeeper 本身就是一个分布式程序（只要半数以上节点存活，ZooKeeper 就能正常服务）。
为了保证高可用，最好是以集群形态来部署 ZooKeeper，这样只要集群中大部分机器是可用的（能够容忍一定的机器故障），那么 ZooKeeper 本身仍然是可用的。

ZooKeeper 将数据保存在内存中，这也就保证了 高吞吐量和低延迟（但是内存限制了能够存储的容量不太大，此限制也是保持znode中存储的数据量较小的进一步原因）。

ZooKeeper 是高性能的。 在“读”多于“写”的应用程序中尤其地高性能，因为“写”会导致所有的服务器间同步状态。（“读”多于“写”是协调服务的典型场景。）

ZooKeeper有临时节点的概念。 当创建临时节点的客户端会话一直保持活动，瞬时节点就一直存在。而当会话终结时，瞬时节点被删除。持久节点是指一旦这个ZNode被创建了，除非主动进行ZNode的移除操作，否则这个ZNode将一直保存在Zookeeper上。

ZooKeeper 底层其实只提供了两个功能：①管理（存储、读取）用户程序提交的数据；②为用户程序提供数据节点监听服务。

## 会话（Session）
Session 指的是 ZooKeeper 服务器与客户端会话。在 ZooKeeper 中，一个客户端连接是指客户端和服务器之间的一个 TCP 长连接。客户端启动的时候，首先会与服务器建立一个 TCP 连接，从第一次连接建立开始，客户端会话的生命周期也开始了。通过这个连接，客户端能够通过心跳检测与服务器保持有效的会话，也能够向Zookeeper服务器发送请求并接受响应，同时还能够通过该连接接收来自服务器的Watch事件通知。 Session的sessionTimeout值用来设置一个客户端会话的超时时间。当由于服务器压力太大、网络故障或是客户端主动断开连接等各种原因导致客户端连接断开时，只要在sessionTimeout规定的时间内能够重新连接上集群中任意一台服务器，那么之前创建的会话仍然有效。

在为客户端创建会话之前，服务端首先会为每个客户端都分配一个sessionID。由于 sessionID 是 Zookeeper 会话的一个重要标识，许多与会话相关的运行机制都是基于这个 sessionID 的，因此，无论是哪台服务器为客户端分配的 sessionID，都务必保证全局唯一。

## Znode
在谈到分布式的时候，我们通常说的“节点"是指组成集群的每一台机器。然而，在Zookeeper中，“节点"分为两类，第一类同样是指构成集群的机器，我们称之为机器节点；第二类则是指数据模型中的数据单元，我们称之为数据节点一一ZNode。

Zookeeper将所有数据存储在内存中，数据模型是一棵树（Znode Tree)，由斜杠（/）的进行分割的路径，就是一个Znode，例如/foo/path1。每个上都会保存自己的数据内容，同时还会保存一系列属性信息。

在Zookeeper中，node可以分为持久节点和临时节点两类。所谓持久节点是指一旦这个ZNode被创建了，除非主动进行ZNode的移除操作，否则这个ZNode将一直保存在Zookeeper上。而临时节点就不一样了，它的生命周期和客户端会话绑定，一旦客户端会话失效，那么这个客户端创建的所有临时节点都会被移除。 另外，ZooKeeper还允许用户为每个节点添加一个特殊的属性：SEQUENTIAL.一旦节点被标记上这个属性，那么在这个节点被创建的时候，Zookeeper会自动在其节点名后面追加上一个整型数字，这个整型数字是一个由父节点维护的自增数字。

## 版本
在前面我们已经提到，Zookeeper 的每个 ZNode 上都会存储数据，对应于每个ZNode，Zookeeper 都会为其维护一个叫作 Stat 的数据结构，Stat 中记录了这个 ZNode 的三个数据版本，分别是version（当前ZNode的版本）、cversion（当前ZNode子节点的版本）和 aversion（当前ZNode的ACL版本）。

## Watcher
Watcher（事件监听器），是Zookeeper中的一个很重要的特性。Zookeeper允许用户在指定节点上注册一些Watcher，并且在一些特定事件触发的时候，ZooKeeper服务端会将事件通知到感兴趣的客户端上去，该机制是Zookeeper实现分布式协调服务的重要特性。

事件类型:(znode节点相关的)

		 EventType:NodeCreated            //节点创建

		 EventType:NodeDataChanged        //节点的数据变更

		 EventType:NodeChildrentChanged   //子节点下的数据变更

		 EventType:NodeDeleted

状态类型:(是跟客户端实例相关的)

		 KeeperState:Disconneced        //连接失败

 		 KeeperState:SyncConnected	//连接成功	 

		 KeeperState:AuthFailed         //认证失败

		 KeeperState:Expired            //会话过期


## ACL
Zookeeper采用ACL（AccessControlLists）策略来进行权限控制，类似于 UNIX 文件系统的权限控制。Zookeeper 定义了如下5种权限。
1，CREATE：创建子节点的权限；

2，READ：获取节点数据和子节点列表的权限；

3，WRITE：更新节点数据的权限；

4，DELETE：删除子节点的权限；

5，ADMIN：设置节点ACL的权限。

其中尤其需要注意的是，CREATE和DELETE这两种权限都是针对子节点的权限控制。

## 特点
顺序一致性： 从同一客户端发起的事务请求，最终将会严格地按照顺序被应用到 ZooKeeper 中去。

原子性： 所有事务请求的处理结果在整个集群中所有机器上的应用情况是一致的，也就是说，要么整个集群中所有的机器都成功应用了某一个事务，要么都没有应用。

单一系统映像 ： 无论客户端连到哪一个 ZooKeeper 服务器上，其看到的服务端数据模型都是一致的。

可靠性： 一旦一次更改请求被应用，更改的结果就会被持久化，直到被下一次更改覆盖。

## 集群角色介绍
最典型集群模式： Master/Slave 模式（主备模式）。在这种模式中，通常 Master服务器作为主服务器提供写服务，其他的 Slave 服务器从服务器通过异步复制的方式获取 Master 服务器最新的数据提供读服务。

但是，在 ZooKeeper 中没有选择传统的 Master/Slave 概念，而是引入了Leader、Follower 和 Observer 三种角色。

ZooKeeper 集群中的所有机器通过一个 Leader 选举过程来选定一台称为 “Leader” 的机器，Leader 既可以为客户端提供写服务又能提供读服务。除了 Leader 外，Follower 和 Observer 都只能提供读服务。Follower 和 Observer 唯一的区别在于 Observer 机器不参与 Leader 的选举过程，也不参与写操作的“过半写成功”策略，因此 Observer 机器可以在不影响写性能的情况下提升集群的读性能。

### Leader
1，事务请求的唯一调度和处理者，保证集群事务处理的顺序性；
2，集群内部各服务器的调度者。

### Follower
1，处理客户端非事务请求，转发事务请求给Leader；
2，参与事务请求proposal的投票；
3，参与Leader选举的投票；

### Observer
Follower 和 Observer 唯一的区别在于 Observer 机器不参与 Leader 的选举过程，也不参与写操作的“过半写成功”策略，因此 Observer 机器可以在不影响写性能的情况下提升集群的读性能。

## 选主
集群选主涉及到两个问题：

1. 谁来做leader

2. leader挂掉了怎么被follower感知到

首先是第一个问题，谁来做leader，其实可以将这个问题看做是多线程中的互斥锁抢占，锁只有一把，并且只能被一个人抢到，这里就把一个zookeeper上的一个节点/leader-info看做是锁，集群中的每台机器都尝试去创建这个节点（抢占锁），因为zookeeper创建节点是原子性操作，所以只有一台机器能够创建成功其它都会失败，创建成功的那台机器就作为leader，其它机器做follower，一般leader抢占成功了之后会在/leader-info节点上存储一些与自己相关的信息，比如hostname、id之类的，以让follower知道谁抢占成功成为了leader，然后去连接leader进行一些数据交换或指令控制之类的。

第二个问题是leader挂掉了怎么通知其它的follower，zookeeper中的节点按照有效时间分为持久节点和临时节点，临时节点跟session绑定，而一个session表示一个客户端，当客户端下线的时候session失效，当session失效的时候跟它绑定的临时节点就会被删除，利用这个特性可以检测节点是否还在存活状态，实现follower对leader下线的感知，只是需要注意在创建/leader-info节点的时候要将其创建为临时节点，然后众多follower都在这个节点上添加一个watcher监听其删除事件，这样当leader挂掉的时候session失效，然后与此session绑定的临时节点会被删除，即/leader-info节点将被删除，同时给所有的follower发送事件通知，follower一看leader挂了就燥起来了，将自己的状态置为looking，开始新一轮的选举。

总结一下选主的流程：

1. 集群中的所有机器将自己置为looking状态，准备开始选举。

2. 所有looking状态的机器尝试去创建/leader-info节点。

3. 创建成功的将自己的状态修改为leader，同时将自己的一些信息写入到/leader-info这个节点上。

4. 创建失败的将自己的状态置为follower，同时尝试从/leader-info获取leader信息进行一些leader改变的逻辑，follower在获取/leader-info节点数据的同时要设置一个watcher，监听此节点的删除事件，当节点被删除事件触发时启动新一轮的选举，因为获取数据设置watcher这个操作是原子性的，所以要么这个节点存在获取数据成功，并且设置watcher也成功，要么节点不存在抛出KeeperException.NoNodeException异常。

5. 为什么在follower设置watcher的时候还有可能会抛异常呢，leader不是已经创建了这个节点了吗？因为follower从尝试创建/leader-info节点失败到去获取此节点的数据同时设置watcher这一段操作不是原子性的，在这中间可能会发生一些变故，leader可能刚成为leader就挂掉了（或者因为一些网络抖动原因，总之是session失效了），leader挂掉之后它创建的临时节点就被zookeeper删除了，所以当follower在设置watcher的时候如果检测到KeeperException.NoNodeException，说明之前的leader挂掉了，此时集群中已经没有了leader，follower又燥起来了，它将自己的状态置为looking开始新一轮的选举。

## ZAB（ZooKeeper Atomic Broadcast 原子广播）
当 Leader 服务器出现网络中断、崩溃退出与重启等异常情况时，ZAB 协议就会进人恢复模式并选举产生新的Leader服务器。这个过程大致是这样的：

1，Leader election（选举阶段）：节点在一开始都处于选举阶段，只要有一个节点得到超半数节点的票数，它就可以当选准 leader。

2，Discovery（发现阶段）：在这个阶段，followers 跟准 leader 进行通信，同步 followers 最近接收的事务提议。

3，Synchronization（同步阶段）:同步阶段主要是利用 leader 前一阶段获得的最新提议历史，同步集群中所有的副本。同步完成之后 准 leader 才会成为真正的 leader。

4，Broadcast（广播阶段） 到了这个阶段，Zookeeper 集群才能正式对外提供事务服务，并且 leader 可以进行消息广播。同时如果有新的节点加入，还需要对新节点进行同步。

# Etcd
一个键值存储仓库，主要用于配置共享和服务发现。

## 优点：
简单：支持 curl 方式的用户 API (HTTP+JSON)

安全：可选 SSL 客户端证书认证

快速：单实例可达每秒 1000 次写操作

可靠：使用 Raft 实现分布式

## Raft（https://www.jianshu.com/p/5aed73b288f7
### 角色
Leader（领袖） Follower（群众） Candidate（候选人） 就像一个民主社会，领袖由民众投票选出。刚开始没有领袖，所有集群中的参与者都是群众，那么首先开启一轮大选，在大选期间所有群众都能参与竞选，这时所有群众的角色就变成了候选人，民主投票选出领袖后就开始了这届领袖的任期，然后选举结束，所有除领袖的候选人又变回群众角色服从领袖领导。这里提到一个概念「任期」，用术语 Term 表达。关于 Raft 协议的核心概念和术语就这么多而且和现实民主制度非常匹配，所以很容易理解。


### Leader选举过程
在极简的思维下，一个最小的 Raft 民主集群需要三个参与者（如：A、B、C），这样才可能投出多数票。初始状态 ABC 都是 Follower，然后发起选举,这里的关键就是随机 timeout，最先从 timeout 中恢复发起投票的一方向还在 timeout 中的另外两方请求投票，这时它们就只能投给对方了，很快达成一致。选出 Leader 后，Leader 通过定期向所有 Follower 发送心跳信息维持其统治。若 Follower 一段时间未收到 Leader 的心跳则认为 Leader 可能已经挂了再次发起选主过程。

### Leader节点对一致性的影响
Raft 协议强依赖 Leader 节点的可用性来确保集群数据的一致性。数据的流向只能从 Leader 节点向 Follower 节点转移。当 Client 向集群 Leader 节点提交数据后，Leader 节点接收到的数据处于未提交状态（Uncommitted），接着 Leader 节点会并发向所有 Follower 节点复制数据并等待接收响应，确保至少集群中超过半数节点已接收到数据后再向 Client 确认数据已接收。一旦向 Client 发出数据接收 Ack 响应后，表明此时数据状态进入已提交（Committed），Leader 节点再向 Follower 节点发通知告知该数据状态已提交。在这个过程中，主节点可能在任意阶段挂掉，看下 Raft 协议如何针对不同阶段保障数据一致性的。

1，数据到达 Leader 节点前 这个阶段 Leader 挂掉不影响一致性

2，数据到达 Leader 节点，但未复制到 Follower 节点 这个阶段 Leader 挂掉，数据属于未提交状态，Client 不会收到 Ack 会认为超时失败可安全发起重试。Follower 节点上没有该数据，重新选主后 Client 重试重新提交可成功。原来的 Leader 节点恢复后作为 Follower 加入集群重新从当前任期的新 Leader 处同步数据，强制保持和 Leader 数据一致。

3，数据到达 Leader 节点，成功复制到 Follower 所有节点，但还未向 Leader 响应接收 这个阶段 Leader 挂掉，虽然数据在 Follower 节点处于未提交状态（Uncommitted）但保持一致，重新选出 Leader 后可完成数据提交，此时 Client 由于不知到底提交成功没有，可重试提交。针对这种情况 Raft 要求 RPC 请求实现幂等性，也就是要实现内部去重机制。

4，数据到达 Leader 节点，成功复制到 Follower 部分节点，但还未向 Leader 响应接收

这个阶段 Leader 挂掉，数据在 Follower 节点处于未提交状态（Uncommitted）且不一致，Raft 协议要求投票只能投给拥有最新数据的节点。所以拥有最新数据的节点会被选为 Leader 再强制同步数据到 Follower，数据不会丢失并最终一致。

5，数据到达 Leader 节点，成功复制到 Follower 所有或多数节点，数据在 Leader 处于已提 交状态，但在 Follower 处于未提交状态

这个阶段 Leader 挂掉，重新选出新 Leader 后的处理流程和阶段 3 一样。

6，数据到达 Leader 节点，成功复制到 Follower 所有或多数节点，数据在所有节点都处于已提交状态，但还未响应 Client

这个阶段 Leader 挂掉，Cluster 内部数据其实已经是一致的，Client 重复重试基于幂等策略对一致性无影响。

7，网络分区导致的脑裂情况，出现双 Leader

网络分区将原先的 Leader 节点和 Follower 节点分隔开，Follower 收不到 Leader 的心跳将发起选举产生新的 Leader。这时就产生了双 Leader，原先的 Leader 独自在一个区，向它提交数据不可能复制到多数节点所以永远提交不成功。向新的 Leader 提交数据可以提交成功，网络恢复后旧的 Leader 发现集群中有更新任期（Term）的新 Leader 则自动降级为 Follower 并从新 Leader 处同步数据达成集群数据一致。

## Etcd vs Zookeeper
etcd在项目实现，一致性协议易理解性，运维，安全等多个维度上，都占据优势。

一致性协议：etcd使用raft协议，zk使用zab（类paxos协议），前者易于理解，方便工程实现。ZooKeeper的部署、维护、使用比较复杂，需要安装客户端，官方只提供了Java和C两种语言的接口。（paxos算法复杂）

api：etcd提供http+json，grpc接口，跨平台语言，zk则需要使用其客户端。

访问安全方面：etcd支持https访问，zk在这方面缺失。

应用场景：配置管理，服务注册发现，选主，应用调度，分布式队列，分布式锁。

etcd读写性能：每个实例每秒支持一千次写操作。这个性能还是相当可观的。 单实例节点支持每秒1000次数据写入。节点越多，由于数据同步涉及到网络延迟，会根据实际情况越来越慢，而读性能会随之变强，因为每个节点都能处理用户请求。

数据持久化。etcd默认数据一更新就进行持久化

数据存储 etcd的存储分为内存存储和持久化（硬盘）存储两部分，内存中的存储除了顺序化的记录下所有用户对节点数据变更的记录外，还会对用户数据进行索引、建堆等方便查询的操作。而持久化则使用预写式日志（WAL：Write Ahead Log）进行记录存储。

# 脑裂
在高可用（HA）系统中，当联系2个节点的“心跳线”断开时，本来为一整体、动作协调的HA系统，就分裂成为2个独立的个体。由于相互失去了联系，都以为是对方出了故障。两个节点上的HA软件像“裂脑人”一样，争抢“共享资源”、争起“应用服务”，就会发生严重后果——或者共享资源被瓜分、2边“服务”都起不来了；或者2边“服务”都起来了，但同时读写“共享存储”，导致数据损坏（常见如数据库轮询着的联机日志出错）。

集群的脑裂通常是发生在集群中部分节点之间不可达而引起的（或者因为节点请求压力较大，导致其他节点与该节点的心跳检测不可用）。当上述情况发生时，不同分裂的小集群会自主的选择出master节点，造成原本的集群会同时存在多个master节点。

## 解决方式
1）添加冗余的心跳线，例如：双线条线（心跳线也HA），尽量减少“裂脑”发生几率；

2）启用磁盘锁。正在服务一方锁住共享磁盘，“裂脑”发生时，让对方完全“抢不走”共享磁盘资源。但使用锁磁盘也会有一个不小的问题，如果占用共享盘的一方不主动“解锁”，另一方就永远得不到共享磁盘。现实中假如服务节点突然死机或崩溃，就不可能执行解锁命令。后备节点也就接管不了共享资源和应用服务。于是有人在HA中设计了“智能”锁。即：正在服务的一方只在发现心跳线全部断开（察觉不到对端）时才启用磁盘锁。平时就不上锁了。

3）设置仲裁机制。例如设置参考IP（如网关IP），当心跳线完全断开时，2个节点都各自ping一下参考IP，不通则表明断点就出在本端。不仅“心跳”、还兼对外“服务”的本端网络链路断了，即使启动（或继续）应用服务也没有用了，那就主动放弃竞争，让能够ping通参考IP的一端去起服务。更保险一些，ping不通参考IP的一方干脆就自我重启，以彻底释放有可能还占用着的那些共享资源。

# 秒杀系统设计
## 热点隔离
秒杀系统设计的第一个原则就是将这种热点数据隔离出来，不要让1%的请求影响到另外的99%，隔离出来后也更方便对这1%的请求做针对性优化。针对秒杀我们做了多个层次的隔离：
业务隔离：把秒杀做成一种营销活动，卖家要参加秒杀这种营销活动需要单独报名，从技术上来说，卖家报名后对我们来说就是已知热点，当真正开始时我们可以提前做好预热。

系统隔离：系统隔离更多是运行时的隔离，可以通过分组部署的方式和另外99%分开。秒杀还申请了单独的域名，目的也是让请求落到不同的集群中。

数据隔离：秒杀所调用的数据大部分都是热数据，比如会启用单独cache集群或MySQL数据库来放热点数据，目前也是不想0.01%的数据影响另外99.99%。

当然实现隔离很有多办法，如可以按照用户来区分，给不同用户分配不同cookie，在接入层路由到不同服务接口中；还有在接入层可以对URL的不同Path来设置限流策略等。服务层通过调用不同的服务接口；数据层可以给数据打上特殊的标来区分。目的都是把已经识别出来的热点和普通请求区分开来。

## 基于时间分片削峰
熟悉淘宝秒杀的都知道，第一版的秒杀系统本身并没有答题功能，后面才增加了秒杀答题，当然秒杀答题一个很重要的目的是为了防止秒杀器，2011年秒杀非常火的时候，秒杀器也比较猖獗，而没有达到全民参与和营销的目的，所以增加的答题来限制秒杀器。增加答题后，下单的时间基本控制在2s后，秒杀器的下单比例也下降到5%以下。

## 数据分层校验
对大流量系统的数据做分层校验也是最重要的设计原则，所谓分层校验就是对大量的请求做成“漏斗”式设计，在不同层次尽可能把无效的请求过滤，“漏斗”的最末端才是有效的请求，要达到这个效果必须对数据做分层的校验，下面是一些原则：将90%的数据缓存在客户端浏览器，将动态请求的读数据Cache在Web端，对读数据不做强一致性校验，对写数据进行基于时间的合理分片，对写请求做限流保护，对写数据进行强一致性校验。

# 海量数据处理面试题
## 海量日志数据，提取出某日访问百度次数最多的那个IP。
算法思想：分而治之+Hash
1.IP地址最多有2^32=4G种取值情况，所以不能完全加载到内存中处理； 
2.可以考虑采用“分而治之”的思想，按照IP地址的Hash(IP)%1024值，把海量IP日志分别存储到1024个小文件中。这样，每个小文件最多包含4MB个IP地址； 
3.对于每一个小文件，可以构建一个IP为key，出现次数为value的Hash map，同时记录当前出现次数最多的那个IP地址；
4.可以得到1024个小文件中的出现次数最多的IP，再依据常规的排序算法得到总体上出现次数最多的IP。

## 有一个1G大小的一个文件，里面每一行是一个词，词的大小不超过16字节，内存限制大小是1M。返回频数最高的100个词。
方案：顺序读文件中，对于每个词x，取hash(x)%5000，然后按照该值存到5000个小文件（记为x0,x1,...x4999）中。这样每个文件大概是200k左右。

    如果其中的有的文件超过了1M大小，还可以按照类似的方法继续往下分，直到分解得到的小文件的大小都不超过1M。
    对每个小文件，统计每个文件中出现的词以及相应的频率（可以采用trie树/hash_map等），并取出出现频率最大的100个词（可以用含100个结点的最小堆），并把100个词及相应的频率存入文件，这样又得到了5000个文件。下一步就是把这5000个文件进行归并（类似与归并排序）的过程了。


## 给定a、b两个文件，各存放50亿个url，每个url各占64字节，内存限制是4G，让你找出a、b文件共同的url？

    方案1：可以估计每个文件安的大小为5G×64=320G，远远大于内存限制的4G。所以不可能将其完全加载到内存中处理。考虑采取分而治之的方法。

    遍历文件a，对每个url求取hash(url)%1000，然后根据所取得的值将url分别存储到1000个小文件（记为a0,a1,...,a999）中。这样每个小文件的大约为300M。

    遍历文件b，采取和a相同的方式将url分别存储到1000小文件（记为b0,b1,...,b999）。这样处理后，所有可能相同的url都在对应的小文件（a0vsb0,a1vsb1,...,a999vsb999）中，不对应的小文件不可能有相同的url。然后我们只要求出1000对小文件中相同的url即可。

    求每对小文件中相同的url时，可以把其中一个小文件的url存储到hash_set中。然后遍历另一个小文件的每个url，看其是否在刚才构建的hash_set中，如果是，那么就是共同的url，存到文件里面就可以了。

## 在2.5亿个整数中找出不重复的整数，注，内存不足以容纳这2.5亿个整数。

    方案1：采用2-Bitmap（每个数分配2bit，00表示不存在，01表示出现一次，10表示多次，11无意义）进行，共需内存2^32 * 2 bit=1 GB内存，还可以接受。然后扫描这2.5亿个整数，查看Bitmap中相对应位，如果是00变01，01变10，10保持不变。所描完事后，查看bitmap，把对应位是01的整数输出即可。

    方案2：也可采用与第1题类似的方法，进行划分小文件的方法。然后在小文件中找出不重复的整数，并排序。然后再进行归并，注意去除重复的元素。

## 给40亿个不重复的unsigned int的整数，没排过序的，然后再给一个数，如何快速判断这个数是否在那40亿个数当中？

    与上第6题类似，我的第一反应时快速排序+二分查找。以下是其它更好的方法：
    方案1：oo，申请512M的内存，一个bit位代表一个unsigned int值。读入40亿个数，设置相应的bit位，读入要查询的数，查看相应bit位是否为1，为1表示存在，为0表示不存在。

    dizengrong：
    方案2：这个问题在《编程珠玑》里有很好的描述，大家可以参考下面的思路，探讨一下：
又因为2^32为40亿多，所以给定一个数可能在，也可能不在其中；
这里我们把40亿个数中的每一个用32位的二进制来表示
假设这40亿个数开始放在一个文件中。

    然后将这40亿个数分成两类:
      1.最高位为0
      2.最高位为1
    并将这两类分别写入到两个文件中，其中一个文件中数的个数<=20亿，而另一个>=20亿（这相当于折半了）；
与要查找的数的最高位比较并接着进入相应的文件再查找

    再然后把这个文件为又分成两类:
      1.次最高位为0
      2.次最高位为1

    并将这两类分别写入到两个文件中，其中一个文件中数的个数<=10亿，而另一个>=10亿（这相当于折半了）；
    与要查找的数的次最高位比较并接着进入相应的文件再查找。
    .......
    以此类推，就可以找到了,而且时间复杂度为O(logn)，方案2完。

## 100w个数中找出最大的100个数。

    方案1：在前面的题中，我们已经提到了，用一个含100个元素的最小堆完成。复杂度为O(100w*lg100)。

    方案2：采用快速排序的思想，每次分割之后只考虑比轴大的一部分，知道比轴大的一部分在比100多的时候，采用传统排序算法排序，取前100个。复杂度为O(100w*100)。

    方案3：采用局部淘汰法。选取前100个元素，并排序，记为序列L。然后一次扫描剩余的元素x，与排好序的100个元素中最小的元素比，如果比这个最小的要大，那么把这个最小的元素删除，并把x利用插入排序的思想，插入到序列L中。依次循环，知道扫描了所有的元素。复杂度为O(100w*100)。


# 算法
## 排序算法（https://juejin.im/post/5b95da8a5188255c775d8124
### 冒泡排序

	public class BubbleSort {
	    public static void sort(int[] array) {
	        if (array == null || array.length == 0) {
	            return;
	        }

	        int length = array.length;
	        //外层：需要length-1次循环比较
	        for (int i = 0; i < length - 1; i++) {
	            //内层：每次循环需要两两比较的次数，每次比较后，都会将当前最大的数放到最后位置，所以每次比较次数递减一次
	            for (int j = 0; j < length - 1 - i; j++) {
	                if (array[j] > array[j+1]) {
	                    //交换数组array的j和j+1位置的数据
	                    swap(array, j, j+1);
	                }
	            }
	        }
	    }

	    /**
	     * 交换数组array的i和j位置的数据
	     * @param array 数组
	     * @param i 下标i
	     * @param j 下标j
	     */
	    public static void swap(int[] array, int i, int j) {
	        int temp = array[i];
	        array[i] = array[j];
	        array[j] = temp;
	    }
	}


算法效率：冒泡排序是稳定的排序算法，最容易实现的排序, 最坏的情况是每次都需要交换, 共需遍历并交换将近n²/2次, 时间复杂度为O(n²). 最佳的情况是内循环遍历一次后发现排序是对的, 因此退出循环, 时间复杂度为O(n). 平均来讲, 时间复杂度为O(n²). 由于冒泡排序中只有缓存的temp变量需要内存空间, 因此空间复杂度为常量O(1)。

## 快速排序

	public class QuickSort {
	    
	public static void quickSort(int[] array) {
	    _quickSort(array, 0, array.length - 1);
	    System.out.println(Arrays.toString(array) + " quickSort");
	}
	 
	 
	private static int getMiddle(int[] list, int low, int high) {
	    int tmp = list[low];    //数组的第一个作为中轴
	    while (low < high) {
	        while (low < high && list[high] >= tmp) {
	            high--;
	        }
	 
	 
	        list[low] = list[high];   //比中轴小的记录移到低端
	        while (low < high && list[low] <= tmp) {
	            low++;
	        }
	 
	 
	        list[high] = list[low];   //比中轴大的记录移到高端
	    }
	    list[low] = tmp;              //中轴记录到尾
	    return low;                  //返回中轴的位置
	}
	 
	 
	private static void _quickSort(int[] list, int low, int high) {
	    if (low < high) {
	        int middle = getMiddle(list, low, high);  //将list数组进行一分为二
	        _quickSort(list, low, middle - 1);      //对低字表进行递归排序
	        _quickSort(list, middle + 1, high);      //对高字表进行递归排序
	    }
	}


## 选择排序

	public class SelectSort {
	    public static void sort(int[] arr) {
	        for (int i = 0; i < arr.length - 1; i++) {
	            int min = i;
	            for (int j = i+1; j < arr.length; j ++) { //选出之后待排序中值最小的位置
	                if (arr[j] < arr[min]) {
	                    min = j;
	                }
	            }
	            if (min != i) {
	                arr[min] = arr[i] + arr[min];
	                arr[i] = arr[min] - arr[i];
	                arr[min] = arr[min] - arr[i];
	            }
	        }
	    }

# 最小堆解决TOP K (https://blog.csdn.net/xiao__gui/article/details/8687982

## 常见算法
### 两数相加
	class Solution {
	    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
	        return addTwoNumbers(l1, l2, null);
	    }

	    public ListNode addTwoNumbers(ListNode l1, ListNode l2, ListNode prev) {
	        ListNode next1 = null;
	        ListNode next2 = null;
	        int val1 = 0;
	        int val2 = 0;
	        if (l1 != null) {
	            val1 = l1.val;
	            next1 = l1.next;
	        }
	        if (l2 != null) {
	            val2 = l2.val;
	            next2 = l2.next;
	        }
	        ListNode newNode = new ListNode(val1 + val2);
	        if (prev != null) {
	            if (prev.val >= 10) {
	                prev.val %= 10;
	                newNode.val += 1;
	            }
	        }
	        if (next1 != null || next2 != null) {
	            newNode.next = addTwoNumbers(next1, next2, newNode);
	        } else if (newNode.val >= 10) {
	            newNode.next = addTwoNumbers(next1, next2, newNode);
	        }
	        return newNode;
	    }
	}

### 无重复字符串的最长子串
	class Solution {
	    public int lengthOfLongestSubstring(String s) {
	        int n = s.length(), ans = 0;
	        Map<Character, Integer> map = new HashMap<>();
	        for (int end = 0, start = 0; end < n; end++) {
	            char alpha = s.charAt(end);
	            if (map.containsKey(alpha)) {
	                start = Math.max(map.get(alpha), start);
	            }
	            ans = Math.max(ans, end - start + 1);
	            map.put(s.charAt(end), end + 1);
	        }
	        return ans;
	    }
	}

### 最长回文子字符串
	class Solution {
	    public String longestPalindrome(String s) {
	        if (s.equals("")) {
	            return "";
	        }
	        int length = s.length();
	        String reversal = new StringBuffer(s).reverse().toString(); // 反转字符串
	        int[][] cell = new int[length][length];
	        int maxLen = 0; // 最长回文子串长度
	        int maxEnd = 0; // 最长回文子串结束位置
	        for (int i = 0; i < length; i++) {
	            for (int j = 0; j < length; j++) {
	                if (reversal.charAt(i) == s.charAt(j)) {
	                    if (i == 0 || j == 0) {
	                        cell[i][j] = 1;
	                    } else {
	                        cell[i][j] = cell[i - 1][j - 1] + 1;
	                    }
	                }
	                /**************修改的地方***************************/
	                // 可为空，不用置为0，减少运行时间
	//                else {
	//                    cell[i][j] = 0;
	//                }
	                /**************************************************/
	                if (cell[i][j] > maxLen) {
	                    /**************修改的地方***************************/
	                    int beforeIndex = length - 1 - i; // 反向子串末尾字符的原始索引
	                    int firstIndex =  j - cell[i][j] + 1; // 子串的首字符索引
	                    if (beforeIndex == firstIndex) { 
	                        maxLen = cell[i][j];
	                        maxEnd = j;
	                    }
	                    /**************************************************/
	                }
	            }
	        }
	        return s.substring(maxEnd + 1 - maxLen, maxEnd + 1);
	    }
	}

### 最多水的容器
	public class Solution {
	    public int maxArea(int[] height) {
	        int maxarea = 0, l = 0, r = height.length - 1;
	        while (l < r) {
	            maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r - l));
	            if (height[l] < height[r])
	                l++;
	            else
	                r--;
	        }
	        return maxarea;
	    }
	}

### 最长公共前缀
	public String longestCommonPrefix(String[] strs) {
	   if (strs.length == 0) return "";
	   String prefix = strs[0];
	   for (int i = 1; i < strs.length; i++)
	       while (strs[i].indexOf(prefix) != 0) {
	           prefix = prefix.substring(0, prefix.length() - 1);
	           if (prefix.isEmpty()) return "";
	       }        
	   return prefix;
	}

### 三数之和
	class Solution {
	    public List<List<Integer>> threeSum(int[] nums) {
	        Arrays.sort(nums);
	        List<List<Integer>> tuples = new ArrayList<>();
	        
	        for(int i = 0; i < nums.length-2; i++){
	            if(i > 0 && nums[i-1] == nums[i]) continue; //去重
	            
	            int l = i+1, r = nums.length-1;
	            if(nums[l] < 0 && Integer.MIN_VALUE-nums[l] > nums[i]) continue; //如果溢出最小值则跳过
	            if(nums[i] > 0 && Integer.MAX_VALUE-nums[l] < nums[i]) break; //溢出最大值直接结束，不可能会有新的三元组出现了
	           
	            while(l < r){
	                if(nums[r] > -nums[i]-nums[l]){
	                    while(l < r && nums[r-1] == nums[r]) r--; //右指针去重
	                    r--;
	                }
	                else if(nums[r] < -nums[i]-nums[l]){
	                    while(l < r && nums[l+1] == nums[l]) l++; //左指针去重
	                    l++;
	                }
	                else{
	                    tuples.add(Arrays.asList(nums[i],nums[l],nums[r]));
	                    while(l < r && nums[r-1] == nums[r]) r--; //左指针去重
	                    while(l < r && nums[l+1] == nums[l]) l++; //右指针去重
	                    r--;
	                    l++;
	                }
	            }
	        }
	        return tuples;
	    }
	}

### 三数之和最接近的数
	class Solution {
	    public int threeSumClosest(int[] nums, int target) {
	        Arrays.sort(nums);
	        int ans = nums[0] + nums[1] + nums[2];
	        for(int i=0;i<nums.length;i++) {
	            int start = i+1, end = nums.length - 1;
	            while(start < end) {
	                int sum = nums[start] + nums[end] + nums[i];
	                if(Math.abs(target - sum) < Math.abs(target - ans))
	                    ans = sum;
	                if(sum > target)
	                    end--;
	                else if(sum < target)
	                    start++;
	                else
	                    return ans;
	            }
	        }
	        return ans;
	    }
	}

### 电话号码的数字组合
	public class Solution {

	    private String letterMap[] = {
	            " ",    //0
	            "",     //1
	            "abc",  //2
	            "def",  //3
	            "ghi",  //4
	            "jkl",  //5
	            "mno",  //6
	            "pqrs", //7
	            "tuv",  //8
	            "wxyz"  //9
	    };

	    private ArrayList<String> res;

	    public List<String> letterCombinations(String digits) {

	        res = new ArrayList<String>();
	        if(digits.equals(""))
	            return res;

	        findCombination(digits, 0, "");
	        return res;
	    }

	    private void findCombination(String digits, int index, String s){

	        if(index == digits.length()){
	            res.add(s);
	            return;
	        }

	        Character c = digits.charAt(index);
	        String letters = letterMap[c - '0'];
	        for(int i = 0 ; i < letters.length() ; i ++){
	            findCombination(digits, index+1, s + letters.charAt(i));
	        }

	        return;
	    }

	}

### 删除链表倒数第N个节点
	class Solution{
	    public ListNode removeNthFromEnd(ListNode head){
	        ListNode A = new ListNode(-1);
	        A.next = head;
	        ListNode p = A;
	        ListNode q = A;
	        for(int i = 1; i <= n+1; i++){
	            p = p.next;
	        }
	        while (p != null){
	            p = p.next;
	            q = q.next;
	        }
	        q.next = q.next.next;
	        return A.next;
	    }
	}   

### 有效的括号
	class Solution {

	  // Hash table that takes care of the mappings.
	  private HashMap<Character, Character> mappings;

	  // Initialize hash map with mappings. This simply makes the code easier to read.
	  public Solution() {
	    this.mappings = new HashMap<Character, Character>();
	    this.mappings.put(')', '(');
	    this.mappings.put('}', '{');
	    this.mappings.put(']', '[');
	  }

	  public boolean isValid(String s) {

	    // Initialize a stack to be used in the algorithm.
	    Stack<Character> stack = new Stack<Character>();

	    for (int i = 0; i < s.length(); i++) {
	      char c = s.charAt(i);

	      // If the current character is a closing bracket.
	      if (this.mappings.containsKey(c)) {

	        // Get the top element of the stack. If the stack is empty, set a dummy value of '#'
	        char topElement = stack.empty() ? '#' : stack.pop();

	        // If the mapping for this bracket doesn't match the stack's top element, return false.
	        if (topElement != this.mappings.get(c)) {
	          return false;
	        }
	      } else {
	        // If it was an opening bracket, push to the stack.
	        stack.push(c);
	      }
	    }

	    // If the stack still contains elements, then it is an invalid expression.
	    return stack.isEmpty();
	  }
	}

### 合并两个有序链表
	class Solution {
	    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
	        // maintain an unchanging reference to node ahead of the return node.
	        ListNode prehead = new ListNode(-1);

	        ListNode prev = prehead;
	        while (l1 != null && l2 != null) {
	            if (l1.val <= l2.val) {
	                prev.next = l1;
	                l1 = l1.next;
	            } else {
	                prev.next = l2;
	                l2 = l2.next;
	            }
	            prev = prev.next;
	        }

	        // exactly one of l1 and l2 can be non-null at this point, so connect
	        // the non-null list to the end of the merged list.
	        prev.next = l1 == null ? l2 : l1;

	        return prehead.next;
	    }
	}

### 两两交换链表中的节点
	class Solution {
	    public ListNode swapPairs(ListNode head) {
	        if(head == null || head.next == null){
	            return head;
	        }
	        ListNode next = head.next;
	        head.next = swapPairs(next.next);
	        next.next = head;
	        return next;
	    }
	}

### 删除排序数组中的重复项
	public int removeDuplicates(int[] nums) {
	    if (nums.length == 0) return 0;
	    int i = 0;
	    for (int j = 1; j < nums.length; j++) {
	        if (nums[j] != nums[i]) {
	            i++;
	            nums[i] = nums[j];
	        }
	    }
	    return i + 1;
	}

### 移除数组中指定元素
	class Solution {
	    public int removeElement(int[] nums, int val) {
	        if (nums.length == 0) {
	            return 0;
	        }
	        
	        int index = 0;
	        for (int i = 0; i < nums.length; i ++) {
	            if (nums[i] != val) {
	                nums[index] = nums[i];
	                index ++;
	            }
	        }
	        return index + 1;
	    }
	}

### 矩阵旋转90度
	class Solution {
	    public void rotate(int[][] matrix) {
	        if(matrix.length == 0 || matrix.length != matrix[0].length) {
	            return;
	        }
	        int nums = matrix.length;
	        int times = 0;
	        while(times <= (nums >> 1)){
	            int len = nums - (times << 1);
	            for(int i = 0; i < len - 1; ++i){
	                int temp = matrix[times][times + i];
	                matrix[times][times + i] = matrix[times + len - i - 1][times];
	                matrix[times + len - i - 1][times] = matrix[times + len - 1][times + len - i - 1];
	                matrix[times + len - 1][times + len - i - 1] = matrix[times + i][times + len - 1];
	                matrix[times + i][times + len - 1] = temp;
	            }
	            ++times;
	        }       
	    }
	}

### 幂次方
	class Solution {
	    public double myPow(double x, int n) {
	        long N = n;
	        if (N < 0) {
	            x = 1 / x;
	            N = -N;
	        }
	        double ans = 1;
	        double current_product = x;
	        for (long i = N; i > 0; i /= 2) {
	            if ((i % 2) == 1) {
	                ans = ans * current_product;
	            }
	            current_product = current_product * current_product;
	        }
	        return ans;
	    }
	}

### 最大子序列的和
	class Solution {
	    public int maxSubArray(int[] nums) {
	        int ans = nums[0];
	        int sum = 0;
	        for(int num: nums) {
	            if(sum > 0) {
	                sum += num;
	            } else {
	                sum = num;
	            }
	            ans = Math.max(ans, sum);
	        }
	        return ans;
	    }
	}

### 矩阵顺时针输出
	class Solution {
		public List<Integer> spiralOrder(int[][] matrix) {
		        if (matrix.length==0) return new ArrayList<>();
		        if (matrix[0].length==0) return new ArrayList<>();
		        int rowStart = 0;
		        int rowEnd = matrix.length-1;
		        int colStart = 0;
		        int colEnd = matrix[0].length-1;
		        List<Integer> list = new ArrayList<>();
		        int count =0;
		        int total = matrix.length*matrix[0].length;
		        boolean flag = false;
		        while (count < total){
		            for (int i=colStart;i<=colEnd;i++){
		                list.add(matrix[rowStart][i]);
		                count++;

		            }
		            rowStart++;
		            if (count>=total) break;
		            for (int i=rowStart;i<=rowEnd;i++){
		                list.add(matrix[i][colEnd]);
		                count++;
		                flag = true;
		            }
		            colEnd--;
		            if (count>=total) break;
		            for (int i=colEnd;i>=colStart;i--){
		                list.add(matrix[rowEnd][i]);
		                count++;

		            }
		            rowEnd--;
		            if (count>=total) break;

		            for (int i = rowEnd;i>=rowStart;i--){
		                list.add(matrix[i][colStart]);
		                count++;

		            }
		            colStart++;
		            if (count>=total) break;

		        }
		        return list;
		    }
	}

### 跳跃游戏
	class Solution {
	    public boolean canJump(int[] nums) {
	        
	        if (nums == null) {
	            return false;
	        }
	        int lastPosition = nums.length - 1;
	        for (int i = nums.length - 1; i >= 0; i--) {
	            // 逐步向前递推
	            if (nums[i] + i >= lastPosition) {
	                lastPosition = i;
	            }
	        }
	        return lastPosition == 0;
	    }
	}

### 旋转链表
	class Solution {
	  public ListNode rotateRight(ListNode head, int k) {
	    // base cases
	    if (head == null) return null;
	    if (head.next == null) return head;

	    // close the linked list into the ring
	    ListNode old_tail = head;
	    int n;
	    for(n = 1; old_tail.next != null; n++)
	      old_tail = old_tail.next;
	    old_tail.next = head;

	    // find new tail : (n - k % n - 1)th node
	    // and new head : (n - k % n)th node
	    ListNode new_tail = head;
	    for (int i = 0; i < n - k % n - 1; i++)
	      new_tail = new_tail.next;
	    ListNode new_head = new_tail.next;

	    // break the ring
	    new_tail.next = null;

	    return new_head;
	  }
	}

### 不同路径（矩阵从左上角到右下角的路径数）
	class Solution {
	    public int uniquePaths(int m, int n) {
	        int[] cur = new int[n];
	        Arrays.fill(cur,1);
	        for (int i = 1; i < m;i++){
	            for (int j = 1; j < n; j++){
	                cur[j] += cur[j-1] ;
	            }
	        }
	        return cur[n-1];
	    }
	}

### 最小路径（矩阵从左上角到右下角的最小路径）
	public class Solution {
	    public int minPathSum(int[][] grid) {
	        for (int i = grid.length - 1; i >= 0; i--) {
	            for (int j = grid[0].length - 1; j >= 0; j--) {
	                if(i == grid.length - 1 && j != grid[0].length - 1)
	                    grid[i][j] = grid[i][j] +  grid[i][j + 1];
	                else if(j == grid[0].length - 1 && i != grid.length - 1)
	                    grid[i][j] = grid[i][j] + grid[i + 1][j];
	                else if(j != grid[0].length - 1 && i != grid.length - 1)
	                    grid[i][j] = grid[i][j] + Math.min(grid[i + 1][j],grid[i][j + 1]);
	            }
	        }
	        return grid[0][0];
	    }
	}

### 加一（给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。）
	class Solution {
	    public int[] plusOne(int[] digits) {
	        for (int i = digits.length - 1; i >= 0; i--) {
	            digits[i]++;
	            digits[i] = digits[i] % 10;
	            if (digits[i] != 0) return digits;
	        }
	        digits = new int[digits.length + 1];
	        digits[0] = 1;
	        return digits;
	    }
	}

### 搜索二维矩阵（矩阵从左到右升序，每行第一个数大于前一行的最后一个数）
	class Solution {
	  public boolean searchMatrix(int[][] matrix, int target) {
	    int m = matrix.length;
	    if (m == 0) return false;
	    int n = matrix[0].length;

	    // 二分查找
	    int left = 0, right = m * n - 1;
	    int pivotIdx, pivotElement;
	    while (left <= right) {
	      pivotIdx = (left + right) / 2;
	      pivotElement = matrix[pivotIdx / n][pivotIdx % n];
	      if (target == pivotElement) return true;
	      else {
	        if (target < pivotElement) right = pivotIdx - 1;
	        else left = pivotIdx + 1;
	      }
	    }
	    return false;
	  }
	}

### 子集
	class Solution {
	    public List<List<Integer>> subsets(int[] nums) {
	        List<List<Integer>> res = new ArrayList<>();
	        backtrack(0, nums, res, new ArrayList<Integer>());
	        return res;

	    }

	    private void backtrack(int i, int[] nums, List<List<Integer>> res, ArrayList<Integer> tmp) {
	        res.add(new ArrayList<>(tmp));
	        for (int j = i; j < nums.length; j++) {
	            tmp.add(nums[j]);
	            backtrack(j + 1, nums, res, tmp);
	            tmp.remove(tmp.size() - 1);
	        }
	    }
	}

### 删除链表中重复的元素（只出现一次）
	public ListNode deleteDuplicates(ListNode head) {
	    ListNode current = head;
	    while (current != null && current.next != null) {
	        if (current.next.val == current.val) {
	            current.next = current.next.next;
	        } else {
	            current = current.next;
	        }
	    }
	    return head;
	}


### 删除链表中重复的元素（一次都不出现）
	class Solution {
	    public ListNode deleteDuplicates(ListNode head) {
	        if (head == null)  return head;
	        if (head.next != null && head.val == head.next.val) {
	            while (head.next != null && head.val == head.next.val) {
	                head = head.next;
	            }
	            return deleteDuplicates(head.next);
	        }
	        else head.next = deleteDuplicates(head.next);
	        return head;    
	    }
	}

### 合并有序数组
	class Solution {
	  public void merge(int[] nums1, int m, int[] nums2, int n) {
	    // Make a copy of nums1.
	    int [] nums1_copy = new int[m];
	    System.arraycopy(nums1, 0, nums1_copy, 0, m);

	    // Two get pointers for nums1_copy and nums2.
	    int p1 = 0;
	    int p2 = 0;

	    // Set pointer for nums1
	    int p = 0;

	    // Compare elements from nums1_copy and nums2
	    // and add the smallest one into nums1.
	    while ((p1 < m) && (p2 < n))
	      nums1[p++] = (nums1_copy[p1] < nums2[p2]) ? nums1_copy[p1++] : nums2[p2++];

	    // if there are still elements to add
	    if (p1 < m)
	      System.arraycopy(nums1_copy, p1, nums1, p1 + p2, m + n - p1 - p2);
	    if (p2 < n)
	      System.arraycopy(nums2, p2, nums1, p1 + p2, m + n - p1 - p2);
	  }
	}


### 镜像对称二叉树
	public boolean isSymmetric(TreeNode root) {
	    return isMirror(root, root);
	}

	public boolean isMirror(TreeNode t1, TreeNode t2) {
	    if (t1 == null && t2 == null) return true;
	    if (t1 == null || t2 == null) return false;
	    return (t1.val == t2.val)
	        && isMirror(t1.right, t2.left)
	        && isMirror(t1.left, t2.right);
	}

### 二叉树的层序遍历
	class Solution {
	    public List<List<Integer>> levelOrder(TreeNode root) {
	        if(root == null) return new ArrayList<>();
	        List<TreeNode> cur = new ArrayList<>(), nex = new ArrayList<>();
	        cur.add(root);
	        List<List<Integer>> res = new ArrayList<>();
	        List<Integer> tmp = new ArrayList<>();
	        while(cur.size() > 0){
	            for(TreeNode r : cur) {
	                tmp.add(r.val);
	                if(r.left != null) nex.add(r.left);
	                if(r.right != null) nex.add(r.right);
	            }
	            res.add(tmp);
	            cur = nex;
	            tmp = new ArrayList<>();
	            nex = new ArrayList<>();
	        }
	        return res;
	    }
	}

### Z型输出二叉树
	class Solution {
	    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
	        List<List<Integer>> res = new ArrayList<>();
	        helper(res, root, 0);
	        return res;

	    }

	    private void helper(List<List<Integer>> res, TreeNode root, int depth) {
	        if (root == null) return;
	        if (res.size() == depth) res.add(new LinkedList<>());
	        if (depth % 2 == 0) res.get(depth).add(root.val);
	        else res.get(depth).add(0, root.val);
	        helper(res, root.left, depth + 1);
	        helper(res, root.right, depth + 1);
	    }
	}

### 从前序与中序遍历序列构造二叉树
	class Solution {
	    public TreeNode buildTree(int[] preorder, int[] inorder) {
	        return build(preorder, 0, inorder, 0, inorder.length);
	    }
	    private TreeNode build(int[] preorder, int p, int[] inorder, int i, int j){
	        if(i >= j) return null;
	        TreeNode root = new TreeNode(preorder[p]);
	        int k = 0;
	        while(inorder[k] != root.val) k++;
	        root.left = build(preorder, p + 1, inorder, i, k);
	        root.right = build(preorder, p + 1 + k - i, inorder, k + 1, j);
	        return root;
	    }
	}

### 从中序与后序遍历序列构造二叉树
	public class Solution {

	    private int[] inorder;
	    private int[] postorder;


	    public TreeNode buildTree(int[] inorder, int[] postorder) {
	        this.inorder = inorder;
	        this.postorder = postorder;
	        int len = inorder.length;
	        return dfs(0, len - 1, 0, len - 1);
	    }


	    private TreeNode dfs(int inl, int inr, int postl, int postr) {
	        if (inl > inr || postl > postr) {
	            return null;
	        }

	        int val = postorder[postr];
	        int k = 0;
	        for (int i = inl; i < inr + 1; i++) {
	            if (inorder[i] == val) {
	                k = i;
	                break;
	            }
	        }

	        TreeNode root = new TreeNode(val);
	        // 注意：第 4 个参数是计算出来的，依据：两边区间长度相等
	        root.left = dfs(inl, k - 1, postl, k - 1 - inl + postl);
	        // 注意：第 3 个参数是计算出来的，依据：两边区间长度相等
	        root.right = dfs(k + 1, inr, postr + k - inr, postr - 1);
	        return root;
	    }

	    public static void main(String[] args) {
	        int[] inorder = {1, 3, 2};
	        int[] postorder = {3, 2, 1};

	        Solution solution = new Solution();

	        TreeNode res = solution.buildTree(inorder, postorder);
	        System.out.println(res);
	    }
	}

### 路径之和
	class Solution {
	  public boolean hasPathSum(TreeNode root, int sum) {
	    if (root == null)
	      return false;

	    sum -= root.val;
	    if ((root.left == null) && (root.right == null))
	      return (sum == 0);
	    return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
	  }
	}

### LRU缓存机制
	class LRUCache extends LinkedHashMap<Integer, Integer>{
	    private int capacity;
	    
	    public LRUCache(int capacity) {
	        super(capacity, 0.75F, true);
	        this.capacity = capacity;
	    }

	    public int get(int key) {
	        return super.getOrDefault(key, -1);
	    }

	    public void put(int key, int value) {
	        super.put(key, value);
	    }

	    @Override
	    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
	        return size() > capacity; 
	    }
	}
