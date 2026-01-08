### Spring Boot practice guide

Here’s a practical, step-by-step guide that covers architecture, environment setup, and three real applications you can run locally, in Docker, and on a production Linux server. For deeper patterns and production hardening, “Spring Boot in Practice” is a solid companion reference with scenario-driven guidance, and this concise best-practices overview is handy for architecture, security, testing, and deployment checklists.

---

### Spring Boot architecture

- **Core idea:** Opinionated auto-configuration around Spring—reduces boilerplate, standardizes project structure, and integrates production features (actuator, metrics, health).
- **Layers:**  
  - **API layer:** Controllers (REST endpoints).  
  - **Service layer:** Business logic, transactions.  
  - **Data layer:** Repositories (JPA/Mongo), entities/records.  
  - **Infrastructure:** Configuration, security, messaging, caching.  
- **Configuration:** Externalized via `application.yml`/profiles; environment variables override for production.
- **Runtime:** Embedded server (Tomcat/Jetty/Netty), fat JAR or layered Docker image; actuator for health/metrics; logging via Logback/SLF4J.
- **Testing:** Unit (JUnit/Mockito), slice tests (`@WebMvcTest`, `@DataJpaTest`), integration tests with `@SpringBootTest`.

> For structured best practices across architecture, security, performance, testing, and deployment, see the curated guide. For scenario-driven solutions (security, microservices, reactive, monitoring), the Manning book is excellent.

---

### Development and production environment requirements

#### Development (Windows/Linux/macOS)
- **Java:** OpenJDK 17 (LTS) or 21.
- **Build tool:** Maven or Gradle (choose one and stick to it).
- **IDE:** IntelliJ IDEA Community or VS Code with Java extensions.
- **Database:** PostgreSQL/MySQL (local Docker optional).
- **Tooling:** Git, Docker Desktop (optional), curl/Postman.

#### Production (Linux, e.g., Ubuntu 22.04)
- **Java runtime:** OpenJDK 17/21 installed via package manager.
- **Reverse proxy:** Nginx or Apache (TLS termination, gzip, caching).
- **Process manager:** systemd or Docker + Compose.
- **Observability:** Spring Boot Actuator, log rotation, metrics endpoint; optional Prometheus/Grafana.
- **Security:** Environment-based secrets, firewall, fail2ban, TLS certificates (Let’s Encrypt).

> The best-practices guide offers concise deployment and monitoring checklists you can adapt to your stack.

---

### Setup and project scaffolding

- **Create project (Maven):**
  - **Command:**
    ```
    mvn -q archetype:generate \
      -DgroupId=com.example \
      -DartifactId=demo \
      -DarchetypeArtifactId=maven-archetype-quickstart \
      -DinteractiveMode=false
    ```
  - **Add Spring Boot:** In `pom.xml`, set parent to `spring-boot-starter-parent`, add starters (`web`, `data-jpa`, `validation`, `actuator`, `security` as needed).
- **Profiles:** `application.yml` + `application-dev.yml` + `application-prod.yml`.
- **Run locally:**
  ```
  ./mvnw spring-boot:run
  ```
- **Build JAR:**
  ```
  ./mvnw clean package
  java -jar target/demo-0.0.1-SNAPSHOT.jar
  ```
- **Docker (optional):**
  - **Dockerfile (layered):**
    ```
    FROM eclipse-temurin:17-jre AS base
    WORKDIR /app
    COPY target/demo-0.0.1-SNAPSHOT.jar app.jar
    ENTRYPOINT ["java","-jar","/app/app.jar"]
    ```
  - **Build & run:**
    ```
    docker build -t demo:latest .
    docker run -p 8080:8080 --env SPRING_PROFILES_ACTIVE=prod demo:latest
    ```

---

### Practical application 1: REST API (stateless, versioned)

#### Installation
- **Dependencies:** `spring-boot-starter-web`, `spring-boot-starter-validation`, `spring-boot-starter-actuator`.
- **Config:** `server.port`, `management.endpoints.web.exposure.include=health,info`.

#### Development
- **DTO + validation:**
  ```java
  record GreetingRequest(@NotBlank String name) {}
  record GreetingResponse(String message) {}
  ```
- **Controller:**
  ```java
  @RestController
  @RequestMapping("/api/v1/greetings")
  class GreetingController {
    @PostMapping
    GreetingResponse greet(@Valid @RequestBody GreetingRequest req) {
      return new GreetingResponse("Hello, " + req.name() + "!");
    }
    @GetMapping("/health")
    Map<String,String> health() { return Map.of("status","ok"); }
  }
  ```
- **Error handling:** `@ControllerAdvice` with `@ExceptionHandler(MethodArgumentNotValidException)` returning 400 JSON.

#### Deployment
- **Local:** `./mvnw spring-boot:run` → test with `curl -X POST localhost:8080/api/v1/greetings -H 'Content-Type: application/json' -d '{"name":"Sudhakaran"}'`.
- **Docker:** Build/run as above; set `SPRING_PROFILES_ACTIVE=prod`.
- **Production (systemd + Nginx):**
  1. **Copy JAR:** `/opt/apps/greeting/app.jar`.
  2. **Service file:** `/etc/systemd/system/greeting.service`
     ```
     [Unit]
     Description=Greeting API
     After=network.target

     [Service]
     User=appuser
     ExecStart=/usr/bin/java -jar /opt/apps/greeting/app.jar --spring.profiles.active=prod
     Restart=always
     Environment=JAVA_OPTS=-Xms256m -Xmx512m

     [Install]
     WantedBy=multi-user.target
     ```
  3. **Enable:** `sudo systemctl daemon-reload && sudo systemctl enable --now greeting`.
  4. **Nginx site:** proxy `server_name api.example.com;` to `http://127.0.0.1:8080;` with TLS.
  5. **Health:** `curl http://127.0.0.1:8080/actuator/health`.

---

### Practical application 2: CRUD service with JPA + PostgreSQL

#### Installation
- **Dependencies:** `spring-boot-starter-data-jpa`, `spring-boot-starter-web`, `postgresql`.
- **Database:** Start Postgres (local or Docker):
  ```
  docker run --name pg -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=products -p 5432:5432 -d postgres:16
  ```
- **Config (`application-dev.yml`):**
  ```
  spring:
    datasource:
      url: jdbc:postgresql://localhost:5432/products
      username: postgres
      password: secret
    jpa:
      hibernate:
        ddl-auto: update
      show-sql: true
  ```

#### Development
- **Entity:**
  ```java
  @Entity
  class Product {
    @Id @GeneratedValue Long id;
    @Column(nullable=false) String name;
    BigDecimal price;
  }
  ```
- **Repository:**
  ```java
  interface ProductRepo extends JpaRepository<Product, Long> {
    List<Product> findByNameContainingIgnoreCase(String q);
  }
  ```
- **Service + Controller:** CRUD endpoints (`POST /api/v1/products`, `GET /api/v1/products/{id}`, `GET /api/v1/products?q=`, `PUT`, `DELETE`).
- **Transactions:** `@Transactional` on service methods that modify data.
- **Validation:** `@NotBlank`, `@DecimalMin("0.0")`.

#### Deployment
- **Local:** Run app; test with `curl` for CRUD operations.
- **Docker Compose (app + db):**
  ```
  services:
    db:
      image: postgres:16
      environment:
        POSTGRES_PASSWORD: secret
        POSTGRES_DB: products
      ports: ["5432:5432"]
    app:
      build: .
      environment:
        SPRING_DATASOURCE_URL: jdbc:postgresql://db:5432/products
        SPRING_DATASOURCE_USERNAME: postgres
        SPRING_DATASOURCE_PASSWORD: secret
        SPRING_PROFILES_ACTIVE: prod
      depends_on: [db]
      ports: ["8080:8080"]
  ```
- **Production:** Managed Postgres (or VM), secure credentials via environment; run app via systemd or Compose; backup strategy (pg_dump), migrations via Flyway.

---

### Practical application 3: Messaging with Kafka (async processing)

#### Installation
- **Dependencies:** `spring-kafka`, `spring-boot-starter-web`, `spring-boot-starter-actuator`.
- **Kafka (Docker):**
  ```
  docker run -d --name kafka -p 9092:9092 -e KAFKA_ZOOKEEPER_CONNECT=zk:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 bitnami/kafka:latest
  ```
  (Or use a single-node stack like `bitnami/kafka` with bundled zookeeper.)

#### Development
- **Producer config:** `KafkaTemplate<String, String>` bean; topic `events.orders`.
- **Controller:** `POST /api/v1/orders` → validate payload → send to Kafka.
  ```java
  @PostMapping("/api/v1/orders")
  ResponseEntity<Void> create(@Valid @RequestBody OrderRequest req) {
    kafkaTemplate.send("events.orders", req.id(), toJson(req));
    return ResponseEntity.accepted().build();
  }
  ```
- **Consumer:** `@KafkaListener(topics="events.orders", groupId="order-workers")` → process and persist.
- **Resilience:** Retries/backoff, dead-letter topic, idempotency keys.

#### Deployment
- **Local:** Run Kafka container; start app; verify with `kafka-console-consumer`.
- **Docker Compose:** Define `kafka` service + app; configure `SPRING_KAFKA_BOOTSTRAP_SERVERS=kafka:9092`.
- **Production:** Managed Kafka (Confluent/Redpanda) or VM; secure with SASL/TLS; monitor lag; scale consumers horizontally.

---

### Best-practices checklist (apply across apps)

- **Configuration:** Externalize secrets; use profiles; fail fast on missing env vars.
- **Security:** Validate inputs; enable HTTPS; set CORS explicitly; use Spring Security for auth; sanitize logs.
- **Observability:** Actuator health/info; structured JSON logs; correlation IDs; metrics (Micrometer).
- **Performance:** Connection pools; caching where appropriate; pagination; avoid N+1 queries.
- **Testing:** Unit + slice + integration; testcontainers for DB/Kafka; contract tests for APIs.
- **Deployment:** Immutable builds; versioned artifacts; zero-downtime restarts; backups; rollbacks; disaster recovery drills.

> For compact, actionable guidance across these areas, the best-practices resource is a good reference. For deeper, scenario-based solutions and production hardening, the Manning book and its repo provide extensive examples.

