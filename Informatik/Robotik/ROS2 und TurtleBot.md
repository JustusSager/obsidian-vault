# Parameter einstellen
``` bash
export TURTLEBOT3_MODEL=burger
```

# TurtleBot starten
Per SSH auf dem TurtleBot einloggen und folgendes ausführen:
`TurtleBot`
``` bash
ros2 launch turtlebot3_bringup robot.launch.py
```
# Topic Monitor
`Remote Machine`
``` bash
rqt
```
Hiermit lassen sich die verschiedenen Topics des TurtleBots einsehen
# Mit Tastatur fernsteuern
`Remote Machine`
``` bash
ros2 run turtlebot3_teleop teleop_keyboard
```

# ROS2 CheatSheet
``` bash
# Inspektionssoftware starten
rqt

# launch executable
ros2 run <package> <executable> []
	--ros-args --remap <default path>:=<remap to> # remapping a path
```
## Nodes
Softwarestückchen die entweder auf dem Roboter oder auf dem Rechner laufen.
``` bash
# Alle Nodes anzeigen
ros2 node list

# Infos zu einer bestimmten node
ros2 node info <node_name>
```
### Parameters
Nodes haben von außen veränderbare Parameter
``` bash
# Alle Parameter aller Nodes anzeigen
ros2 param list
```
## Topics
**Nodes** posten und abonnieren bestimmte **Topics**.
- haben einen bestimmten Typ in dem kommuniziert wird.
- werden über ihren Pfad identifiziert.
``` bash
# Alle Topics anzeigen
ros2 topic list []
	-t # topic type mit anzeigen
	
# Infos zu einem Topic anzeigen
ros2 topic info <topic_name> []
	--verbose # zusätzliche infos
	
# Posts eines topics ansehen
ros2 topic echo <topic_name>

# In ein topic posten
ros2 topic pub [] <topic_name> <msg_type> '<args>'
	--once # nur einmal posten
	-w <number> # wait for <number> matching subscriptions 

# postfrequenz eines topics anzeigen
ros2 topic hz <topic_name>

# Bandbreite eines topics anzeigen
ros2 topic bw <topic_name>

# topic mit bestimmtem Typ finden
ros2 topic find <topic_type>

# den verwendeten msg_type eines topics genauer betrachten
ros2 interface show <msg_type>
```
## Services 
Ähnlich zu **Topics** nur mit Request / Respond System
``` bash
# Alle Services anzeigen
ros2 service list
```
## Actions
``` bash
# Alle Actions anzeigen
ros2 action list
```
## Simulationsumgebung
https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/
### Die Standard mit installierte Simulationsumgebung
- unterstützt allerdings keine Sensoren
``` bash
# Simulationsumgebung starten
ros2 run turtlesim turtlesim_node 

# Tastatursteuerung
ros2 run turtlesim turtle_teleop_key
```
### gazebo
- unterstützt auch Sensoren.
- muss jedoch erst installiert werden.
- können mit dem normalen teleop genutzt werden.
Es gibt 3 verschiedene Welten die von Haus aus dabei sind. Starten lassen sie sich mit:
``` bash
ros2 launch turtlebot3_gazebo empty_world.launch.py

ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py

ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py
```
## Packages kompilieren und einrichten
``` bash
colcon build --symlink-install

source ~/turtlebot3_ws/install/setup.bash
```
**Ein Package löschen:**
1. den entsprechende package Ordner aus dem `(workspace)/src/` löschen
2. die Ordner `(workspace)/build/`, `(workspace)/install/` und `(workspace)/log/`
3. `colcon build --symlink-install` ausführen
