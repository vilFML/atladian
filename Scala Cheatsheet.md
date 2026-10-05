# Scala 3 Cheatsheet

> Quick reference for students coming from Python.
> Uses **indentation syntax** (no braces), matching the CC3002 course style.

---

## 1. Values and Variables

```scala
val x = 10            // immutable (prefer this)
var y = 20            // mutable
y = 21                // OK
// x = 11             // ERROR: val cannot be reassigned
```

Explicit types (usually inferred):

```
val name: String = "Alice"
val age: Int = 30
val price: Double = 9.99
val flag: Boolean = true
val letter: Char = 'A'
```

---

## 2. Primitive Types

| Type ↕▾ | Example ↕▾ | Notes ↕▾ |
|---|---|---|
| −`Int` | `42` | 32-bit integer |
| −`Long` | `42L` | 64-bit integer |
| `Float` | `3.14f` | 32-bit float |
| `Double` | `3.14` | 64-bit float (default) |
| `Boolean` | `true` / `false` |  |
| `Char` | `'a'` | single quotes |
| `String` | `"hello"` | double quotes |
| `Unit` | `()` | like Python's `None` for return type |
⚙

---

## 3. Strings

```
val name = "Alice"

s"Hello, $name"              // interpolation → "Hello, Alice"
s"Sum: ${1 + 2}"             // expressions need braces → "Sum: 3"
"abc".toUpperCase            // "ABC"
"abc".length                 // 3
"a,b,c".split(",")           // Array("a", "b", "c")
"  hi  ".trim                // "hi"
```

Multi-line strings:

```
val text = """line 1
line 2"""
```

---

## 4. Arithmetic and Operators

```
1 + 2       // 3
10 / 3      // 3   (Int division)
10.0 / 3    // 3.333...
10 % 3      // 1
2 * 3       // 6
-5          // negation

math.max(3, 7)   // 7
math.min(3, 7)   // 3
math.abs(-4)     // 4
math.sqrt(16)    // 4.0
math.pow(2, 8)   // 256.0
```

Boolean:

```
true && false   // false
true || false   // true
!true           // false
1 == 1          // true
1 != 2          // true
1 < 2           // true
```

---

## 5. Conditionals

```
if x > 0 then
  println("positive")
else if x < 0 then
  println("negative")
else
  println("zero")
```

`if` is an **expression** — it returns a value:

```
val label = if x >= 0 then "non-negative" else "negative"
```

---

## 6. Loops

`while`:

```
var i = 0
while i < 5 do
  println(i)
  i += 1
```

`for` over a range:

```
for i <- 1 to 5 do println(i)         // inclusive: 1..5
for i <- 1 until 5 do println(i)      // exclusive: 1..4
for i <- 10 to 1 by -1 do println(i)  // step
```

`for` with a filter:

```
for i <- 1 to 10 if i % 2 == 0 do println(i)   // evens only
```

---

## 7. Functions (top-level)

```
def add(a: Int, b: Int): Int =
  a + b

def greet(name: String): Unit =
  println(s"Hello, $name")

def square(x: Int): Int = x * x        // one-liner
```

Default and named arguments:

```
def greet(name: String = "World"): Unit =
  println(s"Hello, $name")

greet()                    // Hello, World
greet("Alice")             // Hello, Alice
greet(name = "Bob")        // Hello, Bob
```

Multiple parameter lists (currying):

```
def add(a: Int)(b: Int): Int = a + b
add(2)(3)                  // 5
```

---

## 8. Classes

```
class Point(val x: Int, val y: Int):
  def move(dx: Int, dy: Int): Point =
    new Point(x + dx, y + dy)

  override def toString: String =
    s"Point($x, $y)"
```

Constructor parameters:

- `val` → public immutable field
- `var` → public mutable field
- no modifier → private to the class body

```
class Counter(var count: Int)          // public mutable
class Secret(private val key: String)  // private field
```

Auxiliary constructor:

```
class Point(val x: Int, val y: Int):
  def this(x: Int) = this(x, 0)        // delegates to primary
```

---

## 9. Traits (Interfaces)

```
trait Animal:
  def name: String                     // abstract
  def talk(): Unit

class Dog(val name: String) extends Animal:
  def talk(): Unit = println(s"$name: Woof!")
```

Mixing multiple traits:

```
trait Legged:
  def walk(): Unit

trait Tailed:
  def wag(): Unit

class Dog extends Legged, Tailed:
  def walk(): Unit = println("walking")
  def wag(): Unit = println("wagging")
```

Default implementations:

```
trait Greeter:
  def name: String
  def greet(): Unit = println(s"Hi, $name")   // provided
```

---

## 10. Abstract Classes

```
abstract class Shape:
  def area: Double                    // abstract
  def describe(): String =            // concrete
    s"Area = $area"

class Circle(val radius: Double) extends Shape:
  def area: Double = math.Pi * radius * radius
```

- **Trait** = contract, no constructor params, can mix many.
- **Abstract class** = partial implementation, has constructor, single inheritance.

---

## 11. Objects (Singletons)

```
object MathUtils:
  val Pi = 3.14159
  def square(x: Int): Int = x * x

MathUtils.Pi          // 3.14159
MathUtils.square(4)   // 16
```

Companion object (same name, same file as class):

```
class Point(val x: Int, val y: Int)

object Point:
  def origin: Point = new Point(0, 0)

Point.origin          // Point(0, 0)
```

---

## 12. Option (No More `null`)

```
val some: Option[Int] = Some(42)
val none: Option[Int] = None
```

| Operation ↕▾ | Meaning ↕▾ |
|---|---|
| −`opt.isEmpty` | true if `None` |
| `opt.isDefined` | true if `Some` |
| `opt.get` | value (throws if `None` — avoid) |
| `opt.getOrElse(default)` | value or default |
| `opt.map(f)` | transform if present |
| `opt.foreach(f)` | side effect if present |
| `opt.exists(p)` | true if present **and** predicate holds |
⚙

```
val x: Option[Int] = Some(5)
x.map(_ * 2)                    // Some(10)
x.getOrElse(0)                  // 5
x.foreach(v => println(v))      // prints 5

val empty: Option[Int] = None
empty.map(_ * 2)                // None
empty.getOrElse(0)              // 0
```

`for` on options:

```
val result =
  for
    a <- Some(1)
    b <- Some(2)
  yield a + b                   // Some(3)
```

---

## 13. Collections

### List

```
val xs = List(1, 2, 3, 4, 5)

xs.head          // 1
xs.tail          // List(2, 3, 4, 5)
xs(0)            // 1
xs.length        // 5
xs.isEmpty       // false

xs :+ 6          // List(1,2,3,4,5,6)  append
0 +: xs          // List(0,1,2,3,4,5)  prepend
```

### Set

```
val s = Set(1, 2, 3)
s.contains(2)    // true
s + 4            // Set(1,2,3,4)
s - 1            // Set(2,3)
```

### Map

```
val m = Map("a" -> 1, "b" -> 2)
m("a")                    // 1 (throws if missing)
m.get("a")                // Some(1)
m.get("z")                // None
m.getOrElse("z", 0)       // 0
m + ("c" -> 3)            // new map
m - "a"                   // without key "a"
```

Iterating:

```
for (k, v) <- m do println(s"$k = $v")
m.values.foreach(println)
m.keys.foreach(println)
```

---

## 14. Collection Operations

Given `val xs = List(1, 2, 3, 4, 5)`:

| Operation ↕▾ | Result ↕▾ |
|---|---|
| −`xs.map(_ * 2)` | `List(2, 4, 6, 8, 10)` |
| −`xs.filter(_ % 2 == 0)` | `List(2, 4)` |
| `xs.filterNot(_ % 2 == 0)` | `List(1, 3, 5)` |
| `xs.flatMap(x => List(x, -x))` | `List(1,-1,2,-2,...)` |
| `xs.foldLeft(0)(_ + _)` | `15` |
| `xs.foldRight(0)(_ + _)` | `15` |
| `xs.reduce(_ + _)` | `15` |
| `xs.sum` | `15` |
| `xs.product` | `120` |
| `xs.max` / `xs.min` | `5` / `1` |
| `xs.reverse` | `List(5,4,3,2,1)` |
| `xs.sorted` | same (already sorted) |
| `xs.distinct` | `List(1,2,3,4,5)` |
| `xs.take(2)` | `List(1, 2)` |
| `xs.drop(2)` | `List(3, 4, 5)` |
| `xs.zip(List("a","b","c","d","e"))` | `List((1,"a"),(2,"b"),...)` |
| `xs.groupBy(_ % 2 == 0)` | `Map(false -> ..., true -> ...)` |
| `xs.exists(_ > 4)` | `true` |
| `xs.forall(_ > 0)` | `true` |
| `xs.find(_ > 3)` | `Some(4)` |
| `xs.count(_ > 2)` | `3` |
⚙

Chaining:

```
List(1, 2, 3, 4, 5, 6)
  .filter(_ % 2 == 0)             // List(2, 4, 6)
  .map(_ * 10)                    // List(20, 40, 60)
  .sum                            // 120
```

---

## 15. For-Comprehensions

Syntactic sugar over `map` / `flatMap` / `withFilter`:

```
for
  x <- List(1, 2, 3)
  y <- List(10, 20)
yield x + y
// List(11, 21, 12, 22, 13, 23)
```

With a filter:

```
for
  x <- 1 to 10
  if x % 2 == 0
yield x * x
// Vector(4, 16, 36, 64, 100)
```

Side effects (no `yield`):

```
for x <- List(1, 2, 3) do println(x)
```

---

## 16. Pattern Matching

```
val x: Any = 42

x match
  case 0        => println("zero")
  case n: Int   => println(s"int: $n")
  case s: String => println(s"string: $s")
  case _        => println("unknown")
```

On `Option`:

```
opt match
  case Some(v) => println(s"got $v")
  case None    => println("nothing")
```

On lists:

```
xs match
  case Nil       => "empty"
  case x :: Nil  => s"one element: $x"
  case x :: rest => s"head $x, rest $rest"
```

---

## 17. Exceptions

```
try
  val n = "abc".toInt
catch
  case e: NumberFormatException => println("not a number")
finally
  println("always runs")
```

Throwing:

```
throw new IllegalArgumentException("bad input")
```

Custom exception:

```
class InvalidPortException(msg: String) extends Exception(msg)
throw new InvalidPortException("port out of range")
```

---

## 18. Generics

```
class Box[T](val value: T):
  def get: T = value

val b1 = new Box[Int](42)
val b2 = new Box[String]("hello")
```

Generic functions:

```
def identity[T](x: T): T = x
identity(42)             // 42
identity("hi")           // "hi"
```

Type bounds:

```
def maxOf[T <: Comparable[T]](a: T, b: T): T =
  if a.compareTo(b) >= 0 then a else b
```

---

## 19. Entry Points

```
@main def hello(): Unit =
  println("Hello, world!")
```

Run with:

```
sbt run                              # runs the only @main
sbt "runMain cl.uchile.dcc.hello"    # runs a specific one
```

---

## 20. Comparison: Python vs Scala

| Python ↕▾ | Scala ↕▾ |
|---|---|
| −`x = 10` | `val x = 10` (immutable) |
| −`def f(a, b):` | `def f(a: Int, b: Int): Int =` |
| `None` | `None` (Option) or `null` (avoid) |
| `if x:` | `if x then` |
| `class Dog(Animal):` | `class Dog extends Animal:` |
| `self.name` | `this.name` (or just `name`) |
| `list`, `dict`, `set` | `List`, `Map`, `Set` |
| `len(xs)` | `xs.length` |
| `x in xs` | `xs.contains(x)` |
| `[x*2 for x in xs]` | `xs.map(_ * 2)` |
| `[x for x in xs if p(x)]` | `xs.filter(p)` |
| `sum(xs)` | `xs.sum` |
| `f"{a}"` | `s"$a"` |
| `@property` | `val` or `def` without parens |
| `try/except` | `try/catch case` |
⚙

---

## 21. Common Pitfalls

**1. `val` vs `var`** — prefer `val`. Only use `var` when mutation is part of the design.

**2. `==` is structural** — compares values, not references. Safe to use everywhere.

**3. Integer division**

```
10 / 3        // 3, not 3.33
10.0 / 3      // 3.333...
```

**4. Method vs field** — no `()` for pure accessors, `()` for side effects:

```
def name: String          // getter — no parens
def talk(): Unit          // action — parens
```

**5. `null` is discouraged** — use `Option[T]` instead.

**6. Match must be exhaustive** — the compiler warns if a `case` is missing. Use `case _ =>` as fallback.

**7. No semicolons, no braces needed** — use indentation:

```
// Preferred (Scala 3)
def greet(): Unit =
  println("hi")

// Works, but not course style
def greet(): Unit = { println("hi") }
```

**8. `_` has many meanings**:

```
xs.map(_ * 2)             // placeholder for a parameter
case _ => ...             // wildcard pattern
import scala._            // package wildcard
```

---

## 22. Handy Snippets

Reverse a list:

```
List(1, 2, 3).reverse                   // List(3, 2, 1)
```

Count occurrences:

```
List("a", "b", "a", "c", "a").groupBy(identity).view.mapValues(_.size).toMap
// Map(a -> 3, b -> 1, c -> 1)
```

Word frequency:

```
val text = "the quick brown fox jumps over the lazy dog the end"
text.split(" ")
  .groupBy(identity)
  .view.mapValues(_.length)
  .toMap
```

Safe integer parse:

```
def toInt(s: String): Option[Int] =
  try Some(s.toInt)
  catch case _: NumberFormatException => None
```

Sort descending:

```
List(3, 1, 4, 1, 5, 9, 2).sortBy(-_)    // List(9, 5, 4, 3, 2, 1, 1)
```

Filter a map:

```
val m = Map("a" -> 1, "b" -> 2, "c" -> 3)
m.filter((k, v) => v > 1)               // Map(b -> 2, c -> 3)
```

Transform map values:

```
m.view.mapValues(_ * 10).toMap          // Map(a -> 10, b -> 20, c -> 30)
```

---

## 23. Scala 3 Syntax Quick Notes

- **No braces needed** — use `:` and indentation.
- **`then` / `do` / `yield`** are keywords in conditionals, loops, and for-comprehensions.
- **`end X`** optional marker to close long blocks (rarely used in this course).
- **`@main def`** replaces `def main(args: Array[String])`.
- **`extension`** adds methods to existing types (not covered in this course).
- **`given` / `using`** replace `implicit` (not covered in this course).

---

*Companion cheatsheet — focus on readability over completeness.*

