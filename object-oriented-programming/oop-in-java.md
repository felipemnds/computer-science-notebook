# chapter 1. the world of objects

## 1) OOP (Object Oriented Programming)
Vídeo que explica o que é POO: [https://youtu.be/1Wjm_MJ_WfQ](https://youtu.be/1Wjm_MJ_WfQ)  

## 2) Fields
For example a *book* object may contain fields like *title*, *author* and *numberOfPages*. Then a library object may contain a field *named* books that will store all *book* objects in an array.
**Accessing a field** in an object is done using the dot modifier ‘.’  

    String title;
    String author;
    int numberOfPages;

To **access** the title field you would use:    

    book.title

## 3) Methods
To **use a method** you call it (just like calling a function). This is also done using the dot modifier.

## 4) Objects & Classes
-   **CLASS** - a guide that contains fields and methods
   
-   **OBJECT** - a variable created based on the class, with specific values

| | Class | Object |
|--|--|--|
| **What:** | A Data Type | A variable |
| **Where:** | Has its own file | Scattered around the project |
| **Why:** | Defines the structure | Used to implement to logic |
| **Naming convention:** | CamelCase | camelCase |
| **Examples:** | Country | australia |
|| Book | lordOfTheRings |
|| Pokemon | pikachu |

In summary, **objects** are to **Classes** what **variables** are to **Data types**.
**String** is a class! That's why it's written with uppercase letter.
**Everything in Java is an object:**

|Class| Primitive type |
|--|--|
| Integer | int |
| Long| long|
| Double| double |
| Character| char |
| String| char[] |

Each of those classes is made up of the corresponding primitive type as its field, but usually also comes with some powerful methods.

## 5) The _main_ method
This is the method that will start a program the very first time:

    public static void main(String [] args){
	    // Start my program here
    }

Let's break it down:
-   **public**: Means you can run this method from anywhere in your Java program (we will talk more about public and private methods later
-   **static**: Means it doesn't need an object to run, which is why the computer starts with this method before even creating any objects (we will also talk more about static methods later on)
-   **void**: Means the main method doesn't return anything, it just runs when the program starts, and once it's done the program terminates
-   **main**: Is the name of the method
-   **String [] args** : Is the input parameter (array of strings) which we will cover how to use it later in this lesson as well!
 

## 6) Constructors

Constructors are special types of methods that are responsible for creating and initializing an object of that class.
**Creating a constructor** is very much like creating a method, except that:
1.  Constructors don't have any return types
2.  Constructors have the same name as the class itself

They can however take **input parameters** like a normal method, and you are allowed to create multiple constructors with different input parameters.

To create an object of a certain class, you will need to use the new keyword followed by the constructor you want to use, for example:  

    Game tetris = new Game();

To create a game that is initialized with a different starting score you can use the second constructor:  

    Game darts = new Game(501);

In some cases, you might want to explicitly set an object to null to indicate that such object is invalid or **yet to be set**. You can do so using the assignment operation:

    Game darts = null;

### Q: Why multiple constructors?
Good point, however, it's considered a good practice to always include a default constructor that initializes all the fields with values that correspond to typical scenarios.
### Q: But you said the default constructor is optional!
However, this privilege goes away once you create any constructor of your own! Which means if you create a parameterized constructor and want to also have a default constructor, you will **have to** create that default constructor yourself as well.

## 7) Self Reference
Sometimes you'll need to refer to an object within one of its methods or constructors, to do so you can use the keyword _this_.
For example, if a Position class was written like this

    class Position {
	    int row = 0;
	    int column = 0;
	    //constructor
	    Position(int r, int c) {
		    row = r;
		    column = c;
	    }
    }

A more readable way would be to use the same names (row & column) for the constructor parameters which means you will have to use the this keyword to seperate between the fields and the paramters:

    class Position {
	    int row = 0;
	    int column = 0;
	    //constructor
	    Position(int row, int column) {
		    this.row = row;
		    this.column = column;
	    }
    }

## 8) Example: The Contacts Manager

Exercício realizado!  

## 9) Public vs Private (for Fields and Methods)
### A) Fields  
To label a field as private or public simply add the modifier just before the field type when declaring it:

    public int score;
    private String password;

It's strongly recommended in Java to label ALL fields as private.  

For example , when defining a Book class, instead of saying:

    class Book{
    	String title;
    	String author;
    }
A proper way would be to define everything private, and only initialize them in the construtor.

    class Book{
    	private String title;
    	private String author;
    	public Book(String title, String author){
    		this.title = title;
    		this.author = author;
    	}
    }
This way you can guarantee that once a book object has been created, the title and author will never change!

**Better Design:** using _GETTERS_ and _SETTERS_
1.  GETTERS - Create a public method that returns each private field, so you can read the value without mistakingly changing it
2.  SETTERS - Create a public method that sets each private field, this way you will know when you are changing a field
### B) Methods
