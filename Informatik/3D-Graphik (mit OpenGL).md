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

# Erste Schritte mit OpenGL
Den Bildschirm mit einer Farbe leeren:
``` C++
//Farbe       R     G     B     A
glClearColor(0.5f, 0.2f, 0.3f, 1.0f); // Die clear color setzen
glClear(GL_COLOR_BUFFER_BIT);
```

Linien zeichnen:
``` C++
// Farbe   R     G     B
glColor3f(1.0f, 0.0f, 0.0f);
// Strichbreite
glLineWidth(5)

// Die Form zeichnen
glBegin(GL_LINES) // Starten
glVertex3f(0.0f, 0.0f, 0.0f); // erster Eckpnukt
glVertex3f(1.0f, 0.0f, 0.0f); // zweiter Eckpnukt
// (...) weitere Eckpunkte
glEnd(); //Beenden
```

# Rotation und Translation
Rotationen und Translationen werden in OpenGL über Matrizen dargestellt. 
Angewendet wird es durch:
``` C++
glMatrixMode(GL_MODELVIEW);
```

## Translation

``` C++
glTranslatef(0.2, 0, 0);
```
Hier wird um 0.2, 0, 0 verschoben.

## Rotation
Eine Rotation ist eine **lineare Transformation** und lässt sich daher als eine Matrixmultiplikation ausdrücken, welche die gedrehten Einheitsvektoren als Spalten enthält. Eine Rotation im 3-Dimensionalen kann um jede der 3 Achsen geschehen, dementsprechend gibt es 3 verschiedene Rotationsmatrizen mit denen multipliziert werden kann.
$$
\begin{align}
\vec{x_p}' &= \begin{pmatrix} 
	\cos(\alpha) & -\sin(\alpha) & 0 \\
	\sin(\alpha) & \cos(\alpha) & 0 \\
	0 & 0 & 1
\end{pmatrix} \cdot \vec{x_p}  \quad \text{Rotation um z-Achse} \\
\vec{x_p}' &= \begin{pmatrix} 
	\cos(\alpha) & 0 & -\sin(\alpha) \\
	0 & 1 & 0 \\
	-\sin(\alpha) & 0 &\cos(\alpha) \\
\end{pmatrix} \cdot \vec{x_p}  \quad \text{Rotation um y-Achse} \\
\vec{x_p}' &= \begin{pmatrix} 
	1 & 0 & 0 \\
	0 & \cos(\alpha) & -\sin(\alpha) \\
	0 & \sin(\alpha) & \cos(\alpha) 
\end{pmatrix} \cdot \vec{x_p} \quad \text{Rotation um x-Achse} \\
\end{align}
$$
In OpenGL muss das zum Glück nicht selbst implementiert werden, sondern kann mit folgendem Befehl umgesetzt werden:
``` C++
glRotatef(rotationAngle, 0, 0, -1);
```
Hierbei wird um den Vektor (0 0 -1) um den Winkel `rotationAngle` (im Bogenmaß) rotiert.
Es können auch Rotationen um mehrere Achsen durchgeführt werden. Hierbei wird jede Rotation einzeln nacheinander durchgeführt. Dabei ist die Reihenfolge jedoch wichtig zu beachten.
### Rotation als Rotationsmatrix
Es kann auch eine Rotationsmatrix erstellt werden, auf die die Rotationen draufmultipliziert wird.
``` C++
//Über die Linmath.h wird eine 4x4 Einheitsmatrix erzeugt
mat4x4 m;
mat4x4_identity(m); 
// Rotation um die y und x-Achse auf die Totationsmatrix m multiplizieren
//                    Winkel ist relativ zur Zeit
mat4x4_rotate_Y(m, m, 1 * ((float)glfwGetTime() / 10));
mat4x4_rotate_X(m, m, 3 * ((float)glfwGetTime() / 10));

// Die Matrix wird in das Shader-Programm übertragen
glUniformMatrix4fv(matrix_access, 1, GL_FALSE, (const GLfloat*)m);
```
Diese Rotationsmatrix lässt sich dann auch an einen Shader übergeben. Siehe dazu [[#Ein einfacher Shader]] und die [[#Rendering Pipeline]].
### Zu viele Rotationen
Wenn zu viele Rotationen durchgeführt werden, kann das dazu führen, dass wegen Berechnungsungenauigkeiten die Rotationsmatrix nicht mehr orthogonal ist. Zu erkennen ist das an der Determinante der Matrix, diese muss immer 1 sein.
Dies lässt sich einfach reparieren:
$$
\begin{align}
R_\omega &= \begin{pmatrix}
	r_{1 1} & r_{1 2} & r_{1 3} \\
	r_{2 1} & r_{2 2} & r_{2 3} \\
	r_{3 1} & r_{3 2} & r_{3 3} \\
\end{pmatrix} = \begin{pmatrix}
	\vec u & \vec v & \vec w
\end{pmatrix} \\
\vec u' &= {\vec u \over |\vec u|}, \quad
\vec v' = {\vec v \over |\vec v|}, \quad
\vec w' = {\vec w \over |\vec w|}
\end{align}
$$

## Rotation und Translation zurücksetzen
``` C++
glLoadIdentity();
```

## Homogene Transformationsmatrix
Die homogene Transformationsmatrix ist eine Kombination aus [[#Rotation]], [[#Translation]], Reflektion, Skalierung und dem perspektivischen Faktor für zentrale Projektion
![[homogene_transformationsmatrix.png|400]]



# Rendering Pipeline

# Ein einfacher Shader

# Licht ()
# Texturen
