In einer eigenen Datei können Testfälle definiert werden:
``` kotlin
import org.junit.jupiter.api
class ExampleTest {
	@Test
	@DisplayName("Testbeschreibung")
	fun test1() {
		assertEquals(1+1, 2);
	}
}
```
Es lassen sich Überprüfungen definieren die zum fehlschlagen des Tests führen, außerdem werden Exceptions, welche nicht vom Code abgefangen werden als Fehlschlag gewertet. 

# Fallüberprüfung
``` kotlin
assertEquals(1+1, 2)

val result = 1
val expectedValue = 2
result shouldBe expectedValue

```

# Parameterisierte Tests
## mit einer Dimension
``` kotlin
@ParameterizedTest  
@DisplayName(  
    """ (TFK001-1)  
    GIVEN a new Calculator,    WHEN adding the digit x,   
    THEN the current number is x.  
""",  
)  
@ValueSource(ints = [1, 0, -1, (Int.MAX_VALUE - 1), Int.MAX_VALUE])  
fun tfk001_1(x: Int) {  
    val calculatorUnderTest = Calculator()  
  
    val result = calculatorUnderTest.add(x)  
  
    result shouldBe x  
    calculatorUnderTest.current shouldBe x  
}
```

## mit mehreren Dimensionen
``` kotlin
@ParameterizedTest  
@DisplayName(  
    """ (TFK002-1)  
    GIVEN a new Calculator,
    WHEN entering the digit x and entering the digit y,    
    THEN the current number is z.
    (Beispiel aus der Übung)
    """,  
)  
@CsvSource(  
    "5, 7, 57",  
    "0, 1, 1",  
    "1, 0, 1",  
    "214748364, 7, 2147483647",  
    "7, 214748364, 2147483647",  
)  
fun tfk002_1(  
    x: Int,  
    y: Int,  
    z: Int,  
) {  
    // Given  
    val calculatorOnTest = Calculator()  
    // When  
    calculatorOnTest.add(x)  
    calculatorOnTest.add(y)  
    // Then  
    calculatorOnTest.current shouldBe z  
}
```

