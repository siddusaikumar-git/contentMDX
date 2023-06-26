# Python

> Note: reference from Educative IO Python course.

## Procedural Programming Language

In procedural programming language, a program is divided into smaller programs called methods, Methods are basic entities used to construct a program. One of the main advantage of procedural program is code reusability.

## Object Oriented Programming

> OOPS relies on Objects and Classes.

In order to model the real-world scenarios using code, Object oriented programming can help.

> On a high level, Objects are collection of data and the their behaviors and classes are blueprint of objects.

#### Benefits of Objects and Classes

1. The use of classes makes it easier to maintain different parts of an application since it is easier to make changes in classes.
2. Objects and classes allow us to create complex applications in Python.

Class name should start with letter or underscore and should only be comprised of numbers, letter or underscores.

> Class have both properties and methods, properties can either be "None" or initialized with value and cannot be simply declared like other languages. These properties are also called as class variables.

### Initializing Objects

An initializer is used to initialize the Object of a class. It is similar to other methods but has a name `__init__` it has first parameter as `self`, which is to refer the Object initialized.

### Class and Instance Variables

Python properties has two parts:

- Class variables
  - These variables are shared by all the instances or objects of the classes. A change in class variable will change the value of that property in all the objects of the class.
- Instance variables
  - The instance variables are unique to each instance or object of the class. A change in the instance variable will change the value of the property in that specific object only.

> Class variables are useful when implementing properties that should be common and accessible to all class objects.

### Types of Methods in Python

Methods act as an interface between a program and the properties of a class in the program and it is group of statements that performs some operations and may or may not return a result.

usage of methods plays a crucial role in `Method Overloading` where method performs different operations based on the nature of the arguments.

> In Python, methods cannot be explicitly overloaded in Python but can be implicitly overloaded.

Advantage of Method overloading in Python is saves memory in the system, overloading methods are compiled faster and cleaner code.

> The difference between method and function is `self` keyword, where in methods `self` keyword is the first argument.

There are three types of methods in Python.

#### 1. Instance methods

In instance methods, first parameter is `self`, followed by all other parameters that are particular to that object created while initialization.

```python
# instance method
class Test:
    def __init__(self, ID=None):
        self.ID = ID
```

#### 2. class methods

Class methods work with class variables and are accessible using the class as well as object. Since all class objects share the class variables, class methods are used to access and modify class variables.

> Class methods are accessed using the class name and can be accessed without creating a class object.

```python
# class methods access class varaibles
class Test:
    classVariable = 'testing'

    @classmethod
    def test(cls):
        return cls.classVariable
```

> `cls` is used to refer the class just like `self` in instance methods. there are not reserved name, these are chosen based on familiarity.

#### 3. Static methods

Static methods are methods that are usually limited to class only and not their objects. They have no direct relation to class variables or instance variables.

> Static methods can be accessed using the class name or the object name. It cannot access either instance or class variables.

```python
class Test:

    @staticmethod
    def test()
        print("I am a static method")
```

### Access Modifiers

There are two types of access modifiers in Python.

**Public attributes**

By default, all methods and properties in a class are publicly available by default.

> Public attributes are those that can be accessed inside the class and outside the class.

**Private attributes**

Unlike in many different languages, it is not a widespread practice in Python to keep the data members private since we do not want to create hindrances for the users. We can make members private using the double underscore `__` prefix

> Private attributes cannot be accessed directly from outside the class but can be accessed from inside the class.

```python
# To showcase the private properties in python
class Test:
    def __init__(self, value):
        self.__value = value  # value is a private property

test = Test(2500)
print("value:", test.__value)  # this will cause an error
```

**Private methods**

```python
# To showcase the private methods in python
class Test:
    def __displayID(self):  # displayID is a private method
        print("ID: 1234")

test = Test()
test.__displayID()  # this will generate an error

```

## Information Hiding

> Information hiding refers to hiding the inner workings of class and providing interface to interact with the class.
>
> <em>
>   Analogy: Doctor providing the medicines, we don't know how he draws the
>   conclusion
> </em>

Data hiding is divided into two components

1. Encapsulation
2. Abstraction

### Encapsulation

> Encapsulation in OOP refers to binding data and the methods to manipulate that data together in a single unit, that is, class.

This is achieved by restricting all the variables of the class as `private` and access them outside the class using `public` methods.

Advantages of Encapsulation:

- Easy to change and maintain.
- Properties to be hidden can be specified easily.
- control which outside functions and classes can access the class properties.

### If data hidden then how to control the properties ?

Then Getters and Setters comes into picture

- Getter method allows reading the property
- Setter method allows modifying the property's value

> Analogy: One example is Username and Password are declared as private methods and accessed using getters and setters in python.

### Inheritance

> The <em>IS A</em> relationship

- Parent class (Super class or Base class): This allows to reuse its public properties and methods
- Child class (Sub Class or Derived class): Inherits and extends the superclass.

> Analogy: Falcon Heavy Inherited the Falcon 9 SpaceX spacecraft.

`super()` function comes into play when we implement inheritance. It is used to refer parent class without using the class name.

```python
# to initialize, this is done in child __init__ function.
super().__init__(a, b)

# to access parent class methods
super().parentMethod()
```

#### Types of Inheritance

1. Single
   - (Car IS A Vehicle)
2. Multi-level
   - Car is a Vehicle
   - Hybrid is a Car
3. Hierarchical
   - A Car IS A Vehicle
   - A Truck IS A Vehicle
4. Multiple
   - HybridEngine IS A ElectricEngine.
   - HybridEngine IS A CombustionEngine as well.
5. Hybrid
   - CombustionEngine IS A Engine.
   - ElectricEngine IS A Engine.
   - HybridEngine IS A ElectricEngine and a CombustionEngine.

#### Advantages of Inheritance

- Code reusability
- Easy of code modification at single place to reflect to all.
- Easily can extend
- Data Hiding

### Polymorphism

> Polymorphism means many forms

The purpose of polymorphism is to make the developer life easier by providing common method name or properties name across different classes such that same function can perform different operations.

> Analogy: Electric car and Combustion engine car can have the mileage function but different implementations of calculating mileages.

#### Method Overriding

> Method overriding is the process of redefining a parent class’s method in a subclass.

This means methods in the parent class are overridden method.

#### Operator Overloading

Operators in Python can be overloaded to operate in a certain user-defined way.

> when the `+` operator is called, it invokes the special function, `__add__`, in Python, but this operator acts differently for different data types.

We can perform Overloading operators for a user-defined class.

| Operator | Method                     |
| -------- | -------------------------- |
| +        | _\_add_\_(self, other)     |
| -        | _\_sub_\_(self, other)     |
| /        | _\_truediv_\_(self, other) |
| \*       | _\_mul_\_(self, other)     |
| <        | _\_lt_\_(self, other)      |
| >        | _\_gt_\_(self, other)      |
| ==       | _\_eq_\_(self, other)      |

#### Implementing Polymorphism using Duck Typing

> Duck Typing means that we can change the type of the object later in the code.

```python
x = 2  # type of x is an integer
print(type(x))

x = "Hello"  # type of x is now string
print(type(x))

```

> Similarly we can pass object as parameters and achieve polymorphism

```python
# Achieve polymorphism using Duck typing.
class Tesla:
    def Engine(self):
        print("Electric")


class Ford:
    def Engine(self):
        print("Combustion")


class Vehicle:
    def Sound(self, car):
        car.Engine()


vehicle = Vehicle()
tesla = Tesla()
ford = Ford()

vehicle.Engine(tesla)
vehicle.Engine(ford)
```

### Abstract Base Classes

> Abstract base classes define a set of methods and properties that a class must implement in order to be considered a duck-type instance of that class.

```python
from abc import ABC, abstractmethod


class Shape(ABC):  # Shape is a child class of ABC
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass


class Square(Shape):
    def __init__(self, length):
        self.length = length

    def area(self):
        return (self.length * self.length)

    def perimeter(self):
        return (4 * self.length)


square = Square(4)
# this code will not generate an error since abastract methods have been
# defined in the child class, Square
```

> Abstract methods must be defined in child classes for proper implementation of inheritance.

## Object relationships

There are three main relationships

1. IS A
2. Part-of (In this relationship, one class object is a component of another class object.)
3. Has-a (In this relationship, once class object reference is in another class, where both can exist independently)

#### Aggregation, Association and Composition

In Python, aggregation, association, and composition are concepts related to object-oriented programming (OOP) and class relationships. Let's explore each of them:

1. Aggregation:
   Aggregation is a relationship where one class contains another class as a part of its own definition, but the contained class can exist independently. It represents a "has-a" relationship. In Python, aggregation is typically implemented by creating a class attribute that references an instance of another class. The aggregated class can be instantiated separately and shared among multiple instances of the aggregating class.

Here's an example of aggregation in Python:

```python
class Car:
    def __init__(self, engine):
        self.engine = engine

class Engine:
    def __init__(self, horsepower):
        self.horsepower = horsepower

engine = Engine(200)
car = Car(engine)
```

In the above example, the `Car` class has an aggregation relationship with the `Engine` class. The `Car` class contains an instance of the `Engine` class as its attribute `engine`. The `Engine` instance can exist independently and can be shared among multiple `Car` instances.

2. Association:
   Association represents a relationship between two or more classes, where objects of one class are related to objects of another class. It signifies a "uses" or "interacts with" relationship. Unlike aggregation, the associated class does not belong to the defining class and can exist independently.

Here's an example of association in Python:

```python
class Player:
    def __init__(self, name):
        self.name = name

class Team:
    def __init__(self):
        self.players = []

    def add_player(self, player):
        self.players.append(player)

player1 = Player("John")
player2 = Player("Mike")
team = Team()
team.add_player(player1)
team.add_player(player2)
```

In the above example, the `Team` class has an association with the `Player` class. The `Team` class maintains a list of `Player` objects in its `players` attribute. The `Player` instances exist independently and are associated with the `Team` class through the `add_player` method.

3. Composition:
   Composition is a strong form of aggregation, where the contained class is part of the defining class and cannot exist independently. It represents a "composed of" relationship. In composition, the lifecycle of the contained object is tightly tied to the lifecycle of the defining object.

Here's an example of composition in Python:

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

class Library:
    def __init__(self):
        self.books = []

    def add_book(self, title, author):
        book = Book(title, author)
        self.books.append(book)

library = Library()
library.add_book("Python Programming", "John Smith")
```

In the above example, the `Library` class has a composition relationship with the `Book` class. The `Library` class creates and owns instances of the `Book` class through the `add_book` method. The `Book` instances cannot exist independently and are tightly tied to the lifecycle of the `Library` instance.

These concepts help in designing and modeling relationships between classes in object-oriented programming and can be applied in Python as well as in other programming languages.
