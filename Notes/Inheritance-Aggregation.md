# Inheritance & Aggregation
- [Inheritance](#Inheritance)
	- [Syntax](#Syntax)
	- [Types of Inheritance](#Types-of-Inheritance)
- [Aggregation](#Aggregation) 

# Inheritance
Inheritance repräsentiert die `IS-A` Beziehung, die auch _parent-child_ genannt wird. Die Idee 
dahinter ist, dass bereits existierende `classes` Grundlage neuer `classes` sein können. So 
können bereits bestehende `methods` und `fields` weiterverwendet werden.

- **Parent:** `super class` / parent `class` ist die `class`, von der das Kind alle 
	Eigenschaften vererbt bekommt
	
- **Child:** `sub class` / child `class` ist die `class`, die Eigenschaften vom Parent vererbt 
	bekommt. Sie wird auch `extended class` genannt.
	
```java
class childClass extends parentClass {
 // do something
}
```

## Types of Inheritance

1) **Single**: `class B` vererbt `class A`
2) **Multilevel**: `class C` vererbt `class B`, die `class A` verwerbt
3) **Hierarchival**: `class C` und `class B` vererben beide an `class A`
	 
_Folgende Types werden von Java nicht unterstützt:_
4) **Multiple**: `class C` vererbt gleichzeitig an `class B` und `class A`
5) **Hybrid**: `class D` vererbt gleichzeitig an `class C` und `class B`, die dann beide an 
	 `class A` vererben
	 
# Aggregation
Aggregation ist eine `HAS-A` Beziehung. So hat eine `class` möglicherweise ein Property, das 
selbst wieder ein `object` ist. Code kann so gut wiederverwendet werden, weil er möglichst 
modular aufgebaut ist und jede Logik zugänglich gemacht werden kann.

```java
class AnotherClass{
 int double(int num) {
  return num * 2;
 }
}

class SampleClass{
 AnotherClass anotherClass; // Aggregation
 int double(int num) {
  return anotherClass.double(num);
 }
 
 public static void main (String[] args) {
  SampleClass sampleClass = new SampleClass();
  System.out.println(this.double(5);); // 10
 }
}
```