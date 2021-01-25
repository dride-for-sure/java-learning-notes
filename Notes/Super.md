# Super
- [Refer immediate parent class](#Refer-immediate-parent-class)
- [Invoke immediate parent class](#Invoke-immediate-parent-class)
- [Invoke immediate parent class constructor](#Invoke-immediate-parent-class-constructor)

Das `super` Keyword referenziert die parent `class`, sodass komfortable darauf zugegriffen 
werden kann.

# Refer immediate parent class
```java
class SampleClass {
 int num = 5;
 
 class ChildrenClass extends SampleClass {
  void sampleMethod() {
   System.out.println(super.num); // 5
  }
 }
}

class InvokerClass {
 public static void main (String[] args) {
  ChildrenClass childrenClass = new ChildrenClass();
  childrenClass.sampleMethod();
 }
}
```

# Invoke immediate parent class
```java
class SampleClass {
 int num = 5;
 void parentClassMethod() {
  return this.num;
 }
 
 class ChildrenClass extends SampleClass {
  void sampleMethod() {
   System.out.println(super.parentClassMethod()); // 5
  }
 }
}

class InvokerClass {
 public static void main (String[] args) {
  ChildrenClass childrenClass = new ChildrenClass();
  childrenClass.sampleMethod();
 }
}
```

# Invoke immediate parent class constructor
```java
class SampleClass {
 SampleClass(){
  System.out.println("Hello"); // Hello
 }
 
 class ChildrenClass extends SampleClass {
  void sampleMethod() {
   super(); // Invokes parents constructor
	}
 }
}

class InvokerClass {
 public static void main (String[] args) {
	ChildrenClass childrenClass = new ChildrenClass(); 
	childrenClass.sampleMethod();
 }
}
```