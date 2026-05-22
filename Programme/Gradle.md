#Informatik 
# Testen in einer GitLab/GitHub Pipeline
``` yaml
image: gradle:alpine
build:
  stage: build
  script: gradle assemble  # Das Projekt compilieren
test_junit:
  stage: test
  script: gradle test  # die definierten Testfälle ausführen
test_sonarlint:
  stage: test
  script: gradle sonarlintMain  # Test des Codingstyles
```

