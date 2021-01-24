# Inhaltsverzeichnis
- [Arrays](#Arrays)

_to be continued_...

# Arrays
In einem Array können mit definierter Reihenfolge Werte (Primitive & Non-Primitve) gespeichert werden. Zum Beispiel könnten Namen sortiert nach dem Anfangsbuchstaben abgelegt werden. Bei der Erstellung eines Array
wird die Länge und der Type fix definiert.

```java
String[] names = {Frieda, Hans, Marie, Otto};
// oder
int[] numbers = {1, 2, 3, 4, 5};
```

Auf Elemente innerhalb eines Array kann mit ihrem numerischen Index zugegriffen werden. Dabei ist zu beachten, dass der Index von `0` bis `Anzahl der Elemente - 1` reicht.

```
int n = Anzahl der Elemente im Array
```
| Elemente des Arrays | Element_1 | Element_2 | ... | Element_n-1 | Element_n |
|---------------------|-----------|-----------|-----|-------------|-----------|
| Index               | 0         | 1         | ... | n-2         | n-1

```java
String[] names = {Frieda, Hans};
System.out.println(names[0]); // Frieda
System.out.println(names[1]); // Hans
```

Über Arrays wird häufig mit Loops iteriert:

```java
String[] names = {Frieda, Hans, Marie, Otto};
for (int i = 0; i < names.length; i++) {
 System.out.println(names[i]); // Frieda Hans Marie Otto
}
``` 

Da ein deklariertes Array nur eine Instanz der `java.utils.Arrays` Class ist, stehen etliche vordefinierte Methoden eben jener Klasse zur Verfügung. Zum Beispiel `Arrays.compare()`:

```
String[] names1 = {Frieda, Hans};
String[] names2 = {Marie, Otto};
System.out.println(Arrays.compare(names1, names2)); // liefert 0, wenn names1 und names2 identisch, liefert != 0, wenn nicht identisch
```

Details über die vorhanden Methoden findet ihr hier https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/Arrays.html