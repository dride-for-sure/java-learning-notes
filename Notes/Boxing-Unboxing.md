# Autoboxing & Unboxing
Dies bezeichnet die automatische Konvertierung in den equivalenten Wrapper Type und zurück.

```java
class SampleClass {
 public static void main (String[] args) {
  int num1 = 5;
  Integer num2 = new Integer( num1 ) // autoboxing
	Integer num3 = 5; // autoboxing
	
	Integer num4 = new Integer( 5 );
	
 }
}
```