## Instalações

- [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/)
- [WSL](https://learn.microsoft.com/pt-br/windows/wsl/install)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Maven](https://maven.apache.org/install.html)
- [Java](https://www.oracle.com/java/technologies/downloads/)
- [Micrometer](https://micrometer.io/)
- [Actuator](https://docs.spring.io/spring-boot/reference/actuator/enabling.html)
- IDE ([IntelliJ](https://www.jetbrains.com/pt-br/idea/#), [Eclipse](https://eclipseide.org/), etc.)

## Documentação
- [Prometheus](https://prometheus.io/docs/introduction/overview/)
  - [Tipos de Métricas](https://prometheus.io/docs/specs/om/open_metrics_spec/#metric-types)

## Comandos

- `wsl --install` para instalar o WSL (Windows Subsystem for Linux)
- `java -version` para verificar a versão do Java instalada
- `mvn -v` para verificar a versão do Maven instalada
- `docker --version` para verificar a versão do Docker instalada
- `docker-compose --version` para verificar a versão do Docker Compose instalada
- `docker-compose up` para iniciar os containers do Docker (executar no diretório em que se encontra o arquivo `docker-compose.yml`)
  - `docker-compose up -d` para iniciar os containers do Docker em modoDetached (modo não bloqueante)
- `docker-compose down` para parar os containers do Docker
- `mvn clean package` para realizar o build (compilar e empacotar) o projeto

## Iniciando a aplicação
- Add VM Options: -Dspring.profiles.active=prod
- Add Enviroment Variables: application-prod.properties

## Definições
- `scrape_interval` é o intervalo de tempo entre cada consulta do Prometheus ao item monitorado
- `logback_events_total{application="app-forum-api", instance="app-forum-api:8080", job="app-forum-api", level="info"}`
  - `logback_events_total` métrica
  -  `application="app-forum-api", instance="app-forum-api:8080", job="app-forum-api", level="info"` labels
- `Instant vector` vetor instantâneo em que cada linha é um série temporal com suas respectivas labels e valores
  - Ex.: Ao buscar por `logback_events_total` (métrica), temos o seguinte _sample_:
      ```json
      logback_events_total(application="app-forum-api", instance="app-forum-api:8080", job job=*app-forum-api um-api", level="debug")                                                                         0
      logback_events_total(application="app-forum-api", instance="app-forum-api:8080", job="a job="app-forum-api n-api", level="error")                                                                    44
      logback_events_total(application="app-forum-api", instance="app-forum-api:8080", job="app-forum-api", level="info")                                                                                       43
      logback_events_total(application app-forum-api", instance"app-forum-api:8080", job="app-forum-api", level="trace")                                                                                      0
      logback_events_total (application="app-forum-api", instance="app-forum-api:8080", job="app-forum-api", level="warn"]                                                                                  42
      ```
- `Range vector` vetor de uma série temporal
  - Ex.: Ao buscar por `logback_events_total[1m]` (métrica no intervalo de 1 minuto), temos o seguinte _sample_:
      ```json
      logback_events_total(application="app-forum-api", instance="app-forum-api:8080", job job=*app-forum-api um-api", level="debug")

      0@1642387142.25
      0@1642387147.25
      0@1642387152.254
      0@1642387157.25
      0@1642387162.25
      ```
  - Também é utilizar subqueries, por exemplo, `logback_events_total[5m:1m]` (métrica no intervalo de 5 minutos coletando dados a cada 1 minuto)
- `Float` vetor do tipo escalar, ou seja, um ponto flutuante
  - Ex.: `hikaricp_connections_idle{application="app-forum-api", pool-"HikariPool-1",}`
- `String` vetor não utilizado, como citado na na documentação do Prometheus.