# Ordnerstruktur
Die Dateien mit den Testfällen sollten separat von dem eigentlichen Code abgelegt werden, da sie nicht zum ausgelieferten Code gehören. Z.B. Für Code "src/main/kotlin/..." und für Testfälle "src/test/kotlin/..."

# Von Testfall zu UnitTest
Ein Testfall führt nicht immer zu einem UnitTest. Ein Testfall kann zu mehreren UnitTests führen, da in jedem UnitTest nur ein einziger Aspekt untersucht werden soll.


# Testbeschreibung
Tests sollten eine gute Beschreibung innerhalb des Testprogramms bekommen. Diese können auf Verschiedene Weise strukturiert werden.

## Given-When-Then Style
Given -> Vorbedingungen
When -> Schritte
Then -> Erwartetes Ergebnis

### Beispiel Given-When-Then Style
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
