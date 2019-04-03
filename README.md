# This repo contains compiled Jar file. You can use it for generating swift 5 clients.
In your CI configuration (e.g. gitlab ci) add these:
```
stages:
  - build

before_script:
  - export LANG=UTF-8
  - env
  - locale

build_master:
  stage: build
  script:
    - echo $GIT_USERNAME
    - echo $PUSH_TOKEN
    - chmod +x ./scripts/swagger-codegen-cli.jar
    - java -jar ./scripts/swagger-codegen-cli.jar generate -i ./path/to/swagger.json -l swift5
    - (if [ -z "$(git status --porcelain)" ]; then echo "Nothing to commit"; else bundle exec fastlane release_api git_username:$GIT_USERNAME push_token:$PUSH_TOKEN; fi);
  only:
   - master
```
