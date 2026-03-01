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
In der Rendering Pipeline werden verschiedene Shader zur graphischen Verarbeitung verwendet. 
![[rendering_pipeline_shape_assemply_rasterization.png]]
Zwischendrin werden jedoch auch noch andere Zwischenschritte durchgeführt. Kurz zusammengefasst passiert folgendes in der Rendering Pipeline:
**Vertex Shader**
Hier werden die rohen Vertices verarbeitet und z.B. im Raum transformiert ([[#Rotation]] und [[#Translation]]) und Berechnungen durchgeführt, welche zur späteren Verarbeitung im Fragment Shader nötig sind. 
Mehr dazu in [[#Vertex Shader]].
**Shape Assembly**
Die jetzt transformierten Vertices (die zu diesem Zeitpunkt einfache Punkte im 3D-Raum sind) werden zu Dreiecken (müssen nicht Dreiecke sein) zusammengesetzt. 
**Rasterization**
Diese Dreiecke werden daraufhin in potenzielle Pixel (Fragmente) übersetzt und die Werte in dem Dreieck zwischen den Eckpunkten (den Vertices) interpoliert.
**Fragment Shader**
Hier werden die finalen Farbwerte der Fragmente berechnet. Es werden also z.B.  Lichteffekte mit auf die ursprünglichen Farben der Vertices eingerechnet. 
Mehr dazu in [[#Fragment Shader]].
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

## Vertexe an den Shader übergeben
Die Vertexe können auf beliebige Weise im Programm organisiert werden, müssen dem Shader jedoch "erklärt" werden, es kann z.B. ein `struct` für die Vertexe angelegt werden.
``` C++
struct myVertexType {
	float x, y, z;
	float r, g, b;
}
myVertexType vertices = ...
```

OpenGL die `vertices` übergeben
``` C++
GLuint vertex_buffer;
glGenBuffers(1, &vertex_buffer);
glBindBuffer(GL_ARRAY_BUFFER, vertex_buffer);
glBufferData(
	GL_ARRAY_BUFFER, 
	numOfVertices * sizeof(myVertexType), // Größe des vertices-Arrays
	vertices, // Pointer oder Variable zum Array
	GL_STATIC_DRAW
);
```
**Hinweis:** Je nachdem ob `vertices` auf dem Heap oder Stack allokiert wurde, gibt `sizeof()` unterschiedliche Werte zurück. Siehe dazu [[Speicherverwaltung#sizeof()]]. Je nachdem muss ob `vertices` auf dem Stack oder Heap liegt muss `numOfVertices * sizeof(myVertexType)` ausgetauscht werden, sodass es die Größe des `vertices`-Arrays in Bytes ergibt.

Dem Shader die `vertices` erklären:
``` C++
// Identifier für den Shader generieren
GLint position_access = glGetAttribLocation(complete_shader_program, "position");
GLint color_access = glGetAttribLocation(complete_shader_program, "color");

// 
glEnableVertexAttribArray(position_access);
glVertexAttribPointer(
	position_access, 3, GL_FLOAT, GL_FALSE,
	sizeof(myVertexType), // stride, also Größe des Datentyps
	(void*)0 // offset des position-Speicherbereichs in myVertexType
);

glEnableVertexAttribArray(color_access);
glVertexAttribPointer(
	color_access, 3, GL_FLOAT, GL_FALSE,
	sizeof(myVertexType), // stride, also Größe des Datentyps
	(void*)(sizeof(float) * 3) // offset des color-Speicherbereichs in myVertexType
);
```

## Vertexe zeichnen
Innerhalb der Fensterschleife:
``` C++
// Ab hier diesen Shader nutzen
//   muss nicht zwingend in der Hauptschleife geschehen
glUseProgram(complete_shader_program); 

// Die Vertices zeichnen
glDrawArrays(
	GL_TRIANGLES, 
	0,             // offset im buffer
	numOfVertices  // Anzahl der Vertexe
);
```

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
glUniformMatrix4fv(
	matrix_access, 
	1,                          // wie viele Elemente?
	GL_FALSE,                   // transponieren?
	(const GLfloat*) matrix_var // wo sind sie zu finden?
);
```
Hier muss je nach Variablentyp die richtige OpenGL-Methode verwendet werden, um die Daten zu übertragen.
`glUniformMatrix4fv` kann dabei sehr gut für eine [[#Rotation als Rotationsmatrix|Rotationsmatrix]] verwendet werden.

# Licht (Phong-Model)
Die Lichtverarbeitung und Berechnung findet fast ausschließlich im [[#Fragment Shader]] statt, jedoch werden hierfür ein paar Dinge benötigt, die vorher definiert / berechnet werden müssen.
Im folgenden wird das Phong-Modell umgesetzt. Dabei lässt sich das Licht in 3 verschiedene Bereiche aufteilen:
- Ambient
- Diffus
- Specular
![[phong_lichtmodell.png]]
Das Phong-Modell hat folgende Einschränkungen:
- Keine Energieerhaltung (?)
- Alle Lichtquellen sind Punktquellen
- Diffuses und spiegelndes Licht werden nur lokal berechnet (keine Schatten)
- Umgebungslicht (Ambientes Licht) wird nur global berechnet
## Ambient
Dies ist das einfachste der 3 Bereiche. Hier wird einfach angenommen, dass jedes Fragment grundsätzlich eine bestimmte fest definierte Menge an Licht bekommt.
Die Umsetzung ist einfach:
$$\begin{align}
R_{neu} &= \text{ambientFaktor} \cdot R_{alt} \\
G_{neu} &= \text{ambientFaktor} \cdot G_{alt} \\
B_{neu} &= \text{ambientFaktor} \cdot B_{alt}
\end{align}$$
Der `ambientFaktor` ist dabei ein Wert zwischen 0 und 1 und wird einfach auf die urspüngliche Farbe drauf multipliziert.

Im Fragment Shader sieht das folgendermaßen aus:
``` GLSL
#version 410
uniform float ambientFactor;
in vec3 colorFrag;
void main()  
{  
    gl_FragColor = vec4(ambientFactor*colorFrag, 1.0);
};
```
## Diffus
Beim Diffusen Licht soll berücksichtigt werden, dass Licht von einer bestimmten Lichtquelle kommt. Je nachdem in welchem Winkel das Licht auf die Oberfläche trifft, wirkt die Oberfläche heller oder dunkler. Das Licht wird gleichmäßig in alle Richtungen verteilt.
Berechnen lässt sich die folgendermaßen:
$$ \begin{align}
\vec l &= \text{Vektor von der Lichtquelle zum Oberflächenpunkt / Fragment} \\
\vec n &= \text{Normalenvektor des Fragments} \\
k_{diff} &= \vec l \cdot \vec n = |\vec l| \cdot |\vec n| \cdot \cos(\alpha) = \cos(\alpha)
\end{align}$$
D.h. der Diffusionsfaktor lässt sich anhand des [[Vektoren, Matrizen#Skalarprodukt|Skalarprodukts]] berechnen. Zusätzlich kann noch ein Faktor genutzt werden, um die Stärke dieses Effekts zu bestimmen.
Wir benötigen also den Normalenvektor der Oberfläche und einen Vektor von der Lichtquelle zum Oberflächenpunkt.

Der Normalenvektor kann im Shader nicht gut berechnet werden, daher ist es sinnvoller diesen in das Objekt mit den Vertices mit aufzunehmen und bei der Erstellung der Vertices mit zu berechnen / zu definieren.
``` C++
struct myVertexType {
	float x, y, z;
	float nx, ny, nz;
	float r, g, b;
}
```
Diese müssen dem Shader jedoch auch noch bekannt gemacht werden. Siehe dazu [[#Vertexe an den Shader übergeben]].
Falls es möglich ist den Normalenvektor anhand einer übergeordneten Struktur besser abzuleiten (Eine Kugel, statt einer Kugel aus einzelnen Flächen), kann dies die Lichtberechnung deutlich verbessern.
![[phong_normalenvektoren_verbessern.png]]
Der Vertex Shader kann nun die Normalenvektoren mit transformieren.
``` GLSL
#version 410
uniform mat4 transformationMatrix;

in vec3 position;
in vec3 normalVector;
in vec3 color;

out vec3 positionFrag;
out vec3 normalVectorFrag;
out vec3 colorFrag;

void main()
{
    gl_Position = matrix * vec4(position, 1.0);
    positionFrag = gl_Position.xyz;
    normalVectorFrag = (transformationMatrix * vec4(normalVector, 1.0)).xyz;
    colorFrag = color;
};
```
Im Fragment Shader kann jetzt das diffuse Licht berechnet werden.
``` GLSL
#version 410
uniform float ambientFactor;
uniform float diffuseFactor;
in vec3 positionFrag;
in vec3 normalVectorFrag;
in vec3 colorFrag;

vec3 lightPos = (0, 0, 1);

void main()  
{  
    float ambient = ambientFactor;
    
    vec3 lightDir = normalize(lightPos - positionFrag);
	float diffuse = max(
		dot(normalVectorFrag, lightDir), 0.0
	) * diffuseFactor;
	
    gl_FragColor = vec4((ambient + diffuse) * colorFrag, 1.0);
};
```
Hier wird eine feste Lichtquelle im Fragment-Shader definiert, diese kann jedoch auch als `uniform` übergeben werden.
## Specular
Bei der spiegelnden Reflektion wird zusätzlich die Position des Betrachters berücksichtigt. Es wird ein Spiegelungseffekt zur Oberfläche hinzugefügt, der wenn der Betrachter genau im optimalen Reflektionsvektor steht, einen "Glanzeffekt" auf die Oberfläche legt.
![[phong_specular.png]]
$$\begin{align}
\vec r &= \text{Vektor für die ideale Reflexion (blau)} \\
\vec v &= \text{Vektor vom Fragment zum Beobachter (rot)} \\
n &= \text{der Strafexponent für die Winkelabweichung} \\
k_{spec} &= (\vec r \cdot \vec v)^n = (|\vec r|\cdot |\vec v| \cdot \cos(\beta))^n = (\cos(\beta))^n
\end{align}$$
Im Fragment Shader kann dies folgendermaßen berechnet werden:
``` GLSL
#version 410
uniform float ambientFactor;
uniform float diffuseFactor;
uniform float specularFactor;
uniform float shininess;
in vec3 positionFrag;
in vec3 normalVectorFrag;
in vec3 colorFrag;

vec3 cameraPos = (0, 0, 1);
vec3 lightPos = (0, 0, 1);

void main()  
{  
    float ambient = ambientFactor;
    
    vec3 lightDir = normalize(lightPos - positionFrag);
	float diffuse = max(
		dot(normalVectorFrag, lightDir), 0.0
	) * diffuseFactor;
	
	vec3 viewDir = normalize(cameraPos - positionFrag);
	vec3 reflectDir = reflect(-lightDir, normalVectorFrag);
	float specular = pow(
		max(dot(viewDir, reflectDir), 0.0), 
		shininess
	) * specularFactor;
	
    gl_FragColor = vec4((ambient + diffuse + specular) * colorFrag, 1.0);
};
```
# Texturen
Texturen sollen es ermöglichen Bitmaps (Bilder) auf ein Objekt zu projizieren um damit innerhalb einer durch Vertices generierten Fläche unterschiedliche Farben darzustellen, welche nicht nur durch den Rasterizer interpoliert werden. 
Statt einer Farbe enthält ein Vertex eine zusätzliche 2D-Koordinate, der **uv-Koordinate**, welche die Position auf einem Bild entspricht. Diese kann durch den Rasterizer interpoliert werden, um die Zwischenpositionen zu generieren.
![[uv_koordinaten.png]]
Anhand der uv-Koordinate kann im Fragment Shader die Farbe aus dem Bild genommen werden.
## Vertices vorbereiten
Die uv-Koordinate ersetzt die `color` in unserem `MyVertexType`:
``` C++
struct myVertexType {
	float x, y, z;
	float nx, ny, nz;
	float u, v;
}
```
Die `vertices` benötigen jetzt zusätzlich die Information, wo auf dem Bild ihre entsprechende Farbe zu finden ist. Es reicht dabei die "Eckpunkte" anzugeben, da der Rasterizer die Koordinaten dazwischen interpoliert. Diese müssen entsprechend übergeben werden ([[#Vertexe an den Shader übergeben]])

## Bitmap laden
Siehe dazu auch [[2D-Grafik#Bilder im Speicher]]. Hier wird eine anderes Skript genutzt um eine Bitmap-Datei als ein Bytearray in den Speicher zu laden.
``` C++
// Das Bild in den RAM laden
int bmpWidth;
int bmpHeight;
unsigned char* image = loadBMP24("Textures/Bear.bmp", &bmpWidth, &bmpHeight);
```

Danach muss das Bytearray an den VRAM von OpenGL übergeben werden:
``` C++
// Das Bild als texture vom RAM in den VRAM übergeben
GLuint textureCube;
glGenTextures(1, &textureCube);
glActiveTexture(GL_TEXTURE0);
glBindTexture(GL_TEXTURE_2D, textureCube);
glTexImage2D(GL_TEXTURE_2D, 0, GL_RGB, bmpWidth, bmpHeight, 0, GL_BGR, GL_UNSIGNED_BYTE, image);
delete[] image; // Den Speicher auf dem RAM wieder freigeben
// glGenerateMipmap(GL_TEXTURE_2D);
```
ggfs. Kann hier auch noch gesagt werden, dass [[#MipMaps]] generiert werden sollen

Jetzt muss noch ein Zugriff für den Fragment Shader auf die im VRAM abgelegte Texture geschaffen werden. Dies geht über einen `uniform` Parameter.
``` C++
GLuint TextureID = glGetUniformLocation(complete_shader_program, "textureCubeSampler");
```
#TODO Wieso findet der Shader die Textur obwohl es keine Verknüpfung zwischen `TextureID` und `textureCube` gibt?

## Im Shader verarbeiten
Der Vertex Shader reicht die uv-Koordinaten unverändert weiter:
``` GLSL
#version 410
uniform mat4 transformationMatrix;
in vec3 position;
in vec2 uv;
out vec2 uvFrag;

void main()
{
    gl_Position = transformationMatrix * vec4(position, 1.0);
    uvFrag = uv;
};
```

Im Fragment Shader wird nun die Farbe anhand eines textureSamplers aus der Textur an der Position der uv-Koordinate abgefragt.
``` GLSL
#version 410
uniform sampler2D myTextureSampler;
in vec2 uvFrag;

void main()  
{  
	vec3 color = texture(myTextureSampler, uvFrag);
    gl_FragColor = vec4(color, 1.0);
};
```

## MipMaps
```
glGenerateMipmap(GL_TEXTURE_2D);
```