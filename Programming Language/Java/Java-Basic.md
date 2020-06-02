# Java Basic  
## Inheritance  
#### super vs this  
* super: call parent class members.  
* this: call current class members.  

#### method overloading vs method overriding  
* method overloading: providing methods with same name but different parameters.  
* method overriding: define a method in child class already exists in parent class(must have same name and smae parameters).  
  * Can't override static methods.  
  * **Constructors and private methods** cannot be overriden.  
  * A subclass can use **super.methodName()** to call superclass version of an overriden method.  
  * Must not have a lower modifier, but may have higner modifier.  

#### static methods  
* Can't access instance methods and instance cariables directly.  
* Usually used for operations don't require any data from an instance of the class(from 'this').  





