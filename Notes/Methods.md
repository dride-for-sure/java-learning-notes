# Methods
- [Method Deklaration](#Method-Deklaration)
- [Typen von Methods](#Typen-von-Methods)
	- [Vordefinierte Methods](#Vordefinierte-Methods)
	- [Benutzerdefinierte Methods](#Benutzerdefinierte-Methods)
- [Static Methods](#Static-Method)
- [Instance Method](#Instance-Method)
	- [Accessor Method](#Accessor-Method)
	- [Mutator Method](#Mutator-Method)
- [Abstract Method](#Abstract-Method)
- [Factory Method](#Factory-Method)

Eine `Method` ist ein Block aus Code oder eine Sammlung an Statements, die zusammen eine bestimmte Aufgabe erfüllen
sollen. Die `Method` exponiert die Funktionalität eines `Objects` nach außen.

### Method Deklaration
Eine `Method` wird deklariert wie folgt:

```java
<access specifier><return type><method name> (<parameter list>){
	<method body>
}
```

- Die `method signature` wird die Kombination aus `<method name>` und `<parameter list>` genannt.
- Der `access specifier` kann folgende Werte annehmen:
	- `public`: Die `Method` kann von allen `Classes` verwendet werden
	- `private`: Auf sie kann nur innerhalb der `Class`, in der sie deklariert wurde, zugegriffen werden
	- `protected`: Die `Method` kann nur innerhalb des selben `package` oder `subclass` verwendet werden
	- `default`: Ist kein `access specifier` angegeben, kann sie nur innerhalb des selben `package` verwendet werden

- Der `return type` gibt an, was für ein Type returned wird. Wird nichts zurückgegeben, so wird `void` angegeben.
- Der `method name` ist eine unique ID, die die Funktionalität repräsentieren soll. `method names` folgen `camelCase`.
- Die `parameter list` enthält alle an die `Method` zu übergebenden Parameter mit Namen und Typ.
- Der `method body` enthält die Funktionalität der `Method` und befindet sich innerhalb der geschweiften Klammern

### Typen von Methods
#### Vordefinierte Methods
Java enthält viele vordefinierte `methods`, die in den 'Java Class Libraries' enthalten sind. Diese werden häufig
auch built-in `methods` genannt. Jede vordefinierte `method` ist innerhalb einer `class` definiert. Beispielsweise
ist `print()` innerhalb von `java.io.PrintStream` deklariert.

Sämtliche `classes` sind in der Doku hier zu finden: https://docs.oracle.com/en/java/javase/15/docs/api/

#### Benutzerdefinierte `methods`
Benutzerdefinierte `methods` werden wie unter [Method Deklaration](#Method-Deklaration) beschrieben definiert.
Aufgerufen werden sie wie folgt:

```java
public class SomeClass {
 public static public static void main (String[] args) {
  testMethod(); // invoke testMethod
 }
 public void testMethod() {
  // do something
 }
}
```

### Static Method
Wird dem `<access specifier>` das Keyword `static` hinzugefügt, so gehört die Methode der `Class` und nicht deren
Instance selbst. Der Vorteil ist, dass die `static method` ohne eine Instanz zu erstellen aufgerufen werden kann.

### Instance Method
Eine `instance method` ist eine non-`static method`. Bevor die `method` aufgerufen werden kann, muss eine Instanz
der zugehörigen `Class` erzeugt werden.

Beispiel:
```java
public class SampleClass {
 public static void main (String[] args) {
	SampleClass instanceOfSampleClass = new SampleClass();
	instanceOfSampleClass.nonStaticMethod(); // hier ist eine instanz erforderlich
	staticMethod(); // hier kann die methode direkt invoked werden
 }
 public static void staticMethod () {
  // do something
 }
 public void nonStaticMethod () {
  // do something else
 }
}
```
#### Accessor Method
Die `accessor methods` sind sogenannte `getters` und können am Prefix `get` erkannt werden. Sie werden benutzt um
Werte eines `private fields` abzufragen.

```java
public void getAccessorMethod() {
 return something;
}
```

#### Mutator Method
Eine `mutator method` ist eine sogenannte `setter` oder `mutator` Methode und kann am Prefix `set` erkannt werden.
Sie wird benutzt um den Wert eines `private fields` zu setzen.

```java
public void setMutatorMethod(int someValue){
 this.privateField = someValue;
}
```

### Abstract Method
Eine `abstract method` muss in einer `abstract class` deklariert werden. Sie ist eine `method` ohne
`body`, denn dieser wird später durch die konkrete Implementation erzeugt.

```java
abstract class sampleClass {
 abstract void sampleMethod ();
}

public class anotherSampleClass extends sampleClass {
 void sampleMethod() { // implements the body of sampleMethod()
  // do something
 }
}
```

### Factory Method
Die `factory method` erzeugt ein `object` zu der `class` zu der sie gehört.

```java
public interface sampleItem {
 void sampleMethod ();
}

public class sampleFactory {
 public static sampleItem getSampleItem () {
  return new sampleItem(); // Erstellt eine neue Instanz vom sampleItem 
 }
}
```