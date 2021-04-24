## Question 1 

Given:

![foto1](images/test1_1.png)

```java
BiPredicate<Path, BasicFileAttributes> pred = (path, fileAttrs) -> {
    return fileAttrs.isDirectory();
};
int depth = 1;
try (var stream = Files.find(Paths.get("/continent"), depth, pred)) {
    stream.forEach(System.out::println);
} catch (IOException e) { 
    e.printStackTrace();
}
```
### References: 
[Files.find](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/nio/file/Files.html#find(java.nio.file.Path,int,java.util.function.BiPredicate,java.nio.file.FileVisitOption...))

### Answer
```bash
resources\continent
resources\continent\country
```

---

## Question 2

Given
```java
    Consumer<String> c1 = arg -> System.out.println(arg);
    c1.accept("c1 accepted");
    Consumer<String> c2 = arg -> System.out.println(arg);
    c2.accept("c2 accepted");
    c2.andThen(c1).accept("after then");
    c2.accept("c2 accepted again");
```
### References

**The java.util.function.Consumer<T>** interface defines an abstract method named **accept** that takes an object of generic type T and returns no result (void).

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```
method **andThen** returns a composed Consumer that performs, in sequence, for the current operation followed by the after operation.
```java
    Consumer<String> c = (x) -> System.out.println(x.toLowerCase());
    c.andThen(c).accept("Java2s.com");

    // java2s.com
    // java2s.com

    List<Integer> values = Arrays.asList(2,4,6,8);
    Consumer<Integer> c = i -> System.out.println( i );

    values.forEach( c ); 
    // or values.foreach( i -> System.out.println( i ));
```
VIDEO: [Consumer example](https://www.youtube.com/watch?v=5uJ8jSf-c9g)

### Answer

c1 accepted
c2 accepted
after then
after then
c2 accepted again

---

## Question 3

Which two statements inserted independently at line 1 enable this code to print *PRRT*?
```java
	public static void main(String[] args) {
		StringBuilder txt1 = new StringBuilder("PPQRRRSTT");
		int i = 0;
		a: while (i < txt1.length()) {
			char x = txt1.charAt(i);
			int j = 0;
			i++;
			b: while (j < txt1.length()) {
				char y = txt1.charAt(j);
				if (i != j && y == x) {
					txt1.deleteCharAt(j);
					// line 1
				}
				j++;
			}
		}
		System.out.println(txt1);
	}
```

### References

Java does not support goto, it is reserved as a keyword just in case they wanted to add it to a later version.

Unlike C/C++, Java does not have goto statement, but java supports label.
The only place where a label is useful in Java is right before nested loop statements.
We can specify label name with break to break out a specific outer loop.
Similarly, label name can be specified with continue.

```java
public class Main {
	public static void main(String[] args)	{

	outer:
		for (int i = 0; i < 10; i++) {
			for (int j = 0; j < 10; j++) {
				if (j == 1)
					break outer;
				System.out.println(" value of j = " + j);
			}
		}
	}
}

// value of j = 0
```
VIDEO: [How to use Labeled Break Statement in Java](https://www.youtube.com/watch?v=JlRgBWWYOSE)

### Answer

```java
break b;
//or
continue a;
```

---
## Question 4

give
```java
import java.io.Serializable;

enum Color implements Serializable {
    R(1),G(2),B(3);
    int c;
    
    public Color(int c) {
        this.c = c;
    }
}
```
### References

Doc: [Java Enums](http://tutorials.jenkov.com/java/enums.html)
Video: [enum in Java](https://www.youtube.com/watch?v=sI4utYmh7O4)

### Answer
```bash
// replace *public Color(int c) {* with *private Color(int c) {*
```

---

## Question 5

```java
public class Test {
    public static void main(String[] args) {
        Locale.setDefault(Locale.FRANCE);
        ResourceBundle msg = ResourceBundle.getBundle("MessageBundle", new Locale("ru"));
        System.out.println("User " + msg.getString("username"));
        System.out.println("Pass " + msg.getString("password"));
    }
}
```

```properties
# MessagesBundle.properties
username=NORMALLL
password=NORMALLL

# MessagesBundle_fr_FR.properties
username=FRFRFRFR
password=frfrfrfrfr

# MessagesBundle_ru.properties
username=RURURURU
password=rurururu
```


### References

Doc: [A Guide to the ResourceBundle](https://www.baeldung.com/java-resourcebundle)
Video: [Curso de Java #95: ResourceBundle](https://www.youtube.com/watch?v=3yr9PBzi6Mw)


### Answer

```bash
MissingResourceException
An insidious question. There is an error in just one letter: "MessageBundle" instead of "MessagesBundle". If it were not for this error, then the content in Russian would be displayed in the console.
```
---

### Question 7

```java

a.-    interface MyRunnable{
            @FunctionalInterface
            public void run();
       }

b.-    @FunctionalInterface
       interface  MyRunnable{} 

c.-     @FunctionalInterface
        interface MyRunnable{
            public default void run() {}
            public void run(String s);  
        }

d.-     @FunctionalInterface
        interface MyRunnable{
            public void run();
            public void call();
        }
```

### Reference

A functional interface in Java is an interface **that contains only a single abstract (unimplemented) method**. A functional interface can contain default and static methods which do have an implementation, in addition to the single unimplemented method.

It's recommended that all functional interfaces have an informative **@FunctionalInterface** annotation. This clearly communicates the purpose of the interface, and also allows a compiler to generate an error if the annotated interface does not satisfy the conditions.

- Doc: [Java Functional Interfaces](http://tutorials.jenkov.com/java-functional-programming/functional-interfaces.html)
- Doc: [Functional Interfaces in Java 8](https://www.baeldung.com/java-8-functional-interfaces)
- Video: [Functional Interface](https://www.youtube.com/watch?v=lhSx1HWaMDw)

### Answer

```java
c.-     @FunctionalInterface
        interface MyRunnable{
            public default void run() {}
            public void run(String s);  
        }
```
---
### Question 8

```java
var numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
// line 1
StringBuilder sb = new StringBuilder();
for (int a : numbers) {
    sb.append(f.apply(a));
    sb.append(" ");
}
System.out.println(sb.toString());
```
Which statement on line 1 enables this code to compile?

### reference

The **java.util.function.Function<T, R>** interface defines an abstract method named apply that takes an object of generic type T as input and returns an object of generic type R.

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}

Function<Integer> x = (x) -> x * 2; 
```

### Answer
```java
Function<Integer,Integer> f = ( x ) -> x * 2; 
```
---
## Question 9

```java
public final class X {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String toString() { return getName(); }
}
```
and
```java
public class Y  extends X {
    public Y(String name) {
        super();
        setName(name);
    }
    public static void main(String[] args) {
        Y y = new Y("HH");
        System.out.println(y);
    }
}
```
What is the result?

### References


### Answer
```bash
A trick question. Without an IDE, **its easy to overlook inheritance from a final class.
```

---
## Question 10

```java
try(Connection conn = DriverManager.getConnection(url, userName, pass);
    PreparedStatement ps = conn.prepareStatement("INSERT INTO EMP VALUES(?, ?, ?) ")) {
        ps.setObject(1, 101, JDBCType.INTEGER);
        ps.setObject(2, "SMITH", JDBCType.VARCHAR);
        ps.setObject(3, "HR", JDBCType.VARCHAR);
        ps.executeUpdate();
        ps.setInt(1, 102);
        ps.setString(2, "JONES");
        ps.executeUpdate();
    }
```
What does executing this code fragment do?

### References

6.1.5 Sending JDBC NULL as an IN parameter

The setNull method allows a programmer to send a JDBC NULL (a generic SQL NULL) value to the database as an IN parameter. Note, however, that one must still specify the JDBC type of the parameter.

A JDBC NULL will also be sent to the database when a Java null value is passed to a setXXX method (if it takes Java objects as arguments). The method setObject, however, can take a null value only if the JDBC type is specified.

So yes they're equivalent.

### Answer

Inserta dos registro : 101 ,smith,HR  y  102,jones,HR

---

## Question 11

```java
public class Tester {
    public static int reduce(int x) {
        int y = 4;
        class Computer {
            int reduce(int x) {
                return x-y--;
            }
        }
        Computer a = new Computer();
        return a.reduce(x);
    }
    public static void main(String[] args) {
        System.out.println(reduce(1));
    }
}
```
What is the result?

### References


### Answer

```bash
Compilations fail
```

---

## Question 12

```java
 1  {
 2    Iterator loop = List.of(1, 2, 3).iterator();
 3    while (loop.hasNext()) {
 4        foo(loop.next());
 5    }
 6    Iterator loop2 = List.of(1, 2, 3).iterator();
 7    while (loop2.hasNext()) {
 8        bar(loop2.next());
 9    }
10  }
11    for (Iterator loop2 = List.of(1,2,3).iterator(); loop.hasNext(); ) {
12        bar(loop2.next());
13    }
14    for (Iterator loop = List.of(1,2,3).iterator(); loop.hasNext(); ) {
15        bar(loop.next());
16    }
```

Which loop incurs a compile time error? 3 , 11 , 7 or 14.

### References

*Syntax of for loop:*
```java
for(initialization; condition ; increment/decrement)
{
   statement(s);
}
```
*Flow of Execution of the for Loop*

![For](images/test1_12.png)


### Answers

Error de compilacion.. linea 11 , la variable lopp esta fuera del scope { }  declarado.

---

## Question 13

```java
public class Main {
    public static void main(String[] args) {
        var lst = List.of(1, 2.0f, "4.0");
        for (var c : lst) {
            System.out.println("> " + c);
        }
        System.out.println();
        lst.add(2, 3);                                //line n1
        for (int c = 0; c < lst.size(); c++) {
            display(lst.get(c));
        }
    }
 
    public static void display(var c) {               //line n2
        System.out.println("> " + c);
    }
}
```

### References

he following are places where you cannot use local variable type inference:

    a) You can’t use local variable type inference with method arguments.
    --> public void countNumberOfFiles(var fileList) // Error de compilacion no puede usar var como parametro del metodo.

    b) You cannot initialize a var variable to null. By assigning null, it is not clear what the type should be, since in Java, any object reference can be null.
    --> var count = null;  // no puede ser null pero si un objeto declarado "var count = myClass"  donde String myClass = null;

   c) You can’t use local variable type inference with lambda expressions, because those require an explicit target type.
   --> var z = () -> {}  // Error de compilacion no puede declarar como una expresion lambda.

### Answer

Error de compilacion

---

## Question 14

```java
public class Menu {
    enum Machine {
        AUTO("Truck"), MEDICAL("Scanner");
        private String type;
        private Machine(String type) {
            this.type = type;
        }
        private void setType(String type) {
            this.type = type;                               //line 1
        }
        private String getType() {
            return type;
        }
    }
    public static void main(String[] args) {
        Machine.AUTO.setType("Sedan");                      //line 2
        for (Machine p : Machine.values()) {
            System.out.println(p + ": " + p.getType());     //line 3
        }
    }
}
```
What is the result?

## References

## Answer

Machine.AUTO: Sedan
Machine.MEDICAL.Scanner

---

## Question 15

Given:
```java
public class MyResource {
    public MyResource() {
    }
    //Resource methods
}
```
You want to use the MyResource class in a try-with-resources statement.

Which change will accomplish this?

### References

Java 7 introdujo el statement try-with-resources que se encarga de cerrar un recurso creado en el try.

Para usarlo basta implementar el interfaz AutoCloseable.
El método close() se llama de forma automática incluso aunque se lance una excepción.

Doc : [Clases AutoCloseable en Java](https://unpocodejava.com/2017/07/23/clases-autocloseable-en-java/)

Video: [Java 7 feature: try-with-resources Statement](https://www.youtube.com/watch?v=7Yxnh40ds2Q)

### Answer

```java
public class MyResource implements Autocloseable{
    public MyResource() {
    }
    @Override
    public void close() {        

    }
}
```
---
## Question 16

Given the code fragment:
```java
int i = 0;
for (; i < 10; i++) {
    System.out.println(++i + " ");
}
```
What is the result?

### References


### Answer
```bash
1 3 5 7 9
```

---

## Question 17

Given:
```java
class CustomType<T> {
    public <T> int count(T[] anArray, T element) {
        int count = 0;
        for (T e : anArray) {
            if (e.equals(element)) ++count;
        }
        return count;
    }
}
```
And
```java
public class Test extends CustomType {
    public static void main(String[] args) {
        String[] words = {"banana", "orange", "apple", "lemon"};
        Integer[] numbers = {1,2,3,4,5};
        CustomType type = new CustomType();
        CustomType<String> stringType = new CustomType<>();
        System.out.println(stringType.count(words, "apple"));
        System.out.println(type.count(words, "apple"));
        System.out.println(type.count(numbers, 3));
    }
}
```
What is the result?

### References

### Answer
 ```bash
 1 
 1 
 1
```
---

## Question 18

Given:
```java
import java.io.FileNotFoundException;
import java.io.IOException;
 
public class Tester {
    public static void main(String[] args) {
        try {
            doA();
        } //line 1
    }
    private static void doA() throws Exception, IndexOutOfBoundsException {
        if (false) { 
            throw new FileNotFoundException();
        } else {
            throw new IndexOutOfBoundsException();
        }
    }
}
```
What must be added in line 1 to compile this class?

### References

Doc: [Exception Handling in Java](https://www.baeldung.com/java-exceptions)
Video: [Java Exceptions - Learn Exceptions in Java](https://www.youtube.com/watch?v=xNVlq9IEBEg)

### Answer
```java
catch(Exception e){

}
```
---

## Question 19

Given:
```java
public class Point {
    @JsonField(type=JsonField.Type.STRING, name="name")
    private String _name;
 
    @JsonField(type = JsonField.Type.INT)
    private int x;
 
    @JsonField(type = JsonField.Type.INT)
    private int y;
 
    public static void main(String[] args) {
        new Point();
    }
}


```
What is the correct definition of the JsonField annotation that makes the Point class compile?

## References

**Java annotations** are typically used for the following purposes:

* Compiler instructions
* Build-time instructions
* Runtime instructions

### @Retention

You can specify for your custom annotation if it should be available at runtime, for inspection via reflection.

* **@Retention(RetentionPolicy.RUNTIME)**.- This is what signals to the Java compiler and JVM that the annotation should be available via reflection at runtime.[Java Reflection Annotations](http://tutorials.jenkov.com/java-reflection/annotations.html)

* **@Retention(RetentionPolicy.CLASS)**.- means that the annotation is stored in the .class file, but not available at runtime. This is the default retention policy, if you do not specify any retention policy at all.

* **@Retention(RetentionPolicy.SOURCE)** .- means that the annotation is only available in the source code, and not in the .class files and not a runtime. If you create your own annotations for use with build tools that scan the code, you can use this retention policy. That way the .class files are not polluted unnecessarily.

### @Target

You can specify which **Java elements** your custom annotation can be used to annotate.

The ElementType class contains the following possible targets:

- ElementType.ANNOTATION_TYPE (the annotation can only be used to annotate other annotations)
- ElementType.CONSTRUCTOR
- ElementType.FIELD
- ElementType.LOCAL_VARIABLE
- ElementType.METHOD
- ElementType.PACKAGE
- ElementType.PARAMETER
- ElementType.TYPE (A type is either a class, interface, enum or annotation)
- ElementType.TYPE_PARAMETER
- ElementType.TYPE_USE

### @Inherited

The @Inherited annotation signals that a custom Java annotation used in a class should be inherited by subclasses inheriting from that class.

### @Documented

The @Documented annotation is used to signal to the JavaDoc tool that your custom annotation should be visible in the JavaDoc for classes using your custom annotation.

### Example

- the java annnotation

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)

public @interface MyAnnotation {
    public String name();
    public String value();
}
```
- the java class

```java
@MyAnnotation(name="someName",  value = "Hello World")
public class TheClass {
}
``` 
- the method annotations

```java
public class TheClass {
  @MyAnnotation(name="someName",  value = "Hello World")
  public void doSomething(){}
}
```
- the parameter annotations
```java
public class TheClass {
  public static void doSomethingElse(
        @MyAnnotation(name="aName", value="aValue") String parameter){
  }
}
```
- the field annotations

```java
Method method = ... //obtain method object
Annotation[][] parameterAnnotations = method.getParameterAnnotations();
Class[] parameterTypes = method.getParameterTypes();

int i=0;
for(Annotation[] annotations : parameterAnnotations){
  Class parameterType = parameterTypes[i++];

  for(Annotation annotation : annotations){
    if(annotation instanceof MyAnnotation){
        MyAnnotation myAnnotation = (MyAnnotation) annotation;
        System.out.println("param: " + parameterType.getName());
        System.out.println("name : " + myAnnotation.name());
        System.out.println("value: " + myAnnotation.value());
    }
  }
}
```

- Class Annotations

```java
Class aClass = TheClass.class;
Annotation[] annotations = aClass.getAnnotations();

for(Annotation annotation : annotations){
    if(annotation instanceof MyAnnotation){
        MyAnnotation myAnnotation = (MyAnnotation) annotation;
        System.out.println("name: " + myAnnotation.name());
        System.out.println("value: " + myAnnotation.value());
    }
}
```

- Method Annotations

```java
Method method = ... // obtain method object
Annotation annotation = method.getAnnotation(MyAnnotation.class);

if(annotation instanceof MyAnnotation){
    MyAnnotation myAnnotation = (MyAnnotation) annotation;
    System.out.println("name: " + myAnnotation.name());
    System.out.println("value: " + myAnnotation.value());
}
```
- Parameter Annotations

```java
Method method = ... //obtain method object
Annotation[][] parameterAnnotations = method.getParameterAnnotations();
Class[] parameterTypes = method.getParameterTypes();

int i=0;
for(Annotation[] annotations : parameterAnnotations){
  Class parameterType = parameterTypes[i++];

  for(Annotation annotation : annotations){
    if(annotation instanceof MyAnnotation){
        MyAnnotation myAnnotation = (MyAnnotation) annotation;
        System.out.println("param: " + parameterType.getName());
        System.out.println("name : " + myAnnotation.name());
        System.out.println("value: " + myAnnotation.value());
    }
  }
}
```

- Field Annotations

```java
Field field = ... //obtain field object
Annotation[] annotations = field.getDeclaredAnnotations();

for(Annotation annotation : annotations){
    if(annotation instanceof MyAnnotation){
        MyAnnotation myAnnotation = (MyAnnotation) annotation;
        System.out.println("name: " + myAnnotation.name());
        System.out.println("value: " + myAnnotation.value());
    }
}
```

Doc: [Java Annotations](http://tutorials.jenkov.com/java/annotations.html)
Video1:[Java Annotations #1 - The Basics](https://www.youtube.com/watch?v=0VPRkVWkM70)
Video2:[Java Annotations #2 - Create your own custom Java Annotations](https://www.youtube.com/watch?v=UlhtkjfxUUU)

https://docs.oracle.com/javase/tutorial/java/annotations/index.html

### Answer

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD)
public @interface JsonField {
    String name() default "";
    enum Type {
        INT, STRING
    }
    Type type();
}
```
---

## Question 20

Given:

```java
    List<String> list1 = new ArrayList<>();
    list1.add("A");
    list1.add("B");
    List list2 = List.copyOf(list1);
    list2.add("C");
    List<List<String>> lists = List.of(list1, list2);
    System.out.println(lists);
```
What is the result?

### References

**Unmodifiable Lists**
The **List.of** and **List.copyOf** static factory methods provide a convenient way to create unmodifiable lists. The List instances created by these methods have the following characteristics:

- They are unmodifiable. Elements cannot be added, removed, or replaced. Calling any mutator method on the List will always cause **UnsupportedOperationException** to be thrown. However, if the contained elements are themselves mutable, this may cause the List's contents to appear to change.
- They disallow null elements. Attempts to create them with null elements result in **NullPointerException**.
- They are serializable if all elements are serializable.
- The order of elements in the list is the same as the order of the provided arguments, or of the elements in the provided array.
- They are value-based. Callers should make no assumptions about the identity of the returned instances. Factories are free to create new instances or reuse existing ones. Therefore, identity-sensitive operations on these instances (reference equality (==), identity hash code, and synchronization) are unreliable and should be avoided.
They are serialized as specified on the Serialized Form page.

```java
		List<String> lista1 = new ArrayList<String>();
		lista1.add("A");
		lista1.add("B");
		List<String> lista2 = List.copyOf(lista1);
		lista2.add("C");
```
```bash
Exception in thread "main" java.lang.UnsupportedOperationException
```

- Doc [List.copyOf](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/List.html#copyOf(java.util.Collection))

### Answer


---

## Question 22

Given:
```java
public interface TestInterface {
    default void samplingProbeProcedure() {
        probeProcedure();
        System.out.println("Collect Sample");
        System.out.println("Leave Asteroid");
        System.out.println("Dock with Main Craft");
    }
    default void explosionProbeProcedure() {
        probeProcedure();
        System.out.println("Explode");
    }
}
```
Examine these requirements:
    - Eliminate code duplication.
    - Keep constant the number of methods other classes may implement from this interface.

Which method can be added to meet these requirements?

### References

To work with extensible applications, we need to understand the following terms:

- **Service Provider Interface**: A set of interfaces or abstract classes that a service defines. It represents the classes and methods available to your application.
- **Service Provider**: Called also Provider, is a specific implementation of a service. It is identified by placing the provider configuration file in the resources directory META-INF/services. It must be available in the application’s classpath.
- **ServiceLoader**: The main class used to discover and load a service implementation lazily. The ServiceLoader maintains a cache of services already loaded. Each time we invoke the service loader to load services, it first lists the cache’s elements in instantiation order, then discovers and instantiates the remaining providers.

```java
public static BookService getInstance(){
    ServiceLoader<BookServiceProvider> sl = ServiceLoader.load(BookServiceProvider.class);
    Iterator<BookServiceProvider> iter = sl.iterator();
    if (!iter.hasNext()){
        throw new RuntimeException("No service providers found!");
    }
    BookServiceProvider provider = null;
    while(iter.hasNext()){
        provider = iter.next();
        System.out.println(provider.getClass());
    }
    return provider.getBookService();
}
```

Doc: [Java Service Provider Interface](https://www.baeldung.com/java-spi)
Doc: [Implementing Plugins with Java's Service Provider Interface](https://reflectoring.io/service-provider-interface/)
Doc: [Java Service Provider Interface (SPI)](https://itnext.io/java-service-provider-interface-understanding-it-via-code-30e1dd45a091)

### Answer

```java
private java.util.ServiceProvider<Print> loader = ServiceProvider.load(Print.class);
```

---

## Question 23

Given:

```java
import java.util.ArrayList;
import java.util.List;
 
public class Fruit {
    public static void main(String[] args) {
        // Line 1
        List<String> fruits = new ArrayList<>(List.of("apple", "orange", "banana"));
        fruits.replaceAll(function);
    }
}
```
Which statement on line 1 enables this code fragment to compile?

## References

Doc: [Java 8 UnaryOperator Examples](https://mkyong.com/java8/java-8-unaryoperator-examples/)

## Answer

```java
UnaryOperator<String> function = String::toUppercase;
```
---

## Question 24

Given:
```java
public class Calculator {
    public static void main(String[] args) {
        MyInterface myInterface = a -> a + 1;
        System.out.println(myInterface.add(10));
    }
}
interface MyInterface {
    int add(int x);
}
```
Which interface from the java.util.function package can be used to refactor the Calculator class?

### References

```java
// FUNCTION
class MiFunction implements Function<Integer,Integer> {
	@Override
	public Integer apply(Integer arg0) {
		return arg0+1;
	}
}

// SUPPLIER
Supplier<LocalDateTime> s = () -> LocalDateTime.now();
LocalDateTime time = s.get();
System.out.println(time);

Supplier<String> s1 = () -> dtf.format(LocalDateTime.now());
String time2 = s1.get();
System.out.println(time2);

// CONSUMER
Consumer<String> print = x -> System.out.println(x);
print.accept("java");   // java

```
### Answer

```java
Function<Integer,Integer> func2 = x -> x + 1;
System.out.println( func2.apply(10) );
```
---

### Question 25

Given:
```java
public class Plant {
}

public class Tulip extends Plant{
}

public class Garden {
    private static Plant plant;
    public static void main(String[] args) {
        plant = new Tulip();
        feed(plant);
        feed(plant);
    }
    public static void feed(Plant p) {
        if (p instanceof Tulip) {
            System.out.println("Take extra care");
        }
        p = null;
    }
}
```
What is the result?

### References

### Answer

```bash
Take extra care
Take extra care
```
---

## Question 28

### Answer 
```java
static float validte3(String s , float min, float max) throws IllegalArgumentException {
    Float f = Float.parseFloat(s);
    if(!Float.isFinite(f) || f < min || f > max){
        throws new IllegalArgumentException();
    }
    return f;
}
```
### References

public static boolean isFinite(float f)
Returns true if the argument is a finite floating-point value; returns false otherwise (for NaN and infinity arguments).

---

## Question 27

Given:
```java
public class Product {
    private double price;
    public Product (double price) {
        this.price = price;
    }
    public double getPrice() { return price; }
}

public class Electronics extends Product{
    public Electronics(double price) {
        super(price);
    }
}

public class Plushy extends Product{
    public Plushy(double price) {
        super(price);
    }
}

public class PriceChecker<T extends Product> {
    private T product;
    public  PriceChecker (T product) {
        this.product = product;
    }
    public boolean isPriceEqual (PriceChecker<?> prod) {
        return this.product.getPrice() == prod.product.getPrice();
    }
 
    public static void main(String[] args) {
        PriceChecker<Electronics> a = new PriceChecker<>(new Electronics(1000.00));
        PriceChecker<Plushy> b = new PriceChecker<>(new Plushy(1.0));
        System.out.println(a.isPriceEqual(b));
    }
}
```
What change will cause the code to compile successfully?

### References

### Answer

---

## Question 28

Given the code fragment:

9    Integer[] ints = {1,2,3,4,5,6,7};
10   var list = Arrays.asList(ints);
11   UnaryOperator<Integer> uo = x -> x * 3;
12   list.replaceAll(uo);

Which can replace line 11?

### References

```java
var list = List.of(10);
int i = list.get(0); //equivalent to: var i = list.get(0);

var list2 = new ArrayList<>(); 
list2.add(10);
System.out.println(list2);
int i = list2.get(0) // ---> Compilation error
int i = (int) list2.get(0) // --> need to cast to get int back

var list3 = new ArrayList<Integer>(); 
list3.add(10); 
System.out.println(list3)
int i = list3.get(0);
```

Doc: [Explore the New Java 10 “var” Type: An Introduction and Hands-on Tutorial](https://www.infoq.com/articles/java-10-var-type/)

### Answer



---

## Question 29

Given the code fragment:

```java
public class Test {
    class L extends Exception { }
    class M extends L { }
    class N extends RuntimeException { }
    public void p() throws L { throw new M(); }
    public void q() throws N { throw new N(); }
    public static void main(String[] args) {
        try {
            Test t = new Test();
            t.p();
            t.q();
        } /* line 1 */ {
            System.out.println("Exception caught");
        }
    }
}
```
What change on line 1 will make this code compile?

### References

### Answer

---

## Question 30

Given:
```java
import java.util.*;
 
public class Main {
    static Map<String, String> map = new HashMap<>();
    static List<String> keys = new ArrayList<>(List.of("S", "p", "Q", "R"));
    static String[] values = {"senate", "people", "of", "rome"};
 
    static {
        for (var i = 0; i < keys.size(); i++) {
            map.put(keys.get(i), values[i]);
        }
    }
 
    public static void main(String[] args) {
        keys.clear();
        values = new String[0];
        System.out.println("Keys: " + keys.size() +
                " Values: " + values.length +
                " Map: " + map.size());
    }
}
```
What is the result?

### References

### Answer

---

## Question 31

Given the code fragment:
```java
ExecutorService es = Executors.newCachedThreadPool();
es.execute(() -> System.out.println("Ping"));
//line 1

Future future = (es)-> es.submit(() _> "Pong");
System.out.println(future.get()); //line 2
es.shutdown();
```
Which statement at line 1 enables to print Ping Pong?

### References

A Future represents the result of an asynchronous computation. Methods are provided to check if the computation is complete, to wait for its completion, and to retrieve the result of the computation. The result can only be retrieved using method get when the computation has completed, blocking if necessary until it is ready.

In fact, there is no need to look for an option with the correct output in this question. It is enough to quickly look through the options and realize that only one of them will allow the program to compile.

    - invokeAny - takes a Collection as input, but we suggest Callable <String>. Result: compilation error.

    - execute - returns nothing and the program waits for Future <String>. Result: compilation error.

    - call() - сomputes a result. In this example, the return type is String but the program is waiting for Future <String>. Result: compilation error.


Doc: [Guide to java.util.concurrent.Future](https://www.baeldung.com/java-future)
### Answer

---

## Question 32

Given:

```java
import java.util.Optional;
 
public class Main {
        Optional<String> value = createValue();
        String str = value.orElse("Duke");
        System.out.println(str);
    }
    
    private static Optional<String> createValue() {
        String s = null;
        return Optional.ofNullable(s);
    }
}
```
What is the output?

### References

Doc: [java.util.Optional – Un pequeño tutorial práctico](https://www.adictosaltrabajo.com/2016/05/24/java-util-optional-un-pequeno-tutorial-practico/)
Video: [Java Optional Tutorial - How to Use Optional Class In Java](https://www.youtube.com/watch?v=PlOSuPVNy7k)

### Answer

Duke

---

## Question 32

Given:
```java
public class Main {
    public static void main(String[] args) {
        try {
            Path path = Paths.get("/u01/work/filestore.txt");
            boolean result = Files.deleteIfExists(path);
            if (result) System.out.println(path + "is deleted.");
            else System.out.println(path + "is not deleted.");
        } catch (IOException e) {
            System.out.println("Exception");
        }
    }
}
```
Assume the file on path does not exist.

What is the result?

### References

- Deletes a file if it exists.
- As with the delete(Path) method, an implementation may need to examine the file to determine if the file is a directory. Consequently this method may not be atomic with respect to other file system operations. If the file is a symbolic link, then the symbolic link itself, not the final target of the link, is deleted.
- If the file is a directory then the directory must be empty. In some implementations a directory has entries for special files or links that are created when the directory is created. In such implementations a directory is considered empty when only the special entries exist.
- On some operating systems it may not be possible to remove a file when it is open and in use by this Java virtual machine or other programs.

Doc: [Files.deleteIfExists](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/nio/file/Files.html#deleteIfExists(java.nio.file.Path))

### Answer
```bash
\u01\work\filestore.txtis not deleted.
```
---

## Question 34

Given the code fragment:

```java
Path currentFile = Paths.get("/scratch/exam/temp.txt");
Path outputFile = Paths.get("/scratch/exam/new.txt");
Path directory = Paths.get("/scratch/");
Files.copy(currentFile, outputFile);
Files.copy(outputFile, directory);
Files.delete(outputFile);
```
The /scratch/exam/temp.txt file exists.
The /scratch/exam/new.txt and /scratch/new.txt files do not exist.

What is the result?

### References

FileAlreadyExistsException - if the target file exists but cannot be replaced because the REPLACE_EXISTING option is not specified (optional specific exception)

**For a program, it makes no difference, whether it is a directory or a file**. To copy the file scratch\exam\new.txt to the directory scratch/new.txt we need to change line 3. Then everything will work as planned.

Path directory = Paths.get("/scratch/new.txt");

### Answer

the program throws a FileAlreadyExistsException 

---

## question 35

Given:
```java
class Super {
    static String greeting() { return "Good Night";}
    String name() {
        return "Harry";
    }
}

class Sub extends Super {
    static String greeting() {
        return "Good Morning";
    }
    String name() {
        return "Potter";
    }
}

class Test {
    public static void main(String[] args) {
        Super s = new Sub();
        System.out.println(s.greeting() + ", " + s.name());
    }
}
```

What is the result?

### References

To give the correct answer to this question, you need to remember that **static members are called by the type of the reference, and non-static ones by the type of the object**. Just like that.


### Answer

```bash
Good Nigth!, Potter
```
---

## Question 36

Given:
```java
class Item {
    public String name;
    public int count;
    public Item(String name, int count) {
        this.name = name;
        this.count = count;
    }
}

public class Test {
    public static void main(String[] args) {
        var items = List.of(new Item("A", 10), new Item("B", 2),
            new Item("C", 12), new Item("D", 5), new Item("E", 6));
        // line 1
        if(items.stream().anyMatch(i -> i.count <0)) {
        System.out.println("There is an item for which the variable count is below zero.");
        }
    }
}
```
You want to examine the Items list if it contains an item for which the variable count is below zero?

Which code fragment at line 1 accomplish this?

### References

**anyMatch()**
The Java Stream anyMatch() method is a terminal operation that takes **a single Predicate as parameter**, starts the internal iteration of the Stream, and applies the Predicate parameter to each element. If the Predicate **returns true for any of the elements**, the anyMatch() method returns true. **If no elements match the Predicate, anyMatch() will return false**.

**allMatch()**
The Java Stream allMatch() method is a terminal operation that takes **a single Predicate as parameter**, starts the internal iteration of elements in the Stream, and applies the Predicate parameter to each element. **If the Predicate returns true for all elements in the Stream**, the allMatch() will return true. **If not all elements match the Predicate, the allMatch() method returns false.**

**noneMatch()**
The Java Stream noneMatch() method is a terminal operation that will iterate the elements in the stream and return true or false, depending on whether no elements in the stream matches the Predicate passed to noneMatch() as parameter. The noneMatch() method will **return true if no elements are matched by the Predicate, and false if one or more elements are matched**

**collect()**
The Java Stream collect() method is a terminal operation that starts the internal iteration of elements, and collects the elements in the stream in a collection or object of some kind.

**count()**
The Java Stream count() method is a terminal operation which starts the internal iteration of the elements in the Stream, and counts the elements.

**findAny()**
The Java Stream findAny() method can find a single element from the Stream. The element found can be from anywhere in the Stream. There is no guarantee about from where in the stream the element is taken.

**findFirst()**
The Java Stream findFirst() method finds the first element in the Stream, if any elements are present in the Stream. The findFirst() method returns an Optional from which you can obtain the element, 

**forEach()**
The Java Stream forEach() method is a terminal operation which starts the internal iteration of the elements in the Stream, and applies a Consumer (java.util.function.Consumer) to each element in the Stream. The forEach() method returns void.

**min()**
The Java Stream min() method is a terminal operation that returns the smallest element in the Stream. Which element is the smallest is determined by the Comparator implementation you pass to the min() method. I have explained how the Comparator interface works in my tutorial about sorting Java collections.

**max()**
The Java Stream max() method is a terminal operation that returns the largest element in the Stream. Which element is the largest is determined by the Comparator implementation you pass to the max() method. I have explained how the Comparator interface works in my tutorial about sorting Java collections.

**reduce()**
The Java Stream reduce() method is a terminal operation that can reduce all elements in the stream to a single element. 

**toArray()**
The Java Stream toArray() method is a terminal operation that starts the internal iteration of the elements in the stream, and returns an array of Object containing all the elements. 




Doc: [Java Stream API](http://tutorials.jenkov.com/java-functional-programming/streams.html)
### Answer

---

## Question 37

Given:
```java
interface MyInterface1 {
    public int method() throws Exception;
    private void pMethod() { /* an implementation of pMethod */ }
}
interface MyInterface2 {
    public static void sMethod() { /* an implementation of sMethod */ }
    public boolean equals();
}
interface MyInterface3 {
    public void method();
    public void method(String str);
}
interface MyInterface4 {
    public void dMethod() { /* an implementation of dMethod */ }
    public void method();
}
interface MyInterface5 {
    public static void sMethod();
    public void method(String str);
}
```
Which two interfaces can be used in lambda expressions?

### References

**@FunctionalInterface**
**A functional interface** in Java is an interface that contains only a single abstract (unimplemented) method. A functional interface can contain default and static methods which do have an implementation, in addition to the single unimplemented method.


### Answer
```java
@FuctionalInterface
interface MyInterface1 {
    public int method() throws Exception;
    private void pMethod() { /* an implementation of pMethod */ }
}

@FunctionalInterface
interface MyInterface2 {
    public static void sMethod() { /* an implementation of sMethod */ }
    public boolean equals();
}
```
---
## Question 38

Given:
```java
public interface AdaptorFirst {
    void showFirst();
}
```
Which three classes successfully override showFirst()?

### References



### Answer

---

## Question 39

Given the declaration:
```java
@interface Resource {
    String name();
    int priority() default 0;
}
```
Examine this code fragment:

/* Loc1 */ class ProcessOrders { }
Which two annotations may be applied at Loc1 in the code fragment? (Choose two.)

### References

### Answer

---

## Question 40

Given:
```java
public interface API { //line 1
        public void checkValue(Object value)
                throws IllegalArgumentException; //line 2
        public boolean isValueANumber (Object val) {
            if (val instanceof  Number) {
                return true;
            } else {
                try {
                    Double.parseDouble(val.toString());
                    return true;
                } catch (NumberFormatException ex) {
                    return false;
                }
            }
        }
}
```
Which two changes need to be made to make this class compile?


### References

### Answer

---

## Question 41

Given the code fragment:
```java
int x = 0;
while (x < 10) {
     System.out.print(x++);
}
```
Which “for” loop produces the same output?

### References

### Answer

for(int x = 0; x < 10 ; ){
    System.out.print(x++);
}

---

## Question 42

Given:
```java
public class Foo {
    private final ReentrantLock lock = new ReentrantLock();
    private Thread.State state;
    public void foo() throws Exception {
        try {
            lock.lock();
            state.mutate();
        }
        finally {
            lock.unlock();
        }
    }
}
```

What is required to make the Foo class thread safe?

### References

### Answer

---

## Question 43

Given:
```java
public interface A {
    abstract void x();
}

public abstract class B /* position 1*/{
    /* position 2 */
    public void x() { }
    public abstract void z();
}

public class C extends B implements A{
     /* position 3 */
}
```
Which code, when inserted at one or more marked position, would allow classes B and C to compile?

### References

### Answer

```java
public class C extends B implements A{
     void x(){}

     @Override
     void z(){}
}
```


---

## Question 44

Given:
```java
List<String> list1 = new LinkedList<String>();
Set<String> hs1 = new HashSet<String>();
String[] v = {"a", "b", "c", "b", "a"};
for (String s : v) {
    list1.add(s);
    hs1.add(s);
}
System.out.print(hs1.size() + " " + list1.size() + " "); 3 - 5
HashSet hs2 = new HashSet(list1); 3
LinkedList list2 = new LinkedList(hs1); 3
System.out.print(hs2.size() + " " + list2.size()); 3 - 3
```
What is the result?

### References

* HasSet
```java
import java.util.HashSet;
public class HashSetExample {
   public static void main(String args[]) {
      // HashSet declaration
      HashSet<String> hset = new HashSet<String>();
      // Adding elements to the HashSet
      hset.add("Apple");
      hset.add("Mango");
      hset.add("Grapes");
      hset.add("Orange");
      hset.add("Fig");
      //Addition of duplicate elements
      hset.add("Apple");
      hset.add("Mango");
      //Addition of null values
      hset.add(null);
      hset.add(null);
      //Displaying HashSet elements
      System.out.println(hset);
    }
}
```
```bash
[null, Mango, Grapes, Apple, Orange, Fig]
# As you can see there all the duplicate values are not 
# present in the output including the duplicate null value.
```

* LinkedList

```java
package com.beginnersbook;
import java.util.*;
public class JavaExample{
   public static void main(String args[]){
     LinkedList<String> list=new LinkedList<String>();
     //Adding elements to the Linked list
     list.add("Steve");
     list.add("Carl");
     list.add("Raj");
     //Adding an element to the first position
     list.addFirst("Negan");
     //Adding an element to the last position
     list.addLast("Rick");
     //Adding an element to the 3rd position
     list.add(2, "Glenn");
     //Iterating LinkedList
     Iterator<String> iterator=list.iterator();
     while(iterator.hasNext()){
       System.out.println(iterator.next());
     }
   } 
} 
```
```bash
[Negan,Steve,Glenn, Carl, Raj,Rick]
```

Doc: [LinkedList in Java with Example](https://beginnersbook.com/2013/12/linkedlist-in-java-with-example/)
Doc: [HashSet Class in Java with example](https://beginnersbook.com/2013/12/hashset-class-in-java-with-example/)

### Answer
3 5 3 3

---

## Question 45

Given:
```java
public class X {
    protected void print(Object obj) {
        System.out.println(obj);
    }
    public final void print(Object... objects) {
        for (Object object : objects) {
            print(object);
        }
    }
    public void print(Collection collection) {
        collection.forEach(System.out::println);
    }
}

public class Y extends X {
    public void print(Object obj) {
        System.out.println("[" + obj + "]");
    }
    public void print(Object... objects) {
        for (Object object : objects) {
            System.out.println("[" + object + "]");
        }
    }
    public void print(Collection collection) {
        print(collection.toArray());
    }
}
```
Why does this compilation fail?

---

## Question 47

Given this enum declaration:

1    enum Alphabet {
2        A, B, C
3
4    }    

Examine this code:

System.out.println(Alphabet.getFirstLetter());

What code should be written at line 3 to make this code print A?

### References

### Answer

---

### Question 49

Given:
```java
 public class Resource {
    private boolean ready = false;
    public void processWork(Worker worker) {
        while (!worker.isFinished()) {
            System.out.println("waiting for a worker");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        setReady(true);
    }
 
    public boolean isReady() {
        return ready;
    }
 
    private void setReady(boolean ready) {
        this.ready = ready;
    }
}
class Worker {
    private boolean finished = false;
 
    public void consumeResource(Resource resource) {
        while (!resource.isReady()) {
            System.out.println("waiting for a resource");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        setFinished(true);
    }
 
    public boolean isFinished() {
        return finished;
    }
 
    private void setFinished(boolean finished) {
        this.finished = finished;
    }
}
And the code fragment:

public class Main {
    public static void main(String[] args) {
        Resource resource = new Resource();
        Worker worker = new Worker();
        Thread t1 = new Thread(() -> resource.processWork(worker));
        Thread t2 = new Thread(() -> worker.consumeResource(resource));
 
        t1.start();
        t2.start();
    }
}
```
Which situation will occur on code fragment execution?

### References

Typical problems in Java concurrency:

* Deadlock.- A deadlock is when two or more threads are blocked waiting to obtain locks that some of the other threads in the deadlock are holding. Deadlock can occur when multiple threads need the same locks, at the same time, but obtain them in different order.
* Deadlock Prevention.- In some situations it is possible to prevent deadlocks. I'll describe three techniques in this text: Lock Ordering / Lock Timeout / Deadlock Detection
* Starvation and Fairness.- The following three common causes can lead to starvation of threads in Java:
    - Threads with high priority swallow all CPU time from threads with lower priority.
    - Threads are blocked indefinately waiting to enter a synchronized block, because other threads are constantly allowed access before it.
    - Threads waiting on an object (called wait() on it) remain waiting indefinitely because other threads are constantly awakened instead of it.
* Nested Monitor Lockout.- The result of nested monitor lockout and deadlock are pretty much the same: The threads involved end up blocked forever waiting for each other.
* Slipped Conditions.- Slipped conditions means, that from the time a thread has checked a certain condition until it acts upon it, the condition has been changed by another thread so that it is errornous for the first thread to act.

Video: [Deadlock in Java](https://www.youtube.com/watch?v=3cgZbACBpxI)

### Answer

DeadLock

---

## Question 50

Given:
```java
public class Test {
    public static void doThings() throws GeneralException {
        try {
            throw new RuntimeException("Something happened");
        } catch (Exception e) {
            throw new SpecificException(e.getMessage());
        }
    }
    public static void main(String[] args) {
        try {
            Test.doThings();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
 
    class GeneralException /* line 1 */ { extends Exception 
        public GeneralException(String s) {super(s);}
    }
    class SpecificException /* line 2 */ { extends GeneralException
        public SpecificException(String s) {super(s);}
    }
```

Which option should you choose to enable to print Something happened?


---

## Other
### Modules in Java

**exports and exports…to**. An exports module directive specifies one of the module’s packages whose public types (and their nested public and protected types) should be accessible to code in all other modules. An exports…to directive enables you to specify in a comma-separated list precisely which module’s or modules’ code can access the exported package—this is known as a qualified export.

**requires**. A requires module directive specifies that this module depends on another module—this relationship is called a module dependency. Each module must explicitly state its dependencies. When module A requires module B, module A is said to read module B and module B is read by module A.

**uses**. A uses module directive specifies a service used by this module—making the module a service consumer. A service is an object of a class that implements the interface or extends the abstract class specified in the uses directive.

---

**jdeps**
jdeps is a Java class dependency analyzer. The jdeps command shows the package-level or class-level dependencies of Java class files. The input class can be a path name to a .class file, a directory, a JAR file, or it can be a fully qualified class name to analyze all class files. The options determine the output. By default, jdeps outputs the dependencies to the system output. It can generate the dependencies in DOT language


---

**@SuppressWarnings**

Below is a list of markers that can be used in the SuppressWarnings annotation:

- all - disable all warnings

- boxing - disable warnings related to casting to classes and simple types

- cast - disable warnings related to type conversion

- dep-ann - disable deprecated annotation warnings

- deprecation - disable deprecation warnings

- fallthrough - disable warnings related to missing breakpoints in select statements

- finally - disable warnings related to final locks that do not return control

- hiding - disable warnings related to local objects hiding variables

- incomplete-switch - disable warnings related to missing elements in selection statements (enum case)
 
- javadoc - disable warnings related to javadoc warnings

- nls - disable warnings related to non-nls literal strings

- null - disable warnings related to null parsing

- rawtypes - disable warnings related to the use of non-parameterized types

- resource - disable warnings related to the use of resources of type Closeable

- restriction - disable warnings related to the use of deprecated or prohibited resources

- serial - disable warnings related to missing serialVersionUID field in serializable class

- static-access - disable warnings related to invalid static access operations

- st- atic-method - disable warnings related to methods that can be defined with the static modifier

- super - disable warnings related to overriding a method without calling the base method

- synthetic-access - disable warnings related to non-optimized access from inner classes

- sync-override - disable warnings due to lack of synchronization when overriding a synchronized method

- unchecked - disable warnings related to unchecked operations

- unqualified-field-access - Disable warnings related to unspecified field access operations

- unused - disable warnings related to unused and dead code

---

