# Abstract
Eine abstrakte `class` wird deklariert mit Hilfe vom Keyword `abstract`. `abstract classes` sind
ähnlich zu Interfaces. Sie können nicht instanziert werden und können `abstract methods`
ohne und `methods` mit Implementation enthalten. `abstract methods` müssen in `abstract classes`
deklariert werden. Im Gegensatz zum Interface müssen Fields allerdings nicht
unumgänglich `public static final` und alle `methods` `public` sein. Darüber hinaus kann nur
eine `class` erweitert, allerdings beliebig viele Interfaces implementiert werden.

`abstract`:
- wenn Code mit nahestehenden `classes` geteilt werden soll
- wenn `classes`, die die `abstract class` erweitern viele gemeinsame `methods` oder Fields 
	enthalten, sowie auf andere `access modifiers` als `public` angewiesen sind
- wenn `non-final` oder `non-static` methods Verwendung finden sollen

```java
abstract class sampleClass {
 abstract void abstractSampleMethod(){};
 void sampleMethod(){};
}

class ChildrenClass extends sampleClass {
 void sampleMethod(){ // childrenClass muss abstractSampleMethod implementieren
  // do something
 }
}
```

Interfaces:
- wenn erwartet werden kann, dass beliebige `classes` das Interface implementieren wollen
- wenn das Verhalten eines Types klar definiert werden soll, ohne sich über die Implementierung 
	Gedanken machen zu müssen
- mehrere Interfaces auf einer `class` implementiert werden sollen
