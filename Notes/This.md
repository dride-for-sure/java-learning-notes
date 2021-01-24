# This Keyword
- [Refer current class instance variable](#Refer-current-class-instance-variable)
- [Invoke current class methods](#Invoke-current-class-methods)
- [Invoke current class constructor](#Invoke-current-class-constructor)
- [Method Argument](#Method-Argument)
- [Constructor Argument](#Constructor-Argument)
- [Within Methods Return](#Within-Methods-Return)

# Refer current class instance variable
Wenn sich `instance variable` und Arguemnte namentlich nicht unterscheiden, so kann `this` den 
Bezug zur aktuellen Instanz der `class` herstellen.

```java
class SampleClass {
 int num;
 SampleClass(int num){
  this.num = num;
 }
}
```
# Invoke current class methods
`this` kann verwendet werden um eine Methode zu invoken. Wird `this` nicht verwendet, so ergänzt 
der Compiler dies automatisch. Insofern ist `this` hier optional.

```java
class SampleClass {
 void m() {
  // do something
 }
 this.m(); // this.m(); and m(); are the same...
 m();
}
```

# Invoke current class constructor
Der `this()` Constructor Call kann dazu verwendet werden, um Constructors miteinander zu 
verknüpfen (`constructor chaining`). So kann der Constructor erneut verwendet werden:

```java
import java.awt.image.SampleModel;

class SampleClass {
 SampleClass () {
  // To this..
  System.out.println("Second Constructor");
 }

 SampleClass(int num) {
  this();
  System.out.println("First Constructor" + num);
 }
}

class SampleClass2 {
 public static void main (String[] args) {
  SampleClass sampleClass = new SampleClass(5); // First Constructor 5, Second Constructor
 }
}
```

# Method Argument
`this` kann als Argument einer `method` als Referenz zur Ursprungsinstanz weitergegeben werden, 
sofern das `object` weiterverwendet werden soll (Event Handling usw...).

```java
class SampleClass{
 void sampleMethod(){
  sampleMethod2(this);
 }
 void sampleMethod2(SampleClass obj){
  System.out.println(obj);
 }

 public static void main (String[] args) {
  SampleClass sampleClass = new SampleClass();
  sampleClass.sampleMethod(); // outputs the object referenz from sampleMethod2
 }
}
```

# Constructor Argument
`this` kann - ähnlich dem `this` als `method` Arugment - auch als `constructor` Argument 
übergeben werden. So kann das `object` weiterverwendet werden.

```java
class SampleClass {
 SampleClass(SampleClass2 obj){
  this.obj = obj;
 }
 
 void sampleMethod () {
  System.out.print( obj.num ); // Prints 10
 }
}

class SampleClass2 {
 int num = 10;
 
 SampleClass2() {
  SampleClass sampleClass = new SampleClass(this);
  sampleClass.sampleMethod();
 }

 public static void main (String[] args) {
  SampleClass2 sampleClass2 = new SampleClass2();
 }
}
```

# Within Methods Return
`this` kann ebenfalls per `return` Value übergeben werden. Dafür muss der `return` Type der 
`method` allerdings der `class` Type (`non-primitive`) sein:

```java
class SampleClass {
 SampleClass getSampleClass() {
  return this;
 }
}

class SampleClass2 {
 public static void main (String[] args) {
  SampleClass sampleClass = new SampleClass();
  System.out.println( sampleClass.getSampleClass(); ); // the SampleClass reference
 }
}
```