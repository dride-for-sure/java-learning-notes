# Polymorphism
- [Compile time polymorphism](#Compile-time-polymorphism)
	- [Method overloading](#Method-overloading)
	- [Method overriding](#Method-overriding)
		- [Covariant return type](#Covariant-return-type)
	- [Instance initializer block](#Instance-initializer-block)
- [Binding](#Binding)
	- [Static](#Static)
	- [Dynamic](#Dynamic)
- [instanceof](#instanceof)
- [Upcasting](#Upcasting)
- [Downcasting](#Downcasting)

Das Konzept des `polymorphism` ist angelehnt an eben jenes aus der Biologie. Dort kann ein 
Organismus einer Spezies viele verschiedene Ausprägungen entwickeln und trotzdem ein gemeinsames 
Set an Eigenschaften mit seiner Spezies teilen.

# Compile time polymorphism
## Method overloading
Um die Anzahl der Methoden zu reduzieren, Übersichtlichkeit zu gewähren und trotzdem auf 
unterschiedliche Situation reagieren zu können, können `methods` überladen werden. Dazu wird ein 
oder mehrere weitere gleichnamige `methods` mit unterschiedlicher Anzahl an Parametern definiert.
Der Compiler wählt dann passend zur Anzahl der übergebenden Parametern die korrekte `method` aus
(Btw.: main() kann auch überladen werden).

Wird keine `method` mit passendem Parameter Type gefunden, so werden die Types wie gehabt 
konvertiert:

```java
byte -> short -> int -> long or float -> double 
char -> int -> long or float -> double
```

```java
class SampleClass {
 void sampleMethod (int num) {
  // do something and return nothing
 }
 String sampleMethod (int num, String str) {
  // do something else and return a String
 }

 public static void main (String[] args) {
  this.sampleMethod( 5 );
  this.sampleMethod( 5, "Hello" );
  this.sampleMethod( 'A' , "Hello"); // char -> int: Also sampleMethod(int num, String str)
 }
}
```

## Method overriding
Besitzt eine `child class` namentlich die selbe `method` wie die `parent class`, stimmen die
Parameter überein und handelt es sich in Bezug auf Vererbung um eine `IS-A` Beziehung, so wird die
`parent class method` überschrieben. Dies ist praktisch um Details der `child class` gegenüber
der `parent class` zu spezifizieren.

`static methods` können natürlich nicht überschrieben werden, weil sie zur `parent class` area
im Speicher gehören. Instanzen gehören zur Heap Area.

```java
class SampleClass {
 void SampleMethod (int num) {
  // do something
 };
 
 class ChildrenClass extends SampleClass {
  void SampleMethod (int num) {
   // do something else
  }
 }
}
```

### Covariant return type
Implementiert eine `children class` eine `method` namentlich und parametertechnisch gleich zur
`parent class` und überschreibt diese, so kann der `return type` ebenfalls überschrieben werden.
Die JVM nutzt `full signature lookup` und so kann eine `class` etliche `methods` besitzen, die
sich nur durch den `return type` unterscheiden.

## Instance initializer block
Dieser Block bei jeder Instanzierung der `class` direkt nach dem `constructor` ausgeführt und 
kann z.B. für komplexere Befüllung der Instanz mit Daten genutzt werden.

```java
class SampleClass {
 // Instance initializer block
 int num = 5;
 System.out.println("Second " + this.num);
 
 SampleClass() {
  System.out.println("First" + this.num);
 }
}
// First 5
// Second 0
```

# Binding
## Static
Wenn der Type zur `compile-time` bestimmt werden kann, nennen wir dies `static binding`.

```java
class SampleClass {
 public static void sampleMethod() {
  System.out.println( "Hello Parent" );
 }
 
 class ChildrenClass extends SampleClass {
  public static void sampleMethod() {
   System.out.println( "Hello Children" );
  }
 }
 
 class Invoker {
  public static void main (String[] args) {
   SampleClass sampleClass1 = new SampleClass();
   SampleClass sampleClass2 = new ChildrenClass();
   sampleClass1.sampleMethod(); // Hello Parent
   sampleClass2.sampleMethod(); // Hello Parent -> static methods können nicht überschrieben werden
  }
 }
}
```

## Dynamic
Wenn der Type zur `runtime` bestimmt wird, nennen wir dies `dynamic binding`.

```java
class SampleClass {
 public void sampleMethod() { // non static
  System.out.println( "Hello Parent" );
 }
 
 class ChildrenClass extends SampleClass {
  public void sampleMethod() { // non static
   System.out.println( "Hello Children" );
  }
 }
 
 class Invoker {
  public static void main (String[] args) {
   SampleClass sampleClass1 = new SampleClass();
   SampleClass sampleClass2 = new ChildrenClass();
   sampleClass1.sampleMethod(); // Hello Parent
   sampleClass2.sampleMethod(); // Hello Children -> kann überschrieben werden, weil non-static
  }
 }
}
```

# instanceof
Mit dem `instanceof` Operator kann getestet werden, ob ein `object` zum spezifischen Typ gehört 
oder nicht. Es ist eine Art `comparison` Operator und gibt `boolean` zurück.

```java
class SampleClass {
 class ChildrenClass extends SampleClass {}
 
 public static void main (String[] args) {
  SampleClass sampleClass = new SampleClass();
  System.out.println(sampleClass instanceof SampleClass); // true
	
  ChildrenClass childrenClass = new ChildrenClass();
  System.out.println(childrenClass instanceof SampleClass); // true
 }
}
```

# Upcasting
Zeigt eine Referenz Variable einer `parent class` auf eine ihrer `child classes`, so nennt sich
dies `upcasting`.

```java
interface SampleInterface {}
class SampleClass {}
class ChildrenClass extends SampleClass implements SampleInterface {
 SampleClass sampleClass = new ChildrenClass(); // Upcasting
}
```

# Downcasting
Soll ein `children class` Type auf ein `parent class object` referenzieren, so geschieht dies 
mit dem `instanceof` operator:

```java
ChildrenClass childrenClass = new ParentClass(); // Compiler Error
ChildrenClass childrenClass = (ChildrenClass) new ParentClass(); // Downcasting
```