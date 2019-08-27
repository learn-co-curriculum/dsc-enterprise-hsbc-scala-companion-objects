
# Companion Objects

## Using Companion Objects

Companion Objects
* Still singletons
* Services a `class`, `trait`, `abstract class`

Companion Object Rules:
* Must have the same name as the class, trait, abstract class it supports
* The class and the object has to be in the same file
* `trait` is analogous to an interface in Java

Companion Object Benefits:
* `class` and `object` can share private information
* This makes `object` perfect for being a factory of the corresponding class
* Stores logic for pattern matching

## Accessing private shared state


```scala
class SecretAgent(val name: String) {
  def shoot(n: Int) {
    SecretAgent.decrementBullets(n) //Can be imported and shortened
                                    //using import SecretAgent._
  }
}

object SecretAgent {
  //This is encapsulated!
  private var b: Int = 3000 //only available privately

  private def decrementBullets(count: Int) {  //only available privately
    if (b - count <= 0) b = 0
    else b = b - count
  }

  def bullets = b
}
```




    defined class SecretAgent
    defined object SecretAgent
    



Running this would look like:


```scala
val bond = new SecretAgent("James Bond")
val felix = new SecretAgent("Felix Leitner")
val jason = new SecretAgent("Jason Bourne")
val _99 = new SecretAgent("99")
val max = new SecretAgent("Max Smart")

bond.shoot(800)
felix.shoot(200)
jason.shoot(150)
_99.shoot(150)
max.shoot(200)

println(SecretAgent.bullets) //How many bullets are left?
```

## Creating a factory

* One of the main uses of a companion object is to use it as a factory
* To do so, lets say, direct invocation of `Department` in the following example is locked with `private`
* We can then create a factory using the companion object to Department class


```scala
class Department private(val name:String)
object Department {
   def create(name:String) = new Department(name)
}
```




    defined class Department
    defined object Department
    



The above really is just a static factory pattern that you would see in Java.

## Calling the factory from the companion object
How can we call the factory?


```scala
val department = Department.create("Toys")
department.name
```




    department: Department = Department@78792922
    res1: String = Toys
    



## **Lab:** Redo `Department`

**Step 1:** Important Question: Is there a better name instead of create? Decide and implement. 

**Step 2:** Look up how you create `List`, `Set`, `Map` in the Scala API https://www.scala-lang.org/files/archive/api/current/

## Companion Object Conclusion

* Companion Objects have the same name as the class that they work for
* Companion Objects must be in the same file.
* Companion Objects have access to their classes private information.
* Classes have access to the companion’s private information.
