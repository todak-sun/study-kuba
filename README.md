# study-kuba

Spring Application

```shell
Project
├── README.md
├── README_1.md
├── configuration
│   ├── deployment.yaml
│   └── service.yaml
├── logs
│   └── spring.log
└── spring
    ├── Dockerfile
    ├── HELP.md
    ├── build
    │   ├── bootJarMainClassName
    │   ├── classes
    │   │   └── java
    │   │       └── main
    │   │           └── com
    │   │               └── example
    │   │                   └── spring
    │   │                       ├── Application.class
    │   │                       ├── api
    │   │                       │   └── HealthApi.class
    │   │                       ├── core
    │   │                       │   └── service
    │   │                       │       └── HealthService.class
    │   │                       └── infrastructure
    │   │                           └── service
    │   │                               └── DefaultHealthService.class
    │   ├── generated
    │   │   └── sources
    │   │       ├── annotationProcessor
    │   │       │   └── java
    │   │       │       └── main
    │   │       └── headers
    │   │           └── java
    │   │               └── main
    │   ├── libs
    │   │   ├── logs
    │   │   │   └── spring.log
    │   │   └── spring-0.0.1-SNAPSHOT.jar
    │   ├── resources
    │   │   └── main
    │   │       ├── application.yml
    │   │       ├── static
    │   │       └── templates
    │   └── tmp
    │       ├── bootJar
    │       │   └── MANIFEST.MF
    │       └── compileJava
    │           └── source-classes-mapping.txt
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
        │       ├── application.yml
        │       ├── static
        │       └── templates
        └── test
            └── java
                └── com
                    └── example
                        └── spring
                            └── ApplicationTests.java
```

Spring Application 코드의 변경사항

- `application.yml`: logback 설정
- `HealthApi.java`: `/health`  endpoint 제공

### 0. checkout branch

각자의 branch를 만들고 해당 branch를 사용, 혹은 각자의 local에서 작성

### 1. Dockerfile 작성 (그대로 사용)

spring boot application을 image로 만들고 GCP Container Registry에 push

- asia.gcr.io/kuba-310814/{각자의 namespace}-app
- tag: 0.1의 형식으로 사용

### 2. deployment.yaml & service.yaml 작성 (service.yaml은 그대로 사용, deployment.yaml만 수정)

Container Registry에 push된 image를 사용하는 pod를 관리할 deployment를 배포하고, 해당 pod들을 바라볼 service도 배포

- 배포될 pod의 갯수는 2개
- 각자의 namespace로 배포
- Liveness probe 추가: `/health` endpoint를 사용하도록 설정
- Readiness Probe 추가: logback에 의해 생성될 `logs/spring.log` 유무를 체크하도록 설정

### 3. Readiness/Liveness Probe 확인

Pod event(describe command로도 가능)를 확인해 Readiness/Liveness Probe가 모두 Pass되었는지 확인

### 4. Readiness probe failed 확인

Readiness Probe로 잡아둔 `logs/spring.log`를 삭제해본다. 어떤 일이 발생되는지 확인

### 5. Liveness Probe 확인

Liveness의 endpoint가 400 Error 응답을 받도록 수 있도록 설정해본다. 어떤 일이 발생되는지 확인