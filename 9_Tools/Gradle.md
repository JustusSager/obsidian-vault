
# Testen in einer GitLab/GitHub Pipeline
``` yaml
image: gradle:alpine
build:
  stage: build
  script: gradle assemble
test_junit:
  stage: test
  script: gradle test
test_sonarlint:
  stage: test
  script: gradle sonarlintMain
```

