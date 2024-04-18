### How Java runs

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

### Output

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

<hr>

### Comparison Operators

`==` is used only for primitive datatypes, for Wrapper types such as `String`, we use `.equals(<value>)` for the same.

<hr>

### Taking Inputs

We have a class named `Scanner` which we need to import from `java.util.Scanner`. We then make an object from that class, generally named `input` and we specify where to take the input from. And then we start using it.

```java
Scanner input = new Scanner(System.in);
int rollno = input.nextInt();
```

in the above code, in the first line we are defining the input variable which is of Wrapper Type Scanner and we are making it out of the class Scanner using the `new Scanner()` with `System.in` as the parameter. It tells the object where to take the input from

then while we want to take input from the user, we use the input object with the `nextInt()` function, which stands for "next Integer" and we store it in a variable with type integer.

There are a lot of other functions/methods as well which can be used to take different types of inputs from the users.

For strings:

```java
String name = next(); // only takes first word
```

```java
String sentence = nextLine(); // Takes whole line
```

<hr>

### Type conversion and TypeCasting

```java
float num = input.nextFloat();
```

If we give integer as an output to the operation that requires a float, it converts the integer into float. 

But if we try to use float where integer is required, it throws an error.

This is because floats are greater than integer. So no data is loss while converting integer to float. But when we convert floats to integer. The data behind the decimal point is lost. So that is not acceptable.

To typecast or explicitly convert floats to integers, we can do something like this :

```java
int num = (int)(88.99f); // num = 88
```

The numbers behind the decimal point are lost in the conversion process but we get an integer number.

<hr>

### Loops

While loop: 

```java
int count = 1;
while(count != 5){
    System.out.println(count);
    count++;
}
```

For loop: 

```java
for(int count = 1; count != 5; count++){
        System.out.println(count);
}
```

## Conditions

### If else

If else statements in Java are quite Straight forward

```java
if (amt > 100) {
    amt += 10;
} else if (amt > 50) {
    amt += 50
} else {
    amt += 100;
}
```

## Loops

### For loop 

```java
for(int i = 0; i < 100; i++){
    System.out.println("Hello world " + i);
}
```

### While loop 

```java
int i = 1;
while(i <= target){
    System.out.println("Hello world while " + i);
    i++;
}
```

We run a while loop when we do not know how many times our loop is going to run.

### Do while loop

```java
do {
    ...
} while (...)

```

The do while loops first runs the code block and then checks the condition