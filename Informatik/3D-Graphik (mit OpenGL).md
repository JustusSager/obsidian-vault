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
Den Bildschirm mit einer Farbe leeren. Farben werden dabei im [[2D-Grafik#RGB-Farbsystem|RGB-Farbsystem]] angegeben
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
Eine Rotation ist eine **lineare Transformation** und lässt sich daher als eine [[Vektoren, Matrizen#Matrizenmultiplikation|Matritzenmultiplikation]] zwischen einer Rotations[[Vektoren, Matrizen#Matrizen|matrix]] und einem [[Vektoren, Matrizen#Vektoren|Vektor]] ausdrücken, welche die gedrehten Einheitsvektoren als Spalten enthält. Eine Rotation im 3-Dimensionalen kann um jede der 3 Achsen geschehen, dementsprechend gibt es 3 verschiedene Rotationsmatrizen mit denen multipliziert werden kann.
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
Rotation um y-Achse:
![[rotation_um_y_achse.png|300]]
In OpenGL muss das zum Glück nicht selbst implementiert werden, sondern kann mit folgendem Befehl umgesetzt werden:
``` C++
glRotatef(rotationAngle, 0, 0, -1);
```
Hierbei wird um den Vektor (0 0 -1) um den Winkel `rotationAngle` (im Bogenmaß) rotiert.
Es können auch Rotationen um mehrere Achsen durchgeführt werden. Hierbei wird jede Rotation einzeln nacheinander durchgeführt. Dabei ist die Reihenfolge jedoch wichtig zu beachten.
### Rotation als Rotationsmatrix
Es kann auch eine Rotationsmatrix erstellt werden, auf die die Rotationen draufmultipliziert wird.
``` C++
#include <linmath.h>
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
### Rotationen umkehren
Eine Rotationsmatrix kann umgekehrt werden indem sie Transponiert wird.
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
Eine Kombination von Rotation und Translation sieht folgendermaßen aus:
$$\vec x_p' = R \cdot \vec x_p + \vec x_t$$
Hier wird um den Koordinatenursprung $(0, 0, 0)$ mit der Rotationsmatrix $R$ rotiert und um den Vektor $\vec x_t$ verschoben. Es kann um einen anderen Punkt rotiert mit folgender Formel:
$$\vec x_p' = R \cdot (\vec x_p - \vec x_{t1}) + \vec x_{t1} + \vec x_{t2}$$
Eine Rotation und Translation kann nicht durch eine Multiplikation von Matrizen realisiert werden.
Translation ist keine lineare Abbildung und daher von einer Graphikkarte schwieriger zu berechnen. Es wird also ein Trick benötigt Translation zu berechnen als wäre es eine lineare Abbildung.
Die **homogene Transformationsmatrix** ist eine Kombination aus [[#Rotation]], [[#Translation]], Reflektion, Skalierung und dem perspektivischen Faktor für [[#zentrale Projektion]]
![[homogene_transformationsmatrix.png|400]]
Hierfür muss jeder Punkt / Vektor um eine weiter Dimension erweitert werden, mit der neuen Komponente immer 1. (Im folgenden Beispielhaft in 2D)
$$\begin{pmatrix} x \\ y \end{pmatrix} \to \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$$

### Herleitung der kombinierten Rotation und Translation
Folgendes ist berechnet Beispielhaft für 2 Dimensionen, lässt sich jedoch analog für 3 Dimensionen durchführen.
Rotation lässt sich dadurch als folgende Matrixmultiplikation darstellen:
$$\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} = \begin{pmatrix} \cos(\alpha) & -\sin(\alpha) & 0 \\ \sin(\alpha) & \cos(\alpha) & 0 \\ 0 & 0 & 1 \end{pmatrix} \cdot \begin{pmatrix} x \\ y \\ 1\end{pmatrix}$$
Translation hierdurch:
$$\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} = \begin{pmatrix} 1 & 0 & x_t \\ 0 & 1 & y_t \\ 0 & 0 & 1 \end{pmatrix} \cdot \begin{pmatrix} x \\ y \\ 1\end{pmatrix} = \begin{pmatrix} x + x_t \\ y + y_t \\ 1\end{pmatrix}$$
Durch die Erweiterung um eine weitere Dimension lassen sich Rotation und Translation in eine gemeinsame Matrix zusammenfassen und berechnen als wäre es eine lineare Abbildung. 
$$\begin{pmatrix} 
	x' \\ y' \\ 1 
\end{pmatrix} = \begin{pmatrix} 
	\cos(\alpha) & -\sin(\alpha) & x_t \\ 
	\sin(\alpha) & \cos(\alpha) & y_t \\ 
	0 & 0 & 1 
\end{pmatrix} \cdot \begin{pmatrix} 
	x \\ y \\ 1 
\end{pmatrix}
$$
**Achtung:** hierbei ist die Rotation immer vor der Translation! Anders herum wäre die Formel deutlich komplizierter.
**Mehrere Transformationen** lassen sich ebenfalls einfach als Matritzenmultiplikation mehrerer Transformationsmatrizen berechnen.

### Zentrale Projektion
![[zentrale_projektion.png]]
Bei der **zentralen Projektion** werden Objekte die weiter weg von der Kamera sind, kleiner auf dem Bildschirm dargestellt. Im Vergleich zur **orthogonalen Projektion**, bei der die Entfernung des Objekts keinen Einfluss auf die Größe der Objekts auf dem Bildschirm hat. 
Der Abstand (die **Kamerakonstante**) zwischen dem virtuellen (Kamera)punkt und der Leinwand (dem Nullpunkt des Koordinatensystems) bestimmt, wie stark die Entfernung die Größe des Objekts verzerrt. Je größer die Entfernung, desto weniger ist der Einfluss der Entfernung. Bei einer "unendlichen" Kamerakonstanten wäre das Ergebnis die orthogonale Projektion. 
**Zentralprojektion:**
$$P_{cp} = \begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 0 \\
0 & 0 & -1/d & 1 \\
\end{pmatrix}$$
Orthogonale Projektion ($d \to \infty$)
$$P_{cp} = \begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 \\
\end{pmatrix}$$
# Rendering Pipeline
![[rendering_pipeline.png]]
In der Rendering Pipeline werden verschiedene Shader zur graphischen Verarbeitung verwendet. Zwischendrin werden noch andere Zwischenschritte durchgeführt, z.B. werden vor dem Fragment Shader automatisch die Vertexe in interpolierte Fragmente umgewandelt.

## Shader
Jeder Shader ist ein eigenes kleines Programm mit Input und Output. Diese werden in einer eigenen Sprache geschrieben, In OpenGL ist das `OpenGL Shading Language (GLSL oder glSlang)`. Ihre Syntax ist von C inspiriert. 
Shader können zur Laufzeit kompiliert werden.

## Vertex Shader
Der Vertex Shader wird für jeden Vertex einzeln durchgeführt. Dabei werden jedoch viele Vertexe parallel abgearbeitet. 
Ein ganz einfacher Vertex ist dabei definiert als die drei Eckpunkt-Koordinaten eines Dreiecks. Ein Vertex-Shader könnte daraufhin anhand einer Transformationsmatrix, den Vertex im Raum rotieren und verschieben. Die Farbe wird einfach durchgereicht.
``` GLSL
#version 410 // 
uniform mat4 transformationMatrix;
in vec3 position;
in vec3 color;
out vec3 colorFrag;
void main()
{
    gl_Position = transformationMatrix * vec4(position, 1.0);
    colorFrag = color;
};
```
`gl_Position` ist eine spezielle eingebaute Variable, welche im Vertex Shader als Ausgabe für die neue Position verwendet wird. Sie ist vom Datentyp `vec4`.
Die übergebene Farbe des Vertex `color` wird als `colorFrag` an den Fragment Shader durchgereicht.
Über der `main()` werden die Eingangs- (`in`) und Ausgangsvariablen (`out`) definiert. Außerdem gibt es auch `uniform`-Variablen. Diese sind über alle Instanzen des Shaders gleich. Also hier z.B. jeder durchlauf des Vertex Shaders für einen Vertex arbeitet mit den selben Werten in `transformationMatrix`, kann aber eine andere `position` und `color` haben.

## Fragment Shader
Ein einfacher Fragment Shader (aufbauend auf dem in [[#Vertex Shader]] definierten Shader) kann folgendermaßen aussehen:
``` GLSL
#version 410
in vec3 colorFrag;
void main()  
{  
    gl_FragColor = vec4(colorFrag, 1.0);  
};
```
Hier bekommt der Fragment Shader vom Vertex Shader eine Farbe übergeben und gibt diese als finalen Farbwert zurück. `gl_FragColor` ist dabei eine eingebaute Variable vom Typ `vec4`, welche am Ende der `main()` den Farbwert des Fragments beinhalten muss (im [[2D-Grafik#RGB-Farbsystem|RGBA-Farbsystem]]). 

**Hinweis:**
`gl_FragColor` ist inzwischen eigentlich veraltet. Stattdessen sollte `layout(location = 0) out vec4 outColor` als Ausgabe-Variable definiert werden. Siehe dazu: https://stackoverflow.com/questions/51459596/using-gl-fragcolor-vs-out-vec4-color und https://wikis.khronos.org/opengl/Fragment_Shader#Outputs. 

# Ein einfacher Shader
Hierfür werden die in [[#Vertex Shader]] und [[#Fragment Shader]] beschriebenen Shader verwendet.

## Kompilieren
Die Shader werden mit folgendem Code zur Laufzeit kompiliert. 
``` C++
// Erzeugen des Vertex-Shaders --------------------------
// Shader aus Datei laden (Andere Bib zum Lesen der Datei LadeShader.h)
char* vertex_shader_code = readTextFileIntoString(
	"Shaders/VertexShaderStart.glsl"
);
// Sicherstellen, dass die Datei erfolgreich geladen wurde!
if (vertex_shader_code == 0) exit(EXIT_FAILURE);
// Shader kompilieren
vertex_shader = glCreateShader(GL_VERTEX_SHADER);
glShaderSource(vertex_shader, 1, &vertex_shader_code, NULL);
glCompileShader(vertex_shader);

// Erzeugen des Fragment-Shaders --------------------------
char* fragment_shader_code = readTextFileIntoString(
	"Shaders/FragmentShaderStart.glsl"
);
if (fragment_shader_code == 0) exit(EXIT_FAILURE);
fragment_shader = glCreateShader(GL_FRAGMENT_SHADER);
glShaderSource(fragment_shader, 1, &fragment_shader_code, NULL);
glCompileShader(fragment_shader);
```

Um Informationen über den Shader zu bekommen kann folgender Code genutzt werden: 
``` C++
char info[500];
int num;
glGetShaderInfoLog(vertex_shader, 500, &num, info);
printf("%s", info);
```
Hier werden Infos zum `vertex_shader` ausgegeben, geht aber auch mit dem `fragment_shader`.

Die beiden Shader (Vertex- und Fragment-Shader) miteinander zu einem vollständigen Shader verbinden:
``` C++
//Linken des Shader-Progamms
complete_shader_program = glCreateProgram();
glAttachShader(complete_shader_program, vertex_shader);
glAttachShader(complete_shader_program, fragment_shader);
glLinkProgram(complete_shader_program);
```

## Vertexe an den Shader übergeben und Ausführen


## uniform-Variablen im Shader
Um Variablen für einen Shader (als `uniform`) erreichbar zu machen, kann folgendes ausgeführt werden. 

Außerhalb der Fensterschleife:
``` C++
// für die Variablen:
float float_var;
vec3 vec3_var;
mat4x4 matrix_var;

// Einen eindeutigen identifier definieren für den Speicherbereich.
GLint float_access = glGetUniformLocation(
	complete_shader_program, "float_in_shader"
);
GLint vec3_access = glGetUniformLocation(
	complete_shader_program, "vec3_in_shader"
);
GLint matrix_access = glGetUniformLocation(
	complete_shader_program, "matrix_in_shader"
);
```
- `matrix_in_shader` ist dabei der Variablenname im Shader. 
- Vorgehensweise ist für jeden Variablentyp gleich, da hier nur der Identifier definiert wird.

Innerhalb der Fensterschleife:
``` C++
// Eine einzelne float übertragen
glUniform1f(float_access, float_var);

// Einen 3D-Vector mit floats übertragen
glUniform3f(vec3_access, vec3_var[0], vec3_var[1], vec3_var[2]);

// Die Matrix m wird in das Shader-Programm übertragen
glUniformMatrix4fv(matrix_access, 1, GL_FALSE, (const GLfloat*) matrix_var);
```
Hier muss je nach Variablentyp die richtige OpenGL-Methode verwendet werden, um die Daten zu übertragen.

# Licht ()
# Texturen
