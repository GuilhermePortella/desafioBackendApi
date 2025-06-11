# Uber Movie Locations

Projeto Spring Boot para consulta de locações de filmes em San Francisco, utilizando dados públicos da prefeitura.

## Sumário

- [Descrição](#descrição)
- [Dependências](#dependências)
- [Como rodar o projeto](#como-rodar-o-projeto)
- [Endpoints disponíveis](#endpoints-disponíveis)
- [Pontos importantes](#pontos-importantes)

---

## Descrição

Esta aplicação expõe uma API REST para buscar locações de filmes em San Francisco, permitindo:
- Listar todos os filmes
- Filtrar filmes por título
- Autocompletar títulos de filmes

Os dados são obtidos dinamicamente do dataset público: [San Francisco Film Locations](https://data.sfgov.org/resource/yitu-d5am.json).

---

## Dependências

As principais dependências estão listadas no [pom.xml](pom.xml):

- **Spring Boot Starter Web**: Para criação da API REST.
- **Spring Boot Starter WebFlux**: Para chamadas reativas HTTP (WebClient).
- **Spring Boot Starter JSON**: Suporte a JSON.
- **Lombok**: Redução de boilerplate em classes Java.
- **Spring Boot DevTools**: Hot reload (opcional).
- **Spring Boot Starter Test**: Testes automatizados.
- **Reactor Test**: Testes reativos.

---

## Como rodar o projeto

1. **Pré-requisitos**:
   - Java 17+
   - Maven 3.9+

2. **Clonar o repositório**:
   ```sh
   git clone <url-do-repositorio>
   cd uber
   ```

3. **Build do projeto**:
   ```sh
   ./mvnw clean package
   ```

4. **Executar a aplicação**:
   ```sh
   ./mvnw spring-boot:run
   ```
   Ou rode o JAR gerado:
   ```sh
   java -jar target/uber-0.0.1-SNAPSHOT.jar
   ```

5. **Acessar os endpoints**:
   - A aplicação estará disponível em: `http://localhost:8080`

---

## Endpoints disponíveis

- **GET `/movies`**  
  Lista todos os filmes ou filtra por título.
  - Parâmetro opcional: `title`
  - Exemplo:  
    ```
    GET http://localhost:8080/movies
    GET http://localhost:8080/movies?title=Matrix
    ```

- **GET `/movies/autocomplete?q=prefixo`**  
  Autocompleta títulos de filmes a partir do prefixo informado.
  - Exemplo:  
    ```
    GET http://localhost:8080/movies/autocomplete?q=Sta
    ```

Veja exemplos de uso em [src/docs/rest.http](src/docs/rest.http).

---

## Pontos importantes

- **WebClient**: O serviço [`spring.boot.desafio.uber.service.MovieLocationService`](src/main/java/spring/boot/desafio/uber/service/MovieLocationService.java) utiliza WebClient para buscar os dados externos.
- **Lombok**: Certifique-se de que seu IDE suporta Lombok.
- **Dados Externos**: A aplicação depende da disponibilidade do endpoint público da prefeitura de San Francisco.
- **Testes**: Testes básicos estão em [`spring.boot.desafio.uber.UberApplicationTests`](src/test/java/spring/boot/desafio/uber/UberApplicationTests.java).
- **Configuração**: O nome da aplicação pode ser alterado em [src/main/resources/application.properties](src/main/resources/application.properties).

---