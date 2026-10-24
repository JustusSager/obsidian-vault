# In der GitLab PipeLine mit Gradle
- Bei einem Gradle Projekt mit dem Image gradle:alpine
- Mit "gradle build" werden auch checks durchgeführt
	- Soll das nicht passieren "assemble" benutzen
- Mit "gradle sonarlint" werden die statischen Tests durchgeführt
- Mit "gradle spotlessCheck" wird der Codestyle überprüft

``` docker
image: gradle:alpine

stages:
	- build
	- test

build-jobs:
	- 
```
