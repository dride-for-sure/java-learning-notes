# Constructor
- [Non Argument](#Non-Argument-Constructor)
- [Parameterized](#Parameterized-Constructor)
- [Constructor Overloading](#Constructor-Overloading)
- [Copy Constructor](#Copy-Constructor)

Wenn eine `class` neu instanziert wird, wird Speicherplatz reserviert und der `constructor`,
eine Methode, ausgeführt. Jedes Mal, wenn eine `class` mit dem `new` Keyword instanziert und ein
`object` erzeugt wird, wird der wenigstens ein `constructor` ausgeführt. Wenn kein
benutzerdefinierter `constructor` vorhanden ist, wird der `default constructor` verwendet.

- Der Name des `constructors` muss gleich der Name der `class` sein
- Er darf kein expliziten `return` Type besitzen
- Er ist weder `abstract`, `static`, `final` oder `synchronized`

## Non Argument Constructor
Der `non-arg constructor` versorgt das erzeugte `object` mit den default Values für benötigten
`type`.

```java
class SampleClass{
 int num;
 String str;
 
 void sampleMethod(){System.out.print( num + str );}

 public static void main (String[] args) {
	SampleClass sampleClass = new SampleClass();
	sampleClass.sampleMethod(); // 0 null ... default values provided by the constructor
 }
}
```

##Parameteterized Constrcutor
Ein `constructor` mit eine bestimmten Anzahl an Parametern. Bei der Instanzierung und Erstellung
eines `objects` können so bestimmte Parameter gesetzt werden.

```java
class SampleClass{
 
 SampleClass(int num, String str) {
  this.num = num;
  this.str = str;
 }
 
 void sampleMethod(){System.out.println( num + str);}

 public static void main (String[] args) {
	SampleClass sampleClass = new SampleClass(5, "Hello");
	sampleClass.sampleMethod(); // 5 Hello
 }
}
```

## Constructor Overloading
Bedarf es mehr als einem `constructor` und mit unterschiedlicher Anzahl an Parametern, so können
mehrere `constructors` tatsächlichverwendet werden, die vom Compiler nach der Anzahl der
Parameter selbstständig unterschieden werden.

```java
import java.awt.image.SampleModel;

class SampleClass {
 SampleClass(int num, String str) {
  this.num = num;
  this.str = str;
 }
 SampleClass(int num, String str, boolean bool){
  this.num = num;
  this.str = str;
  this.bool = bool;
 }
 void sampleMethod(){System.out.println(num + str + bool);}

 public static void main (String[] args) {
	SampleClass sampleClass1 = new SampleClass(5, "Hello");
	SampleClass sampleClass2 = new SampleClass(5, "Hello", true);
	sampleClass1(); // 5 Hello false (false ist boolean default value)
	sampleClass2(); // 5 Hello true
 }
}
```

##Copy Constructor
Um Properties eines `objects` auf ein anderes `object` zu übertragen, kann ein `constructor`
verwendet werden:

```java
class SampleClass{
 SampleClass(int num, String str){
  this.num = num;
  this.str = str;
 }
 SampleClass(SampleClass copy){ // kopiert properties von sampleClass zu sampleClassCopy
  this.num = copy.num;
  this.str = copy.str;
 }
 
 void sampleMethod(){System.out.println( num + str );}

 public static void main (String[] args) {
	SampleClass sampleClass = new SampleClass(5, "Hello");
	SampleClass sampleClassCopy = new SampleClass(sampleClass);
 }
}
```