Siehe hierzu auch [[Agenten]].
# Sense-Plan-Act
![[sense-plan-act-architektur.png]]
Anhand alles Sensordaten wird ein Plan erstellt, wie zu handeln ist.
# reaktive Architektur
![[reaktive_architektur.png]]
Es wird kein Plan anhand aller Sensordaten erstellt. Stattdessen wird, falls ein Sensor ein bestimmtes Event triggert, dieses als Verhalten ausgeführt. Diese Kopplung wird `Behavior` genannt. Die verschiedenen Verhalten werden kombiniert ausgeführt.
Für die Kombination der verschiedenen Verhaltensmuster wird ein verfahren wie einer Priorisierung benötigt um Konflikte zu vermeiden. 
# Hybride Architektur
Eine Kombination von [[#Sense-Plan-Act]] und [[#reaktive Architektur|reaktiver Architektur]]. Dabei kann z.B. die reaktive Architektur für die unmittelbare Kollisionsvermeidung genutzt werden, um eine möglichst direkte Schadensvermeidung zu haben. Die Sense-Plan-Act-Architektur kann verwendet werden um komplexere Planung umzusetzen.
# Multi-Level-Architektur
ist auch eine Kombination von anderen Architekturen, bei der die einzelnen Architekturen in Schichten aufgebaut werden.