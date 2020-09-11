# Java Class 2

#### September 5th, 2020

### Softablitz Class 2 [Recording](https://drive.google.com/file/d/1bQ1yqUEC-87pW8I0VZFfcMCD-bOqNDPq/view?usp=sharing)

## Class Content :-

### Clarification regarding class name and file name in java :-
- We are allowed to **use any name for a filename only when class is not public**. In the case of a public class, we can’t use a different file name.
- The filename must have the same name as the public class name in that file, which is the way to tell the JVM that this is an entry point. Suppose when we create a program in which more than one class resides and after compiling a java source file, it will generate the same number of the .class file as classes reside in our program. In this condition, we will not able to easily identify which class need to interpret by java interpreter and which class containing Entry point for the program.
- As a consequence of above point we can have **only one public class in a single java file**. If you want yous software to have multiple public classes then they have to be in different files.
- As a practice what we do is keep only the main class (Class having main function) Public for JVM to access and rest of the classes are kept as default access specifies or private until and unless it needs to be public.
- For Example:
  If you put the below code in a single file:

    ```java
    public class Employee
    {
        public static void main()
        {
        
        }
    }
    class Manager
    {
            
    }
    ```
  Then you need to name the file as Employee.java only

### Encapsulation :-
- Encapsulation in Java and many OOP languages is the process of wrapping information and functionality in a class and providing methods of accessing them in order to provide a simple way for users to access the information and make use of the functionality of the class.
- Through encapsulation, you can control what parts of a program can access the members of a class. By controlling
access, you can prevent misuse. For example, allowing access to data only through a welldefined set of methods, you can prevent the misuse of that data.
- A class creates a *black box* which may be used, but the inner workings of which are not open to tampering.

#### **[1.java](1.java)**
```java
// This class defines an integer stack that can hold 10 values. 
class Stack {
    /* Now, both stck and tos are private.  This means
        that they cannot be accidentally or maliciously
        altered in a way that would be harmful to the stack.
    */
    private int stck[] = new int[10];
    private int tos;
    
    // Initialize top-of-stack
    Stack() {
        tos = -1;
    }

    // Push an item onto the stack
    void push(int item) {
        if(tos==9) 
        System.out.println("Stack is full.");
        else 
        stck[++tos] = item;
    }

    // Pop an item from the stack
    int pop() {
        if(tos < 0) {
        System.out.println("Stack underflow.");
        return 0;
        }
        else 
        return stck[tos--];
    }
}
class TestStack {
    public static void main(String args[]) {
        Stack mystack1 = new Stack();
        Stack mystack2 = new Stack();

        // push some numbers onto the stack
        for(int i=0; i<10; i++) mystack1.push(i);
        for(int i=10; i<20; i++) mystack2.push(i);

        // pop those numbers off the stack
        System.out.println("Stack in mystack1:");
        for(int i=0; i<10; i++) 
        System.out.println(mystack1.pop());

        System.out.println("Stack in mystack2:");
        for(int i=0; i<10; i++) 
        System.out.println(mystack2.pop());

        // these statements are not legal
        // mystack1.tos = -2;
        // mystack2.stck[3] = 100; 
    }
}
```

### Static Keyword :-
- When a member is declared static, it can be accessed before any objects of its class are created, and without reference to any object.
- You can declare both methods and variables to be static. The most common example of a static member is ```main( )```. ```main( )``` is declared as static because it must be called before any objects exist.
- When objects of its class are declared, no copy of a static variable is made. Instead, all instances of the class share the same static variable.
- Outside of the class in which they are defined, static methods and variables can be used independently of any object. 
- 	 For Static Methods,
    - They can only directly call other static methods.
    - They can only directly access static data.
    - They cannot refer to this or super in any way.

#### **[2.java](2.java)**
```java
class StaticDemo {
    static int a = 42;
    int c;
    static int b = 99;
    static void callme() {
        System.out.println("a = " + a);
    }
}

class StaticByName {
    public static void main(String args[]) {
        StaticDemo.callme();
        StaticDemo a = new StaticDemo();
        StaticDemo b = new StaticDemo();
        int x = a.c;
        int y = StaticDemo.a;

        System.out.println("b = " + StaticDemo.b);
    }
}
```

### final keyword :-

- A field can be declared as final. Doing so prevents its contents from being modified. 
- You must initialize a final field when it is declared. You can do this in one of two ways: 
    - First, you can give it a value when it is declared.
    - Second, you can assign it a value within a constructor.

#### **[3.java](3.java)**
```java
final int FILE_NEW = 1;
final int FILE_OPEN = 2;
final int FILE_SAVE = 3;
final int FILE_SAVEAS = 4;
final int FILE_QUIT = 5;
```

### Inheritance :-

- Using inheritance, you can create a general class that defines traits common to a set of related items.
- To inherit a class, you simply incorporate the definition of one class into another by using the **extends** keyword.
- Although a subclass includes all of the members of its superclass, it cannot access those members of the superclass that have been declared as private.
- Once you have created a superclass that defines the general aspects of an object, that superclass can be inherited to form specialized classes. Each subclass simply adds its own unique attributes. This is the essence of inheritance.

#### **[4.java](4.java)**
```java
// This program uses inheritance to extend Box.
class Box {
    double width;
    double height;
    double depth;

    // construct clone of an object
    Box(Box ob) { // pass object to constructor
        width = ob.width;
        height = ob.height;
        depth = ob.depth;
    }

    // constructor used when all dimensions specified
    Box(double w, double h, double d) {
        width = w;
        height = h;
        depth = d;
    }

    // constructor used when no dimensions specified
    Box() {
        width = -1;  // use -1 to indicate
        height = -1; // an uninitialized
        depth = -1;  // box
    }

    // constructor used when cube is created
    Box(double len) {
        width = height = depth = len;
    }

    // compute and return volume
    double volume() {
        return width * height * depth;
    }
}

// Here, Box is extened to include weight.
class BoxWeight extends Box {
    double weight; // weight of box

    // constructor for BoxWeight
    BoxWeight(double w, double h, double d, double m) {
        width = w;
        height = h;
        depth = d;
        weight = m;
    }    
}

class RefDemo {
    public static void main(String args[]) {
        BoxWeight weightbox = new BoxWeight(3, 5, 7, 8.37);
        Box plainbox = new Box();
        double vol;

        vol = weightbox.volume();
        System.out.println("Volume of weightbox is " + vol);
        System.out.println("Weight of weightbox is " + weightbox.weight);
        System.out.println();

        // assign BoxWeight reference to Box reference
        plainbox = weightbox;

        vol = plainbox.volume(); // OK, volume() defined in Box
        System.out.println("Volume of plainbox is " + vol);

        /* The following statement is invalid because plainbox
        does not define a weight member. */
    //  System.out.println("Weight of plainbox is " + plainbox.weight);
    }
}

```


### super keyword

- Whenever a subclass needs to refer to its immediate superclass, it can do so by use of the keyword super.
- super has two general forms. 
    - The first calls the superclass’ constructor.
    #### **[5.java](5.java)**
    ```java
    // BoxWeight now uses super to initialize its Box attributes.
    class BoxWeight extends Box {
        double weight; // weight of box

        // initialize width, height, and depth using super()
        BoxWeight(double w, double h, double d, double m) {
            super(w, h, d); // call superclass constructor
            weight = m;
        }    
    }
    ```
    - The second is used to access a member of the superclass that has been hidden by a member of a subclass.
    #### **[6.java](6.java)**
    ```java
    // Using super to overcome name hiding.
    class A {
        int i;
    }

    // Create a subclass by extending class A.
    class B extends A {
        int i; // this i hides the i in A

        B(int a, int b) {
            super.i = a; // i in A
            i = b; // i in B
        }

        void show() {
            System.out.println("i in superclass: " + super.i);
            System.out.println("i in subclass: " + i);
        }
    }
    
    class UseSuper {
        public static void main(String args[]) {
            B subOb = new B(1, 2);
            subOb.show();
        }
    }
    ```
- In a class hierarchy, constructors complete their execution in order of derivation, from superclass to subclass. 
- Further, since super( ) must be the first statement executed in a subclass’
constructor, this order is the same whether or not super( ) is used.
- If super( ) is not used, then the default or parameterless constructor of each superclass will be executed. 

#### **[7.java](7.java)**
```java
// Demonstrate when constructors are called.

// Create a super class.
class A {
    A() { 
        System.out.println("Inside A's constructor.");
    }
}

// Create a subclass by extending class A.
class B extends A {
    B() {
        System.out.println("Inside B's constructor.");
    }
}

// Create another subclass by extending B.
class C extends B {
    C() {
        System.out.println("Inside C's constructor.");
    }
}
  
class CallingCons {
    public static void main(String args[]) {
        C c = new C();
    }
}
```
