Priority for configuration

| Priority | Mechanism             | Example                                          |     |
| -------- | --------------------- | ------------------------------------------------ | --- |
| 1        | CLI                   | -PmyProperty='Hi, world'                         |     |
| 2        | System properties     | org.gradle.project.myProperty='Hi, world'        |     |
| 3        | Gradle properties     | myProperty='Hi, world'                           |     |
| 4        | Environment variables | export ORG_GRADLE_PROJECT_myProperty='Hi, world' |     |

https://docs.gradle.org/8.10.1/userguide/build_environment.html