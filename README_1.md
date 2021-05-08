# study-kuba

```shell
Project
├── README.md
├── configuration
│   ├── deployment.yaml <
│   └── service.yaml <
└── spring
    ├── Dockerfile <
    ├── HELP.md
    ├── build.gradle
    ├── gradle
    │   └── wrapper
    │       ├── gradle-wrapper.jar
    │       └── gradle-wrapper.properties
    ├── gradlew
    ├── gradlew.bat
    ├── settings.gradle
    ├── spring.iml
    └── src
        ├── main
        │   ├── java
        │   │   └── com
        │   │       └── example
        │   │           └── spring
        │   │               ├── Application.java
        │   │               └── api
        │   │                   └── HealthApi.java
        │   └── resources
        │       ├── application.properties
        │       ├── static
        │       └── templates
        └── test
            └── java
                └── com
                    └── example
                        └── spring
                            └── ApplicationTests.java
```
### 0. checkout branch
각자의 branch를 만들고 해당 branch를 사용, 혹은 각자의 local에서 작성

### 1. Dockerfile 작성
spring boot application을 image로 만들고 GCP Container Registry에 push
- asia.gcr.io/kuba-310814/{각자의 namespace}-app
- tag: 0.1의 형식으로 사용

### 2. deployment.yaml & service.yaml 작성
Container Registry에 push된 image를 사용하는 pod를 관리할 deployment를 배포하고, 해당 pod들을 바라볼 service도 배포
- 배포될 pod의 갯수는 2개
- 각자의 namespace로 배포

### 3. /health endpoint 확인
kubectl의 port forward 커맨드를 사용해 배포된 애플리케이션이 정상적으로 동작하는지 확인