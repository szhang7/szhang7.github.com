---
layout: post
title: "Java Handbook"
description: ""
category: java
tags: [java]
---
{% include JB/setup %}

## Introduction
Java was originally developed by James Gosling at Sun Microsystems and released in 1995 as a core component of Sun Microsystems' Java platform.

Java technology is both a programming language and a platform. The Java programming language is a high-level language that can be characterized by all of the following buzzwords: `Simple, Object oriented, Distributed, Multithreaded, Dynamic, Architecture neutral, Portable, High performance, Robust, Secure`.
The Java platform is a software-only platform that runs on top of other hardware-based platforms, which has two components: `The Java Virtual Machine and The Java Application Programming Interface (API)`.

The general-purpose, high-level Java programming language is a powerful software platform. Every full implementation of the Java platform gives you the following features: `Development Tools, Application Programming Interface (API), Deployment Technologies, User Interface Toolkits, Integration Libraries`.

###The Java Editions
    Java ME (Java Platform, Micro Edition) - targeting environments with limited resources.
    Java SE (Java Platform, Standard Edition) - targeting workstation environments.
    Java EE (Java Platform, Enterprise Edition) - targeting large distributed enterprise or Internet environments.

## The Java Programming Environment
Downloads [Java SE 6](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-javase6-419409.html), choose the stable version--[jdk1.6.0_32 for windows](http://download.oracle.com/otn/java/jdk/6u32-b05/jdk-6u32-windows-i586.exe) or [jdk1.6.0_32 for linux](http://download.oracle.com/otn/java/jdk/6u32-b05/jdk-6u32-linux-i586.bin).

###Windows 2000/XP/Win7

1. Install jdk-6u32-windows-i586.exe. These instructions assume you chose D:\windows\jdk\jdk1.6.0_32.

2. Add the JAVA_HOME environment variable by opening up the system properties (WinKey + Pause), selecting the "Advanced" tab, and the "Environment Variables" button, then adding the JAVA_HOME variable in the user variables with the value `D:\windows\jdk\jdk1.6.0_32`.

3. Optional: In the same dialog, add the JAVA_OPTS environment variable in the user variables to specify JVM properties, e.g. the value `-Xms512m -Xmx1024m -XX:PermSize=128m -XX:MaxPermSize=256m`. This environment variable can be used to supply extra options to Java.

4. In the same dialog, update/create the Path environment variable in the user variables and prepend the value %JAVA_HOME%\bin to add Java available in the command line.

5. Open a new command prompt `(Winkey + R then type cmd)` and run `java --version` to verify that it is correctly installed.

###Unix-based Operating Systems(Linux, Solaris and Mac OS X)

1. Extract the distribution archive, `$ tar -zxvf jdk-6u32-linux-i586.bin`.

2. In a command terminal, add the JAVA_HOME environment variable, e.g. export JAVA_HOME=/data/ubuntu/jdk/jdk1.6.0_32.

3. Optional: Add the JAVA_OPTS environment variable to specify JVM properties, e.g. export JAVA_OPTS="-Xms512m -Xmx1024m -XX:PermSize=128m -XX:MaxPermSize=256m". This environment variable can be used to supply extra options to Java.

4. Add JAVA_HOME environment variable to your path, e.g. export PATH=$JAVA_HOME/bin:$PATH.

5. Run `java --version` to verify that it is correctly installed.

###HelloWorld.java
    public class HelloWorld{
        public static void main(String[] args){
            System.out.println("Hello World!");
        }
    }

    $ javac HelloWorld.java     #compile
    $ java HelloWorld           #run the program
    Hello World!
    $

##-------------------------------------------------------------------------------------------------------

## Language Basics
Describes the traditional features of the language, including concepts, comments, data types, arrays, variables, operators, and control flow.

###Object-Oriented Programming Concepts
- Object      : An object is a software bundle of related state and behavior. Software objects are often used to model the real-world objects that you find in everyday life.
- Class       : A class is a blueprint or prototype from which objects are created.
- Inheritance : Inheritance provides a powerful and natural mechanism for organizing and structuring your software.
- Interface   : An interface is a contract between a class and the outside world.
- Package     : A package is a namespace for organizing classes and interfaces.

###Comments
Comments in Java, as in most programming languages, do not show up in the executable program.

    //          - comment from the // to the end of the line.
    /* and */   - comment from /* to start and */ to end.

###Primitive Data Types
There are eight primitive data types: byte, short, int, long, float, double, char, and boolean.

####Integer Types
The integer types are for numbers without fractional parts. Negative values are allowed.

    Type    Storage requirement     Range(inclusive)
    int     4bytes                  -2,247,483,648 to 2,147,483,647
    short   2bytes                  -32,768 to 32,767
    long    8bytes                  -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
    byte    1byte                   -128 to 127

####Floating-Point Types
The floating-point types denote numbers with fractional parts.

    Type    Storage requirement     Range(inclusive)
    float   4bytes                  Approximately -3.40282347E+38F to +3.40282347E+38F
                                    (6-7 significant decimal digits)
    double  8bytes                  Approximately -1.79769313486231570E+308 to +1.79769313486231570E+308
                                    (15 significant decimal digits)

####The char Type
The `char` type is uesd to describe individual characters.

    Escape sequence     Name                Unicode value
    \b                  Backspace           \u0008
    \t                  Tab                 \u0009
    \n                  Linefeed            \u000a
    \r                  Carriage return     \u000d
    \"                  Double quote        \u0022
    \'                  Single quote        \u0027
    \\                  Backslash           \u005c

####The boolean Type
The `boolean` type has two values, false and true. It is used for evaluating logical conditions. You cannot convert between integers and boolean values.

###Variables
The Java programming language defines the following kinds of variables: `Instance Variables (Non-Static Fields), Class Variables (Static Fields), Local Variables, Parameters)`. The rules and conventions for naming your variables can be summarized as follows:

- Variable names are case-sensitive.
- Subsequent characters may be letters, digits, dollar signs, or underscore characters.
- If the name you choose consists of only one word, spell that word in all lowercase letters. If it consists of more than one word, capitalize the first letter of each subsequent word. For example, currentDate. If your variable stores a constant value, capitalizing every letter and separating subsequent words with the underscore. For example, static final NUM_GEARS = 6. By convention, the underscore character is never used elsewhere.

    Type variable_name;         //declare variable

    double salary;              //declare salary
    System.out.println(salary); //ERROR--variable not initialized

    int n=0;                    //int n; n=0;
    int i, j;                   //declare i and j

    final double CM_PER_INCH = 2.54;        //declare a constant
    static final double CM_PER_INCH = 2.54; //delcare a class constant

In Java, it is considered good style to declare variables as closely as possible to the point where they are first used. Never use the value of an uninitialized variable!

###Arrays
An array is a container object that holds a fixed number of values of a single type. Each item in an array is called an element, and each element is accessed by its numerical index.

    int[] array;              //declare an array of integers
    array = new int[10];      //create an array of integers
    array[0] = 100;           //initialize first element
    array[1] = 200;           //initialize second element
    array[2] = 300;           //initialize third element

    int[] array = {           //create and initialize an array
        100,200,300,
        400,500,600,
        700,800,900,1000
    };

    new int[] {17, 19, 23};   //initialize an anonymous array

    array = new int[] {17, 19, 23};
    is shorthand for:
    int [] anonymous = {17, 19, 23};
    array = anonymous;

    String[][] names = {      //multidimensional array
        {"Mr. ", "Mrs. ", "Ms. "},
        {"Smith", "Jones"}
    };

####Copying Arrays
    class ArrayCopyDemo {
        public static void main(String[] args) {
            char[] copyFrom = { 'd', 'e', 'c', 'a', 'f', 'f', 'e',
			        'i', 'n', 'a', 't', 'e', 'd' };

            char[] copyTo = new char[7];
            System.arraycopy(copyFrom, 2, copyTo, 0, 7);

            //char[] copyTo = java.util.Arrays.copyOfRange(copyFrom, 2, 9);
            System.out.println(new String(copyTo));
        }
    }

####Array Sorting
    int[] array = {1, 2, 3, 4, 5};
    java.util.Arrays.sort(array);

###Operators
Operators are special symbols that perform specific operations on one, two, or three operands, and then return a result.

####Operator Precedence
    Operators               Precedence
    postfix                 expr++ expr--
    unary                   ++expr --expr +expr -expr ~ !
    multiplicative          * / %
    additive                + -
    shift                   << >> >>>
    relational              < > <= >= instanceof
    equality                == !=
    bitwise AND             &
    bitwise exclusive OR    ^
    bitwise inclusive OR    |
    logical AND             &&
    logical OR              ||
    ternary                 ? :
    assignment              = += -= *= /= %= &= |= <<= >>= >>>=

#####The Unary Operators
    +       Unary plus operator; indicates positive value
    -       Unary minus operator; negates an expression
    ++      Increment operator; increments a value by 1
    --      Decrement operator; decrements a value by 1
    !       Logical complement operator; iverts the value of a boolean

The increment/decrement operators can be applied before (prefix) or after (postfix) the operand. The code result++; and ++result; will both end in result being incremented by one. The only difference is that the prefix version (++result) evaluates to the incremented value, whereas the postfix version (result++) evaluates to the original value.

    int m = 7;
    int n = 7;
    int a = 2 * ++m;    //now a is 16, m is 8
    int b = 2 * n++;    //now b is 14, n is 8

####Relational and boolean Operators
    ==      equality
    !=      inequality
    <       less than
    >       greater than
    <=      less than or equal
    >=      greater than or equal
    &&      logical and
    ||      logical or
    !       logical negation

    condition ? expression1 : expression2
    //evaluates to the first expression if the condition is true, to the second expression otherwise.

####Bitwise Operators
    &       and
    |       or
    ^       xor
    ~       not
    >>      shift a bit pattern to the right
    <<      shift a bit pattern to the left
    >>>     fills the top bits with zero

    For examples
    int fourthBitFromRight = (n & 0b1000) / 0b1000;
    //or
    int fourthBitFormRight = (n & (1 << 3)) >>3;

####Conversions between Numeric Types
without information loss:

            char-->int
    byte-->short-->int-->long
                   int-->double

may lose precision:

    int-->float
    long-->float
    long-->double

####Casts
Conversions in which loss of information is possible are done by means of casts.

    double x = 9.997;
    int nx = (int) x;               //nx is 9
    //round a floating-point number to the nearest integer
    int nx = (int) Math.round(x);   //nx is 10, round return long value

####Parentheses and Operator Hierarchy
Operator Precedence

    Operators                                   Associativity
    [] . () (method call)                       Left to right
    ! ~ ++ -- +(unary) -(unary) ()(cast) new    Right to left
    * / %                                       Left to right
    + -                                         Left to right
    << >> >>>                                   Left to right
    < <= > >= instanceof                        Left to right
    == !=                                       Left to right
    &                                           Left to right
    ^                                           Left to right
    |                                           Left to right
    &&                                          Left to right
    ||                                          Left to right
    ?:                                          Right to left
    = += -= *= /= %= &= |= ^= <<= >>= >>>=      Right to left

####Enumerated Types
    enum Size { SMALL, MEDIUM, LARGE, EXTRA_LARGE };
    Size s = Size.MEDIUM;

###Input and Output

####Reading Input
    import java.util.Scanner;
    //Scanner plainly input
    Scanner in = new Scanner(System.in);
    System.out.print("What is your name?");
    String name = in.nextLine();    //read words
    String firstName = in.next();   //read a single word
    int age = in.nextInt();         //read an integer

    Console cons = System.console();
    String username = cons.readLine("Username: ");
    char[] password = cons.readPassword("Password: ");

    java.lang.System
    java.util.Scanner
    java.io.Console

####File Input and Output
    java.util.Scanner
    java.io.PrintWriter
    java.nio.file.Paths

    Scanner in = new Scanner(Paths.get("myfile.txt"));
    PrintWriter out = new PrintWriter("myfile.txt");

    Scanner in = new Scanner("myfile.txt"); //ERROR? the scanner will see ten characters of data.

###Control Flow Statements
Control flow statements break up the flow of execution by employing decision making, looping, and branching, enabling your program to conditionally execute particular blocks of code.

####Expressions
An expression is construct made up of variables, operators, and method invocations, which are constructed according to the syntax of the language, that evaluates to a single value.

    (x + y) / 100

####Statements
Statements are roughly equivalent to sentences in natural languages. A statement forms a complete unit of execution, terminate the expression with a semicolon `;`.

    int n = 0;
    n++;
    System.out.println("Hello World!");
    Bicycle myBike = new Bicycle();

####Block Scope
A block is a group of zero or more statements between balanced braces and can be used anywhere a single statement is allowed.

    public class Test{
        public static void main(String[] args){
            int n;
            {
                int k;
                int n;  //ERROR--can't redefine n in inner block
            }//k is only defined up to here
        }
    }

####Conditional Statements
    if (condition) statement

    if (condition){
        statement(s)
    }

    if (condition) statement1 else statement2

    if (condition){
        statement(s)
    } else {
        statement(s)
    }

####Loops
    while (condition) statement

    while (condition) {
        statement(s)
    }

    do statement while (condition)

    do {
        statement(s)
    } while (condition)

####Determinate Loops
    for (initialization; termination; increment) {
        statement(s)
    }

    for (int i=1; i<10; i++) {
        System.out.println("Count is: " + i);
    }

    //infinite loop
    for ( ; ; ) {
        statement(s)
    }

#####The "for each" Loop
    for (variable : collection) statement

    //iteration through Collections and arrays
    int[] numbers = {1,2,3,4,5,6,7,8,9,10};
    for (int item : numbers) {
        System.out.println("Count is: " + item);
    }

####Multiple Selections - The switch Statement
Unlike if-then and it-then-else statements, the switch statement can have a number of possible execution paths. A switch works with the byte, short, char, and int primitive data types. It also works with enumerated types, the string class, and a few special classes that wrap certain primitive types: Character, Byte, Short, and Interger.

#####switch Demo1
    public class SwitchDemo {
        public static void main(String[] args) {

            int month = 8;
            String monthString;
            switch (month) {
                case 1:  monthString = "January";
                         break;
                case 2:  monthString = "February";
                         break;
                case 3:  monthString = "March";
                         break;
                case 4:  monthString = "April";
                         break;
                case 5:  monthString = "May";
                         break;
                case 6:  monthString = "June";
                         break;
                case 7:  monthString = "July";
                         break;
                case 8:  monthString = "August";
                         break;
                case 9:  monthString = "September";
                         break;
                case 10: monthString = "October";
                         break;
                case 11: monthString = "November";
                         break;
                case 12: monthString = "December";
                         break;
                default: monthString = "Invalid month";
                         break;
            }
            System.out.println(monthString);
        }
    }

#####switch Demo2
    class SwitchDemo2 {
        public static void main(String[] args) {

            int month = 2;
            int year = 2000;
            int numDays = 0;

            switch (month) {
                case 1: case 3: case 5:
                case 7: case 8: case 10:
                case 12:
                    numDays = 31;
                    break;
                case 4: case 6:
                case 9: case 11:
                    numDays = 30;
                    break;
                case 2:
                    if (((year % 4 == 0) &&
                         !(year % 100 == 0))
                         || (year % 400 == 0))
                        numDays = 29;
                    else
                        numDays = 28;
                    break;
                default:
                    System.out.println("Invalid month.");
                    break;
            }
            System.out.println("Number of Days = "
                               + numDays);
        }
    }

#####Using String in switch Statements
    public class StringSwitchDemo {

        public static int getMonthNumber(String month) {

            int monthNumber = 0;

            if (month == null) {
                return monthNumber;
            }

            switch (month.toLowerCase()) {
                case "january":
                    monthNumber = 1;
                    break;
                case "february":
                    monthNumber = 2;
                    break;
                case "march":
                    monthNumber = 3;
                    break;
                case "april":
                    monthNumber = 4;
                    break;
                case "may":
                    monthNumber = 5;
                    break;
                case "june":
                    monthNumber = 6;
                    break;
                case "july":
                    monthNumber = 7;
                    break;
                case "august":
                    monthNumber = 8;
                    break;
                case "september":
                    monthNumber = 9;
                    break;
                case "october":
                    monthNumber = 10;
                    break;
                case "november":
                    monthNumber = 11;
                    break;
                case "december":
                    monthNumber = 12;
                    break;
                default:
                    monthNumber = 0;
                    break;
            }

            return monthNumber;
        }

        public static void main(String[] args) {

            String month = "August";

            int returnedMonthNumber =
                StringSwitchDemo.getMonthNumber(month);

            if (returnedMonthNumber == 0) {
                System.out.println("Invalid month");
            } else {
                System.out.println(returnedMonthNumber);
            }
        }
    }

####Branching Statements

#####The break Statement
The break statement has two forms: labeled and unlabeled. You can use an unlabeled break to terminate switch and for, while, or do-while loop. However, a labeled break terminates an outer statement.

    class BreakWithLabelDemo {
        public static void main(String[] args) {

            int[][] arrayOfInts = {
                { 32, 87, 3, 589 },
                { 12, 1076, 2000, 8 },
                { 622, 127, 77, 955 }
            };
            int searchfor = 12;

            int i;
            int j = 0;
            boolean foundIt = false;

        search:
            for (i = 0; i < arrayOfInts.length; i++) {
                for (j = 0; j < arrayOfInts[i].length;
                     j++) {
                    if (arrayOfInts[i][j] == searchfor) {
                        foundIt = true;
                        break search;
                    }
                }
            }

            if (foundIt) {
                System.out.println("Found " + searchfor + " at " + i + ", " + j);
            } else {
                System.out.println(searchfor + " not in the array");
            }
        }
    }

    This is the output of the program.

    Found 12 at 1, 0

#####The continue Statement
The continue statement skips the current iteration of a for, while , or do-while loop. The unlabeled form skips to the end of the innermost loop's body and evaluates the boolean expression that controls the loop.

#####The return Statement
The return statement exits from the current method, and control flow returns to where the method was invoked.

    return count;   //return a value
    return;         //return void

####Big Numbers
java.math.BigInteger implements arbitrary-precision integer arithmetic, and java.math.BigDecimal does the same for floating-point numbers.

    //equivalent statement
    lotteryOdds = lotteryOdds * (n - i + 1) /i;
    //when big numbers are used, it becomes
    lotteryOdds = lotteryOdds.multiply(BigInteger.valueOf(n - i + 1)).divide(BigInteger.valueOf(i));

## Classes and Objects
Describe how to write the classes from which objects are created, and how to create and use the objects.

###Classes
A class is the template or blueprint from which objects are made.

####Declaring Classes
    class MyClass {
        //field, constructor, and
        //method declarations
    }

    class MyClass extends MySuperClass implements YourInterface {
        //field, constructor, and
        //method declarations
        public MyClass() {      //constructor
        ...
        }
    }

In general, class declarations can include these components, in order:

    1. Modifiers such as public, private, and a number of others.
    2. The class name, with the initial letter capitalized by convention.
    3. The name of the class's parent (superclass), if any, preceded by the keyword extends. A class can only extend (subclass) one parent.
    4. A comma-separated list of interfaces implemented by the class, if any, preceded by the keyword implements. A class can implement more than one interface.
    5. the class body, surrounded by braces, {}.

####Declaring Member Variables - Fields
Field declarations are composed of three components, in order:

    1. Zero or more modifiers, such as public or private.
    2. The field's type.
    3. The field's name.

####Defining Methods
More generally, method declarations have six components, in order:

    1. Modifiers--such as public, private, and others.
    2. The return type--the data type of the value returned by the method, or void if the method does not return a vaule.
    3. The method name--the firt word should be a verb in lowercase, the first letter of each of other words should be capitalized.
    4. The parameters list in parenthesis--a comma-delimited list of input parameters, preceded by their data types, enclosed by parentheses, (). If there are no parameters, you must use empty parenttheses.
    5. An exception list--to be discussed later.
    6. The method body, enclosed between braces--the method's code, including the declaration of local variables, goes here.

#####Overloading Methods
Methods within a class can have the same name if they have different parameter lists.

    public class DataArtist {
        ...
        public void draw(String s) {
            ...
        }
        public void draw(int i) {
            ...
        }
        public void draw(double f) {
            ...
        }
        public void draw(int i, double f) {
            ...
        }
    }

####Providing Constructors for Your Classes
A class contains constructors that are invoked to create objects from the class blueprint. Constructor declarations look like method declarations--except that they use the name of the class and have no return type.

###Objects

####Creating Objects
In general, creating object statement has three parts:

    1. Declaration: The code set are all variable declarations that associate a variable name with an object type.
    2. Instantiation: The new keyword is a Java operator that create the object.
    3. Initialization: The new operator is followed by a call to a constructor, which initialize the new object.

    Point pt = new Point(23, 94);
    Rectangle rt1 = new Rectangle(pt, 100, 200);
    Rectangle rt2 = new Rectangle(50, 100);

####Using Objects
Use dot operator to invoke an object's field or method.

    objectReference.fieldName;
    objectReference.methodName(argrmentList);

###More on Classes

####Returning a Value from a Method
A method returns the code that invoked it when it

    completes all the statements in the method,
    reaches a return statement, or
    throws an exception.

####Using the this keyword
Within an instance method or a constructor, `this` is a reference to the current object. You can refer to any member of the current object from within an instance method or a constructor by using `this`.

####Controlling Access to Members of a Class
    Modifier    Class   Package Subclass    World
    public      Y       Y       Y           Y
    protected   Y       Y       Y           N
    no modifier Y       Y       N           N
    private     Y       N       N           N

###Nested Classes
The Java programming language allows you to define a class within another class. Such a class is called nested class.

    class OuterClass {
        ...
        static class StaticNestedClass {
            ...
        }
        class InnerClass {
            ...
        }
    }

    public class Outer {
        public static void main(String[] args) {
            Outer outer = new Outer();
            Outer.Inner inner = outer.new Inner();
            inner.print("Outer.new");

            inner = outer.getInner();
            inner.print("Outer.get");
        }

        // 个人推荐使用getxxx()来获取成员内部类，尤其是该内部类的构造函数无参数时
        public Inner getInner() {
            return new Inner();
        }

        public class Inner {
            public void print(String str) {
                System.out.println(str);
            }
        }
    }

###Enum Types
An enum type is a special data type that enables for a variable to be a set of predefined constants.

    public enum Day {
        SUNDAY, MONDAY, TUESDAY, WEDNESDAY,
        THURSDAY, FRIDAY, SATURDAY
    }

## Interfaces and Inheritance

###Interfaces
In the Java programming language, an interface is a reference type, similar to a class, that can contain only constants, method signatures, and nested types.

####Defining an Interface
An interface declaration consists of modifiers, the keyword interface, the interface name, a comma-separated list of parent interfaces (if any), and the interface body.

    public interface GroupedInterface extends Interface1, Interface2, Interface3 {

        // constant declarations

        // base of natural logarithms
        double E = 2.718282;

        // method signatures
        void doSomething (int i, double x);
        int doSomethingElse(String s);
    }

####Implementing an Interface
To declare a class that implements an interface, you include an implements clause in the class declaration.

    public interface IRectangle {
        public int isLargerThan(IRectangle other);
    }

    public class Rectangle implements IRectangle {
        public int width = 0;
        public int height = 0;

        public int getArea() {
            return width * height;
        }

        public int isLargerThan(IRectangle other) {
            Rectangle otherRect = (Rectangle)other;
            if (this.getArea() < otherRect.getArea())
                return -1;
            else if (this.getArea() > otherRect.getArea())
                return 1;
            else
                return 0;
        }
    }

####Using an Interface as a Type
If you define a reference variable whose type is an interface, any object you assign to it must be an instance of a class that implements the interface.

    public boolean isEqual(Object object1, Object object2) {
       Relatable obj1 = (Relatable)object1;
       Relatable obj2 = (Relatable)object2;
       if ( (obj1).isLargerThan(obj2) == 0)
          return true;
       else
          return false;
    }

####Rewriting Interfaces
    public interface DoIt {
       void doSomething(int i, double x);
       int doSomethingElse(String s);
    }

    public interface DoItPlus extends DoIt {
       boolean didItWork(int i, double x, String s);
    }

###Inheritance
A class that is derived from another class class is called a subclass (also a derived class, extended class, or child class). The class from which the subclass is derived is called a superclass (also a base class or a parent class).

####Overriding and Hiding Methods
An instance method in a subclass with the same signature (name, plus the number and the type of its parameters) and return type as an instance method in the superclass overrides the superclass's method.

If a subclass defines a class method with the same signature as a class method in the superclass, the method in the subclass hides the one in the superclass.

    public class Animal {
        public static void testClassMethod() {
            System.out.println("The class" + " method in Animal.");
        }
        public void testInstanceMethod() {
            System.out.println("The instance " + " method in Animal.");
        }
    }

    public class Cat extends Animal {
        public static void testClassMethod() {
            System.out.println("The class method" + " in Cat.");
        }
        public void testInstanceMethod() {
            System.out.println("The instance method" + " in Cat.");
        }

        public static void main(String[] args) {
            Cat myCat = new Cat();
            Animal myAnimal = myCat;
            Animal.testClassMethod();
            myAnimal.testInstanceMethod();
        }
    }

####Polymorphism
Subclasses of a class can define their own unique behaviors and yet share some of the same functionality of the parent class.

    public class Bicycle {

        // the Bicycle class has three fields
        public int cadence;
        public int gear;
        public int speed;

        // the Bicycle class has one constructor
        public Bicycle(int startCadence, int startSpeed, int startGear) {
            gear = startGear;
            cadence = startCadence;
            speed = startSpeed;
        }

        // the Bicycle class has four methods
        public void setCadence(int newValue) {
            cadence = newValue;
        }

        public void setGear(int newValue) {
            gear = newValue;
        }

        public void applyBrake(int decrement) {
            speed -= decrement;
        }

        public void speedUp(int increment) {
            speed += increment;
        }

        public void printDescription(){
            System.out.println("\nBike is " + "in gear " + this.gear
                + " with a cadence of " + this.cadence +
                " and travelling at a speed of " + this.speed + ". ");
        }
    }

    public class MountainBike extends Bicycle {
        private String suspension;

        public MountainBike(
                   int startCadence,
                   int startSpeed,
                   int startGear,
                   String suspensionType){
            super(startCadence,
                  startSpeed,
                  startGear);
            this.setSuspension(suspensionType);
        }

        public String getSuspension(){
          return this.suspension;
        }

        public void setSuspension(String suspensionType) {
            this.suspension = suspensionType;
        }

        public void printDescription() {
            super.printDescription();
            System.out.println("The " + "MountainBike has a" +
                getSuspension() + " suspension.");
        }
    }

    public class RoadBike extends Bicycle{
        // In millimeters (mm)
        private int tireWidth;

        public RoadBike(int startCadence,
                        int startSpeed,
                        int startGear,
                        int newTireWidth){
            super(startCadence,
                  startSpeed,
                  startGear);
            this.setTireWidth(newTireWidth);
        }

        public int getTireWidth(){
          return this.tireWidth;
        }

        public void setTireWidth(int newTireWidth){
            this.tireWidth = newTireWidth;
        }

        public void printDescription(){
            super.printDescription();
            System.out.println("The RoadBike" + " has " + getTireWidth() +
                " MM tires.");
        }
    }

    public class TestBikes {
      public static void main(String[] args){
        Bicycle bike01, bike02, bike03;

        bike01 = new Bicycle(20, 10, 1);
        bike02 = new MountainBike(20, 10, 5, "Dual");
        bike03 = new RoadBike(40, 20, 8, 23);

        bike01.printDescription();
        bike02.printDescription();
        bike03.printDescription();
      }
    }

####Hiding Fields
Within a class, a field that has the same name as a field in the superclass hides the superclass's field, even if their types are different.

####Using the Keyword super
By using the keyword super, you can invoke the overridden method and a superclass's constructor. For example class MountainBike.

####Object as a Superclass
The Object class, in the java.lang package, sits at the top of the class hierarchy tree. Every class is a descendant, direct or indirect, of the Object class. The methods inherited from Object that are discussed in this section are:

    protected Object clone() throws CloneNotSupportedException
    public boolean equals(Object obj)
    protected void finalize() throws Throwable
    public final Class getClass()
    public int hashCode()
    public String toString()

####Writing Final Classes and Methods
You can declare some or all of a class's method final. You use the final keyword in a method declaration to indicate the method cannot be overridden by subclasses.

####Abstract Methods and Classes
An abstract class is a class that is declared abstract--it may or may not include abstract methods. Abstract classes cannot be instantiated, but they can be subclassed.

    public abstract class GraphicObject {
       // declare fields
       // declare non-abstract methods
       abstract void draw();
    }

## Numbers and Strings

###Numbers

####The Numbers Classes
All of the numeric wrapper classes are subclasses of the abstract class Number: Byte, Integer, Short, Long, Float, Double. There are four other subclasses of Number: BigInteger, BigDecimal, AtomicInteger, AtomicLong. The following lists methods in the Integer class. Methods for the other Number subclasses are similar.

    int intValue()      //Converts the value of this Number object to the primitive data type returned.
    int compareTo(Integer anotheInteger)    //compares this Number object to the argument.

    boolean equals(Object obj)  //The methods return true if the argument is not null and is an object of the same type and with the same numeric value.

    static Integer decode(String s)     //Decodes a string into an integer.
    static int parseInt(String s)       //Returns an integer.
    static int parseInt(String s, int radix)    //Returns an integer (radix equals 10,2,8,or 16).
    String toString()                   //Returns a string object
    static String toString(int i)       //Returns a string object.
    static Integer valueOf(int i)       //Returns a Integer object.
    static Integer valueOf(String s)    //Returns a Integer object.
    static Integer valuesOf(String s, int radix)    //Returns an Integer object.

####Formating Numeric Print Output
The java.io package includes a PrintStream class that has two formatting methods: format and printf. Each of the format specifiers that start with a % character is replaced with the corresponding argument.

    System.out.printf("%8.2f", x);

    Conversion character    Type                            Example
    d                       Decimal integer                 16
    x                       Hexadecimal integer             9f
    o                       Octal integer                   237
    f                       Fixed-point floating-point      15.9
    e                       Exponential floating-point      1.59e+01
    g                       General floating-point(the shorter of e and f)
    a                       Hexadecimal floating-point      0x1.fccd
    tB                      locale-specific full name of month
    td,te                   2-digit day of month. td has leading zeroes as needed, te does not.
    ty,tY                   ty = 2-digit year, tY = 4-digit year.
    tl                      hour in 12-hour clock.
    tM                      minutes in 2 digits, with leading zeroes as necessary
    tp                      locale-specific am/pm(lower case)
    tm                      months in 2 digits, with leading zeroes as necessary
    tD                      date as %tm%td%ty
                08          Eight characters in width, with leading zeroes as necessay.
                +           Includes sign, whether positive or negative.
                ,           Includes locale-specific grouping characters.
                -           Left-justified
                .3          Three places after decimal point.
                10.3        Then characters in width, right justified, with three places after decimal point.
    s                       String                          Hello
    c                       Character                       H
    b                       boolean                         true
    h                       Hash code                       42628b2
    %                       The percent symbol              %
    n                       The platform-dependent line separator

#####Format Example
    import java.util.Calendar;
    import java.util.Locale;

    public class TestFormat {

        public static void main(String[] args) {
          long n = 461012;
          System.out.format("%d%n", n);      //  -->  "461012"
          System.out.format("%08d%n", n);    //  -->  "00461012"
          System.out.format("%+8d%n", n);    //  -->  " +461012"
          System.out.format("%,8d%n", n);    // -->  " 461,012"
          System.out.format("%+,8d%n%n", n); //  -->  "+461,012"

          double pi = Math.PI;

          System.out.format("%f%n", pi);       // -->  "3.141593"
          System.out.format("%.3f%n", pi);     // -->  "3.142"
          System.out.format("%10.3f%n", pi);   // -->  "     3.142"
          System.out.format("%-10.3f%n", pi);  // -->  "3.142"
          System.out.format(Locale.FRANCE,
                            "%-10.4f%n%n", pi); // -->  "3,1416"

          Calendar c = Calendar.getInstance();
          System.out.format("%tB %te, %tY%n", c, c, c); // -->  "May 29, 2006"

          System.out.format("%tl:%tM %tp%n", c, c, c);  // -->  "2:34 am"

          System.out.format("%tD%n", c);    // -->  "05/29/06"
        }
    }

####The DecimalFormat Class
    import java.text.DecimalFormat;

    public class DecimalFormatDemo {

       static public void customFormat(String pattern, double value ) {
          DecimalFormat myFormatter = new DecimalFormat(pattern);
          String output = myFormatter.format(value);
          System.out.println(value + "  " + pattern + "  " + output);
       }

       static public void main(String[] args) {

          customFormat("###,###.###", 123456.789);
          customFormat("###.##", 123456.789);
          customFormat("000000.000", 123.78);
          customFormat("$###,###.###", 12345.67);
       }
    }

####Beyond Basic Arithmetic
The Math class contains an assortment of mathematical functions. `import static java.lang.Math.*;` to avoid the Math prefix.

    Math.sqrt       //take the square root of a number
    Math.pow(x,a);  //x raised to the power a
    //trigonometric functions
    Math.sin
    Math.cos
    Math.tan
    Math.atan
    Math.atan2
    //the exponential function, the natural logarithm, the decimal logarithm
    Math.exp
    Math.log
    Math.log10
    //two constants
    Math.PI
    Math.E

###Characters
    java.lang.Character

    boolean isLetter(char ch)
    boolean isDigit(char ch)

    boolean isWhitespace(char ch)

    boolean isUpperCase(char ch)
    boolean isLowerCase(char ch)

    char toUpperCase(char ch)
    char toLowerCase(char ch)

    toString(char ch)

###Strings
In the Java programming language, strings are objects. String is a sequence of characters.

    String e = ""                           //an empty string
    String greeting = "Hello world!";       //Creating Strings
    int len = greeting.length();            //String Length

    string1.concat(string2);                //Concatenating Strings
    "Hello " + "world" + "!"

    String s = String.format("The value is %f", f); //Creating Format Strings

####Converting Between Numbers and Strings
    float a = (Float.valueOf(s1)).floatValue();
    float b = (Float.valueOf(s2)).floatValue();

    String s1 = "" + i;
    String s2 = String.valueOf(i);
    String s3 = Integer.toString(i);
    String s4 = Double.toString(d);

####Manipulating Characters in a String
Methods in the String class for manipulating Strings

    Char charAt(int index)
    CharSequence subSequence(int beginIndex, int endIndex)

    String substring(int beginIndex, int endIndex)
    String substring(int beginIndex)

    String[] split(String regex)
    String[] split(String regex, int limit)

    String trim()

    String toLowerCase()
    String toUpperCase()

    int indexOf(int ch)
    int lastIndexOf(int ch)

    int indexOf(int ch, int fromIndex)
    int lastIndexOf(int ch, int fromIndex)

    int indexOf(String str)
    int lastIndexOf(String str)

    int indexOf(String str, int fromIndex)
    int lastIndexOf(String str, int fromIndex)

    boolean contains(CharSequence s)

    String replace(char oldChar, char newChar)
    String replace(CharSequence target, CharSequence replacement)
    String replaceAll(String regex, String replacement)
    String replaceFirst(String regex, String replacement)

####Comparing Strings and Portions of Strings
    boolean endsWith(String suffix)
    boolean startsWith(String prefix)
    boolean startsWith(String prefix, int offset)

    int compareTo(String anotherString)
    int compareToIgnoreCase(String str)

    boolean equals(Object anObject)
    boolean equalsIgnoreCase(String anotherString)

    boolean regionMatches(int toffset, String other, int ooffset, int len)
    boolean regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len)

    boolean matches(String regex)

#####The StringBuilder Class
StringBuilder objects are like String objects, except that they can be modified.

    StringBuilder()
    StringBuilder(CharSequence cs)
    StringBuilder(int initCapacity)
    StringBuilder(String s)

    void setLength(int newLength)
    void ensureCapacity(int minCapacity)

    StringBuilder append(Object obj)
    StringBuilder delete(int start, int end)
    StringBuilder deleteCharAt(int index)
    StringBuilder insert(int offset, char c)
    StringBuilder replace(int start, int end, String s)
    void setCharAt(int index, char c)
    StringBuilder reverse()
    String toString()

###Autoboxing and Unboxing
Autoboxing is the automatic conversion that the Java compiler makes between the primitive types and their corresponding object wrapper classes. If the conversion goes the other way, this is called unboxing.

####Autoboxing
    Character ch = 'a';

    List<Integer> li = new ArrayList<>();
    for (int i=1; i<50; i +=2)
        li.add(i);

####Unboxing
    import java.util.ArrayList;
    import java.util.List;

    public class Unboxing {

        public static void main(String[] args) {
            Integer i = new Integer(-8);

            // 1. Unboxing through method invocation
            int absVal = absoluteValue(i);
            System.out.println("absolute value of " + i + " = " + absVal);

            List<Double> ld = new ArrayList<>();
            ld.add(3.1416);    // Π is autoboxed through method invocation.

            // 2. Unboxing through assignment
            double phi = ld.get(0);
            System.out.println("phi = " + phi);
        }

        public static int absoluteValue(int i) {
            return (i < 0) ? -i : i;
        }
    }

## Generics
###Why Use Generics?
In a nutshell, generics enable types `(classes and interfaces)` to be parameters when defining classes, interfaces and methods. Code that use generics has many benefits over non-generic code:

    Stronger type checks at compile time.
    Elimination of casts.
    Enabling programmers to implement generic algorithms.

###Generic Types
A generic type is a generic class or interface that is parameterized over types.

####A Simple Box Class
    public class Box {
        private Object object;

        public void set(Object object) { this.object = object; }
        public Object get() { return object; }
    }

####A Generic Version of the Box Class
A generic class is defined with the following format:

    class name<T1, T2, ..., Tn> { /*...*/ }

    public class Box<T> {
        // T stands for "Type"
        private T t;

        public void set(T t) { this.t = t; }
        public T get() { return t; }
    }

####Type Parameter Naming Conventions
By convention, type parameter names are single, uppercase letters. The most commonly used type parameter names are:

    E - Element (used extensively by the Java Collections Framework)
    K - Key
    N - Number
    T - Type
    V - Value
    S,U,V etc. - 2nd, 3rd, 4th types

####Invoking and Instantiating a Generic Type
    Box<Integer> integerBox = new Box<Integer>();

####The Diamond
In Java SE 7 and later, you can replace the type arguments required to invoke the constructor of a generic class with an empty set of type arguments `(<>)` as long as the compiler can determine, or infer, the type arguments from the context. This pair of angle brackets, `<>`, is informally called the diamond.

    Box<Integer> integerBox = new Box<>();

####Multiple Type Parameters
    public interface Pair<K, V> {
        public K getKey();
        public V getValue();
    }

    public class OrderedPair<K, V> implements Pair<K, V> {

        private K key;
        private V value;

        public OrderedPair(K key, V value) {
	    this.key = key;
	    this.value = value;
        }

        public K getKey()	{ return key; }
        public V getValue() { return value; }
    }

    Pair<String, Integer> p1 = new OrderedPair<String, Integer>("Even", 8);
    Pair<String, String>  p2 = new OrderedPair<String, String>("hello", "world");

    OrderedPair<String, Integer> p1 = new OrderedPair<>("Even", 8);
    OrderedPair<String, String>  p2 = new OrderedPair<>("hello", "world");


####Parameterized Types
You can also substitute a type parameter with a parameterized type.

    OrderedPair<String, Box<Integer>> p = new OrderedPair<>("primes", new Box<Integer>(...));

####Raw Types
A raw type is the name of a generic class or interface without any type arguments.

    Box<Integer> intBox = new Box<>();      //create a parameterized type of Box<T>
    Box rawBox = new Box();                 //create a raw type of Box<T>

    Box<String> stringBox = new Box<>();
    Box rawBox = stringBox;                 //OK
    rawBox.set(8);                          //warning: unchecked invocation to set(T)

    Box rawBox = new Box();
    Box<Integer> intBox = rawBox;           //warning: unchecked conversion

    -Xlint:unchecked    //reveals all "unchecked" warnings
    -Xlint:-unchecked   //completely disable unchecked warnings

###Generic Methods
Generic methods are methods that introduce their own type parameters.

    public class Util {
        // Generic static method
        public static <K, V> boolean compare(Pair<K, V> p1, Pair<K, V> p2) {
            return p1.getKey().equals(p2.getKey()) &&
                   p1.getValue().equals(p2.getValue());
        }
    }

    public class Pair<K, V> {

        private K key;
        private V value;

        // Generic constructor
        public Pair(K key, V value) {
            this.key = key;
            this.value = value;
        }

        // Generic methods
        public void setKey(K key) { this.key = key; }
        public void setValue(V value) { this.value = value; }
        public K getKey()   { return key; }
        public V getValue() { return value; }
    }

    The complete syntax for invoking this method would be:

    Pair<Integer, String> p1 = new Pair<>(1, "apple");
    Pair<Integer, String> p2 = new Pair<>(2, "pear");
    boolean same = Util.<Integer, String>compare(p1, p2);   //the type has been explicitly provided.
    boolean same = Util.compare(p1, p2);                    //type inference

###Bounded Type Parameters
To declare a bounded type parameter, list the type parameter's name, followed by the extends keyword, followed by its upper bound.

    public class NaturalNumber<T extends Integer> {

        private T n;

        public NaturalNumber(T n)  { this.n = n; }

        public boolean isEven() {
            return n.intValue() % 2 == 0;
        }

        // ...
    }

####Multiple Bounds
    <T extends B1 & B2 & B3>

    Class A { /* ... */ }
    interface B { /* ... */ }
    interface C { /* ... */ }

    class D <T extends A & B & C> { /* ... */ }
    class D <T extends B & A & C> { /* ... */ }  // compile-time error

If one of the bounds is a class, it must be specified first.

####Generic Methods and Bounded Type Parameters
Consider the following method that counts the number of elements in an array `T[]` that are greater than a specified element elem.

    public interface Comparable<T> {
        public int compareTo(T o);
    }
    public static <T extends Comparable<T>> int countGreaterThan(T[] anArray, T elem) {
        int count = 0;
        for (T e : anArray)
            if (e.compareTo(elem) > 0)
                ++count;
        return count;
    }

###Generics, Inheritance, and Subtypes
    Box<Number> box = new Box<Number>();
    box.add(new Integer(10));   // OK
    box.add(new Double(10.1));  // OK

####Generic Classes and Subtyping
The relationship between the type parameters of one class or interface and the type parameters of another are determined by the extends and implements clauses.

    interface PayloadList<E,P> extends List<E> {
      void setPayload(int index, P val);
      ...
    }

    The following parameterizations of PayloadList are subtypes of List<String>:

    PayloadList<String,String>
    PayloadList<String,Integer>
    PayloadList<String,Exception>

###Type Inference
Type inference is a Java compiler's ability to look at each method invocation and corresponding declaration to determine the type argument `(or arguments)` that make the invocation applicable.

####Type Inference and Generic Methods
Generic Methods introduced you to type inference, which enables you to invoke a generic method as you would an ordinary method, without specifying a type between angle brackets.

####Type Inference and Instantiation of Generic Classes
You can replace the type arguments required to invoke the constructor of a generic class with an empty set of type parameters `(<>)` as long as the compiler can infer the type arguments from the context. This pair of angle brackets is informally called the diamond.

    Map<String, List<String>> myMap = new HashMap<String, List<String>>();
    Map<String, List<String>> myMap = new HashMap<>();

####Type Inference and Generic Contructors of Generic and Non-Generic Classes
Note that constructors can be generic `(in other words, declare their own formal type parameters)` in both generic and no-generic classes.

    class MyClass<X> {
      <T> MyClass(T t) {
        // ...
      }
    }
    MyClass<Integer> myObject = new MyClass<>("");

In this example, the compiler infers the type Integer for the formal type parameter, X, of the generic `class MyClass<X>`. It infers the type String for the formal type parameter, T, of the constructor of this generic class.

###Wildcards
In generic code, the question mark `(?)`, called the wildcard, represents an unkown type.

####Upper Bounded Wildcards
To declare an upper-bounded wildcard, use the wildcard character `('?')`, followed by the extends keyword, followed by its upper bound.

    public static void process(List<? extends Foo> list) {
        for (Foo elem : list) {
            // ...
        }
    }

####Unbounded Wildcards
The unbounded wildcard type is specified using the wildcard character `(?)`, for example, `List<?>`. This is called a list of unknown type.

    public static void printList(List<?> list) {
        for (Object elem: list)
            System.out.print(elem + " ");
        System.out.println();
    }

Because for any concrete type A, `List<A>` is a subtype of `List<?>`, you can use printList to print a list of any type:

####Lower Bounded Wildcards
A lower bounded wildcard is expressed using the wildcard character `('?')`, following by the super keyword, followed by its lower bound: `<? super A>`.

    public static void addNumbers(List<? super Integer> list) {
        for (int i = 1; i <= 10; i++) {
            list.add(i);
        }
    }

####Wildcards and Subtyping
    List<? extends Integer> intList = new ArrayList<>();
    List<? extends Number>  numList = intList;  // OK. List<? extends Integer> is a subtype of List<? extends Number>

Because Integer is a subtype of Number, and numList is a list of Number objects, a relationship now exists between intList `(a list of Integer objects)` and numList.

####Wildcard Capture and Helper Methods
The WildcardError example produces a capture error when compiled:

    import java.util.List;

    public class WildcardError {

        void foo(List<?> i) {
            i.set(0, i.get(0));
        }
    }

In this case, you can work around the problem by creating the private helper method, fooHelper, as shown in WildcardFixed:

    public class WildcardFixed {

        void foo(List<?> i) {
            fooHelper(i);
        }


        // Helper method created so that the wildcard can be captured
        // through type inference.
        private <T> void fooHelper(List<T> l) {
            l.set(0, l.get(0));
        }

    }

####Guidelines for Wildcard Use
- An "in" variable is defined with an upper bounded wildcard, using the extends keyword.
- An "out" variable is defined with a lower bounded wildcard, using the super keyword.
- In the case where the "in" variable can be accessed using methods defined in the object class, use an unbounded wildcard.
- In the case where the code needs to access the variable as both an "in" and an "out" variable, do not use a wildcard.

###Type Erasure
Type erasure ensures that no new classes are created for parameterized types; consequently, generics incur no runtime overhead.

####Erasure of Generic Types
During the type erasure process, the Java compiler erases all type parameters and replaces each with its first bound if the type parameter is bounded, or Object if the type parameter is unbounded.

####Erasure of Generic Methods
The Java compiler also erases type parameters in generic method arguments.

####Effects of Type Erasure and Bridge Methods
    public class Node<T> {

        private T data;

        public Node(T data) { this.data = data; }

        public void setData(T data) {
            System.out.println("Node.setData");
            this.data = data;
        }
    }

    public class MyNode extends Node<Integer> {
        public MyNode(Integer data) { super(data); }


        // Bridge method generated by the compiler
        //
        public void setData(Object data) {
            setData((Integer) data);
        }

        public void setData(Integer data) {
            System.out.println("MyNode.setData");
            super.setData(data);
        }
    }

###Non-Reifiable Types
A feifiable type is a type whose type information is fully available at runtime, This includes primitives, non-generic types, raw types, and invocations of unbound wildcards.

Non-reifiable types are types where information has been removed at compile-time by type erasure — invocations of generic types that are not defined as unbounded wildcards. A non-reifiable type does not have all of its information available at runtime.

####Heap Pollution
Heap pollution occurs when a variable of a parameterized type refers to an object that is not of that parameterized type.

####Potential Vulnerabilities of Varargs Methods with Non-Reifiable Formal Parameters
Generic methods that include vararg input parameters can cause heap pollution.

####Prevent Warnings from Varargs Methods with Non-Reifiable Formal Parameters
    @SuppressWarnings({"unchecked", "varargs"})

## Packages
A package is a grouping of related types providing access protection and name space management.

###Creating and Using Packages

####Creating a Package
To make types easier to find and use, to avoid naming conflicts, and to control access, programmers bundle groups of related types into packages.

####Naming a Package
Naming Conventions

    Package names are written in all lower case to avoid conflict with the names of classes or interfaces.
    Companies use their reversed Internet domain name to begin their package names--for example com.cbay.mypackage
    Name collisions that occur within a single company need to be handled by convention within that company, perhaps by including the region or the project name after the company name.
    Packages in the Java language itself begin with java. or javax.
    In some cases, the internet domain name may not be a valid package name. This can occur if the domain name contains a hyphen or other special character, if the package name begins with a digit or other character that is illegal to use as the beginning of a Java name, or if the package name contains a reserved Java keyword, such as "int". In this event, the suggested convention is to add an underscore.

    for example:
    hyphenated-name.example.org 	org.example.hyphenated_name
    example.int 	                int_.example
    123name.example.com 	        com.example._123name

####Using Package Memebers
To use a public package member from outside its package, you must do one of the following.

#####Refer to the member by its fully qualified name
    graphics.Rectangle myRect = new graphics.Rectangle();

#####Import the package member
    import graphics.Rectangle;
    Rectangle myRectangle = new Rectangle();

#####Import the member's entire package
    import graphics.*;
    Circle myCircle = new Circle();
    Rectangle myRectangle = new Rectangle();

####Apparent Hierarchies of Packages
At first, packages appear to be hierarchical, but they are not.

    import java.awt.*;
    //imports all of the types in the java.awt package, but it does not import java.awt.color, java.awt.font
    import java.awt.color.*;

####Name Ambiguities
If a member in one package shares its name with a member in another package and both package are imported, you must refer to each member by its qualified name.

    graphics.Rectangle rect;
    java.awt.Rectangle rc;

####The Static Import Statement
    import java.lang.Math;

    double r = Math.cos(Math.PI * theta);

    import static java.lang.Math.PI;
    //or
    import static java.lang.Math.*;

    double r = cos(PI * theta);

###Managing Source and Class Files
The strategy is as follows.

    Put the source code for a class, interface, enumeration, or annotation type in a text file whose name is the simple name of the type and whose extension is .java.
    Then, put the source file in a directory whose name reflects the name of the package to which the type belongs
    The qualified name of the package member and the path name to the file are parallel, assuming the Microsoft Windows file name separator backslash (for Unix, use the forward slash).
    class name – graphics.Rectangle
    pathname to file – graphics\Rectangle.java

####Setting the CLASSPATH System Variable
    In Windows:   C:\> set CLASSPATH
    In Unix:      export $CLASSPATH

##-------------------------------------------------------------------------------------------------------

## Exceptions
The Java programming language uses exceptions to handle errors and other exceptional events.

###What Is an Exception?
An exception is an event, which occurs during the execution of a program, that disrupts the normal flow of the program's instructions.

###The Catch or Specify Requirement
    A try statement that catches the exception.
    A method that specifies that it can throw the exception.

####The Three Kinds of Exceptions
- The first kind of exception is the checked exception. These are exceptional conditions that a well-written application should anticipate and recover from.
- The second kind of exception is the error. These are exceptional conditions that are external to the application, and that the application usually cannot anticipate or recover from.
- The third kind of exception is the runtime exception. These are exceptional conditions that are internal to the application, and that the application usually cannot anticipate or recover from.

####Bypassing Catch or Specify
Some programmers consider the Catch or Specify Requirement a serious flaw in the exception mechanism and bypass it by using unchecked exceptions in place of checked exceptions. In general, this is not recommended.

###Catching and Handling Exceptions

####The Try Block
    try {
        code
    }
    catch and finally blocks ...

####The catch Blocks
    try {
    } catch (ExceptionType name) {
    } catch (ExceptionType name) {
    }

    //catch more than one type of exception with one exception handler
    catch (IOException | SQLException ex) {
        logger.log(ex);
        throw ex;
    }

####The finally Block
The finally block always executes when the try block exits. Putting cleanup code in a finally block is always a good practice, even when no exceptions are anticipated.

    finally {
        if (out != null) {
            System.out.println("Closing PrintWriter");
            out.close();
        } else {
            System.out.println("PrintWriter not open");
        }
    }

####The try-with-resources Statement
    static String readFirstLineFromFile(String path) throws IOException {
        try (BufferedReader br =
                       new BufferedReader(new FileReader(path))) {
            return br.readLine();
        }
    }

####Putting It All Together
    import java.io.PrintWriter;
    import java.io.FileWriter;
    import java.io.IOException;
    import java.util.Vector;

    public void writeList() {
        PrintWriter out = null;

        try {
            System.out.println("Entering" + " try statement");

            out = new PrintWriter(new FileWriter("OutFile.txt"));
            Vector<String> vector = new Vector<String>(3);
            vector.add("Hello");
            vector.add("Johnny");
            vector.add("Jayne");
            for (int i = 0; i < vector.size(); i++)
                out.println("Value at: " + i + " = " + vector.elementAt(i));

        } catch (ArrayIndexOutOfBoundsException e) {
            System.err.println("Caught ArrayIndexOutOfBoundsException: "
                               +  e.getMessage());

        } catch (IOException e) {
            System.err.println("Caught IOException: " +  e.getMessage());

        } finally {
            if (out != null) {
                System.out.println("Closing PrintWriter");
                out.close();
            }
            else {
                System.out.println("PrintWriter not open");
            }
        }
    }

###Specifying the Exceptions Thrown by a Method
    public void writeList() throws IOException {
        PrintWriter out = new PrintWriter(new FileWriter("OutFile.txt"));
        for (int i = 0; i < SIZE; i++) {
            out.println("Value at: " + i + " = " + vector.elementAt(i));
        }
        out.close();
    }

###How to Throw Exceptions
All exception classes are descendants of the Throwable class.

    throw someThrowableObject           //the throw statement

####Chained Exceptions
An application often responds to an exception by throwing another exception. The following are the methods and constructors in Throwable that support chained exceptions.

    Throwable getCause()                //returns the exception that caused the current exception
    Throwable initCause(Throwable)      //sets the current exception's cause
    Throwable(String, Throwable)        //the same to init
    Throwable(Throwable)                //the same to init

#####Accessing Stack Trace Information
    catch (Exception cause) {
        StackTraceElement elements[] = cause.getStackTrace();
        for (int i = 0, n = elements.length; i < n; i++) {
            System.err.println(elements[i].getFileName()
                + ":" + elements[i].getLineNumber()
                + ">> "
                + elements[i].getMethodName() + "()");
        }
    }

#####Logging API
    try {
        Handler handler = new FileHandler("OutFile.log");
        Logger.getLogger("").addHandler(handler);

    } catch (IOException e) {
        Logger logger = Logger.getLogger("package.name");
        StackTraceElement elements[] = e.getStackTrace();
        for (int i = 0, n = elements.length; i < n; i++) {
            logger.log(Level.WARNING, elements[i].getMethodName());
        }
    }

####Creating Exception Classes
    public class ExceptionEx extends Exception {
    }

###Unchecked Exceptions — The Controversy
If a client can reasonably be expected to recover from an exception, make it a checked exception. If a client cannot do anything to recover from the exception, make it an unchecked exception.

###Advantages of Exceptions
1. Separating Error-Handling Code from "Regular" Code
2. Propagating Errors Up the Call Stack
3. Grouping and Differentiating Error Types

## Basic I/O
Most of the classes covered in the I/O Streams section are in the java.io package. Most of the classes covered in the File I/O section are in the java.nio.file package.

###I/O Streams
An I/O Stream represents an input source or an output destination. A stream can represent many different kinds of sources and destinations, including disk files, devices, other programs, and memory arrays.

####Byte Streams
Programs use byte streams to perform input and output of 8-bit bytes. All byte stream classes are descended from InputStream and OutputStream.

#####Using Byte Streams
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;

    public class CopyBytes {
        public static void main(String[] args) throws IOException {

            FileInputStream in = null;
            FileOutputStream out = null;

            try {
                in = new FileInputStream("xanadu.txt");
                out = new FileOutputStream("outagain.txt");
                int c;

                while ((c = in.read()) != -1) {
                    out.write(c);
                }
            } finally {
                if (in != null) {   //always close streams to avoid serious resource leaking.
                    in.close();
                }
                if (out != null) {
                    out.close();
                }
            }
        }
    }

####Character Streams
The Java platform stores character values using Unicode conventions. Character stream I/O automatically translates this internal format to and from the local character set.

#####Using Character Streams
    import java.io.FileReader;
    import java.io.FileWriter;
    import java.io.IOException;

    public class CopyCharacters {
        public static void main(String[] args) throws IOException {

            FileReader inputStream = null;
            FileWriter outputStream = null;

            try {
                inputStream = new FileReader("xanadu.txt");
                outputStream = new FileWriter("characteroutput.txt");

                int c;
                while ((c = inputStream.read()) != -1) {
                    outputStream.write(c);
                }
            } finally {
                if (inputStream != null) {
                    inputStream.close();
                }
                if (outputStream != null) {
                    outputStream.close();
                }
            }
        }
    }

#####Line-Oriented I/O
    import java.io.FileReader;
    import java.io.FileWriter;
    import java.io.BufferedReader;
    import java.io.PrintWriter;
    import java.io.IOException;

    public class CopyLines {
        public static void main(String[] args) throws IOException {

            BufferedReader inputStream = null;
            PrintWriter outputStream = null;

            try {
                inputStream = new BufferedReader(new FileReader("xanadu.txt"));
                outputStream = new PrintWriter(new FileWriter("characteroutput.txt"));

                String l;
                while ((l = inputStream.readLine()) != null) {
                    outputStream.println(l);
                }
            } finally {
                if (inputStream != null) {
                    inputStream.close();
                }
                if (outputStream != null) {
                    outputStream.close();
                }
            }
        }
    }

####Buffered Streams
Buffered input streams read data from a memory area known as a buffer; the native input API is called only when the buffer is empty.

    inputStream = new BufferedReader(new FileReader("xanadu.txt"));
    outputStream = new BufferedWriter(new FileWriter("characteroutput.txt"));

    flush()     //to flush a stream manually.

####Scanning and Formatting
The scanner API breaks input into individual tokens associated with bits of data. The formatting API assembles data into nicely formatted, human-readable form.

#####Scanning

######Breaking Input into Tokens
    import java.io.*;
    import java.util.Scanner;

    public class ScanXan {
        public static void main(String[] args) throws IOException {
            Scanner s = null;
            try {
                s = new Scanner(new BufferedReader(new FileReader("xanadu.txt")));

                while (s.hasNext()) {
                    System.out.println(s.next());
                }
            } finally {
                if (s != null) {
                    s.close();
                }
            }
        }
    }

    s.useDelimiter(",\\s*");    //the token separator to be a comma, optionally followed by white space.

######Translating Individual Tokens
    import java.io.FileReader;
    import java.io.BufferedReader;
    import java.io.IOException;
    import java.util.Scanner;
    import java.util.Locale;

    public class ScanSum {
        public static void main(String[] args) throws IOException {
            Scanner s = null;
            double sum = 0;
            try {
                s = new Scanner(new BufferedReader(new FileReader("usnumbers.txt")));
                s.useLocale(Locale.US);

                while (s.hasNext()) {
                    if (s.hasNextDouble()) {
                        sum += s.nextDouble();
                    } else {
                        s.next();
                    }
                }
            } finally {
                s.close();
            }

            System.out.println(sum);
        }
    }

#####Formatting
Stream objects that implement formatting are instances of either PrintWriter, a character stream class, or PrintStream, a byte stream class.

    public class Root {
        public static void main(String[] args) {
            int i = 2;
            double r = Math.sqrt(i);

            System.out.print("The square root of ");
            System.out.print(i);
            System.out.print(" is ");
            System.out.print(r);
            System.out.println(".");

            i = 5;
            r = Math.sqrt(i);
            System.out.println("The square root of " + i + " is " + r + ".");

            System.out.format("The square root of %d is %f.%n", i, r);
        }
    }

####I/O from the Command Line

#####Standard Streams
    InputStreamReader cin = new InputStreamReader(System.in);

#####The Console
    import java.io.Console;
    import java.util.Arrays;
    import java.io.IOException;

    public class Password {

        public static void main (String args[]) throws IOException {

            Console c = System.console();
            if (c == null) {
                System.err.println("No console.");
                System.exit(1);
            }

            String login = c.readLine("Enter your login: ");
            char [] oldPassword = c.readPassword("Enter your old password: ");

            if (verify(login, oldPassword)) {
                boolean noMatch;
                do {
                    char [] newPassword1 = c.readPassword("Enter your new password: ");
                    char [] newPassword2 = c.readPassword("Enter new password again: ");
                    noMatch = ! Arrays.equals(newPassword1, newPassword2);
                    if (noMatch) {
                        c.format("Passwords don't match. Try again.%n");
                    } else {
                        change(login, newPassword1);
                        c.format("Password for %s changed.%n", login);
                    }
                    Arrays.fill(newPassword1, ' ');
                    Arrays.fill(newPassword2, ' ');
                } while (noMatch);
            }

            Arrays.fill(oldPassword, ' ');
        }

        // Dummy change method.
        static boolean verify(String login, char[] password) {
            // This method always returns
            // true in this example.
            // Modify this method to verify
            // password according to your rules.
            return true;
        }

        // Dummy change method.
        static void change(String login, char[] password) {
            // Modify this method to change
            // password according to your rules.
        }
    }

####Data Streams
Data streams support binary I/O of primitive data type values (boolean, char, byte, short, int, long, float, and double) as well as String values.

    import java.io.DataInputStream;
    import java.io.DataOutputStream;
    import java.io.BufferedInputStream;
    import java.io.BufferedOutputStream;
    import java.io.FileInputStream;
    import java.io.FileOutputStream;

    import java.io.IOException;
    import java.io.EOFException;

    File dataFile=new File("dataFile.dat");
    DataOutputStream dos = null;
    try {
        dos = new DataOutputStream(new BufferedOutputStream(new FileOutputStream(dataFile)));
        double[] priceArr = {9.99, 19.99, 29.99, 39.99};
        int[] unitArr = {10, 20, 30, 40};
        String[] descArr = {"Apple", "Banana", "Cucumber", "Orange"};
        for(int i=0; i<priceArr.length; i++) {
            dos.writeDouble(priceArr[i]);
            dos.writeInt(unitArr[i]);
            dos.writeUTF(descArr[i]);
        }
        dos.flush();
    } finally {
        if(dos != null) dos.close();
    }

    DataInputStream dis = null;
    double total = 0.0;
    try {
        dis = new DataInputStream(new BufferedInputStream(new FileInputStream(dataFile)));
        while (true) {
            double price = dis.readDouble();
            int unit = dis.readInt();
            String desc = dis.readUTF();
            System.out.format("You ordered %d" + " units of %s at $%.2f%n",
                unit, desc, price);
            total += unit * price;
        }
    } catch (EOFException e) {
        System.out.format("Total cost is $%.2f%n", total);
    } finally {
        if(dis != null) dis.close();
    }

####Object Streams
Object streams support I/O of objects.

    import java.util.ArrayList;
    import java.util.List;

    import java.io.File;
    import java.io.BufferedInputStream;
    import java.io.BufferedOutputStream;
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.ObjectInput;
    import java.io.ObjectOutput;
    import java.io.ObjectInputStream;
    import java.io.ObjectOutputStream;

    File dataFile=new File("objectFile.dat");
    ObjectOutput out = null;
    try {
        out = new ObjectOutputStream(new BufferedOutputStream(new FileOutputStream(dataFile)));
        List<String> list = new ArrayList<String>();
        for (int i=0; i<5; i++) {
            list.add("Hello " + i);
        }
        out.writeObject((Object) list);
        Object obj = new Point(10, 10);
        out.writeObject(obj);
        out.flush();
    } finally {
        if(out != null) out.close();
    }

    ObjectInput in = null;
    try {
        TestApp ta = new TestApp();
        in = new ObjectInputStream(new BufferedInputStream(new FileInputStream(dataFile)));
        Object obj = in.readObject();
        @SuppressWarnings("unchecked")      //suppress warnings from an unchecked call or an unchecked cast
        List<String> list =  (List<String>) obj;
        for (String str : list) {
            System.out.println(str);
        }
        Point pt = (Point)in.readObject();
        System.out.println(pt);
    } catch (EOFException e) {
        System.out.format("read finished%n");
    }  catch(ClassNotFoundException e) {
        System.out.format("class Point not found!%n");
    } finally {
        if(in != null) in.close();
    }

    public class Point implements Serializable {
        private int x;
        private int y;

        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }

        public void setX(int x) {
            this.x = x;
        }

        public int getX() {
            return this.x;
        }

        public void setY(int y) {
            this.y = y;
        }

        public int getY() {
            return this.y;
        }

        @Override
        public String toString() {
            return "Point(" + this.x + ", " + this.y + ")";
        }
    }

###File I/O

####What Is a Path?
A file is identified by its path through the file system, beginning from the root node. For example, `/etc/profile`

    An absolute path always contains the root element and the complete directory list required to locate the file.
    A relative path needs to be combined with another path in order to access a file.
    A symbolic link is a special file that serves as a reference to another file.

####The Path Class
The Path class, introduced in the Java SE 7 release, is one of the primary entrypoints of the java.nio.file package. If you have pre-JDK7 code that uses java.io.File, you can still take advantage of the Path class functionality by using the File.toPath method.

#####Creating a Path
    Path p1 = Paths.get("/tmp/foo");
    Path p2 = Paths.get(args[0]);
    Path p3 = Paths.get(URI.create("file:///Users/joe/FileTest.java"));

    The Paths.get method is shorthand for the following code:
    Path p4 = FileSystems.getDefault().getPath("/users/sally");
    If you are on windows:
    Path p5 = Paths.get(System.getProperty("user.home"),"logs", "foo.log");

#####Retrieving Information about a Path
    // None of these methods requires that the file corresponding
    // to the Path exists.
    // Microsoft Windows syntax
    Path path = Paths.get("C:\\home\\joe\\foo");

    // Solaris syntax
    Path path = Paths.get("/home/joe/foo");

    System.out.format("toString: %s%n", path.toString());
    System.out.format("getFileName: %s%n", path.getFileName());
    System.out.format("getName(0): %s%n", path.getName(0));
    System.out.format("getNameCount: %d%n", path.getNameCount());
    System.out.format("subpath(0,2): %s%n", path.subpath(0,2));
    System.out.format("getParent: %s%n", path.getParent());
    System.out.format("getRoot: %s%n", path.getRoot());

#####Removing Redundancies From a Path
Many file systems use "." notation to denote the current directory and ".." to denote the parent directory.

    The normalize method removes any redundant elements, which includes any "." or "directory/.." occurrences.

#####Converting a Path
    public class FileTest {
        public static void main(String[] args) {

            if (args.length < 1) {
                System.out.println("usage: FileTest file");
                System.exit(-1);
            }

            // Converts the input string to a Path object.
            Path inputPath = Paths.get(args[0]);
            Path fullPath = inputPath.toAbsolutePath(); //convert a path to an absolute path.
            Path p1 = Paths.get("/home/logfile");
            System.out.format("%s%n", p1.toUri());      //convert a path to a string that can be opened from a browser
            Path fp =p1.toRealPath();                   //return the real path of an existing file.
        }
    }

#####Joining Two Paths
    //Solaris
    Path p1 = Paths.get("/home/joe/foo");
    System.out.format("%s%n", p1.resolve("bar"));       //result is /home/joe/foo/bar

    //Windows
    Path p1 = Paths.get("C:\\home\\joe\\foo");
    System.out.format("%s%n", p1.resolve("bar");        //result is C:\home\joe\foo

#####Creating a Path Between Two Paths
    Path p1 = Paths.get("joe");
    Path p2 = Paths.get("sally");
    Path p1_to_p2 = p1.relativize(p2);      // Result is ../sally
    Path p2_to_p1 = p2.relativize(p1);      // Result is ../joe

    Path p1 = Paths.get("home");
    Path p3 = Paths.get("home/sally/bar");
    Path p1_to_p3 = p1.relativize(p3);      // Result is sally/bar
    Path p3_to_p1 = p3.relativize(p1);      // Result is ../..

A relative path cannot be constructed if only one of the paths includes a root elemetn. If both paths include a root element, the capability to construct a relative path is system dependent.

#####Comparing Two Paths
    Path path = ...;
    Path otherPath = ...;
    Path beginning = Paths.get("/home");
    Path ending = Paths.get("foo");

    if (path.equals(otherPath)) {
        // equality logic here
    } else if (path.startsWith(beginning)) {
        // path begins with "/home"
    } else if (path.endsWith(ending)) {
        // path ends with "foo"
    }

    //The Path class implements the Iterable interface.
    Path path = ...;
    for (Path name: path) {
        System.out.println(name);
    }

####File Operations
The Files class is the other primary entrypoint of the java.nio.file package.

#####Releasing System Resources
Many of the resources that are used in this API, such as streams or channels, implement or extend the java.io.Closeable interface.

#####Catching Exceptions
All methods that access the file system can throw an IOException.

    Charset charset = Charset.forName("US-ASCII");
    String s = ...;
    try (BufferedWriter writer = Files.newBufferedWriter(file, charset)) {
        writer.write(s, 0, s.length());
    } catch (IOException x) {
        System.err.format("IOException: %s%n", x);
    }

#####Varargs
    import static java.nio.file.StandardCopyOption.*;

    Path source = ...;
    Path target = ...;
    Files.move(source, target, REPLACE_EXISTING, ATOMIC_MOVE);

#####Atomic Operations
Several Files methods, such as move, can perform certain operations atomically in some file systems.

#####Method Chaining
    String value = Charset.defaultCharset().decode(buf).toString();
    UserPrincipal group = file.getFileSystem().getUserPrincipalLookupService().lookupPrincipalByName("me");

#####What Is a Glob?
A glob pattern is specified as a string and is matched against other strings, such as directory or file names. Glob syntax follows several simple rules:

    An asterisk, *, matches any number of characters (including none).
    Two asterisks, **, works like * but crosses directory boundaries.
    A question mark, ?, matches exactly one character.
    Braces specify a collection of subpatterns. For example: {sun, moon, starts} {temp*, tmp*}
    Square brackets convey a set of single characters or, when the hyphen character (-) is used, a range of characters. For example, [aeiou] [0-9] [A-Z] [a-z, A-Z]
    All other characters match themselves.
    To match *, ?, or the other special characters, you can escape them by using the backslash character, \. For exmaple: \\, \?, \*

#####Link Awareness
The Files class is "link aware."

####Checking a File or Directory

#####Verifying the Existence of a File or Directory
    Files.exists(path)
    Files.notExists(path)

#####Checking File Accessibility
    Files.isReadable(path)
    Files.isWritable(path)
    Files.isExecutable(path)

#####Checking Whether Two Paths Locate the Same File
    Files.isSameFile(p1, p2)

####Deleting a File or Directory
    try {
        Files.delete(path);
    } catch (NoSuchFileException x) {
        System.err.format("%s: no such" + " file or directory%n", path);
    } catch (DirectoryNotEmptyException x) {
        System.err.format("%s not empty%n", path);
    } catch (IOException x) {
        // File permission problems are caught here.
        System.err.println(x);
    }

####Copying a File or Directory
    import static java.nio.file.StandardCopyOption.*;
    ...
    Files.copy(source, target, REPLACE_EXISTING);
    //Options: REPLACE_EXISTING, COPY_ATTRIBUTES, NOFOLLOW_LINKS

####Moving a File or Directory
    import static java.nio.file.StandardCopyOption.*;
    ...
    Files.move(source, target, REPLACE_EXISTING);
    //Options: REPLACE_EXISTING, ATOMIC_MOVE

####Managing Metadata
    size(Path) 	Returns the size of the specified file in bytes.
    isDirectory(Path, LinkOption) 	Returns true if the specified Path locates a file that is a directory.
    isRegularFile(Path, LinkOption...) 	Returns true if the specified Path locates a file that is a regular file.
    isSymbolicLink(Path) 	Returns true if the specified Path locates a file that is a symbolic link.
    isHidden(Path) 	Returns true if the specified Path locates a file that is considered hidden by the file system.
    getLastModifiedTime(Path, LinkOption...)
    setLastModifiedTime(Path, FileTime) 	Returns or sets the specified file's last modified time.
    getOwner(Path, LinkOption...)
    setOwner(Path, UserPrincipal) 	Returns or sets the owner of the file.
    getPosixFilePermissions(Path, LinkOption...)
    setPosixFilePermissions(Path, Set<PosixFilePermission>) 	Returns or sets a file's POSIX file permissions.
    getAttribute(Path, String, LinkOption...)
    setAttribute(Path, String, Object, LinkOption...) 	Returns or sets the value of a file attribute.

    readAttributes(Path, String, LinkOption...) 	Reads a file's attributes as a bulk operation. The String parameter identifies the attributes to be read.
    readAttributes(Path, Class<A>, LinkOption...) 	Reads a file's attributes as a bulk operation. The Class<A> parameter is the type of attributes requested and the method returns an object of that class.

####Reading, Writing, and Creating Files

#####The OpenOptions Parameter
The following StandardOpenOptions enums are supported:

    WRITE – Opens the file for write access.
    APPEND – Appends the new data to the end of the file. This option is used with the WRITE or CREATE options.
    TRUNCATE_EXISTING – Truncates the file to zero bytes. This option is used with the WRITE option.
    CREATE_NEW – Creates a new file and throws an exception if the file already exists.
    CREATE – Opens the file if it exists or creates a new file if it does not.
    DELETE_ON_CLOSE – Deletes the file when the stream is closed. This option is useful for temporary files.
    SPARSE – Hints that a newly created file will be sparse. This advanced option is honored on some file systems, such as NTFS, where large files with data "gaps" can be stored in a more efficient manner where those empty gaps do not consume disk space.
    SYNC – Keeps the file (both content and metadata) synchronized with the underlying storage device.
    DSYNC – Keeps the file content synchronized with the underlying storage device.

#####Commonly Used Methods for Small Files
    Path file = ...;
    byte[] fileArray;
    fileArray = Files.readAllBytes(file);

    byte[] buf = ...;
    Files.write(file, buf);

#####Buffered I/O Methods for Text Files
    import java.nio.file

    Charset charset = Charset.forName("US-ASCII");
    try (BufferedReader reader = Files.newBufferedReader(file, charset)) {
        String line = null;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
    } catch (IOException x) {
        System.err.format("IOException: %s%n", x);
    }

    Charset charset = Charset.forName("US-ASCII");
    String s = ...;
    try (BufferedWriter writer = Files.newBufferedWriter(file, charset)) {
        writer.write(s, 0, s.length());
    } catch (IOException x) {
        System.err.format("IOException: %s%n", x);
    }

#####Methods for Unbuffered Streams and Interoperable with java.io APIs
    Path file = ...;
    try (InputStream in = Files.newInputStream(file);
        BufferedReader reader =
          new BufferedReader(new InputStreamReader(in))) {
        String line = null;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
    } catch (IOException x) {
        System.err.println(x);
    }

    import static java.nio.file.StandardOpenOption.*;

    Path logfile = ...;
    String s = ...;
    byte data[] = s.getBytes();// Convert the string to a byte array.

    try (OutputStream out = new BufferedOutputStream(
                     logfile.newOutputStream(CREATE, APPEND))) {
        ...
        out.write(data, 0, data.length);
    } catch (IOException x) {
        System.err.println(x);
    }

#####Methods for Channels and ByteBuffers
    // Defaults to READ
    try (SeekableByteChannel sbc = Files.newByteChannel(file)) {
        ByteBuffer buf = ByteBuffer.allocate(10);

        // Read the bytes with the proper encoding for this platform.  If
        // you skip this step, you might see something that looks like
        // Chinese characters when you expect Latin-style characters.
        String encoding = System.getProperty("file.encoding");
        while (sbc.read(buf) > 0) {
            buf.rewind();
            System.out.print(Charset.forName(encoding).decode(buf));
            buf.flip();
        }
    } catch (IOException x) {
        System.out.println("caught exception: " + x);
    }

    //Write
    import static java.nio.file.StandardCopyOption.*;

    // Create the set of options for appending to the file.
    Set<OpenOptions> options = new HashSet<OpenOption>();
    options.add(APPEND);
    options.add(CREATE);

    // Create the custom permissions attribute.
    Set<PosixFilePermission> perms =
        PosixFilePermissions.fromString("rw-r------");
    FileAttribute<Set<PosixFilePermission>> attr =
        PosixFilePermissions.asFileAttribute(perms);

    // Convert the string to a ByteBuffer.
    String s = ...;
    byte data[] = s.getBytes();
    ByteBuffer bb = ByteBuffer.wrap(data);

    try (SeekableByteChannel sbc = Files.newByteChannel(file, options, attr)) {
        sbc.write(bb);
    } catch (IOException x) {
        System.out.println("exception thrown: " + x);
    }

#####Methods for Creating Regular and Temporary Files
    Path file = ...;
    try {
        // Create the empty file with default permissions, etc.
        Files.createFile(file);
    } catch (FileAlreadyExistsException x) {
        System.err.format("file named %s" +
            " already exists%n", file);
    } catch (IOException x) {
        // Some other sort of failure, such as permissions.
        System.err.format("createFile error: %s%n", x);
    }

    try {
        Path tempFile = Files.createTempFile(null, ".myapp");
        System.out.format("The temporary file" + " has been created: %s%n", tempFile);
    } catch (IOException x) {
        System.err.format("IOException: %s%n", x);
    }

####Random Access Files

    position – Returns the channel's current position
    position(long) – Sets the channel's position
    read(ByteBuffer) – Reads bytes into the buffer from the channel
    write(ByteBuffer) – Writes bytes from the buffer to the channel
    truncate(long) – Truncates the file (or other entity) connected to the channel

    String s = "I was here!\n";
    byte data[] = s.getBytes();
    ByteBuffer out = ByteBuffer.wrap(data);

    ByteBuffer copy = ByteBuffer.allocate(12);

    try (FileChannel fc = (FileChannel.open(file, READ, WRITE))) {
        // Read the first 12
        // bytes of the file.
        int nread;
        do {
            nread = fc.read(copy);
        } while (nread != -1 && copy.hasRemaining());

        // Write "I was here!" at the beginning of the file.
        fc.position(0);
        while (out.hasRemaining())
            fc.write(out);
        out.rewind();

        // Move to the end of the file.  Copy the first 12 bytes to
        // the end of the file.  Then write "I was here!" again.
        long length = fc.size();
        fc.position(length-1);
        copy.flip();
        while (copy.hasRemaining())
            fc.write(copy);
        while (out.hasRemaining())
            fc.write(out);
    } catch (IOException x) {
        System.out.println("I/O Exception: " + x);
    }

####Creating and Reading Directories

#####Listing a File System's Root Directories
    Iterable<Path> dirs = FileSystems.getDefault().getRootDirectories();
    for (Path name: dirs) {
        System.err.println(name);
    }

#####Creating a Directory
    try {
        Path path = Paths.get(System.getProperty("user.dir") + "/path");
        Files.createDirectory(path);
    } catch (IOException ex) {
        System.out.println(ex.toString());
    }

#####Creating a Temporary Directory
    try {
        Path path = Paths.get(System.getProperty("user.dir"));
        Files.createTempDirectory(path, "temp");
    } catch (IOException ex) {
        System.out.println(ex.toString());
    }

#####Listing a Directory's Contents
    Path dir = Paths.get(System.getProperty("user.dir"));
    try (DirectoryStream<Path> stream = Files.newDirectoryStream(dir)) {
        for (Path file: stream) {
            System.out.println(file.getFileName());
        }
    } catch (IOException | DirectoryIteratorException x) {
        // IOException can never be thrown by the iteration.
        // In this snippet, it can only be thrown by newDirectoryStream.
        System.err.println(x);
    }

#####Filtering a Directory Listing By Using Globbing
    Path dir = Paths.get(System.getProperty("user.dir"));
    try (DirectoryStream<Path> stream =
         Files.newDirectoryStream(dir, "*.{java,class,jar}")) {
        for (Path entry: stream) {
            System.out.println(entry.getFileName());
        }
    } catch (IOException x) {
        // IOException can never be thrown by the iteration.
        // In this snippet, it can // only be thrown by newDirectoryStream.
        System.err.println(x);
    }

#####Writing Your Own Directory Filter
    DirectoryStream.Filter<Path> filter = new DirectoryStream.Filter<Path>() {
        public boolean accept(Path path) {
            return (Files.isDirectory(path));
        }
    };

    Path dir = Paths.get(System.getProperty("user.dir"));
    try (DirectoryStream<Path> stream = Files.newDirectoryStream(dir, filter)) {
        for (Path entry: stream) {
            System.out.println(entry.getFileName());
        }
    } catch (IOException x) {
        System.err.println(x);
    }

####Links, Symbolic or Otherwise
Hard links are more restrictive than symbolic links, as follows:

    The target of the link must exist.
    Hard links are generally not allowed on directories.
    Hard links are not allowed to cross partitions or volumes. Therefore, they cannot exist across file systems.
    A hard link looks, and behaves, like a regular file, so they can be hard to find.
    A hard link is, for all intents and purposes, the same entity as the original file. They have the same file permissions, time stamps, and so on. All attributes are identical.

Because of these restrictions, hard links are not used as often as symbolic links, but the Path methods work seamlessly with hard links.

#####Creating a Symbolic Link
    String path = System.getProperty("user.dir");
    Path newLink = Paths.get(path + "/Point.lnk");;
    Path target = Paths.get(path + "/com/cbay/Point.java");
    try {
        Files.createSymbolicLink(newLink, target);
    } catch (IOException x) {
        System.err.println(x);
    } catch (UnsupportedOperationException x) {
        // Some file systems do not support symbolic links.
        System.err.println(x);
    }

#####Creating a Hard Link
    String path = System.getProperty("user.dir");
    Path newLink = Paths.get(path + "/Point.jv");
    Path existingFile = Paths.get(path + "/com/cbay/Point.java");
    try {
        Files.createLink(newLink, existingFile);
    } catch (IOException x) {
        System.err.println(x);
    } catch (UnsupportedOperationException x) {
        // Some file systems do not
        // support adding an existing
        // file to a directory.
        System.err.println(x);
    }

#####Detecting a Symbolic Link
    String path = System.getProperty("user.dir");
    path += "/Point.jv";
    Path file = Paths.get(path);
    try {
        boolean isSymbolicLink = Files.isSymbolicLink(file);
        if (isSymbolicLink) {
            System.out.println(path + " is a symbolic link.");
        } else {
            System.out.println(path + " is not a symbolic link.");
        }
    } catch (UnsupportedOperationException x) {
        // Some file systems do not
        // support adding an existing
        // file to a directory.
        System.err.println(x);
    }

#####Finding the Target of a Link
    String path = System.getProperty("user.dir");
    Path link = Paths.get(path + "/Point.lnk");
    try {
        Path target = Files.readSymbolicLink(link);
        System.out.format("Target of link " +
            "'%s' is '%s'%n", link, target);
    } catch (IOException x) {
        System.err.println(x);
    } catch (UnsupportedOperationException x) {
        // Some file systems do not
        // support adding an existing
        // file to a directory.
        System.err.println(x);
    }

####Walking the File Tree

#####The FileVisitor Interface
To walk a file tree, you first need to implement a FileVisitor. The interface has four methods that correspond to these situations:


    preVisitDirectory – Invoked before a directory's entries are visited.
    postVisitDirectory – Invoked after all the entries in a directory are visited. If any errors are encountered, the specific exception is passed to the method.
    visitFile – Invoked on the file being visited. The file's BasicFileAttributes is passed to the method, or you can use the file attributes package to read a specific set of attributes. For example, you can choose to read the file's DosFileAttributeView to determine if the file has the "hidden" bit set.
    visitFileFailed – Invoked when the file cannot be accessed. The specific exception is passed to the method. You can choose whether to throw the exception, print it to the console or a log file, and so on.

#####Kickstarting the Process
There are two walkFileTree methods in the Files class.

    walkFileTree(Path, FileVisitor)
    walkFileTree(Path, Set<FileVisitOption>, int, FileVisitor)

    Path startingDir = Paths.get(System.getProperty("user.dir"));

    System.out.println("[INFO] walkFileTree(Path, FileVisitor)");
    PrintFiles pf = new PrintFiles();
    try {
        Files.walkFileTree(startingDir, pf);
    } catch (IOException e) {
        System.err.println(e);
    }
    //遍历的时候跟踪链接
    System.out.println("");
    System.out.println("[INFO] walkFileTree(Path, Set<FileVisitOption>, int, FileVisitor)");
    EnumSet<FileVisitOption> opts = EnumSet.of(FOLLOW_LINKS);
    try {
        String pattern = "*.{java,class,jar}";
        Finder finder = new Finder(pattern);
        Files.walkFileTree(startingDir, opts, Integer.MAX_VALUE, finder);
    } catch (IOException e) {
        System.err.println(e);
    }

#####Considerations When Creating a FileVisitor
    @Override
    public FileVisitResult
        visitFileFailed(Path file,
            IOException exc) {
        if (exc instanceof FileSystemLoopException) {
            System.err.println("cycle detected: " + file);
        } else {
            System.err.format("Unable to copy:" + " %s: %s%n", file, exc);
        }
        return CONTINUE;
    }

#####Controlling the Flow
The FileVisitor methods return a FileVisitResult value. You can abort the file walking process or control whether a directory is visited by the values you return in the FileVisitor methods:

    CONTINUE – Indicates that the file walking should continue. If the preVisitDirectory method returns CONTINUE, the directory is visited.
    TERMINATE – Immediately aborts the file walking. No further file walking methods are invoked after this value is returned.
    SKIP_SUBTREE – When preVisitDirectory returns this value, the specified directory and its subdirectories are skipped. This branch is "pruned out" of the tree.
    SKIP_SIBLINGS – When preVisitDirectory returns this value, the specified directory is not visited, postVisitDirectory is not invoked, and no further unvisited siblings are visited. If returned from the postVisitDirectory method, no further siblings are visited. Essentially, nothing further happens in the specified directory.

####Finding Files
    PathMatcher matcher =
        FileSystems.getDefault().getPathMatcher("glob:*.{java,class}");
    Path filename = Paths.get("Test.java");
    if (matcher.matches(filename)) {
        System.out.format("'%s' does match.%n", filename);
    } else {
        System.out.format("'%s' does not match.%n", filename);
    }
    
    System.out.println("");
    System.out.println("[INFO] testFinder()");
    TestFinder tf = new TestFinder();
    tf.testFinder();

####Watching a Directory for Changes
The java.nio.file package provides a file change notification API, called the Watch Service API.

#####Watch Service Overview
Here are the basic steps required to implement a watch service:

    Create a WatchService "watcher" for the file system.
    For each directory that you want monitored, register it with the watcher. When registering a directory, you specify the type of events for which you want notification. You receive a WatchKey instance for each directory that you register.
    Implement an infinite loop to wait for incoming events. When an event occurs, the key is signaled and placed into the watcher's queue.
    Retrieve the key from the watcher's queue. You can obtain the file name from the key.
    Retrieve each pending event for the key (there might be multiple events) and process as needed.
    Reset the key, and resume waiting for events.
    Close the service: The watch service exits when either the thread exits or when it is closed (by invoking its closed method).

#####Creating a Watch Service and Registering for Events
    import static java.nio.file.StandardWatchEventKinds.*;

    WatchService watcher = FileSystems.getDefault().newWatchService();

    Path dir = ...;
    try {
        WatchKey key = dir.register(watcher,
                               ENTRY_CREATE,    //a directory entry is created.
                               ENTRY_DELETE,    //a directory entry is deleted.
                               ENTRY_MODIFY);   //a directory entry is modified.
    } catch (IOException x) {
        System.err.println(x);
    }

#####Processing Events
The order of events in an event processing loop follow:

    Get a watch key.
    Process the pending events for the key.
    Retrieve the type of event by using the kind method.
    Retrieve the file name associated with the event.
    After the events for the key have been processed, you need to put the key back into a ready state by invoking reset. If this method returns false, the key is no longer valid and the loop can exit. This step is very important. If you fail to invoke reset, this key will not receive any further events.

#####Retrieving the File Name
    WatchEvent<Path> ev = (WatchEvent<Path>)event;
    Path filename = ev.context();
    
    @SuppressWarnings("unchecked")      //avoid 'uses unchecked or unsafe operations' error.
    static <T> WatchEvent<T> cast(WatchEvent<?> event) {
        return (WatchEvent<Path>)event;
    }

####Other Useful Methods

#####Determining MIME Type
MIME - Multipurpose Internet Mail Extensions.

    Path filename = Paths.get("OutFile.txt");
    try {
        String type = Files.probeContentType(filename);
        if (type == null) {
            System.err.format("'%s' has an" + " unknown filetype.%n", filename);
        } else if (type.equals("text/plain")) {
            System.out.format("'%s' is " + "a plain text file.%n", filename);
            //continue;
        } else {
            System.out.format("'%s' is " + "%s%n", filename, type);
        }
    } catch (IOException x) {
        System.err.println(x);
    }

#####Default File System
    PathMatcher matcher =
        FileSystems.getDefault().getPathMatcher("glob:*.*");

#####Path String Separator
    String separator = File.separator;
    String separator = FileSystems.getDefault().getSeparator();

#####File System's File Stores
A file system has one or more file stores to hold its files and directories. The file store represents the underlying storage device.
    
    FileSystem fs = FileSystems.getDefault();
    for (FileStore store: fs.getFileStores()) {
        DiskUsage.printFileStore(store);
    }

####Legacy File I/O Code
The java.io.File class provides the toPath method, which converts an old style File instance to a java.nio.file.Path instance, as follows:

    try {
        File file = new File("TestApp$1.class");
        if(file.isDirectory()){
            System.out.println(file.getPath());
        }
        file.delete();
        Path fp = file.toPath();
        Files.delete(fp);
    } catch (IOException ex) {
        System.err.println(ex.toString());
    }
    
## Concurrency

    java.util.concurrent

### Processes and Threads
In concurrent programming, there are two basic units of execution: processes and threads.

####Processes
A process has a self-contained execution environment. A process generally has a complete, private set of basic run-time resources; in particular, each process has its own memory space.

####Threads
Threads exist within a process -- every process has at least one. Threads share the process's resources, including memory and open files.

###Thread Objects
Each thread is associated with an instance of the class Thread. There are two basic strategies for using Thread objects to create a concurrent application.

    To directly control thread creation and management, simply instantiate Thread each time the application needs to initiate an asynchronous task.
    To abstract thread management from the rest of your application, pass the application's tasks to an executor.

####Defining and Starting a Thread
An application that creates an instance of Thread must provide the code that will run in that thread. There are two ways to do this:

#####Provide a Runnable object
public class HelloRunnable implements Runnable {

    public void run() {
        System.out.println("Hello from a thread which implements runnable!");
    }

    public static void main(String args[]) {
        (new Thread(new HelloRunnable())).start();
    }

}

#####Subclass Thread
public class HelloThread extends Thread {

    public void run() {
        System.out.println("Hello from a thread which extends thread!");
    }

    public static void main(String args[]) {
        (new HelloThread()).start();
    }

}

`Notice that both examples invoke Thread.start in order to start the new thread.`

####Pausing Execution with Sleep
`Thread.sleep` causes the current thread to suspend execution for a specified period.

####Interrupts
An interrupt is an indication to a thread that it should stop what it is doing and do something else. A thread sends an interrupt by invoking `interrupt` on the Thread object for the thread to be interrupted.

    if (Thread.interrupted()) {
        throw new InterruptedException();
    }

####Joins
The `join` method allows one thread to wait for the completion of another. If t is a Thread object whose thread is currently executing, `t.join();` causes the current thread to pause execution until t's thread terminates.

####The SimpleThreads Example
    public class SimpleThreads {

        // Display a message, preceded by
        // the name of the current thread
        public static void threadMessage(String message) {
            String threadName =
                Thread.currentThread().getName();
            System.out.format("%s: %s%n",
                              threadName,
                              message);
        }

        public static class MessageLoop
            implements Runnable {
            public void run() {
                String importantInfo[] = {
                    "Mares eat oats",
                    "Does eat oats",
                    "Little lambs eat ivy",
                    "A kid will eat ivy too"
                };
                try {
                    for (int i = 0;
                         i < importantInfo.length;
                         i++) {
                        // Pause for 4 seconds
                        Thread.sleep(4000);
                        // Print a message
                        threadMessage(importantInfo[i]);
                    }
                } catch (InterruptedException e) {
                    threadMessage("I wasn't done!");
                }
            }
        }

        public static void main(String args[])
            throws InterruptedException {

            // Delay, in milliseconds before
            // we interrupt MessageLoop
            // thread (default one hour).
            long patience = 1000 * 60 * 60;

            // If command line argument
            // present, gives patience
            // in seconds.
            if (args.length > 0) {
                try {
                    patience = Long.parseLong(args[0]) * 1000;
                } catch (NumberFormatException e) {
                    System.err.println("Argument must be an integer.");
                    System.exit(1);
                }
            }

            threadMessage("Starting MessageLoop thread");
            long startTime = System.currentTimeMillis();
            Thread t = new Thread(new MessageLoop());
            t.start();

            threadMessage("Waiting for MessageLoop thread to finish");
            // loop until MessageLoop
            // thread exits
            while (t.isAlive()) {
                threadMessage("Still waiting...");
                // Wait maximum of 1 second
                // for MessageLoop thread
                // to finish.
                t.join(1000);
                if (((System.currentTimeMillis() - startTime) > patience)
                      && t.isAlive()) {
                    threadMessage("Tired of waiting!");
                    t.interrupt();
                    // Shouldn't be long now
                    // -- wait indefinitely
                    t.join();
                }
            }
            threadMessage("Finally!");
        }
    }

###Synchronization
Threads communicate primarily by sharing access to fields and the objects reference fields refer to. This form of communication is extremely efficient, but makes two kinds of errors possible: thread interference and memory consistency errors. The tool needed to prevent these errors is synchronization.

####Thread Interference
Interference happens when two operations, running in different threads, but acting on the same data, interleave. This means that the two operations consist of multiple steps, and the sequences of steps overlap.

####Memory Consistency Errors
Memory consistency errors occur when different threads have inconsistent views of what should be the same data. The key to avoiding memory consistency errors is understanding the happens-before relationship.

####Synchronized Methods
The Java programming language provides two basic synchronization idioms: synchronized methods and synchronized statements. `To make a method synchronized, simply add the synchronized keyword to its declaration`
    
    public synchronized void increment() {
        c++;
    }
    
####Intrinsic Locks and Synchronization
Synchronization is built around an internal entity known as the intrinsic lock or monitor lock. Intrinsic locks play a role in both aspects of synchronization: enforcing exclusive access to an object's state and establishing happens-before relationships that are essential to visibility.

#####Locks in Synchronized Methods
When a thread invokes a synchronized method, it automatically acquires the intrinsic lock for that method's object and releases it when the method returns. The lock occurs even if the return was caused by an uncaught exception.

#####Synchronized Statements
Another way to create synchronized code is with synchronized statements. Unlike synchronized methods, synchronized statements must specify the object that provides the intrinsic lock:

    public void addName(String name) {
        synchronized(this) {
            lastName = name;
            nameCount++;
        }
        nameList.add(name);
    }

#####Reentrant Synchronization
Recall that a thread cannot acquire a lock owned by another thread. But a thread can acquire a lock that it already owns. Allowing a thread to acquire the same lock more than once enables reentrant synchronization.

####Atomic Access
In programming, an atomic action is one that effectively happens all at once.

    Reads and writes are atomic for reference variables and for most primitive variables (all types except long and double).
    Reads and writes are atomic for all variables declared volatile (including long and double variables).

###Liveness
A concurrent application's ability to execute in a timely manner is known as its liveness.

####Deadlock
Deadlock describes a situation where two or more threads are blocked forever, waiting for each other.

####Starvation and Livelock

#####Starvation
Starvation describes a situation where a thread is unable to gain regular access to shared resources and is unable to make progress.

#####Livelock
A thread often acts in response to the actionof another thread.

####Guarded Blocks
Threads often have to coordinate their actins. The most common coordination idiom is the guarded block. Such a block begins by polling a condition that must be true before the block can proceed.

    public synchronized void guardedJoy() {
        // This guard only loops once for each special event, which may not
        // be the event we're waiting for.
        while(!joy) {
            try {
                wait();
            } catch (InterruptedException e) {}
        }
        System.out.println("Joy and efficiency have been achieved!");
    }

###Immutable Objects
An object is considered immutable if its state cannot change after it is constructed.

####A Synchronized Class Example
    public class SynchronizedRGB {

        // Values must be between 0 and 255.
        private int red;
        private int green;
        private int blue;
        private String name;

        private void check(int red,
                           int green,
                           int blue) {
            if (red < 0 || red > 255
                || green < 0 || green > 255
                || blue < 0 || blue > 255) {
                throw new IllegalArgumentException();
            }
        }

        public SynchronizedRGB(int red,
                               int green,
                               int blue,
                               String name) {
            check(red, green, blue);
            this.red = red;
            this.green = green;
            this.blue = blue;
            this.name = name;
        }

        public void set(int red,
                        int green,
                        int blue,
                        String name) {
            check(red, green, blue);
            synchronized (this) {
                this.red = red;
                this.green = green;
                this.blue = blue;
                this.name = name;
            }
        }

        public synchronized int getRGB() {
            return ((red << 16) | (green << 8) | blue);
        }

        public synchronized String getName() {
            return name;
        }

        public synchronized void invert() {
            red = 255 - red;
            green = 255 - green;
            blue = 255 - blue;
            name = "Inverse of " + name;
        }
    }

####A Strategy for Defining Immutable Objects
The following rules define a simple strategy for creating immutable objects.
    
    Don't provide "setter" methods — methods that modify fields or objects referred to by fields.
    Make all fields final and private.
    Don't allow subclasses to override methods. The simplest way to do this is to declare the class as final. A more sophisticated approach is to make the constructor private and construct instances in factory methods.
    If the instance fields include references to mutable objects, don't allow those objects to be changed:
        Don't provide methods that modify the mutable objects.
        Don't share references to the mutable objects. Never store references to external, mutable objects passed to the constructor; if necessary, create copies, and store references to the copies. Similarly, create copies of your internal mutable objects when necessary to avoid returning the originals in your methods.

After these changes, we have ImmutableRGB:

    final public class ImmutableRGB {

        // Values must be between 0 and 255.
        final private int red;
        final private int green;
        final private int blue;
        final private String name;

        private void check(int red,
                           int green,
                           int blue) {
            if (red < 0 || red > 255
                || green < 0 || green > 255
                || blue < 0 || blue > 255) {
                throw new IllegalArgumentException();
            }
        }

        public ImmutableRGB(int red,
                            int green,
                            int blue,
                            String name) {
            check(red, green, blue);
            this.red = red;
            this.green = green;
            this.blue = blue;
            this.name = name;
        }


        public int getRGB() {
            return ((red << 16) | (green << 8) | blue);
        }

        public String getName() {
            return name;
        }

        public ImmutableRGB invert() {
            return new ImmutableRGB(255 - red,
                           255 - green,
                           255 - blue,
                           "Inverse of " + name);
        }
    }

###High Level Concurrency Objects
    java.util.concurrent

####Lock Objects
    import java.util.concurrent.locks.Lock;
    import java.util.concurrent.locks.ReentrantLock;
    import java.util.Random;

    public class Safelock {
        static class Friend {
            private final String name;
            private final Lock lock = new ReentrantLock();

            public Friend(String name) {
                this.name = name;
            }

            public String getName() {
                return this.name;
            }

            public boolean impendingBow(Friend bower) {
                Boolean myLock = false;
                Boolean yourLock = false;
                try {
                    myLock = lock.tryLock();
                    yourLock = bower.lock.tryLock();
                } finally {
                    if (! (myLock && yourLock)) {
                        if (myLock) {
                            lock.unlock();
                        }
                        if (yourLock) {
                            bower.lock.unlock();
                        }
                    }
                }
                return myLock && yourLock;
            }
                
            public void bow(Friend bower) {
                if (impendingBow(bower)) {
                    try {
                        System.out.format("%s: %s has"
                            + " bowed to me!%n", 
                            this.name, bower.getName());
                        bower.bowBack(this);
                    } finally {
                        lock.unlock();
                        bower.lock.unlock();
                    }
                } else {
                    System.out.format("%s: %s started"
                        + " to bow to me, but saw that"
                        + " I was already bowing to"
                        + " him.%n",
                        this.name, bower.getName());
                }
            }

            public void bowBack(Friend bower) {
                System.out.format("%s: %s has" +
                    " bowed back to me!%n",
                    this.name, bower.getName());
            }
        }

        static class BowLoop implements Runnable {
            private Friend bower;
            private Friend bowee;

            public BowLoop(Friend bower, Friend bowee) {
                this.bower = bower;
                this.bowee = bowee;
            }
        
            public void run() {
                Random random = new Random();
                for (;;) {
                    try {
                        Thread.sleep(random.nextInt(10));
                    } catch (InterruptedException e) {}
                    bowee.bow(bower);
                }
            }
        }
                

        public static void main(String[] args) {
            final Friend alphonse =
                new Friend("Alphonse");
            final Friend gaston =
                new Friend("Gaston");
            new Thread(new BowLoop(alphonse, gaston)).start();
            new Thread(new BowLoop(gaston, alphonse)).start();
        }
    }

####Executors
Objects that encapsulate these thread functions are known as executors.

#####Executor Interfaces
The java.util.concurrent package defines three executor interfaces:

    Executor, a simple interface that supports launching new tasks.
    ExecutorService, a subinterface of Executor, which adds features that help manage the lifecycle, both of the individual tasks and of the executor itself.
    ScheduledExecutorService, a subinterface of ExecutorService, supports future and/or periodic execution of tasks.

######The Executor Interface
    (new Thread(r)).start();
    e.execute(r);

######The ExecutorService Interface
The ExecutorService interface supplements execute with a similar, but more versatile submit method.

######The ScheduledExecutorService Interface
The ScheduledExecutorService interface supplements the methods of its parent ExecutorService with schedule, which executes a Runnable or Callable task after a specified delay. In addition, the interface defines scheduleAtFixedRate and scheduleWithFixedDelay, which executes specified tasks repeatedly, at defined intervals.

#####Thread Pools
Most of the executor implementations in `java.util.concurrent` use thread pools, which consist of worker threads. This kind of thread exists separately from the Runnable and Callable tasks it executes and is often used to execute multiple tasks.

An important advantage of the fixed thread pool is that applications using it degrade gracefully. A simple way to create an executor that uses a fixed thread pool is to invoke the newFixedThreadPool factory method in java.util.concurrent.Executors This class also provides the following factory methods:

    The newCachedThreadPool method creates an executor with an expandable thread pool. This executor is suitable for applications that launch many short-lived tasks.
    The newSingleThreadExecutor method creates an executor that executes a single task at a time.
    Several factory methods are ScheduledExecutorService versions of the above executors.

#####Fork/Join





## Q & A

###warning: unchecked call to getDeclaredMethod as a member of the raw type Class
####Example
    import java.lang.reflect.Method;

    public class Warning {
        void m() {
            try {
                Warning warn = new Warning();
                Class c = warn.getClass();
                Method m = c.getDeclaredMethod("m");
            } catch (NoSuchMethodException x) {
                x.printStackTrace();
            }
        }
    }
    $ javac Warning.java
    Note: Warning.java uses unchecked or unsafe operations.
    Note: Recompile with -Xlint:unchecked for details.
    $ javac -Xlint:unchecked Warning.java
    Warning.java:8: warning: [unchecked] unchecked call to getDeclaredMethod            (java.lang.String,java.lang.Class<?>...) as a member of the raw type java.lang.Class
                Method m = c.getDeclaredMethod("m");
                                              ^
    1 warning

####Answer
To remove the warning, the declaration of c should be modified to include an appropriate generic type. In this case, the declation should be:

    Class<?> c = warn.getClass();

(Read more: <http://docs.oracle.com/javase/6/docs/technotes/guides/reflection/enhancements.html>)

###warning: unchecked call to put(K,V) as a member of the raw type Map

####Example
    Map actions = new HashMap();
    for (int i = 0; i < menu.length; i++) {
        Object mnemonic = menu[i][0];
        Object action = menu[i][2];
        actions.put(mnemonic, action);
    }

####Answer
    Map<Object, Object> actions = new HashMap<Object, Object>();

(Read more: <http://www.open-open.com/lib/view/open1353144198545.html>)

## REFERENCES
- [The Java Tutorials](http://docs.oracle.com/javase/tutorial/index.html)
- Core Java 9th Edition, Cay S. Horstmann and Gary Cornell
- [Java内部类的使用小结](http://android.blog.51cto.com/268543/384844)
- [Java对象序列化ObjectOutputStream和ObjectInputStream示例](http://www.linuxidc.com/Linux/2012-08/68360.htm)
- [命令行交互的一种Java实现](http://www.iteye.com/topic/86988)
- [Java获取当前路径](http://www.cnblogs.com/diyunpeng/archive/2011/06/06/2073567.html)
- [Java 判断操作系统类型(适用于各种操作系统)](http://www.2cto.com/kf/201212/180156.html)
- [在控制台输出表格形式的内容](http://www.oschina.net/code/snippet_100347_708)
- [Java™ Platform Standard Ed. 6](http://docs.oracle.com/javase/6/docs/api/)
- [JAVA 反射-getDeclaredMethod()实例](http://bluewens.blog.163.com/blog/static/699130720125445620187/)
- [Java泛型总结](http://www.open-open.com/lib/view/open1353144198545.html)

