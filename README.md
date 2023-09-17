# Pillars of Python  

## Pillars of Python Programming

There are 4 pillars in Python Programming. 
1. Encapsulation
   2. Abstraction
   3. Inheritance (Already covered earlier.)
   4. Polymorphism 

## Encapsulation 

* Encapsulation is the concept of bundling data (attributes) and methods (functions) that operate on 
**that** data into a single unit called a *class*. 
  * It allows you to control access to the data and restrict external entities from directly modifying it.
  * In Python, this is achieved through classes and access modifiers like public, private, and protected.

```commandline
class BankAccount:
    def __init__(self, account_number, balance):
        self._account_number = account_number  # Protected attribute
        self.__balance = balance  # Private attribute

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            print(f"Deposited ${amount}. New balance: ${self.__balance}")
        else:
            print("Invalid deposit amount.")

    def withdraw(self, amount):
        if amount > 0 and amount <= self.__balance:
            self.__balance -= amount
            print(f"Withdrew ${amount}. New balance: ${self.__balance}")
        else:
            print("Invalid withdrawal amount or insufficient balance.")

    def get_balance(self):
        return self.__balance


# Creating an instance of the BankAccount class
account = BankAccount("12345", 1000)

# Accessing protected attributes (conventionally considered non-public)
print("Account Number:", account._account_number)  # Accessing protected attribute

# Accessing private attributes (name mangling applied)
# This is not recommended; it's just to show the behavior
print("Balance:", account._BankAccount__balance)  # Accessing private attribute

# Using methods to deposit and withdraw
account.deposit(500)
account.withdraw(200)
account.withdraw(800)

# Accessing the balance through a method (recommended)
print("Current Balance:", account.get_balance())
```

In this example, we have a `BankAccount` class that encapsulates the account's data and methods. 
Here's how encapsulation is demonstrated:

1. **Attributes**:  The class has two attributes: `_account_number` (protected) and `__balance` (private).
Conventionally, *attributes starting with a single underscore are considered protected*, and *those starting with 
double underscores are considered private.*

   2. **Methods**: The class defines methods for depositing, withdrawing, and retrieving the balance. 
   These methods provide controlled access to the attributes, ensuring that the data is manipulated safely and following 
   specific rules.

   3. **Access Control**: While Python doesn't enforce strict access control, it uses name mangling to make it more 
   difficult to directly access private attributes from outside the class. However, it's still possible to access them 
   (as demonstrated in the example), but it's generally not recommended.

By encapsulating the data and providing controlled access through methods, encapsulation helps maintain the integrity 
of the data and provides a clear interface for interacting with the class, promoting good programming practices and 
making it easier to manage and maintain the code.

## Abstraction 

* Abstraction is the process of simplifying complex systems by breaking them down into smaller, more manageable parts.
  * In Python, you can achieve abstraction through *classes* and *interfaces*
  * You create abstract classes to define common behavior and attributes, and then concrete classes inherit from these 
  abstract classes to provide specific implementations.
  * It involves simplifying complex systems by breaking them down into smaller, more manageable parts.

```commandline
from abc import ABC, abstractmethod

# Abstract class (Shape) representing a geometric shape
class Shape(ABC):
    def __init__(self, name):
        self.name = name

    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

# Concrete class (Circle) inheriting from the abstract class Shape
class Circle(Shape):
    def __init__(self, name, radius):
        super().__init__(name)
        self.radius = radius

    def area(self):
        return 3.14 * self.radius * self.radius

    def perimeter(self):
        return 2 * 3.14 * self.radius

# Concrete class (Rectangle) inheriting from the abstract class Shape
class Rectangle(Shape):
    def __init__(self, name, length, width):
        super().__init__(name)
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

    def perimeter(self):
        return 2 * (self.length + self.width)

# Function that calculates and prints area and perimeter of a shape
def print_shape_info(shape):
    print(f"Shape: {shape.name}")
    print(f"Area: {shape.area()}")
    print(f"Perimeter: {shape.perimeter()}")

# Creating instances of Circle and Rectangle
circle = Circle("Circle", 5)
rectangle = Rectangle("Rectangle", 4, 6)

# Using the print_shape_info function to demonstrate abstraction
print_shape_info(circle)
print()
print_shape_info(rectangle)
```
In this example, we have used abstraction to create an abstract class `Shape` that defines the common interface for all 
geometric shapes. Here's how abstraction is demonstrated:

1. **Abstract Class**: `Shape` is an abstract class that defines two abstract methods, `area` and `perimeter`.
An abstract class cannot be instantiated directly, but it provides a blueprint for concrete classes.
   2. **Concrete Class**: `Circle` and `Rectangle` are concrete classes that inherit from the abstract class `Shape`.
   These classes provide specific implementations of the `area` and `perimeter` methods, which are required by the abstract class.
   3. **Polymorphism**: The `print_shape_info` function demonstrates polymorphism. 
    It can work with objects of any class that inherits from `Shape`, regardless of whether it's a `Circle` or a `Rectangle`.
   This showcases abstraction in action, as the function operates on the abstract concept of a "Shape" without knowing the specific shape type.

Abstraction allows you to create a clear separation between the interface (abstract class) and the implementation (concrete classes), 
making it easier to extend and maintain your code. It also promotes code reusability and helps manage complexity in larger software systems.

<b><span style="background-color:gray; color:red">Inheritance has already been covered earlier. Please see earlier 
topics</span>

## Polymorphism

* The word Polymorphism refers to "many forms"
* In python, polymorphism means methods/functions/operators with same name that can be executed on many objects or 
  classes.
* Polymorphism is a fundamental concept in object-oriented programming (OOP), including Python. 
* In Python, polymorphism is significant because it enables flexibility, reusability, and abstraction in your code.

### Significance of Polymorphism 
1. **Code Reusability**: Polymorphism allows you to write code that can work with objects of different classes in a uniform way.
This means you can reuse the same code for different objects that share a common interface or behavior, rather than having to write separate code for each specific class.
2. **Abstraction**: Polymorphism promotes a higher level of abstraction in your code. You can focus on what objects do (their behavior or methods) rather than what they are (their specific class or type). This simplifies the design and makes your code more maintainable.
3. **Flexibility**: Polymorphism makes your code more flexible and adaptable to changes. If you add a new class that conforms to the same interface (i.e., has the same methods), your existing code can work with objects of this new class without modification.
4. **Code Organization**: Polymorphism encourages better code organization through the use of inheritance and interfaces. You can define a common superclass or interface that specifies the methods all related classes should have, and then each subclass can provide its own implementation of those methods.
5. **Dynamic Behavior**: In Python, polymorphism is often achieved through dynamic method dispatch. This means that the appropriate method to execute is determined at runtime based on the actual object's class. This dynamic behavior is powerful because it allows for runtime flexibility and extensibility.

### Illustration

```
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius * self.radius

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width
    
    def area(self):
        return self.length * self.width

def calculate_area(shape):
    return shape.area()

circle = Circle(5)
rectangle = Rectangle(4, 6)

print(calculate_area(circle))     # Output: 78.5
print(calculate_area(rectangle))  # Output: 24
```
In this example, we have a `Shape` superclass with a common method `area()`. Both `Circle` and `Rectangle` classes inherit from Shape and provide their own implementations of the `area()` method. The `calculate_area()` function can work with objects of any class that inherits from `Shape`, demonstrating polymorphism. This design makes it easy to add more shapes in the future without modifying the existing code.  

* In summary, polymorphism in Python is a powerful and essential concept in object-oriented programming that allows for code reuse, abstraction, flexibility, and dynamic behavior, ultimately making your code more maintainable and extensible.

### Achieving Polymorphism

Polymorphism in Python is often achieved through **method overriding** and **duck typing**. Here's an overview of how it works:

1. **Method Overriding**: In Python, you can define a method in a subclass with the same name as a method in its superclass. This is called method overriding. When you call the method on an object of the subclass, it will execute the overridden method in the subclass rather than the one in the superclass.

```
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# Polymorphism in action
def animal_sound(animal):
    return animal.speak()

dog = Dog()
cat = Cat()

print(animal_sound(dog))  # Output: "Woof!"
print(animal_sound(cat))  # Output: "Meow!"
```

2. **Duck Typing**: Python follows a dynamic typing system, and it's not necessary for objects to explicitly inherit from a common superclass to exhibit polymorphic behavior. Instead, Python relies on "duck typing," which means that an object's suitability is determined by its behavior (i.e., if it walks like a duck and quacks like a duck, it's treated as a duck).

```
class Bird:
    def speak(self):
        pass

class Duck(Bird):
    def speak(self):
        return "Quack!"

class Crow(Bird):
    def speak(self):
        return "Caw!"

def bird_sound(bird):
    return bird.speak()

duck = Duck()
crow = Crow()

print(bird_sound(duck))  # Output: "Quack!"
print(bird_sound(crow))  # Output: "Caw!"
```
In both examples, we have different classes that implement a `speak` method. By passing objects of these classes to the `animal_sound` and `bird_sound` functions, we demonstrate polymorphism because the appropriate `speak` method for each object is invoked, even though they belong to different classes.

