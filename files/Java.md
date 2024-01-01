#### How Java runs

`.java file`<br>then<br>`.class file (byte code)` needs JVM to run<br>then<br>`Machine code`

Java code can run on any machine which has JVM (Java Virtual Machine) installed in it.

Every file that ends with .java is a class itself

The names of classes start with a capital letter. It is not compulsory but it is industry standard

```java
public class Demo {
    public static void main(String[] args) {
         System.out.println("Hello World!");
    }
}
```

We have the keyword `public` with `class` because we want this class to be accessible publicly

name of the public class has to be same as the file name

within the public class, we have to have a `main` function which is the entry point of the java program. The main function is also public because it has to be run 

The public class should be only the class which is the name of the file

we have static in front of `main` because we want to run it without creating an instance / object of the Demo Class

void is the return type of the function 

<hr>

```java
System.out.println("Hello, World!");
// and 
System.out.print("Hello, World!");
```

can be used to print something to the console, `println` adds a new line after it prints the output and `print` does not add a new line after the output is printed

<hr>

### Primitive Data Types

Primitive data types are the data types which cannot be broken further

```java
int rollno = 64;
```

Here, rollno is the variable name and `int` is the datatype

```java
char letter = 'r';
```

Here `char` is the datatype of the variable letter which is 

```java
float marks = 98.33f;
```

Float is the dataype used to store decimal numbers, an f should be added at the end of the numbers compulsorily

```java
double largeDecimalNumber = 289389023.23920392;
long largeIntegers = 23728932838L;
```

These two are self explanatory, again capital L is compulsory at the end of long value

```java
boolean check = false;
```

Boolean is boolean!

