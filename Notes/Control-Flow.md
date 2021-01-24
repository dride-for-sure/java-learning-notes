# Inhaltsverzeichnis
- [Control Flow](#Control-Flow)
    - [Decision Making Statements](#Decision-Making-Statements)
        - [If else](#If-else)
        - [Switch](#Switch)
    - [Looping Statements](#Looping-Statements)
        - [For loops](#For-loops)
        - [While loop](#While-loops)
        - [Do while loop](#Do-while-loops)
        - [For each loop](#For-each-loops)
    - [Branching Statements](#Branching-Statements)
        - [Break](#Break)
        - [Continue](#Continue)
        - [Return](#Return)
            - [Rekursion](#Rekursion)
    

# Control Flow
Geschriebener Code wird idR. von oben nach unten ausgeführt. Allerdings sind häufig Fallentscheidungen nötig, die dann darauf Einfluss nehmen, welcher Block mit Code
in welchen Fällen als Nächstes ausgeführt werden soll. Fallunterscheidungen werden mit **Control flow statements** definiert.

Wir unterscheiden:

| Decision Making Statements | Looping Statements | Branching Statements |
| ---------------------------|--------------------|----------------------|
| if statement               | for loop           | break statement      |
| if-else statement          | while loop         | continue statement   |
| switch statement           | do-while loop      | return statement     |
|                            | _for-each loop_    |                      |


## Decision Making Statements
### If else

```
wenn (dies wahr) {
    führe das durch
oder wenn (dies wahr) {
    führe dies durch
in allen anderen Fällen {
    jenes
}
```

Dies sähe beispielsweise so aus:

```java
if (i > 5) {
    // führe das, wenn i größer als 5 ist, aus
} else if (i == 5) {
    // führe dies, wenn i == 5 ist, aus
} else {
    // führe dies in allen anderen Fällen aus
}
```

### Switch

```
es geht um (i) {
  für den fall, dass i DAS ist: 
    führe das aus
    verlasse das switch statement
  für den fall, dass i DIES ist:
    führe dies aus
    verlasse das switch statement
  für alle anderen fälle von i:
    führe jenes aus
}
```

Dies sähe beispielsweise so aus:

```java
switch (i) {
 case 1:
   // führe das aus, wenn i == 1 ist
   break;      
 case 2:
   // führe dies aus, wenn i == 2 ist
   break;
 default:
   // führe jenes in allen anderen fällen aus
}
```
## Looping Statements
### For loops
```
(Startwert, Bedingung, Vernderung nach jedem Durchlauf) {
 führe dies aus 
}
```

Die nachfolgende `for` Loop gibt alle Buchstaben des `String letters` nacheinander in der Console aus:

```java
String letters = "ABCDEFG";

for (int i = 0; i < letters.length(); i++) {
 System.out.println(letters.charAt(i)); // gibt den Buchstaben an der Position i aus
}
```

### While loops
```
solange (die bedingung erfüllt ist) {
 führe dies aus
}
```

```java
String letters = "ABCDEFG";
int i = 0;

while (i < letters.length()) {
 System.out.println(letters.charAt(i)); // gibt den Buchstaben an der Position i aus
 i += 1;
}
```
### Do while loops
Im Gegensatz zur `while` Loop checkt die `do while` Loop nicht zuerst die Bedingung und führt dann den
Code Block aus, sondern führt ihn erst aus und checkt dann, ob die Endbedingung erfüllt ist.

```
{ führe dies aus } solange (die bedingung erfüllt ist);
```

Das sieht dann so aus:

```java
String letters = "ABCDEFG";
int i = 0;

do {
 System.out.println(letters.charAt(i)); // gibt den Buchstaben an der Position i aus
 i += 1;
} while (i < letters.length() - 1); // die begingung wird nach dem "do" evaluiert, wir müssen also einen turnaround vorher stoppen
```

### For each loops
Ein `for each` Loop ist der `for` Loop sehr ähnlich und für das Iterieren über Arrays und Collections gedacht.
`for each` Loops sind eigentlich "Syntactic Sugar" und könnten vollständig durch `for` Loops ersetzt werden. Es steht also jedem frei
das ein oder andere zu verwenden.

```
Array = {Element_1, ... , Element_n}

für jedes Element im Array führe Folgendes aus {
 führe Folgendes aus
}
```

```java
String[] wortListe = {"Ich", "bin", "ein", "Array"};

for (String wort: wortListe) {
 System.out.println(wort); 
}
```
## Branching Statements
### Break
`break` beendet den innersten Loop und führt den dem Block nachfolgenden Code aus.

```java
String letters = "ABCDEFG";
int i = 0;

while (i < letters.length()) {

 if ( letters.charAt( i ) == 'D' )  // wenn der aktuelle Buchstabe 'D' ist -> break;
  break;
 }
 
 System.out.println(letters.charAt(i)); // gibt den Buchstaben an der Position i aus
 i += 1;
}
```

An dieser Stelle kann erwähnt werden, dass es für den Fall von verschachtelten Loops labeled-`break` Statements gibt, die einen der äußeren Loops beenden können.
Dies kann hilfreich sein, wenn eine der inneren Loops die Beendigung eines bestimmten äußeren Loops auslösen soll.

Infos darüber findet ihr in der Doku an dieser Stelle: https://docs.oracle.com/javase/tutorial/java/nutsandbolts/branch.html

### Continue
Das `continue` Statement hält die aktuelle Iteration eines Loops an und geht direkt zur nächsten Iteration über.

```java
String word = "FooBar";
 for ( int i = 0; i < word.length(); i++ ) {
  if ( word.charAt( i ) == 'B' ) {
   continue; // im Fall von 'B' wird direkt zur nächsten Iteration gesprungen
  }
 System.out.println( word.charAt( i ) ); // F o o a r
}
```

### Return
Das `return` Statement findet sich innerhalb (am Ende) einer Methode (Funktion), beendet diese und führt zurück zu der Stelle, von der die Methode
aufgerufen wurde.

`return;` kann entweder nichts, eine Variable `return foo;` oder eine Expression `return 1+1;` folgen.

Wird `return` mit einer Variablen kombiniert, so wird die Methode beendet und der Wert der Variable an die die Methode aufrufende Variable übergeben.
Wird `return` mit einer Expression verwendet, so wird zunächst die Expression evaluiert, before die Methode beendet wird. Gibt die evaluierte Expression einen Wert zurück,
so wird dieser an die die Methode aufrufende Variable mit übergeben.

#### Rekursion
Rekursive Programmierung bezeichnet den Selbstaufruf einer Methode (Funktion). Häufig bietet es sich an Schleifen durch rekursive Methodenaufrufe leserlicher
zu schreiben. Wichtig bei rekursiver Programmierung ist eine Abbruchbedingung, damit sich die Funktion theoretisch nicht unendlich oft selbst aufruft.

```
funktion fakultät (n) {
wenn (n gleich 0) {
  gib 1 zurück
} sonst {
  gib n * fakultät(n-1) zurück
} 
```
Die Funktion `fakultät` ruft sich also bei jedem Durchlauf mit einem um 1 verringerten Wert selbst erneut auf. Wir können uns das für `n = 4` so vorstellen:

`4 * (fakultät(4 - 1) * (fakultät(3 - 1) * fakultät(2 - 1)));`

So sieht das dann implementiert aus:
```java
public static int factorial (int number) {
 if ( number == 0 ) {
  return 1;
 } else {
  return ( number * factorial( number - 1 ) );
 }
}
```