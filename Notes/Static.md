# Static Keyword

- [Static Variable](#Static-Variable)
- [Static Method](#Static-Method)
- [Static Block](#Static-Block)
- [Static Nested Class](#Static-Nested-Class)

Das Keyword `static` kann sowohl auf eine `variable` (class variable), auf eine `method` (class 
method), auf einen Block oder 
`nested class` angewendet werden und dient vornehmlich des Speichermanagements.

## Static Variable
Eine `static variable` kann benutzt werden, um auf die gemeinsamen Properties eines `objects`, 
also die Eigenschaften der `class`, die jenes `object` erzeugt hat, zuzugreifen.

```java
class SampleClass{
 int num = 5; // instance variable: jede instanz verbraucht nun speicherplatz für num = 5
 int static staticNum = 5; // static variable: einmalig wird speicherplatz für num = 5 reserviert
}
```

## Static Method
Eine `static method` gehört zur `class` selbst und nicht zum erzeugten `object`. Sie kann 
außerdem invoked werden, ohne eine Instanz eines `objects` erzeugen zu müssen und kann sowohl auf 
`static` Data zugreife, als auch deren Wert verändern.

````java
class SampleClass{
 static int staticVariable = 5;
 static void changeStaticVariable() {
  staticVariable = 10; // possible
 }
 void tryToChangeStaticVariable() {
  staticVariable = 10; // not possible!
 }
}
````

Es gibt zwei wesentliche Restriktionen für `static methods`: 
- Sie können auf kein `non static` Data oder `non static methods` direkt zugreifen **und**
- `this` und `super` können nicht im `static` Kontext verwendet werden.

```java
class SampleClass{
 int nonStaticVariable= 5;
 static void tryToReadNonStatic() {
  System.out.println(nonStaticVariable); // Error
 }
}
```

Btw.: `main method` ist `static`, weil dann das Objekt nicht erst instanziert werden muss. Dies 
spart Speicherplatz.