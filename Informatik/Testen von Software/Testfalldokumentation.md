Tests sollten eine gute Beschreibung innerhalb des Testprogramms bekommen. Diese können auf Verschiedene Weise strukturiert werden.

# Im Markdown

| ID                  | TF0001                             |
| ------------------- | ---------------------------------- |
| Beschreibung        | Eine kurze Beschreibung des Tests. |
| Voraussetzungen     | Voraussetzungen für den Test.      |
| Ablauf              | Testablauf.                        |
| Daten               | Verwendete Daten.                  |
| Erwartetes Ergebnis | Ergebnis des Tests.                |
| Endzustand          | Zustand nach Ablauf des Tests.     |

# Im Code
## Given-When-Then Style
Given -> Vorbedingungen
When -> Schritte
Then -> Erwartetes Ergebnis

### Beispiel
Beispiel anhand von [[Testen mit JUnit5]].
``` kotlin
@Test
@DisplayName("""" 
	Given -> a new Calculator,
	When -> getting the result,
	Then -> it should be 0
""")
fun givenANewCalculatorWhenGettingTheResulrItIs0() {
	// Given
	val calculatorUnderTest = Calculator();
	// When
	val result = calculatorUnderTest.result
	// Then
	val expectedValue = 0
	result shouldBe expectedValue
}
```
