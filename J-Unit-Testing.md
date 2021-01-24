# Inhaltsverzeichnis
- [Test mit JUnit](#Test-mit-JUnit)
    - [Tests schreiben](#Tests-schreiben)
- [Parametrisierte Tests](#Parametrisierte-Tests)
    - [Sources of Arumgents](#Sources-of-Arguments)
        - [@ValueSource](#@ValueSource)
        - [@CsvSource](#@CsvSource)
        - [@MethodSource](#@MethodSource)

# Test mit JUnit
J-Unit ist ein Testing-Framework für Java. Mit diesem können Methoden in Bezug auf ihren return-Value bei vorgegebenem Input überprüft werden.
So können Fehler nicht nur im Voraus vermieden werden, sondern auch im Zuge der Weiterentwicklung der Software fortlaufend automatisiert detektiert werden.
Gleichermaßen ist zu jeder Zeit sichergestellt, dass zu mindestens die Funktionalität der Methoden gegeben ist, für die Tests geschrieben wurden.

## Tests schreiben
Im Verzeichnis `src/test/...(/...)?<TestClass>` werden Tests angelegt.

Ein TestClass-File besteht aus dem Import des J-Unit Test Module, der Definition der Klasse und mit @Test (hier sind auch anderen Annotationen für komplexere Tests möglich) annotierten Methoden innerhalb jener, die die einzelne Testlogik beinhalten.
```Java
import org.junit.jupiter.api.Test;

public class TestClass {

@Test
public void testMethod () {
// Test something
}

}
```

### Beispiel:
In der eigentlichen Application befindet sich eine Methode duplicate(int number). Selbstverständlich soll überprüft werden, ob diese Methode die Erwartungen erfüllt.

```Java
public int duplicate (int value){
  return value * 2;
}
```
Z.B. könnte automatisiert bei jedem build (mit Hilfe von GitHub Actions -> Workflow auch bei jedem pull request) überprüft werden, ob bei int value = 3 auch tatsächlich 6 returned wird und die Funktion anscheinend den Input Value verdoppelt. Die Testmethode könnte dann mit Hilfe der Assertion assertEquals so ausschauen:

```Java
import static org.junit.jupiter.api.Assertions.assertEquals; // Import des passenden Assertions Modules

public class TestClass {

@Test
public void testDuplicate() {
  int testValue = 3;
  assertEquals( 6, duplicate(testValue)); // das ist offensichtlich 'true'
  }

}
```
Weitere Details zu den unterschiedlichen Annotationen findet ihr hier: https://junit.org/junit5/docs/current/user-guide/#writing-tests bzw. zu den verschiedenen Assertions & Assumptions hier:
https://junit.org/junit5/docs/current/user-guide/#writing-tests-assertions

# Parametrisierte Tests
Ein Test mit J-Unit besteht im minimalsten Fall aus einer Annotation `@Test`, der eigentlichen Test Methode und einer Behauptung (Assertion) bzw. Annahme (Assumption).

Dies könnte so aussehen:
```java
@Test
@DisplayName("Hier wird die testMethode getestet")
void testMethod() {
 assertTrue(functionToTest()); // checked ob functionToTest() true liefert
}
```

Mit parametrisierten Tests können Tests mit unterschiedlichen Argumenten mehrmalig ausgeführt werden. Das erspart das Anlegen eines Tests für jeden einzelnen Case.
Dazu muss wenigstens eine Source definiert werden, die die Argumente für jeden Testdurchlauf liefert. Diese im Source definierten Werte werden von der Testmethode typischerweise einer nach dem anderen
konsumiert (siehe [Consuming of Arguments](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-consuming-arguments)). Der parametrisierte Test wird
wie folgt gekennzeichnet:

```java
@ParameterizedTest
@ParameterizedTest(name = "Das ist das Testmethoden Argument {0} und dies {1} usw...")
```

## Sources of Arguments
### @ValueSource
`ValueSource` ist ein einfaches Array aus Literals. Es liefert pro Iteration der Testmethode genau einen Wert:

```java
@ParameterizedTest
@ValueSource( ints = {1,2,3,4} )
void testMethode(int value) {
 // ein Test...
}
```

Dies ergibt folgenden Testzyklus:

```java
testMethode(1);
testMethode(2);
testMethode(3);
testMethode(4);
```

Weitere Details hier in der Doku: https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-ValueSource.
### @CsvSource
Die `CsvSource` ist eine Comma-separated-list mit dem Delimiter `,`. Das Quote Zeichen innerhalb der `CsvSource` ist ein einfaches Anführungszeichen. So könnte eine `CsvSource` zum Beispiel
so aussehen:

```java
@ParameterizedTest
@CsvSource({
  "Name1, true",
  "Name2, false"
 )
}
void testMethode(String argument1, Boolean argument2) {
 // ein Test...
}
```

Die einzelnen Argumente werden pro Zeile auf die Argumente des Testmethode verteilt. Obiges Beispiel ergibt folgenden Testzyklus:

```java
testMethode("Name1", true);
testMethode("Name2", false);
```

Weitere Details hier in der Doku: https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-CsvSource
### @MethodSource
Mit `MethodSource` erlaubt es uns eine (oder mehrere) _factory_ Methode(n) zu verwenden. Diese müssen einen Stream mit Argumenten generieren, so dass jedes Argument als
ein echtes Argument an die Testmethode übergeben werden kann.

Im einfachsten Fall könnte das so aussehen:

```java
@ParameterizedTest
@MethodSource("factoryMethod") // <-- Name der Factory Methode; wenn leer, dann wird nach einer gleichnamigen gesucht
void testMethod(int num) {
 // ein Test...
}

static Stream<int> factoryMethod() { // Return value ist ein Stream mit Integern
  return Stream.of(1,2,3,4);
}
```

Dies ergibt dann folgenden Testzyklus:

```java
testMethod(1);
testMethod(2);
testMethod(3);
testMethod(4);
```

Der Stream kann auch komplexere Argumente enthalten. So können mehrere Werte, ähnlich der CsvSource, übergeben werden. Dies sieht dann so aus:

```java
@ParameterizedTest
@MethodSource("factoryMethod")
void testMethod(int num, boolean bool, String str) {
 // ein Test...
 }
 
 static Stream<Arguments> factoryMethod() {
 return Stream.of(
      Arguments.of(1, false, "String1"),
      Arguments.of(2, true, "String2")
   );
 }
 ```

Dies ergibt folgenden Testzyklus:

```java
testMethod(1, false, "String1");
testMethod(2, true, "String2");
```

Weitere Details hier in der Doku: https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests-sources-MethodSource
