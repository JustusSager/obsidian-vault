#Informatik #Computergraphik 
Erste Entscheidung / Einschränkung ist, ob etwas so realistisch wie möglich oder mit Zeitbegrenzung gerendert werden soll. 
Das realistische Rendern mit eines einzigen Bildes kann mehrere Tage dauern da es physikalische Prozesse möglichst ohne Kompromisse wiederspiegeln soll. Dabei spielt die Rechenzeit keine (oder nur geringe) Rolle.
Beim Rendern mit Zeitbegrenzung soll eine Mindestzahl an Bildern pro Sekunde (FPS -> Frames per Second) gerendert werden, typischerweise min. 20 FPS. 

# Was ist OpenGL
Eine Programmierschnittstelle welche Betriebssystem und Hardwareunabhängig mit möglichst wenigen Kommandos arbeitet. 
- als Client-Server-Architektur implementiert.
OpenGL bietet nicht:
- Fenstermanagement (siehe [[#Ein Fenster (mit GLFW)]])
- Objektgenerierung (z.B. eine Kugel)
- Funktionen zum laden von Bildern

# Ein Fenster (mit GLFW)
GLFW ist eigentlich nicht Teil von OpenGL kann jedoch verwendet werden um ein Fenster zu erstellen, da OpenGL keine Funktionen dafür zur Verfügung stellt.
``` C++
#include<GLFW/glfw3.h>
```

## Fenster erstellen
``` C++
//GLFW initialisieren
if (!glfwInit())
	exit(EXIT_FAILURE);

//Fenster mit 1280x1024 Pixel erstellen
window = glfwCreateWindow(
	1280, // (int) width
	1024, // (int) height
	"Happy Cube", // (char*) title
	NULL, // (GLFWmonitor*) monitor
	NULL // (GLFWwindow) window
);
if (!window)
{
	glfwTerminate(); // GLFW beenden
	exit(EXIT_FAILURE);
}
```

## Hauptschleife
``` C++
// solange das Fenster nicht geschlossen werden soll
while (!glfwWindowShouldClose(window))
{
	//Hauptscheife
}
// Ansonsten das Programm beenden
glfwDestroyWindow(window);
glfwTerminate();
exit(EXIT_SUCCESS);
```

## Callbacks und Events
GLFW unterstützt die Verarbeitung von Callbacks und Events. Die Verknüpfung zwischen Fenster und Methode muss einmal gesetzt werden. Siehe dazu z.B. [[#Key Callback]] für Tastaturanschläge.
Innerhalb der [[#Hauptschleife]] sollten die Callbacks und Events verarbeitet werden, z.B. am Ende damit die Änderungen für den nächsten Frame bereitstehen.
``` C++
glfwPollEvents(); // nicht blockierend
// oder
glfwWaitEvents(): // blockierend
```
Ein Callback kann dabei z.B. eine Variable verändern, welche dann in der Hauptschleife verwendet wird.

### Key Callback
In der `main()` das Fenster `window` mit der `key_callback()`-Methode verbinden:
``` C++
glfwSetKeyCallback(
	window, // (GLFWwindow*) das Fenster, dass eingefangen werden soll
	key_callback // (GLFWkeyfun) die Methode, die aufgerufen wird
);//Key-Callback setzten
glfwMakeContextCurrent(window);//Verbindung mit dem Fenster
gladLoadGL(glfwGetProcAddress);//Laden der Fuktionszeiger
```
Die `key_callback()`-Methode:
``` C++
void key_callback(GLFWwindow* window, int key, int scancode, int action, int mods)
{
	if (action != 0)//nur beim Hinunterdrücken einer Taste
	{
		if (key == GLFW_KEY_A)//Wenn diese Taste "A" war
		{
			if (mods == 1)//Wenn Shift zusätzlich gehalten ist
				// Do something
			else
				// Do something else
		}
		// (...) weitere Tasten (...)
	}
}
```
## GLFW Fenster mit OpenGL verbinden (mit GLAD)
Um das GLFW Fenster mit OpenGL zu verbinden benötigt man die "loader library" GLAD. 
``` C++
#include <glad/gl.h>
```

Nachdem das Fenster erstellt ([[#Fenster erstellen|...]]) wurde, kann man mithilfe von GLAD eine Verbindung zwischen OpenGL und dem GLFW Fenster herstellen.
``` C++
glfwMakeContextCurrent(window); //Verbindung mit dem Fenster
gladLoadGL(glfwGetProcAddress); //Laden der Fuktionszeiger
```

# Double Buffering
Dadurch, dass ein Programm immer Schrittweise ausgeführt wird, werden auch Objekte schrittweise in den Speicherbereich geschrieben auf den vom Bildschirm zugegriffen wird um ihn zu zeichnen. Dadurch entsteht ein Flackern, da Pixel die bereits auf den Bildschirm gezeichnet wurden ggf. nicht mehr zu den darauf folgenden Pixeln passen, wenn sie in der Zwischenzeit von dem Rechner anders berechnet und in den Speicher geschrieben wurden. Um dies zu verhindern verwendet man einen Double Buffer.
Hierbei wird nicht nur ein Speicherbereich für den Bildschirm bereitgestellt, auf den sowohl Bildschirm als auch Renderer gleichzeitig zugreifen, sondern zwei. Je einer ist immer in einem moment für den Renderer reserviert und der andere für das Darstellen auf dem Bildschirm. Erst wenn der Renderer fertig ist mit der Erstellung des Bildes wird der Befehl zum tauschen der beiden Speicherbereiche gegeben, und der Bildschirm kann auf das neue Bild zugreifen, während der Renderer das alte Bild im zweiten Speicherbereich überschreibt für das nächst folgende Bild.
![[double_buffer.png|250]]
In GLFW lässt sich der buffer tauschen mit:
``` C++
glfwSwapBuffers(window);
```
Dies sollte am Ende der Hauptschleife durchgeführt werden.

# Rendering Pipeline
# Licht ()
# Texturen
