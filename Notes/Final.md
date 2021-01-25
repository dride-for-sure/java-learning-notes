# Final
- [Final Variable](#Final-Variable)
- [Final Method](#Final-Method)
- [Final Class](#Final-Class)

Das `final` Keyword deklariert eine `variable`, `method` oder  `class` als unveränderbar und 
beschränkt so den Umgang. Sie können trotzdem weiterhin vererbt werden

# Final Variable
`final` Variablen sind konstante Variablen (auch als Parameter in einer `method` möglich), deren 
Wert nicht 
verändert werden kann. Eine mit 
keinem Value deklarierte `final` Variable nennt sich `blank final` oder `uninitialized final` 
Variable. Darüber hinaus kann sie natürlich auch `static` sein, sofern sie sich auch in einem 
`static` Block of Code befindet.

```java
class SampleClass{
 final init num = 5;

 public static void main (String[] args) {
  SampleClass sampleClass = new SampleClass();
  sampleClass.num = 10; // Error
  System.out.println(num); // 5
 }
}
```

# Final Method
`final methods` wie `variables` auch, können nicht überschrieben werden:

```java
class SampleClass {
 final void sampleMethod () {
	System.out.println( "Hello" );
 }

 public static void main (String[] args) {
	SampleClass sampleClass = new SampleClass();
	sampleClass.sampleMethod(){ // Error
	 // do something else on sampleMethod
	}
 }
}
```

# Final Class
`final classes` können nicht erweitert werden:

```java
final class SampleClass{
 class ChildrenClass extends SampleClass {
	public static void main (String[] args) {
	 ChildrenClass childrenClass = new ChildrenClass(); // Error
	}
 }
}
```