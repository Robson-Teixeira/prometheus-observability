## Instalações

- [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/)
- [WSL](https://learn.microsoft.com/pt-br/windows/wsl/install)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Maven](https://maven.apache.org/install.html)
- [Java](https://www.oracle.com/java/technologies/downloads/)
- [Micrometer](https://micrometer.io/)
- [Actuator](https://docs.spring.io/spring-boot/reference/actuator/enabling.html)
- IDE ([IntelliJ](https://www.jetbrains.com/pt-br/idea/#), [Eclipse](https://eclipseide.org/), etc.)

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