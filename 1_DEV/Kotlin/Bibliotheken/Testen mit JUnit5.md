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


