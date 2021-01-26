# Collections

- [Interfaces](#Interfaces)
- [Implementations](#Implementations)
- [Algorithms](#Algorithms)

Das Collection Framework von Java stellt die Architektur für das Speichern und Manipulieren von 
Gruppen an Objekten zur Verfügung. Die bereitgestellten Methoden reichen weit über die des 
generischen `arrays` hinaus. Darüber hinaus sind die bereitgestellten Klassen deutlich flexibler 
als das "vergleichsweise" statische `array`.

Das Collections Framework stellt folgendes zur Verfügung:
- **Interfaces**
- **Implementations**
- **Algorithms:**

Die Hierarchie des Colletions Frameworks ist wie folgt:
![Hierarchy](/Images/collections.png)

# Interfaces
## Iterator interface
Stellt die Methoden für das Iterieren in Richtung vom Anfang zum Ende zur Verfügung. Dies sind 
drei an der Zahl `hasNext()`, `next()`, `remove()`. Da der Iterator nur in eine Richtung 
iterieren kann, muss er für jeden Durchlauf neu initializiert werden. Details siehe z.B. 
[ArrayList](#ArrayList) oder [HashSet](#HashSet).

## Iterable interface
Dies ist das Basisinterface für alle Klassen des Collection Frameworks und enthält lediglich 
eine abstrakte Methode, die den Iterator für das Element mit Type `T` returned.

```java
Iterator<T> iterator()
```

### Collection interface
Das Collection Interface bildet die Grundlage für alle Klasse und deklariert sämtliche Methoden. 
Alle Methoden werden dann von den einzelnen Klasse konkret implementiert.

#### List interface
Das List Interface wird konkret implementiert von `ArrayList`, `LinkedList`, `Vector` und 
`Stack`. Es fordert eine typenbasierte Datenstruktur.

```java
List<data-type> sampleList = new ArrayList();
List<data-type> sampleList = new LinkedList();
List<data-type> sampleList = new Vector();
List<data-type> sampleList = new Stack(); 
```

Darüber hinaus fordert das List Interface die Umsetzung von einigen wichtigen Methoden wie z.B. 
`insert`, `delete` und wie auf Elemente der Liste zugegriffen werden kann (z.B. `get`).

##### ArrayList
ArrayList verwendet ein dynamisches Array, das intern das ursprüngliche `array` verwendet. Aus 
diesem Grund ist die Performance im Vergleich zur LinkedList auch beeinträchtigt. Die ArrayList 
Klasse behält die Reihenfolge bei, kann Dubletten speichern und ist nicht synchronisiert. Auf 
Elemente im ArrayList kann beliebige zugegriffen werden.

```java
ArrayList<String> sampleList = new ArrayList<String>; // Instanzierung
list.add("Foo"); // {"Foo"}
list.add("Bar"); // {"Foo", "Bar"}
```

Da die ArrayList neben dem List Interface, auch das Collection Interface, deshalb auch das 
Iterable Interface und somit auch das Iterator Interface implementiert, steht z.B. `hasNext()` 
_(nächstes Element ? true : false)_
und  `next()` _(returned das aktuelle element und bewegt den pointer ein Element weiter)_ zur 
Verfügung:

```java
ArrayList<String> sampleList = new ArrayList();
list.add("Foo"); // {"Foo"}
list.add("Bar"); // {"Foo", "Bar"}
Iterator itr = sampleList.iterator(); 
while(itr.hasNext()) {
 System.out.println(itr.next()) // Foo ... Bar
}
```
##### LinkedList
Im Gegensatz zur ArrayList ist die LinkedList eine doppelt verlinkte Liste. Jedes Element an der 
Position `n` enthält Informationen über seinen Vorgänger an der Position `n-1` und Nachfolger 
mit `n+1`. Das hat den Vorteil, dass ein (oder mehrere) Element schneller hinzugefügt oder entfernt 
werden kann, weil kein "Shifting" nötig ist und lediglich der Vorgänger und Nachfolger neu 
verknüpft werden müssen. Bei einer ArrayList muss "geshifted" und intern das gesamte Array 
neu aufgebaut werden. 
Wenn jedoch Element gelesen werden soll, so muss im Gegensatz zur ArrayList, die sich an Indizes orientiert, 
die gesamte LinkedList abgelaufen werden. Das kostet Performance. Insofern sollte vorher je nach Nutzungsart 
entschieden werden, ob Linkedlist (viele Änderungen) oder ArrayList (Speichern & Lesen) passend ist.

```java
LinkedList<String> sampleList = new LinkedList();
list.add("Foo"); // {"Foo"}
list.add("Bar"); // {"Foo", "Bar"}
Iterator theIterator = sampleList.iterator(); 
while(theIterator.hasNext()) {
 System.out.println(itr.next()) // Foo ... Bar
}
```

##### Vector
Vector ist ähnlich zur ArrayList. Es ist ein dynamisches Array, aber synchronisiert und enthält 
viele Methoden, die nicht Teil des Collection Frameworks sind.

```java
Vector<String> sampleList = new Vector();
list.add("Foo"); // {"Foo"}
list.add("Bar"); // {"Foo", "Bar"}
Iterator theIterator = sampleList.iterator(); 
while(theIterator.hasNext()) {
 System.out.println(itr.next()) // Foo ... Bar
}
```
##### Stack
Der Stack ist eine Subklasse vom Vector und implementiert das _last-in-first-out_ Prinzip: Ein 
Stack. Es enthält alle Methoden der Vector Klasse und fügt einige eigene hinzu, wie z.B. `peek()
`, `push()`, `pop()` und `empty()`:

```java
Stack<String> sampleStack = new Stack();
stack.push("A"); // {"A"}
stack.push("B"); // {"B", "A"}
stack.pop(); // {"A"}
stack.empty(); // false
```

### Queue interface
(aktuell unspannend...)
#### PriorityQueue
(aktuell unspannend...)
### Deque interface
(aktuell unspannend...)
#### ArrayDeque
(aktuell unspannend...)

### Set interface
Das Set Interface erweitert, wie auch schon das List Interface, das Collection Interface. Es 
stellt im Gegensatz zum List Interface ungeordnete Datensammlung (daraus folgt auch ohne Dubletten) 
zur Verfügung.

```java
Set<data-type> sampleSet = new HashSet<data-type>();
Set<data-type> sampleSet = new LinkedHashSet<data-type>();
Set<data-type> sampleSet = new TreeSet<data-type>();
```
#### HashSet
Das HashSet verwendet für die Speicherung ein HashTable. Das ermöglicht einen schnellen Zugriff. 
Das HashSet besitzt keine Methoden, die den direkten Aufruf eines Elements ermöglichen. Dafür 
muss wie im Beispiel der ArrayList der Iterator, der über das Iterable Interface zur Verfügung 
gestellt wird, initialisiert werden.

```java
HashSet<String> sampleHashSet = new HashSet<String>();
sampleHashSet.add("A");
sampleHashSet.add("B");

Iterator itr = sampleHashSet.iterator();
while (sampleHashSet.hasNext()) {
 System.out.println(sampleHashSet.next()) // A...B
}
```
#### LinkedHashSet
Hier verhält es sich zum HashSet ähnlich der LinkedList zur ArrayList. 

### SortedSet interface
#### TreeSet
Hier werden Elemente in einer Baumstruktur sortiert. Alle Objekte, die in einem TreeSet 
gespeichert werden sollen, müssen das `Comparable` Interface, dass die Methode 
`compareTo` fordert, implementieren:

```java
class sampleObject implements Comparable {
 private int num;
 public int getNum() {
  return this.num;
 }
 public void setNum(int num) {
  this.num = num;
 }
 public int compareTo(Object compareObject) {
  // hier muss eine nun eine Vergleichslogik implementiert werden
	int compared = -2;
	// das zu vergleichende Objekt wird zum Typ SampleObject umgewandelt
	SampleObject compareSampleObject = (SampleObject) compareObject;
	if (this.int == compareSampleObject.getNum()) {
	 compared = 0;
	}
	if (this.int < compareSampleObject.getNum()) {
	 compared = -1;
	}
	if (this.int > compareSampleObject.getNum()) {
	 compared = 1;
	}
	return compared;
 }
}
```
