## Ranges
```scala
1 to 10
1 until 10
1 to 10 by 3
```

### Partial Functions

- Functions that are defined only by cases
- Can be chained `pf1 orElse pf2 orElse pf3`
- Has a method `isDefinedAt` to check

```scala
  val pf1: PartialFunction[Any,String] = { case s:String => "YES" }
```

### Method Declaration

- case classes have a method called `copy` where you can specify the changing arguments

#### Multiple Argument List

- Allows nice blocking structure syntax, better default
- Type inference in subsequent lists
- Last list can be used implicitly

### implicit

- Parameters that are declared impicit do not have to be defined if an implict val is declared in scope

### Recursion note

- we have to declare the return type of recursive functions. Scala cant infer

## Type Inference

- type annotation: ex. HashMap<Integer, String>
  Cases where you have to specify type
  - var or val where you don't assign a value
  - All method parameters
  - Method return types in these cases:
    - When you use return
    - Recursive methods
    - Overloaded method that calls the other method
    - When the inferred return type is more general than you needed

## Literal Values

look them up

## Option, Some, None

- Option is an abstract class with child classes, Some and None
- Has methods `get` or `getOrElse`

## Imports

```scala
  import java.math.BigInteger.{
    ONE => _,   \\Inaccessible
    TEN,
    ZERO => JAVAZERO \\Alias
  }
```

## Package Objects

- Look it up

## Parameterized vs Abstract

```scala
  abstract class BulkReader {
    type In
    val source: In
    def read: String // Read source and return a String
  }
  class StringBulkReader(val source: String) extends BulkReader {
    type In = String
    def read: String = source
  }
  class FileBulkReader(val source: File) extends BulkReader {
    type In = File
    def read: String = {
      val in = new BufferedInputStream(new FileInputStream(source))
      val numBytes = in.available()
      val bytes = new Array[Byte](numBytes)
      in.read(bytes, 0, numBytes)
      new String(bytes)
    }
  }
```

- It is better to use type members (type In for example) when the type evolves or needs to match a certain behaviour
- Still unsure about this