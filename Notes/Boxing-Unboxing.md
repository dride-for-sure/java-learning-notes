# Boxing & Unboxing
Dies bezeichnet die automatische Konvertierung in den equivalenten Wrapper Type und zurück.

```java
class SampleClass {
 public static void main (String[] args) {
  int num1 = 5;
  Integer num2 = new Integer( num1 ); // boxing
  Integer num3 = 5; // boxing
	
  Integer num4 = new Integer( 5 ); // boxing
  int num5 = num4; // unboxing
 }
}
```

Dies funktioniert ebenfalls automatisch im Zusammenhang mit Vergleichsoperatoren:

```java
class SampleClass {
 public static void main (String[] args) {
  Integer num = 5; // boxing
	
  if (num < 10){ // unboxing
   // do this
  }
 }
}
```

Zu beachten ist, dass `widening` das Autoboxing überstimmt:

```java
class SampleClass {
 void sampleMethod(int num){}; // können existieren...
 void sampleMethod(Integer num){}; // wegen method overloading
 
 public static void main (String[] args) {
  this.sampleMethod( 5 ); // invoked sampleMethod(int num) weil widening boxing überstimmt
 }
} 
```

Allerdings wird überstimmt Autoboxing `varargs`:

```java
class SampleClass {
 void sampleMethod(Integer num){};
 void sampleMethod(Integer ...num){};

 public static void main (String[] args) {
  this.sampleMethod( 5 ); // invoked sampleMethod(Integer num), weil boxing varargs überstimmt
 }
}
```