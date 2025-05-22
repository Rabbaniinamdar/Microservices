# Microservices


## ✅ What is **Microservices** Architecture?

**Microservices** is an architectural style where an application is **broken down into small, independent services**, each responsible for a specific business capability.

**Microservices is an architectural approach to developing a single application as a suite of small, independent services.** Each service runs in its own process, communicates through lightweight mechanisms (such as HTTP or messaging), is centered around a specific business capability, and can be deployed independently using fully automated deployment pipelines.

### 🔹 Key Features:

* Each service runs in its **own process**
* Services **communicate** via APIs (usually REST, gRPC, or messaging)
* **Decentralized** development, deployment, and scaling
* Each service can use its own **database and tech stack**
* Promotes **agility**, **scalability**, and **resilience**

### 🔹 Example:

An e-commerce app might be split into:

* **Product Service**
* **Order Service**
* **Payment Service**
* **User Service**

---

## ✅ What is a **Monolithic** Architecture?

A **monolithic application** is built as a **single, large unit** where all functionalities are tightly coupled and run in one process.

### 🔹 Key Characteristics:

* All components (UI, business logic, data access) are in **one codebase**
* **One build** and **one deployment**
* Hard to scale individual parts
* **Tightly coupled** – a change in one part can affect the whole system

### 🔹 Example:

An e-commerce app where product, order, payment, and user logic all exist in one Spring Boot application.

---

## ✅ What is **SOA (Service-Oriented Architecture)**?

**SOA** is an architectural pattern where applications are built as a **collection of services**, but these services typically share a **common infrastructure** like:

* **Enterprise Service Bus (ESB)**
* **Centralized governance and security**

### 🔹 Differences from Microservices:

| Feature       | SOA                                  | Microservices                        |
| ------------- | ------------------------------------ | ------------------------------------ |
| Communication | ESB (heavy, centralized)             | REST, lightweight messaging          |
| Coupling      | Loosely coupled, but often shared DB | Fully independent, often private DBs |
| Deployment    | Often deployed together              | Independently deployable             |
| Granularity   | Coarse-grained services              | Fine-grained, focused services       |

---

## 🔁 Summary

| Architecture      | Description                                            | Pros                                 | Cons                           |
| ----------------- | ------------------------------------------------------ | ------------------------------------ | ------------------------------ |
| **Monolithic**    | All-in-one app with tightly coupled components         | Simple to build & deploy             | Hard to scale, slow to update  |
| **SOA**           | Distributed services using shared infrastructure (ESB) | Promotes reuse                       | Can be complex and heavyweight |
| **Microservices** | Small, independently deployable services               | Scalable, resilient, faster delivery | Complex DevOps & communication |


## ✅ Why **Spring Boot** for Microservices?

Spring Boot is widely regarded as one of the **best frameworks** for building microservices due to its **simplicity, power, and rich ecosystem**. Here's why:

---

### 🔹 1. **Self-Contained Deployable JARs (Fat JARs)**

* Traditional applications were deployed as **WARs** and required **external servers** like Tomcat or JBoss.
* Spring Boot packages applications as **standalone JARs** with:

  * Embedded servers (Tomcat, Jetty, or Undertow)
  * All required dependencies
* This enables each microservice to run **independently** on any machine with a JVM—ideal for microservice architecture.

---

### 🔹 2. **Auto-Configuration and Rapid Setup**

* Spring Boot reduces boilerplate code with **auto-configuration**.
* With a few annotations and **starter dependencies**, you can:

  * Connect to databases
  * Secure endpoints
  * Configure queues, schedulers, etc.
* Speeds up development and avoids repetitive manual setup.

---

### 🔹 3. **Built-in Support for Production-Ready Features**

* Integrated **Actuator** module provides:

  * Health checks
  * Metrics
  * Logging
  * Application info endpoints
* Useful for **monitoring and maintaining** microservices in production environments.

---

### 🔹 4. **Externalized Configuration**

* Easily externalize properties using:

  * `application.properties` or `.yml`
  * Command-line arguments
  * Environment variables
* Makes microservices **portable** and easy to configure per environment (dev, test, prod).

---

### 🔹 5. **Cloud-Native Friendly**

* Spring Boot integrates well with cloud platforms and tools:

  * Kubernetes
  * Docker
  * Spring Cloud
* Enables service discovery, centralized configuration, circuit breakers, distributed tracing, and more.

---

### 🔹 6. **Microservice Starter Ecosystem**

* Spring Boot provides **pre-configured starter dependencies**:

  * `spring-boot-starter-web` for REST APIs
  * `spring-boot-starter-data-jpa` for database access
  * `spring-boot-starter-security` for security
* These starters simplify setup for commonly used features.

---

### 🔹 7. **Scalable Architecture Support**

* Spring Boot is **modular**, making it easy to break functionality into **separate microservices**.
* Works seamlessly with tools like:

  * Eureka (Service Discovery)
  * Zuul/Gateway (Routing)
  * Config Server (Externalized Config)
  * Sleuth & Zipkin (Distributed Tracing)

---

## 🔁 Summary: WAR vs JAR Deployment

| Traditional (WAR)                      | Microservices with Spring Boot (JAR)  |
| -------------------------------------- | ------------------------------------- |
| Requires external server               | Includes embedded server              |
| Heavier and tightly coupled deployment | Lightweight, modular services         |
| Harder to scale and maintain           | Scalable and independently deployable |




## ✅ **1. Externalizing Configurations in Spring Boot**

Spring Boot allows you to **externalize application configuration** to make your apps flexible and environment-agnostic. These external sources override values in `application.properties` or `application.yml`.

---

### 🔹 A. **Using Command-Line Arguments**

**Syntax:**

```bash
java -jar app.jar --property.name=value
```

**Example:**

```bash
java -jar accounts-service.jar --build.version=1.1
```

* Spring Boot automatically maps this to `build.version=1.1`.
* **Precedence:** Highest among all property sources.
* **Use Case:** Temporary overrides, quick deployments, CI/CD pipelines.

---

### 🔹 B. **Using JVM System Properties**

**Syntax:**

```bash
java -Dproperty.name=value -jar app.jar
```

**Example:**

```bash
java -Dbuild.version=1.2 -jar accounts-service.jar
```

* Mapped directly to Spring's `Environment` object.
* **Precedence:** Lower than CLI arguments, but higher than environment variables and property files.

---

### 🔹 C. **Using Environment Variables**

**Syntax:**

```bash
# Windows
set BUILD_VERSION=1.3
java -jar accounts-service.jar

# Linux/macOS
BUILD_VERSION=1.3 java -jar accounts-service.jar
```

**Mapping Rules (Relaxed Binding):**

* Property name: `build.version`
* Environment Variable: `BUILD_VERSION`

Spring Boot converts:

* Dots (`.`) and hyphens (`-`) to underscores (`_`)
* Lowercase to uppercase

**Precedence:** Lower than CLI and JVM args, but higher than `application.properties`.

---

### 🔹 D. **Using `application.properties` or `application.yml`**

**Example:**

```properties
build.version=1.0
```

This is the **default configuration** within your application.

---

## 📊 **Spring Boot Property Precedence Order (Highest to Lowest)**

1. **Command-line arguments** (`--build.version=1.1`)
2. **JVM system properties** (`-Dbuild.version=1.2`)
3. **Environment variables** (`BUILD_VERSION=1.3`)
4. **Application properties file**
5. **Default properties**

---

## ❗ Problems with Manual External Configuration (Spring Boot Alone)

1. **Manual Setup & Human Errors**

   * Manually setting CLI args, env vars, or JVM options can lead to mistakes in deployments.

2. **No Revision History**

   * Changing `application.properties` or env vars leaves **no audit trail**.

3. **Lack of Access Control**

   * Env vars can't control **who can read/change** configs.

4. **Scaling Issues**

   * Managing configs for **100+ instances** is hard without centralized config.

5. **No Encryption**

   * Secrets in `application.properties`, env vars, etc., are in **plain text**.

6. **Dynamic Config Reload**

   * Changing a config requires a **restart** unless you add dynamic refresh logic.

---

## 🛠️ Recommended Solutions for Enterprise Applications

### ✅ **1. Centralized Configuration with Spring Cloud Config**

* Store configs in **Git**, **Vault**, **File System**, or **DB**.
* Clients fetch their configuration from a **central config server**.
* Allows **versioning**, rollback, and easy updates.

> ✅ Use `@RefreshScope` for beans to auto-refresh on config changes.

---

### ✅ **2. Secrets Management with Vault**

* Use **HashiCorp Vault**, AWS Secrets Manager, or Azure Key Vault.
* Spring Boot integrates with **Spring Cloud Vault**:

  * Secure storage.
  * Fine-grained access.
  * Encrypted secrets.

```yaml
spring:
  cloud:
    vault:
      uri: http://localhost:8200
      token: s.xxxxxxxx
```

---

### ✅ **3. Dynamic Refresh with Actuator + Spring Cloud Bus**

* Use Spring Actuator to expose `POST /actuator/refresh`.
* Trigger a **refresh event** using Spring Cloud Bus (RabbitMQ/Kafka) to notify all instances.

```bash
curl -X POST http://localhost:8080/actuator/refresh
```

> Only works with properties marked using `@RefreshScope`.

---

### ✅ **4. Audit & Access Control**

* Store configuration in **version-controlled systems** like Git.
* Use CI/CD pipelines to control **who can change** what.
* Log configuration load events for audit trails.

---

### ✅ **5. Use Profiles for Environment Separation**

```bash
java -jar app.jar --spring.profiles.active=prod
```

* Separate files like:

  * `application-dev.properties`
  * `application-prod.properties`

---

## ✅ Summary Table

| Method                | Example                                         | Precedence | Supports Encryption | Supports Dynamic Reload |
| --------------------- | ----------------------------------------------- | ---------- | ------------------- | ----------------------- |
| Command-line args     | `--build.version=1.1`                           | Highest    | ❌                   | ❌                       |
| JVM system properties | `-Dbuild.version=1.2`                           | High       | ❌                   | ❌                       |
| Env variables         | `BUILD_VERSION=1.3`                             | Medium     | ❌                   | ❌                       |
| Property files        | `build.version=1.0` in `application.properties` | Low        | ❌                   | ❌                       |
| Spring Cloud Config   | Git-based config server                         | Custom     | ✅ (via Vault)       | ✅ (with Bus)            |

---

Here's a clear and concise explanation of **Spring Cloud** and how it helps in **microservices development**, based on your notes:

---

## ✅ What is **Spring Cloud**?

**Spring Cloud** is a set of tools built on top of Spring Boot to help developers implement **common microservice patterns** like:

* Service Discovery
* Centralized Configuration
* Routing
* Load Balancing
* Security
* Distributed Tracing
* Messaging

It simplifies the development of **cloud-native, scalable, and distributed systems**.

---

## 🚀 Why Use **Spring Cloud** for Microservices?

Spring Cloud helps you manage the complexity of microservices with **out-of-the-box solutions** to common problems.

---

### 🔹 1. **Service Registration & Discovery**

* ✅ Tool: **Spring Cloud Netflix Eureka**
* New microservices **register themselves** with Eureka Server.
* Other services discover them using a **logical name**, not an IP.

  **Benefit:** No hardcoding of addresses, supports dynamic scaling.

---

### 🔹 2. **Routing (API Gateway) & Tracing**

* ✅ Tool: **Spring Cloud Gateway + Sleuth + Zipkin**
* All requests go through a **single entry point** (gateway) to the backend services.
* Each request is **traced end-to-end** with a unique trace ID.

  **Benefit:** Better monitoring, debugging, and secured routing.

---

### 🔹 3. **Spring Cloud Config (Centralized Configuration)**

* ✅ Tool: **Spring Cloud Config Server**
* Externalizes microservice configurations to a **central server** (can be Git, file system, etc.)
* All instances share the **same versioned configuration**.

  **Benefit:** No need to redeploy apps for config changes.

---

### 🔹 4. **Load Balancing**

* ✅ Tool: **Spring Cloud LoadBalancer (or Netflix Ribbon)**
* Distributes traffic among multiple instances of a microservice.

  **Benefit:** Improves performance, reliability, and fault tolerance.

---

### 🔹 5. **Spring Cloud Security**

* ✅ Tool: **Spring Security with OAuth2/JWT**
* Provides token-based security for microservices.

  **Benefit:** Central authentication and fine-grained authorization.

---

### 🔹 6. **Distributed Tracing & Messaging**

* ✅ Tools: **Spring Cloud Sleuth + Zipkin**, **Spring Cloud Stream**
* Track requests across microservices with trace IDs.
* Enable **asynchronous communication** via message brokers (Kafka, RabbitMQ).

  **Benefit:** Helps in monitoring, fault analysis, and creating resilient event-driven systems.

---

## ✅ Summary

| Feature                  | Tool/Support in Spring Cloud       | Purpose                                  |
| ------------------------ | ---------------------------------- | ---------------------------------------- |
| Service Discovery        | Eureka                             | Register & locate services dynamically   |
| API Gateway              | Spring Cloud Gateway               | Central routing and entry point          |
| Configuration Management | Spring Cloud Config Server         | Centralize & version application configs |
| Load Balancing           | Spring Cloud LoadBalancer / Ribbon | Distribute requests evenly               |
| Security                 | Spring Security + OAuth2           | Secure APIs with token-based auth        |
| Distributed Tracing      | Sleuth + Zipkin                    | Track requests across services           |
| Messaging                | Spring Cloud Stream                | Asynchronous, scalable communication     |

Here's a **clean and structured explanation** of how **Spring Cloud Config** helps with centralized configuration in microservices:

---

## ✅ What is **Spring Cloud Config**?

**Spring Cloud Config** is a framework that provides **server and client-side support** for managing **externalized configuration** in a **centralized, versioned, and secure** way for distributed systems (microservices).

---

## 🔄 Why Centralized Configuration?

In a microservices architecture:

* Each service runs independently.
* Configurations vary by environment (dev, test, prod).
* Managing config across multiple services manually becomes error-prone and inefficient.

---

## 🔧 Spring Cloud Config Architecture

### 🔹 1. **Central Repository** (e.g., Git, SVN, File System)

* Stores configuration files (like `application.yml`, `service-name.yml`)
* Supports **version control**, **access control**, and **history tracking**
* Example:

  ```
  config-repo/
    ├── application.yml
    ├── accounts-service.yml
    └── loans-service.yml
  ```

### 🔹 2. **Spring Cloud Config Server**

* Acts as a **middle layer** between microservices and the configuration source.
* Fetches properties from the central repo and serves them to client applications via REST endpoints.
* Example endpoint:

  ```
  GET /{application}/{profile}
  /accounts-service/dev → returns dev config for accounts-service
  ```

### 🔹 3. **Spring Cloud Config Clients**

* Microservices act as **Config clients**
* At startup, they contact the **Config Server** to fetch their configurations.
* Uses bootstrap configuration (`bootstrap.yml` or `bootstrap.properties`) to connect to the Config Server.

---

## 📦 Configuration Flow

```plaintext
Microservices (Clients)
     ↓ fetch config
Config Server
     ↓ load from repo
Central Config Repository (Git/File System)
```

---

## ✅ Key Benefits

| Feature                         | Benefit                                                                 |
| ------------------------------- | ----------------------------------------------------------------------- |
| **Centralized Management**      | One place to manage config for all services across environments         |
| **Versioned Configuration**     | Use Git/SVN for history, rollback, auditing                             |
| **Environment Specific Config** | Supports profiles like `dev`, `test`, `prod`                            |
| **Secure Config Delivery**      | Config server can be secured with Spring Security + encrypted values    |
| **Dynamic Refreshing**          | With `@RefreshScope` and Spring Bus, some configs can be refreshed live |

---

## ✅ Example `bootstrap.yml` (Client Side)

```yaml
spring:
  application:
    name: accounts-service
  cloud:
    config:
      uri: http://localhost:8888
      profile: dev
```

---

## ✅ Example Repo Structure

```
config-repo/
  ├── application.yml                 # Global config
  ├── accounts-service.yml           # Service-specific config
  └── accounts-service-dev.yml       # Environment-specific config
```

---

## 🧠 Conclusion

Using **Spring Cloud Config** for centralized configuration solves the key problems of:

* Manual property management
* Environment inconsistencies
* Lack of config versioning and auditing
* Inability to dynamically update config without restarting apps

It brings scalability, maintainability, and control to distributed microservice architectures.

Here are well-structured notes on **refreshing Spring Cloud Config at runtime** using `/actuator/refresh` along with **code snippets** and explanations. It also addresses **scaling to multiple instances** in production.

---

## 🔁 Refreshing Config at Runtime in Spring Cloud

### ✅ Goal:

Enable dynamic configuration updates in a Spring Boot microservice using the `/actuator/refresh` endpoint **without restarting the service**.

---

## 🔧 1. Add Spring Boot Actuator Dependency (in Client Service)

**pom.xml** (for `accounts`, `loans`, `cards`, etc.):

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

## ⚙️ 2. Enable `/actuator/refresh` Endpoint

**application.yml** (in microservice):

```yaml
management:
  endpoints:
    web:
      exposure:
        include: refresh  # expose only the refresh endpoint
```

---

## 📤 3. Trigger Refresh via HTTP POST

Use a tool like `curl` or Postman to send:

```bash
POST http://localhost:8080/actuator/refresh
```

➡️ This will:

* Reload the configuration properties
* Pull the latest config from the Config Server
* Apply the changes live, without restarting

---

## 🔄 Refresh Flow Diagram Summary

1. **Developer pushes new config** ➝ Git Config Repo
2. **Config Server detects change** (on next request)
3. **Microservice manually or programmatically calls** `/actuator/refresh`
4. **Config Server fetches latest config**
5. **Client microservice reloads properties dynamically**

---

## 🧪 Example

**Updated config in Git repo:**

```yaml
message: "Hello from production!"
```

**Refresh via POST:**

```bash
curl -X POST http://localhost:8080/actuator/refresh
```

**Access updated property:**

```java
@RefreshScope
@RestController
public class MessageController {

    @Value("${message}")
    private String message;

    @GetMapping("/message")
    public String getMessage() {
        return message;
    }
}
```

🔁 `@RefreshScope` is essential to re-initialize the bean with updated properties.


### 🌐 What is **Spring Cloud Bus**?

**Spring Cloud Bus** is a Spring Cloud component used to **broadcast events** (like configuration changes) to multiple instances of microservices using a **message broker** such as **RabbitMQ** or **Kafka**.

---

## 🔑 Key Purpose

In a distributed system with multiple microservice instances, when configuration changes occur (e.g., in Spring Cloud Config), it's inefficient to manually refresh every instance.
**Spring Cloud Bus** solves this by **automatically propagating** events (like `/refresh`) to all connected services **over the message broker**.

---

## ✅ Main Features

| Feature                          | Description                                                            |
| -------------------------------- | ---------------------------------------------------------------------- |
| 🔄 Dynamic Configuration Refresh | Propagates config updates to all services using `/actuator/busrefresh` |
| 📨 Event Broadcasting            | Sends custom or system events to all nodes via RabbitMQ/Kafka          |
| 🧩 Lightweight Integration       | Plugs into Spring Boot Actuator and Spring Cloud Config easily         |
| ⚙️ Works with Message Brokers    | Supports **RabbitMQ**, **Kafka**, etc.                                 |

---

## 🛠️ How It Works (In Brief)

1. You update a config value in your Git repo.
2. Push it to the remote repo (e.g., GitHub).
3. Call `POST /actuator/busrefresh` on **any one** microservice.
4. Spring Cloud Bus uses RabbitMQ to send a **refresh event** to **all services**.
5. All services reload updated configuration dynamically.

---

## 📦 Typical Stack

* **Spring Cloud Config Server**
* **Spring Cloud Config Clients** (Accounts, Loans, etc.)
* **RabbitMQ** or **Kafka** (as the transport layer)
* **Spring Boot Actuator**
* **Spring Cloud Bus**

---

## 📘 Example Scenario

Let's say you have:

* 3 microservices (Accounts, Loans, Cards)
* Central config in GitHub (Spring Cloud Config)
* Config Server running
* RabbitMQ running

After pushing a config change:

```bash
curl -X POST http://localhost:8080/actuator/busrefresh
```

🔁 All three services automatically reload the updated config — **no restart needed**.

---

## 🚫 Without Spring Cloud Bus

You would have to:

* Call `/actuator/refresh` **on each instance manually**, or
* Restart each app

✅ Spring Cloud Bus removes that pain by **centralizing the refresh process**.

---


## 🧩 Architecture Overview

```
     ┌────────────────┐           ┌────────────────┐
     │ Config Repo    │  Push     │ Config Server  │
     │ (GitHub)       ├──────────►│ (Spring Cloud) │
     └────────────────┘           └────────────────┘
                                         │
                         Refresh event via /actuator/busrefresh
                                         ▼
   ┌────────────┬────────────┬────────────┐
   │ Accounts   │ Loans      │ Cards      │ ← Microservices
   │ Service    │ Service    │ Service    │
   └────────────┴────────────┴────────────┘
           ▲            ▲            ▲
           └───── Message Broker (RabbitMQ) ─────┘
```

---

## ✅ How it works

1. Configuration is stored in a **Git repository**.
2. **Spring Cloud Config Server** fetches the latest configuration.
3. On triggering `/actuator/busrefresh`, a **refresh event is sent via RabbitMQ**.
4. All microservices receive this event and re-bind their `@RefreshScope` beans with the new configuration.

---

## 📦 Step-by-Step Setup

---

### ✅ 1. Add Required Dependencies

Add the following dependencies in **`pom.xml`** of:

* Config Server
* All microservices (Accounts, Loans, Cards)

```xml
<!-- Spring Boot Actuator for exposing refresh endpoints -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

<!-- Spring Cloud Bus with RabbitMQ -->
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>
```

---

### ✅ 2. Expose the `/busrefresh` Endpoint

By default, `/actuator/busrefresh` is not exposed. You must explicitly include it in the YAML config:

**application.yml (for all services and config server):**

```yaml
management:
  endpoints:
    web:
      exposure:
        include: busrefresh
```

To expose all endpoints (used commonly in dev/test environments):

```yaml
management:
  endpoints:
    web:
      exposure:
        include: "*"
```

---

### ✅ 3. Run RabbitMQ via Docker

You can start a RabbitMQ instance using Docker:

```bash
docker run -d --hostname rabbitmq-host --name rabbitmq \
  -p 5672:5672 -p 15672:15672 \
  rabbitmq:3-management
```

* Web UI: [http://localhost:15672](http://localhost:15672)
* Default credentials: `guest` / `guest`

---

### ✅ 4. Configure RabbitMQ in Application YML

**All services and config server must include RabbitMQ details:**

```yaml
spring:
  rabbitmq:
    host: "localhost"
    port: 5672
    username: "guest"
    password: "guest"
```

---

### ✅ 5. Config Server Full Configuration (As Provided)

```yaml
spring:
  application:
    name: "configserver"
  profiles:
    active: git
  cloud:
    config:
      server:
        git:
          uri: "https://github.com/eazybytes/eazybytes-config.git"
          default-label: main
          timeout: 5
          clone-on-start: true
          force-pull: true
  rabbitmq:
    host: "localhost"
    port: 5672
    username: "guest"
    password: "guest"

management:
  endpoints:
    web:
      exposure:
        include: "*"
  health:
    readiness-state:
      enabled: true
    liveness-state:
      enabled: true
  endpoint:
    health:
      probes:
        enabled: true

encrypt:
  key: "45D81EC1EF61DF9AD8D3E5BB397F9"

server:
  port: 8071
```

---

### ✅ 6. Use `@RefreshScope` for Dynamic Beans

Use `@RefreshScope` on beans whose values should refresh without restart:

```java
@RefreshScope
@RestController
public class MessageController {

    @Value("${message}")
    private String message;

    @GetMapping("/message")
    public String getMessage() {
        return message;
    }
}
```

---

### ✅ 7. Trigger Refresh Event Manually

Trigger this using a POST request to any one microservice:

```bash
curl -X POST http://localhost:8080/actuator/busrefresh
```

This will:

* Fetch the updated configuration from Git
* Broadcast refresh event via RabbitMQ
* Reload `@RefreshScope` beans in all microservices

---

## ⚡ BONUS: Fully Automate with GitHub Webhook

To **automate the config refresh after every Git push**, follow these steps:

---

### 🛠️ Step 1: Add an API to Trigger `/busrefresh`

```java
@RestController
public class AutoRefreshController {

    @Autowired
    private RestTemplate restTemplate;

    @PostMapping("/webhook/refresh")
    public ResponseEntity<String> autoRefresh() {
        restTemplate.postForObject("http://localhost:8080/actuator/busrefresh", null, String.class);
        return ResponseEntity.ok("Config refresh triggered");
    }
}
```

---

### 🌐 Step 2: Create GitHub Webhook

* Go to your GitHub repo (e.g., `eazybytes-config`)
* Navigate to **Settings > Webhooks > Add webhook**
* Payload URL: `http://<your-host>:<port>/webhook/refresh`
* Content type: `application/json`
* Trigger on: `Just the push event`

✅ Now, **every push to GitHub** will automatically trigger a refresh of all microservices.

---

## ✅ Summary

| Step                                | Description                                   |
| ----------------------------------- | --------------------------------------------- |
| Add dependencies                    | Actuator + Spring Cloud Bus AMQP              |
| Expose endpoints                    | Enable `/busrefresh` or `*` in YAML           |
| Configure RabbitMQ                  | Use Docker, setup all service configs         |
| Annotate beans with `@RefreshScope` | So updated values are injected on refresh     |
| Use `/actuator/busrefresh`          | Triggers global config reload via RabbitMQ    |
| Automate with GitHub Webhook        | Optional step to automate refresh on Git push |

---

##**automatically refresh Spring Cloud Config properties at runtime** using **Spring Cloud Bus** and **Spring Cloud Config Monitor**:

## 🧩 Components Involved:

* **Spring Cloud Config Server**
* **Spring Cloud Config Clients** (Accounts, Loans, Cards)
* **Spring Cloud Bus** (backed by RabbitMQ)
* **Spring Cloud Config Monitor**
* **RabbitMQ** (for broadcasting config change events)
* **GitHub Webhook** (to notify Config Server on config updates)

---

## 🔁 How It Works – Step-by-Step:

### **1. Add Required Dependencies**

#### ✅ In all microservices & config server (`pom.xml`):

```xml
<!-- Spring Boot Actuator -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

<!-- Spring Cloud Bus for AMQP (RabbitMQ) -->
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>
```

#### ✅ In **Config Server only**:

```xml
<!-- Spring Cloud Config Monitor -->
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-config-monitor</artifactId>
</dependency>
```

---

### **2. Enable `/actuator/busrefresh` and `/monitor` endpoints**

#### ✅ In all microservices & config server (`application.yml`):

```yaml
management:
  endpoints:
    web:
      exposure:
        include: busrefresh,refresh,health,info
```

---

### **3. Add Spring Cloud Bus and RabbitMQ configuration**

#### ✅ `application.yml` (Config Server & Clients):

```yaml
spring:
  rabbitmq:
    host: localhost
    port: 5672
    username: guest
    password: guest
```

---

### **4. Setup RabbitMQ via Docker (if not already)**

#### 🐳 Docker command:

```bash
docker run -d --hostname rabbit --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
```

Access UI at: `http://localhost:15672`
(Default user/pass: `guest` / `guest`)

---

### **5. Push Config Changes to GitHub**

* Update your config files (e.g., `accounts.yml`, `loans.yml`) in your GitHub repository.

---

### **6. Create a GitHub Webhook**

1. Go to your GitHub config repo → **Settings** → **Webhooks**
2. Click **Add Webhook**
3. Use the following configuration:

   * **Payload URL**: `http://localhost:8071/monitor` (your config server's address)
   * **Content type**: `application/json`
   * **Event**: Push events
   * Click **Add webhook**

---

### **7. Monitor Endpoint Triggered Automatically**

Once the GitHub webhook hits `/monitor` on the Config Server:

* Spring Cloud Config Monitor detects the config repo change
* Publishes an event to RabbitMQ
* **Spring Cloud Bus** propagates the event
* All microservices receive a **refresh signal**
* Updated configuration is fetched without restarting any app

---

## 🧠 Behind the Scenes

| Step | What Happens                                   | Component                   |
| ---- | ---------------------------------------------- | --------------------------- |
| 1    | You commit config changes to GitHub            | GitHub                      |
| 2    | Webhook sends POST to `/monitor`               | GitHub                      |
| 3    | Config Server receives the event               | Spring Cloud Config Monitor |
| 4    | Publishes refresh event to RabbitMQ            | Spring Cloud Bus            |
| 5    | All client microservices receive `/busrefresh` | Spring Cloud Bus            |
| 6    | Clients fetch the latest config dynamically    | Spring Cloud Config Clients |

---

## ✅ Final Outcome:

✅ **No manual trigger**
✅ **All instances updated instantly**
✅ **Zero downtime**
✅ **Centralized config with live propagation**

---
Certainly! Below is the same `application.yml` file for the **Accounts microservice**, now with detailed **inline comments** explaining each section:

```yaml
# Server configuration: Specifies the port where the Accounts microservice will run
server:
  port: 8080

# Spring application configuration
spring:
  application:
    # Name of the application, used for Spring Cloud Config to load the relevant config files (e.g., accounts.yml)
    name: "accounts"

  profiles:
    # Active profile for the application. It specifies which profile to use when fetching configuration from the Config Server.
    active: "prod"  # In this case, 'prod' profile will be used to load 'accounts-prod.yml' from the config repo.

  # Data source configuration for the Accounts microservice.
  datasource:
    # H2 in-memory database configuration for testing/development purposes.
    url: jdbc:h2:mem:testdb
    driverClassName: org.h2.Driver
    username: sa
    password: ''  # Empty password for the H2 database

  # Enable the H2 console for accessing the database via browser for testing.
  h2:
    console:
      enabled: true

  # JPA (Java Persistence API) configuration for Hibernate, enabling automatic DB schema updates and SQL logging.
  jpa:
    # Defines the Hibernate dialect for H2 database
    database-platform: org.hibernate.dialect.H2Dialect
    hibernate:
      ddl-auto: update  # Automatically updates the DB schema (for testing/dev purposes)
    show-sql: true  # Logs all SQL queries for debugging

  # Spring Cloud Config integration, importing configuration from the Config Server
  config:
    # The Config Server URI where the configuration will be fetched from.
    # The "optional:" prefix ensures that the application will not crash if the Config Server is temporarily unavailable.
    import: "optional:configserver:http://localhost:8071/"  # Config Server running at localhost on port 8071

  # RabbitMQ configuration for Spring Cloud Bus integration
  rabbitmq:
    # Connection details for RabbitMQ message broker, used to broadcast refresh events to all connected microservices.
    host: "localhost"  # RabbitMQ host
    port: 5672  # Default RabbitMQ port
    username: "guest"  # Default username for RabbitMQ
    password: "guest"  # Default password for RabbitMQ

# Management endpoint configuration (for Spring Boot Actuator)
management:
  endpoints:
    web:
      # Exposing all actuator endpoints for management and monitoring purposes.
      exposure:
        include: "*"  # Exposing all endpoints like /actuator/health, /actuator/refresh, /actuator/busrefresh
```

---

### 🧩 **Key Sections Explained**:

1. **Server Configuration**: The microservice is set to run on port `8080`.

2. **Spring Application Settings**:

   * Defines the service name as `"accounts"`, which helps **Spring Cloud Config** fetch the right configuration file (e.g., `accounts.yml`) from the repository.
   * The active profile is set to `prod`, which indicates that the service will use the configuration related to the `prod` profile.

3. **Datasource and JPA Configuration**:

   * Configures an **H2 database** to be used during development/testing.
   * Enables **automatic schema updates** and logs SQL queries for easy debugging.

4. **Spring Cloud Config**:

   * Configures the microservice to **fetch external configurations from the Config Server** running on `http://localhost:8071`. The `optional:` prefix ensures that the application doesn't fail if the Config Server is temporarily unavailable.

5. **RabbitMQ Configuration**:

   * Configures the **RabbitMQ connection** to facilitate communication through **Spring Cloud Bus**, which helps propagate configuration changes across all microservices. It listens to events like `RefreshRemoteApplicationEvent` to reload the configuration.

6. **Management Endpoints**:

   * Exposes all **Spring Boot Actuator endpoints**, such as `/actuator/busrefresh`, which is crucial for triggering the refresh event when **Spring Cloud Bus** broadcasts it across the network.

---

This configuration enables your microservice to leverage **Spring Cloud Config**, **Spring Cloud Bus**, and **Spring Cloud Config Monitor** for dynamic, hot-reloadable configuration changes across multiple microservices in a production environment.

---

### 🧠 **What are Liveness and Readiness Probes?**

| **Probe Type** | **Purpose**                                   | **Outcome on Failure**                 |
| -------------- | --------------------------------------------- | -------------------------------------- |
| **Liveness**   | Checks if the app is alive (i.e., not stuck)  | Restarts the container                 |
| **Readiness**  | Checks if the app is ready to handle requests | Stops sending traffic to the container |

---

### 🔄 **Liveness Probe**

* **Question it answers**: “Is the application alive?”
* If this probe fails, Kubernetes (or Docker) assumes the app is **not recoverable** in its current state and **restarts** the container.
* Useful for detecting deadlocks, hung threads, or unrecoverable memory conditions.

#### ✅ Example Use Case:

* Your Spring Boot app gets stuck during a long database operation — it's alive but non-responsive.
* Liveness probe detects this and **restarts the app** to self-heal.

---

### 📶 **Readiness Probe**

* **Question it answers**: “Is the application ready to receive traffic?”
* If this fails, Kubernetes stops routing traffic to this pod **without restarting it**.
* Useful during **startup**, **warm-up**, or **when dependencies (like DB or config server) are not yet available**.

#### ✅ Example Use Case:

* Spring Boot app is still initializing beans or waiting for an external config server.
* Readiness probe fails → Load balancer doesn't route traffic → No 502 errors to users.

---

### 🛠️ **Spring Boot Integration (via Actuator)**

Spring Boot integrates **liveness** and **readiness** probes using:

1. **`ApplicationAvailability` Interface** – Tracks availability status of the app.
2. **Health Indicators**:

   * `LivenessStateHealthIndicator`
   * `ReadinessStateHealthIndicator`

---

### 📍 **Actuator Endpoints**

With Spring Boot Actuator and health groups enabled, you can access:

* `/actuator/health` → Global health info (includes liveness & readiness)
* `/actuator/health/liveness` → Only liveness info
* `/actuator/health/readiness` → Only readiness info

---

### 🧾 **Required YAML Config to Enable These Probes**

```yaml
management:
  health:
    livenessstate:
      enabled: true  # Enables liveness probe
    readinessstate:
      enabled: true  # Enables readiness probe
  endpoint:
    health:
      probes:
        enabled: true  # Enables /actuator/health/liveness and /actuator/health/readiness endpoints
  endpoints:
    web:
      exposure:
        include: "*"  # Exposes all actuator endpoints including health groups
```

---

### 🔄 Example Output of Probes

**GET `/actuator/health/liveness`**

```json
{
  "status": "UP",
  "components": {
    "livenessState": {
      "status": "UP"
    }
  }
}
```

**GET `/actuator/health/readiness`**

```json
{
  "status": "UP",
  "components": {
    "readinessState": {
      "status": "UP"
    }
  }
}
```

---

### ✅ Summary

* **Liveness** → Keeps your app running properly by restarting when needed.
* **Readiness** → Keeps your users happy by only sending traffic when the app is ready.
* **Spring Boot Actuator** simplifies implementation of these health checks via dedicated endpoints.


## 🔧 **Challenges in Microservices Communication**

1. **How do services locate each other inside a network?**

   * In microservices, each service has its own dynamic host and port.
   * Services can scale dynamically, causing IPs to change.
   * Static IP/DNS isn’t reliable in such an environment.

2. **How do new service instances enter into the network?**

   * When instances are added (due to auto-scaling or failure recovery), they need to be discoverable immediately.
   * Clients or other services must be able to find and use them without manual intervention.

3. **How to load balance and share service info?**

   * Multiple instances of a service need **load balancing**.
   * Each instance’s info must be accessible dynamically.
   * Static DNS round-robin is inefficient and outdated here.

---

## ✅ **Solutions**

### 1. **Service Registration**

Each microservice instance **registers itself** with a **Service Registry** (e.g., Eureka, Consul, or Zookeeper) upon startup.

* Contains metadata like:

  * Service name
  * IP address
  * Port
  * Health status

### 2. **Service Discovery**

Other services or clients query the registry to **discover active instances** of a given service.

* **Client-side discovery** (e.g., Netflix Eureka + Ribbon):
  The client asks the registry for service instances and chooses one.

* **Server-side discovery** (e.g., Kubernetes, AWS ALB):
  A load balancer queries the registry and routes requests.

### 3. **Load Balancing**

* Done either **client-side** (e.g., Ribbon, RestTemplate, Feign)
  or **server-side** (e.g., NGINX, Spring Cloud Gateway).
* Helps distribute traffic among healthy instances.

---

## 🕸️ Traditional Apps vs Microservices

| Feature         | Traditional Apps | Microservices          |
| --------------- | ---------------- | ---------------------- |
| Communication   | Static IP / DNS  | Dynamic discovery      |
| Service Scaling | Manual           | Auto-scaled            |
| Load Balancing  | Optional         | Essential              |
| Fault Tolerance | Limited          | Built-in, self-healing |

---

## 🔁 Example: Spring Cloud + Eureka

* **Eureka Server**: Central service registry.
* **Accounts Microservice**: Registers with Eureka.
* **Loans Microservice**: Registers with Eureka.
* **Accounts** can discover and call **Loans** dynamically via service name (e.g., `http://LOANS-SERVICE`).


You're referring to how **traditional load balancers** work — especially in **monolithic** or **early service-oriented architectures (SOA)** — before the rise of containerized microservices with dynamic scaling and discovery.

Here’s a breakdown of **how traditional load balancers work**:

---

## 🏗️ **How Traditional Load Balancers Work**

### 🧭 1. **Clients Use a Generic DNS Name**

Clients (browsers, other services, etc.) don’t need to know the exact location (IP\:port) of backend services. Instead, they access a general DNS like:

```
services.eazybank.com/accounts
services.eazybank.com/loans
services.eazybank.com/cards
```

This DNS resolves to a **load balancer**, not a direct server.

---

### 🎯 2. **DNS Resolves to Load Balancer**

* `services.eazybank.com` points to an IP address managed by a **load balancer**.
* This could be a hardware appliance, cloud load balancer (e.g., AWS ELB), or NGINX/HAProxy software-based.

---

### ⚖️ 3. **Routing & Load Balancing Logic**

The load balancer:

* Uses **routing rules** to forward traffic based on path:

  * `/accounts` → Accounts service
  * `/loans` → Loans service
  * `/cards` → Cards service
* Applies **load balancing strategy** like:

  * Round Robin
  * Least Connections
  * IP Hash

---

### 🩺 4. **Health Checks**

* Load balancer **pings each instance** of a service regularly.
* If a service instance fails, it's **removed** from the routing table temporarily.

---

### 🔁 5. **Failover with Secondary Load Balancer**

* If the **Primary Load Balancer** fails:

  * DNS may be re-pointed (or automatically failover) to a **Secondary Load Balancer**.
  * This ensures **high availability**.

---

## 🧠 Visual Summary

```
Client
  |
  v
DNS (services.eazybank.com)
  |
  v
Primary Load Balancer  <--- Fallback to Secondary if needed
  |
  +--> /accounts --> Accounts Service (multiple instances)
  +--> /loans    --> Loans Service (multiple instances)
  +--> /cards    --> Cards Service (multiple instances)
```

---

## 📌 Limitations in Microservices Context

| Issue                    | Why It's a Problem                                                        |
| ------------------------ | ------------------------------------------------------------------------- |
| Static Routing           | Services scale dynamically; static routing is hard to maintain            |
| Central Point of Failure | If not highly available, the load balancer is a bottleneck                |
| No Service Awareness     | Load balancers don’t understand service metadata or health without config |
| Slower Adaptation        | Load balancers need manual config updates or external scripts             |

---

In **modern microservices**, dynamic service registries (like Eureka, Consul, or Kubernetes DNS) and **client-side load balancing** solve these issues by making service discovery automatic and resilient.

---

## ❌ **Limitations of Traditional Load Balancers**

### 1. 🔁 **Limited Horizontal Scalability & Licensing Costs**

* Traditional load balancers work well with a **fixed number of backend servers**.
* Microservices, on the other hand, scale **dynamically** based on load (auto-scaling).
* Most traditional solutions (like F5 or hardware appliances) are **expensive**, licensed per instance, and don't scale cost-effectively in dynamic environments.

---

### 2. ☠️ **Single Point of Failure & Centralized Chokepoints**

* All traffic flows through the load balancer.
* If the load balancer fails (and no failover is in place), the **entire system can go down**.
* It can become a **bottleneck** under high load.

---

### 3. 🛠️ **Manually Managed Configuration**

* Someone must **manually update routing tables** whenever:

  * A new service instance is added
  * An instance crashes
  * IPs/ports change (common in container orchestration)
* This is **unmanageable** in a dynamic microservices environment.

---

### 4. 🧩 **Not Container- or Cloud-Native Friendly**

* Containers are **ephemeral** — they start, stop, and move across hosts frequently.
* Traditional load balancers were not designed for environments like:

  * Docker Swarm
  * Kubernetes
  * AWS ECS / Fargate
* They **cannot track container lifecycle events** in real time.

---

### 5. 🧱 **Increased Complexity**

* Managing multiple services, versions, environments (dev, stage, prod) through a static routing mechanism becomes **very complex**.
* Traditional LB doesn't handle **service versioning** (e.g., `/v1`, `/v2`) or **service metadata** well.

---

### 6. 🚫 **Lack of Service Awareness**

* Traditional load balancers don’t understand **service registry or discovery mechanisms**.
* They operate at the **network level**, not the **application/service level**.

---

## 🔄 Why It's a Problem in Microservices

| Traditional LB   | Microservices Needs               |
| ---------------- | --------------------------------- |
| Static           | Dynamic & auto-scaled             |
| IP-based routing | Service name-based discovery      |
| Manual config    | Self-registration, auto-discovery |
| Centralized      | Decentralized, fault-tolerant     |
| Stateful         | Stateless and ephemeral instances |

---

## ✅ Modern Alternative

To overcome these limitations, modern microservices use:

* **Service Discovery** (Eureka, Consul, Kubernetes DNS)
* **Client-side Load Balancing** (Ribbon, Spring Cloud LoadBalancer)
* **Service Meshes** (Istio, Linkerd)
* **API Gateways** (Spring Cloud Gateway, Zuul)

Exactly — you've captured the **essence of Service Discovery and Registration** in modern microservice architectures. Let's build on that and organize the core ideas clearly.

---

## 🚀 **What is Service Discovery & Registration?**

In a **microservices architecture**, service instances:

* **Scale dynamically**
* **Crash and recover automatically**
* **Have short lifespans (ephemeral)**
* Are **distributed across networks or nodes**

This makes **tracking the current location (IP\:Port)** of each service **very complex** for clients.

---

## ✅ **Service Discovery & Registration Solves This**

It introduces a **centralized system** to track which services are alive, their locations, and their health.

### 🔗 Key Components:

1. ### 🧠 **Service Registry (Central Server)**

   * A live database of **all running service instances**.
   * Examples: **Netflix Eureka**, **Consul**, **Zookeeper**, **Kubernetes Service Registry**.

2. ### 📝 **Service Registration**

   * Each microservice **registers itself** when it starts.
   * Sends info like:

     * Service name (e.g., `loans-service`)
     * IP & port
     * Metadata (e.g., zone, version)

3. ### ❤️ **Health Checks / Heartbeats**

   * Services send **heartbeat signals** at regular intervals.
   * If the heartbeat fails, the registry **automatically removes** the service instance.
   * Ensures only **healthy services are discoverable**.

4. ### ❌ **Deregistration**

   * When a service shuts down gracefully, it **deregisters itself**.
   * Prevents clients from calling dead endpoints.

5. ### 🔍 **Service Discovery**

   * Clients or other services **query the registry** to get the list of active instances.
   * Used for:

     * **API calls**
     * **Client-side load balancing**
     * **Dynamic routing**

---

## 🔁 Flow Diagram (Text Format)

```
  +-------------+          Register         +------------------+
  |  Service A  | -----------------------> |  Service Registry |
  | (e.g. Loans)|                         |   (e.g. Eureka)    |
  +-------------+                         +------------------+
          |                                       ^
          | Heartbeat                             |
          |-------------------------------------->|
          |                                       |
          | Discovery Request                     |
          |<--------------------------------------|
          | Receives Service B location info      |
          v
  +-------------+
  |  Service B  |
  | (e.g. Cards)|
  +-------------+
```

---

## 🧩 Use Case in Spring Cloud with Eureka

* **Eureka Server** = Central registry
* **Eureka Clients** (Accounts, Loans, Cards services):

  * Register on startup
  * Deregister on shutdown
  * Send heartbeat regularly
* Services call each other using:

  ```
  http://LOANS-SERVICE/api/...
  ```

---

## 📦 Benefits

| Benefit                   | Description                                   |
| ------------------------- | --------------------------------------------- |
| 🔄 Dynamic service lookup | No need to hardcode IPs or ports              |
| ⚖️ Load balancing         | Get a list of instances to distribute traffic |
| ⚠️ Fault tolerance        | Avoid dead services through health checks     |
| 🚀 Scalability            | Auto-discover newly started instances         |


## ⚙️ **Client-Side Load Balancing in Microservices**

### 🔄 **How It Works:**

1. **Service Registration**

   * Each microservice (e.g., `Loans-Service`) registers itself with the **Service Discovery** system (like **Eureka**).
   * It sends **heartbeat signals** at intervals to indicate it’s alive.
   * If a service stops sending heartbeats, its entry is **removed** from the registry.

2. **Service Discovery Cache**

   * When another microservice (e.g., `Accounts-Service`) needs to communicate with `Loans-Service`, it:

     * First checks its **local cache** for the list of available instances.
     * If not found, it fetches from the **Service Discovery** system.

3. **Client-Side Load Balancing**

   * After retrieving the list of service instances, the **client itself** performs **load balancing** using:

     * **Round Robin**
     * **Random**
     * **Latency-based**, etc.
   * The client directly sends the request to the chosen instance.

4. **Periodic Cache Refresh**

   * The local cache of service instances is automatically **refreshed in the background** from the service discovery layer to stay updated with new or removed instances.

---

### 📌 **Key Characteristics:**

| Feature                          | Description                                                                       |
| -------------------------------- | --------------------------------------------------------------------------------- |
| ✅ **Local Caching**              | Clients store service instance data locally to reduce lookup overhead.            |
| ✅ **Direct Invocation**          | Clients call service instances directly, skipping service registry for each call. |
| ✅ **Client-side Load Balancing** | Each client balances its requests independently using its own logic.              |
| 🔁 **Background Sync**           | Service info is kept fresh by periodic sync with the service registry.            |
| ❌ **No Central Load Balancer**   | Each client handles load distribution; there's no central point of routing.       |

---

### 🧠 **Example Flow:**

1. `Accounts-Service` wants to call `Loans-Service`
2. Checks local cache:

   * ✅ If available → pick one instance using round robin → call it.
   * ❌ If not available → query service registry → update cache → pick instance → call it.
3. Registry nodes (e.g., Eureka servers) sync with each other and manage service health via heartbeat.



### ✅ **Step 1: Create Spring Boot Project**

You can generate the project from [https://start.spring.io](https://start.spring.io) with the following:

* **Project:** Maven
* **Spring Boot:** 2.7.x or 3.x (depending on Spring Cloud version)
* **Dependencies:**

  * Spring Boot DevTools (optional)
  * Spring Web
  * Spring Cloud Discovery → *Eureka Server*

Or, manually add the following **Maven dependency**:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
    </dependency>
</dependencies>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2021.0.8</version> <!-- Change as per compatibility -->
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

---

### ✅ **Step 2: Add Configuration in `application.yml` or `application.properties`**

```yaml
# src/main/resources/application.yml
server:
  port: 8070

eureka:
  instance:
    hostname: localhost
  client:
    register-with-eureka: false
    fetch-registry: false
    service-url:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
```

---

### ✅ **Step 3: Enable Eureka Server in Main Class**

```java
// src/main/java/com/example/EurekaServerApplication.java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```

---

### ✅ **Step 4: Run the Application**

Run the application using your IDE or:

```bash
./mvnw spring-boot:run
```

Then open the Eureka Dashboard at:

```
http://localhost:8070
```

You should see a dashboard with no services registered yet.

Here are the **complete steps with code** to register a microservice as a **Eureka Client** in Spring Boot:

---

### ✅ **Step 1: Create a Spring Boot Project**

Go to [https://start.spring.io](https://start.spring.io) and select:

* **Project:** Maven
* **Spring Boot Version:** 2.7.x or 3.x (with compatible Spring Cloud version)
* **Dependencies:**

  * Spring Web
  * Spring Boot DevTools (optional)
  * **Eureka Discovery Client** (spring-cloud-starter-netflix-eureka-client)

Or manually add this to your `pom.xml`:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2021.0.8</version> <!-- Match your Spring Boot version -->
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

---

### ✅ **Step 2: Configure `application.yml`**

```yaml
# src/main/resources/application.yml
server:
  port: 8081

spring:
  application:
    name: accounts-service  # This is the registered service name

eureka:
  instance:
    prefer-ip-address: true
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://localhost:8070/eureka/
```

> Replace `accounts-service` with your actual service name, and `8070` with your Eureka Server port if different.

---

### ✅ **Step 3: Add @EnableDiscoveryClient (Optional)**

As of Spring Boot 2.1+, this annotation is optional when using `spring-cloud-starter-netflix-eureka-client`, but you can still include it:

```java
// src/main/java/com/example/AccountsServiceApplication.java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
// import org.springframework.cloud.client.discovery.EnableDiscoveryClient;

@SpringBootApplication
// @EnableDiscoveryClient  // Optional
public class AccountsServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(AccountsServiceApplication.class, args);
    }
}
```

---

### ✅ **Step 4: Run and Verify**

* Start your **Eureka Server** (on port 8070).
* Start this **Eureka Client** (on port 8081).
* Open your browser and go to:
  👉 `http://localhost:8070`

You should see `ACCOUNTS-SERVICE` listed in the Eureka dashboard.

Great question! Let's understand how **load balancing works with Feign clients** in a **Spring Cloud microservices** setup.

---

### 🔄 **What is Feign Client?**

Feign is a declarative HTTP client in Spring Cloud. Instead of manually writing `RestTemplate` or WebClient code, you define a Java interface and Spring auto-generates the implementation.

---

### ⚖️ **How Load Balancing Works with Feign Client**

In a **Spring Cloud Netflix Eureka + Feign setup**, load balancing is done automatically **via client-side load balancing** using **Spring Cloud LoadBalancer** (previously Ribbon).

#### 🔁 Steps:

1. **Service Registration:**

   * Each instance of a service (e.g., `loans-service`) registers itself to **Eureka Server** with a unique IP and port.

2. **Feign Client Declaration:**

   ```java
   @FeignClient("loans-service")
   public interface LoansFeignClient {
       @GetMapping("/loans/{mobileNumber}")
       ResponseEntity<LoansDto> fetchLoanDetails(@PathVariable String mobileNumber);
   }
   ```

   * Here, `"loans-service"` is the **application name** registered in Eureka (not a host/IP).

3. **Service Discovery & Load Balancing:**

   * When the Feign client is called, Spring Cloud:

     * Looks up all available instances of `loans-service` from **Eureka**.
     * Picks one instance based on the **load balancing strategy** (default is **round-robin**).
     * Sends the request to the selected instance.

4. **Caching:**

   * Feign + LoadBalancer keeps a local cache of service instances to reduce constant Eureka lookups.
   * The cache is periodically refreshed.

---

### 📦 Example in Action

Suppose you have 3 instances of `loans-service`:

* `http://localhost:9001`
* `http://localhost:9002`
* `http://localhost:9003`

When you call:

```java
loansFeignClient.fetchLoanDetails("9999999999");
```

Spring Cloud LoadBalancer will:

* Get the list of 3 instances from Eureka.
* Pick one (e.g., round-robin to port 9002).
* Route the HTTP call to `http://localhost:9002/loans/9999999999`.

---

### ⚙️ **How to Enable Load Balancing**

Spring Boot 2.4+ uses Spring Cloud LoadBalancer by default.

To make it work:

```xml
<!-- Add Feign and Eureka dependencies -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

Enable Feign:

```java
@SpringBootApplication
@EnableFeignClients
public class YourApplication { }
```

---

### ✅ Summary

* Feign + Eureka + LoadBalancer = seamless client-side load balancing.
* Feign calls use **service names** (not IPs).
* Spring resolves those via Eureka and balances requests among available service instances.

Sure! Let's break down **load balancing using Feign client** in Spring Cloud into simple, detailed parts — with examples of how it works under the hood and how you can control it.

---

## 🔹 What is Feign Client?

**Feign Client** is a declarative web service client in Spring Cloud. You define Java interfaces annotated with `@FeignClient`, and Spring will generate the implementation at runtime, which will call REST endpoints.

Example:

```java
@FeignClient(name = "loans-service")
public interface LoansFeignClient {
    @GetMapping("/api/loans")
    ResponseEntity<LoansDto> fetchLoanDetails(@RequestParam String mobileNumber);
}
```

Here, `loans-service` is the **service name registered with Eureka**.

---

## 🔹 How Feign Works with Eureka + Load Balancer

1. **Service Registration**: `loans-service` registers with Eureka on startup.
2. **Feign Client + Eureka**:

   * When `AccountsService` calls `loans-service`, Feign asks Eureka for all available instances of `loans-service`.
3. **Load Balancer**:

   * A load balancing strategy (default: round-robin) picks one instance from the list.
   * Feign then calls the selected instance.

---

## 🔹 Load Balancing Strategies

Spring Cloud uses **Spring Cloud LoadBalancer** behind the scenes with Feign. Here are the common strategies:

### 1. **Round Robin** (default)

* Requests are distributed equally in rotation across instances.
* No external configuration needed.

### 2. **Random**

* Each request goes to a randomly selected instance.
* Useful if you want randomness over fairness.

### 3. **Latency-based** (custom)

* Picks the fastest-responding instance.
* Requires custom implementation (e.g., storing historical response times).

---

## 🔹 How to Customize Load Balancing

### ✅ Step 1: Add Dependencies

Your **`pom.xml`** needs:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-loadbalancer</artifactId>
</dependency>
```

---

### ✅ Step 2: Feign Client Interface

```java
@FeignClient(name = "loans-service", configuration = LoansFeignClientConfig.class)
public interface LoansFeignClient {
    @GetMapping("/api/loans")
    ResponseEntity<LoansDto> fetchLoanDetails(@RequestParam String mobileNumber);
}
```

---

### ✅ Step 3: Custom Load Balancer Configuration

```java
@Configuration
public class LoansFeignClientConfig {

    @Bean
    public ReactorLoadBalancer<ServiceInstance> randomLoadBalancer(Environment environment,
            LoadBalancerClientFactory factory) {
        String name = environment.getProperty(LoadBalancerClientFactory.PROPERTY_NAME);
        return new RandomLoadBalancer(factory.getLazyProvider(name, ServiceInstanceListSupplier.class), name);
    }
}
```

This example uses a **random load balancer**. You can replace `RandomLoadBalancer` with other implementations or custom ones.

Other options include:

* `RoundRobinLoadBalancer`
* `CustomLatencyAwareLoadBalancer` (you need to implement this)

---

### ✅ Step 4: Register Services with Eureka

In **`application.yml`**:

```yaml
eureka:
  client:
    registerWithEureka: true
    fetchRegistry: true
  instance:
    preferIpAddress: true
```

In Eureka server’s dashboard, all service instances will be listed.

---

## 🔹 How It Works Internally

When `fetchLoanDetails()` is called:

1. Spring Cloud Feign intercepts the call.
2. It contacts Eureka to get all instances of `loans-service`.
3. Applies your configured load balancing strategy to pick one instance.
4. Makes an HTTP call to the selected instance's IP/port.

---

## 🔹 Summary Table

| Feature                 | Description                                   |
| ----------------------- | --------------------------------------------- |
| Feign Client            | Declarative REST client                       |
| Eureka                  | Service registry                              |
| Load Balancer           | Selects one service instance from many        |
| Default Strategy        | Round-robin                                   |
| Custom Strategy Example | Random (with `RandomLoadBalancer`)            |
| Benefits                | Fault-tolerance, scalability, zero manual IPs |

Great question! Let’s break it down clearly and simply.

---

## 🧭 **ROUTING & CROSS-CUTTING CONCERNS in Microservices**

**Source: eazybytes – Challenge 6**

---

## ❓ **Problem Statement**

In a microservices architecture, we often face **three key challenges**:

---

### 1️⃣ **Single Entry Point Challenge**

> ✅ **How do we maintain a single entry point into our microservices network?**

🔍 **Problem**:
Clients shouldn't need to know the location or number of services. Imagine a mobile app trying to talk to 10 different microservices—this is complex, error-prone, and tightly coupled.

🎯 **Solution**:
Introduce a **Gateway (Edge Server)** that acts as the **single entry point** for all client requests.

---

### 2️⃣ **Cross-Cutting Concerns Challenge**

> ✅ **How do we handle common logic across services like logging, security, and tracing?**

🔍 **Problem**:
Each microservice may need similar functionalities like:

* Logging
* Authentication & Authorization
* Metrics
* Tracing
* Rate Limiting

Writing this logic in every microservice causes **code duplication** and **inconsistencies**.

🎯 **Solution**:
Move these responsibilities to the **Edge Server**, where such logic can be **centralized and consistently applied**.

---

### 3️⃣ **Dynamic Routing Challenge**

> ✅ **How do we route requests based on custom rules (headers, parameters, etc.)?**

🔍 **Problem**:
We might need to:

* Route requests based on version (e.g., `v1`, `v2`)
* Forward requests based on user roles
* Use headers or parameters to decide target services

🎯 **Solution**:
Use a **gateway with dynamic routing capabilities**, which can inspect and route based on headers, URIs, or other criteria.

---

## 🚀 **Solution: Use an Edge Server (API Gateway)**

A modern **Edge Server** (like **Spring Cloud Gateway**, **Netflix Zuul**, or **Kong**) can address all of these challenges:

### ✅ Features Provided:

| Feature              | Description                                                                                     |
| -------------------- | ----------------------------------------------------------------------------------------------- |
| **Routing**          | Forward requests to the appropriate microservice based on URI, headers, parameters, etc.        |
| **Security**         | Centralized authentication & authorization (e.g., OAuth2, JWT).                                 |
| **Logging**          | Centralized request and response logging.                                                       |
| **Tracing**          | Add correlation IDs and forward them to trace requests across services (e.g., Sleuth + Zipkin). |
| **Rate Limiting**    | Protect services from being overwhelmed.                                                        |
| **Retry / Fallback** | Automatically retry failed requests or provide fallback responses.                              |



## 🧩 Summary

| Challenge                 | Solved By                                         |
| ------------------------- | ------------------------------------------------- |
| 🧭 Single entry point     | API Gateway (Edge Server)                         |
| 🧰 Cross-cutting concerns | Centralized filters & policies in gateway         |
| 🔀 Custom routing         | Dynamic routing rules (header, path, query param) |

Here's a clear and structured breakdown of the **important tasks performed by an API Gateway** based on your list:

---

## ✅ **Key Responsibilities of an API Gateway**

An **API Gateway** acts as a **single entry point** into your microservices system and performs a variety of cross-cutting, routing, and system management functions.

---

### 1️⃣ **Request Validation**

* **Purpose**: Check if incoming requests are valid.
* **Includes**:

  * Validate required headers
  * Validate API keys or tokens
  * Validate request format (JSON/XML)
* **Example**: Reject requests without a `Content-Type: application/json` header.

---

### 2️⃣ **Authentication (AuthN)**

* **Purpose**: Verify the identity of the caller.
* **How**:

  * Validate tokens (JWT, OAuth2)
  * Integrate with identity providers (Keycloak, Auth0)

---

### 3️⃣ **Authorization (AuthZ)**

* **Purpose**: Ensure that the caller has permission to access the resource.
* **How**:

  * Role-based access control (RBAC)
  * Scope-based permissions

---

### 4️⃣ **Rate Limiting**

* **Purpose**: Control the number of requests a client can make in a time window.
* **How**:

  * Prevent abuse
  * Protect backend services
* **Example**: Max 100 requests per minute per IP.

---

### 5️⃣ **Circuit Breaker & Exception Handling**

* **Purpose**:

  * **Circuit Breaker**: Prevent cascading failures if a service is down.
  * **Exception Handling**: Return consistent error responses.
* **Tools**: Resilience4j, Hystrix (deprecated)

---

### 6️⃣ **Protocol Conversion**

* **Purpose**: Convert between protocols like:

  * HTTP ↔ gRPC
  * WebSocket ↔ HTTP
* **Why**: So clients can speak one protocol while services use another.

---

### 7️⃣ **Request/Response Modification**

* **Purpose**:

  * Add/Remove headers
  * Transform response body
  * Inject trace IDs (e.g., `eazybank-correlation-id`)

---

### 8️⃣ **Service Discovery & Dynamic Routing**

* **Purpose**:

  * Dynamically route requests to instances registered in service registry (e.g., Eureka, Consul)
* **How**:

  * Use service name instead of hardcoded URLs

---

### 9️⃣ **Caching, Logging & Monitoring**

* **Caching**:

  * Store responses temporarily to reduce load (e.g., Redis, Hazelcast)
* **Logging**:

  * Log request/response data for audit & debugging
* **Monitoring**:

  * Track metrics (latency, error rates)
  * Tools: Prometheus, Grafana, ELK, Zipkin, Jaeger

---

## 🔁 Full Flow Summary

```
Client Request
    ↓
[API Gateway]
    → Validate Request
    → AuthN / AuthZ
    → Rate Limit
    → Circuit Breaker / Exception Handling
    → Convert Protocol (if needed)
    → Modify Request/Response
    → Discover Service & Route
    → Log, Monitor, Cache
    ↓
Target Microservice
```

---

## 📌 Tools Often Used

| Task              | Tool                                        |
| ----------------- | ------------------------------------------- |
| Rate Limiting     | Redis, Bucket4j                             |
| AuthN/AuthZ       | Spring Security, OAuth2                     |
| Monitoring        | Prometheus + Grafana                        |
| Logging           | ELK stack (Elasticsearch, Logstash, Kibana) |
| Service Discovery | Netflix Eureka, Consul                      |
| Circuit Breaking  | Resilience4j                                |

Here are the **detailed notes** based on your input about **Spring Cloud Gateway**, explained in a concise and structured way:

---

## 📘 **Spring Cloud Gateway – Overview (eazy bytes)**

**Spring Cloud Gateway** is a powerful, modern, and **reactive API gateway** built on top of **Spring WebFlux**. It serves as a **gateway/entry point** for all client requests into a microservices-based architecture.

---

### ✅ **Key Features of Spring Cloud Gateway**

| Feature                     | Description                                                                                                                   |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Edge Service**            | Acts as the first line of contact for all requests entering the system (Edge Service).                                        |
| **Reactive & Non-blocking** | Built using **Spring WebFlux** and **Project Reactor**, which makes it **non-blocking** and suitable for handling high loads. |
| **Easy to Set Up**          | Looks and behaves like a normal Spring Boot app — familiar and simple for Spring developers.                                  |
| **Smart Routing**           | Can inspect requests and route them **dynamically or statically** based on:                                                   |

* Path
* Query parameters
* Request headers (like API version)
* Method, etc. |
  \| **Sticky Sessions** | Supports session-based routing when needed. |
  \| **Circuit Breaker Support** | Can easily integrate with **Resilience4j** for fault-tolerance. |
  \| **Service Discovery** | Integrates with **Eureka**, **Consul**, etc., for dynamic routing to service instances. |
  \| **Better Alternative to Zuul** | Outperforms Zuul (1.x) in speed, scalability, and extensibility. |
  \| **Central Policy Enforcement** | Acts as a **Policy Enforcement Point (PEP)** for:
* Authentication and Authorization
* Request filtering
* Logging, tracing, and more |

---

### 📍 **Typical Use Case in Microservices**

```
Client (Web/App/Postman)
        ↓
 [Spring Cloud Gateway]
        ↓
 Routes Requests To →
    ↳ Accounts Service
    ↳ Loans Service
    ↳ Cards Service
```

---

### 🧠 **Why Use Spring Cloud Gateway?**

* ✅ Centralized Routing Logic
* ✅ Enforce cross-cutting concerns like security and logging in one place
* ✅ Minimize the number of public endpoints exposed directly
* ✅ Improve security posture by avoiding direct service exposure
* ✅ Scalable and performant for modern, reactive systems

---

### 🔧 **Capabilities Summary (Tasks Gateway Can Do)**

| Task                             | Example                                            |
| -------------------------------- | -------------------------------------------------- |
| ✅ Static & Dynamic Routing       | Route based on path, headers, or parameters        |
| ✅ Authentication & Authorization | OAuth2, JWT integration                            |
| ✅ Load Balancing                 | With Netflix Eureka or Spring Cloud LoadBalancer   |
| ✅ Rate Limiting                  | Protects services from overuse                     |
| ✅ Logging & Tracing              | Centralized logging, headers like `correlation-id` |
| ✅ Protocol Conversion            | HTTP ↔ WebSocket if needed                         |
| ✅ Request/Response Manipulation  | Add/modify headers, payload transformation         |
| ✅ Fallback Support               | Circuit breakers with fallback mechanisms          |

Here's a detailed explanation of the **Spring Cloud Gateway Internal Architecture** based on your diagram and text:

---

## 🧠 **Spring Cloud Gateway – Internal Architecture** (Eazy Bytes)

Spring Cloud Gateway acts as the **entry point** to your system, managing **routing**, **filtering**, and **policy enforcement** before requests reach microservices. Below is how the internal flow works:

---

### 🧾 **Step-by-Step Request Flow**

```plaintext
1. Client sends a request
2. Gateway Handler Mapping finds the correct route (based on predicates)
3. If matched:
   → Pre-filters run
   → Request forwarded to target microservice
4. Microservice processes and sends response
5. Post-filters run on the response
6. Response returned to the client
```

---

### 🔁 **Detailed Components**

| 🔷 Component                | 📘 Description                                                                                                                                                               |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Client**                  | A web/mobile app or another service that makes HTTP calls to the gateway.                                                                                                    |
| **Gateway Handler Mapping** | It holds all routing configurations. Responsible for finding the right route for a request.                                                                                  |
| **Predicates**              | **Conditions** defined in the route config that determine **if a request matches a route**.<br>Examples: Path, Header, Method, Query Parameter, etc.                         |
| **Pre Filters**             | Executed **before the request** is forwarded to the microservice.<br>Common tasks: Authentication, Logging, Modifying headers, Rate limiting.                                |
| **Microservice**            | The actual backend service (like Accounts, Loans, etc.) that processes the business logic.                                                                                   |
| **Post Filters**            | Executed **after the response** is returned from the microservice but **before going to the client**.<br>Common tasks: Response logging, Adding headers, Modifying response. |

---

### 🔍 **Visualized Flow**

```plaintext
          ┌────────────┐
          │   CLIENT   │
          └─────┬──────┘
                │
                ▼
    ┌──────────────────────────────┐
    │  Spring Cloud Gateway        │
    │  ┌────────────────────────┐  │
    │  │ Gateway Handler Mapping│  │
    │  └────────┬───────────────┘  │
    │           ▼                  │
    │     Route Predicates         │ <─ Matches?
    │           │                  │
    │           ▼                  │
    │       Pre-Filters            │ ← Modify request, log, auth, etc.
    │           │                  │
    │           ▼                  │
    │     Forward to service ──────┼────► MICROSERVICE
    │           │                  │
    │           ▼                  │
    │       Post-Filters           │ ← Modify response, log, headers
    │           │                  │
    │           ▼                  │
    └───────────┬──────────────────┘
                ▼
             RESPONSE
                │
                ▼
          ┌────────────┐
          │   CLIENT   │
          └────────────┘
```

---

### 🧩 **Common Use Cases of Filters**

| Filter Type     | Use Cases                                                                                                              |
| --------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Pre-filter**  | - Validate Auth Token<br>- Add trace headers (e.g. correlation-id)<br>- Modify request path or body<br>- Rate limiting |
| **Post-filter** | - Add response headers<br>- Modify response<br>- Log response data<br>- Metrics and tracing                            |

Here are the **step-by-step instructions with explanations and comments** for creating a **Spring Cloud Gateway** using **Spring Boot + Eureka**:

---

## 🚀 Steps to Create a Spring Cloud Gateway (Eazy Bytes Style)

---

### ✅ **Step 1: Set Up the Spring Boot Project**

Create a new project using [Spring Initializr](https://start.spring.io/) with the following dependencies:

```xml
<!-- Add in your pom.xml -->
<dependencies>
  <!-- Spring Boot Web + Gateway -->
  <dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
  </dependency>

  <!-- Eureka Client -->
  <dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
  </dependency>

  <!-- Spring Config Client (optional) -->
  <dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
  </dependency>
</dependencies>
```

---

### ✅ **Step 2: Add Configurations in `application.yml`**

```yaml
spring:
  application:
    name: "gatewayserver"  # 👈 This is the name of the Spring Boot application (used by Eureka & Actuator)

  config:
    import: "optional:configserver:http://localhost:8071/"  
    # 👈 This tells Spring Boot to optionally fetch external configuration from Spring Cloud Config Server

  cloud:
    gateway:
      discovery:
        locator:
          enabled: false  # 👈 Service discovery routing is turned off (routes must be defined manually)
          lowerCaseServiceId: true  # 👈 If enabled, converts service IDs to lowercase for consistency

management:
  endpoints:
    web:
      exposure:
        include: "*"  # 👈 Expose all actuator endpoints over HTTP (e.g., /actuator/health, /actuator/gateway)

  endpoint:
    gateway:
      access: unrestricted  # 👈 Allows unrestricted access to the `/actuator/gateway` endpoint

  info:
    env:
      enabled: true  # 👈 Allows exposing environment info at `/actuator/info`

info:
  app:
    name: "gatewayserver"  # 👈 Application name metadata shown on `/actuator/info`
    description: "Eazy Bank Gateway Server Application"  # 👈 Description for the app
    version: "1.0.0"  # 👈 Version for display in actuator/info

logging:
  level:
    com:
      eazybytes:
        gatewayserver: DEBUG  # 👈 Enables debug-level logs for your application's package

```

> 📝 This config:
>
> * Registers the gateway with Eureka
> * Enables dynamic routing via service discovery (`discovery.locator.enabled=true`)

---

### ✅ **Step 3: Create Routing Configuration via `RouteLocatorBuilder`**

Here’s your `RouteLocator` bean method with **detailed comments** explaining what each part does in a Spring Cloud Gateway configuration:

```java
@Bean
public RouteLocator eazyBankRouteConfig(RouteLocatorBuilder routeLocatorBuilder) {
    return routeLocatorBuilder.routes()

        // Route all requests starting with /eazybank/accounts/** to the ACCOUNTS service
        .route(p -> p.path("/eazybank/accounts/**")
            // Filters applied to the request
            .filters(f -> f
                // Rewrite the path by removing the prefix and forwarding only the inner segment
                // Example: /eazybank/accounts/123 -> /123
                .rewritePath("/eazybank/accounts/(?<segment>.*)", "/${segment}")
                // Adds a response header to track response time
                .addResponseHeader("X-Response-Time", LocalDateTime.now().toString()))
            // Load balances the request to the service with name ACCOUNTS registered in Eureka
            .uri("lb://ACCOUNTS"))

        // Route all requests starting with /eazybank/loans/** to the LOANS service
        .route(p -> p.path("/eazybank/loans/**")
            .filters(f -> f
                .rewritePath("/eazybank/loans/(?<segment>.*)", "/${segment}")
                .addResponseHeader("X-Response-Time", LocalDateTime.now().toString()))
            .uri("lb://LOANS"))

        // Route all requests starting with /eazybank/cards/** to the CARDS service
        .route(p -> p.path("/eazybank/cards/**")
            .filters(f -> f
                .rewritePath("/eazybank/cards/(?<segment>.*)", "/${segment}")
                .addResponseHeader("X-Response-Time", LocalDateTime.now().toString()))
            .uri("lb://CARDS"))

        // Build the route configuration
        .build();
}
```

---

### ✅ What This RouteLocator Does:

| Feature                  | Description                                                                        |
| ------------------------ | ---------------------------------------------------------------------------------- |
| `path(...)`              | Matches request paths (e.g., `/eazybank/accounts/**`)                              |
| `rewritePath(...)`       | Removes the service prefix before forwarding the request                           |
| `addResponseHeader(...)` | Adds a timestamp header in the response                                            |
| `uri("lb://SERVICE")`    | Forwards the request using **Eureka load-balancing** to the specified service name |
| `.build()`               | Finalizes the route definitions                                                    |

---

### ✅ **Step 4: Run and Test**

Run the application using:

```
./mvnw spring-boot:run
```

Then access services via:

```
http://localhost:8072/eazybank/accounts/fetch
http://localhost:8072/eazybank/loans/fetch
http://localhost:8072/eazybank/cards/fetch
```

> ☑️ These requests will be routed dynamically via Eureka to their respective services.

---

### 🎯 Summary

| Task                             | What It Does                                                |
| -------------------------------- | ----------------------------------------------------------- |
| `spring-cloud-starter-gateway`   | Sets up the gateway                                         |
| `discovery.locator.enabled=true` | Enables automatic route discovery from Eureka               |
| `RouteLocatorBuilder`            | Allows manual, customized route definitions                 |
| `rewritePath()`                  | Removes prefix like `/eazybank/accounts/` before forwarding |
| `uri("lb://SERVICE")`            | Uses Eureka load balancing to call services                 |
| `addResponseHeader()`            | Adds metadata to response for observability                 |

---
### ✅ What is a **Correlation ID**?

A **Correlation ID** is a **unique identifier** (usually a UUID) assigned to each **client request** when it enters a distributed system (like a microservices architecture). It helps **track and trace the lifecycle** of a request as it passes through multiple services.

---

### 🔍 Why is Correlation ID Needed?

In a **monolithic** application, you can easily trace a request through logs.
But in **microservices**, one user request may go through:

```
Client → API Gateway → Service A → Service B → Service C → Response
```

If there’s an error or you want to debug what happened, it’s very hard to **connect the logs** from each service — unless you have a **common trace identifier**.

💡 That’s where the **correlation ID** helps!

---

### 🛠️ What Does It Do?

* **Uniquely tags** a request across the system
* **Passes that ID** between services via HTTP headers
* **Logs include the correlation ID**, so you can search for it in your logging system (like ELK, Splunk, etc.)
* Helps in:

  * **Debugging**
  * **Monitoring**
  * **Auditing**
  * **Tracing**
  * **Performance analysis**

---

### 🧱 How it Works in Your Spring Cloud Gateway Example

1. **Incoming Request** → API Gateway checks if `eazybank-correlation-id` is present:

   * If **yes**, uses it
   * If **no**, creates a new UUID

2. This ID is:

   * **Added to the request** header
   * **Logged** in the gateway and downstream microservices
   * **Returned in the response**, so the client knows the request ID

3. If something breaks (like service timeout), you can:

   * Search all logs using this correlation ID
   * Quickly find out where and why the issue happened

---



## 🔧 `FilterUtility.java`

```java
@Component
public class FilterUtility {

    // Custom header name for tracing
    public static final String CORRELATION_ID = "eazybank-correlation-id";

    // Retrieves the correlation ID from incoming request headers
    public String getCorrelationId(HttpHeaders requestHeaders) {
        if (requestHeaders.get(CORRELATION_ID) != null) {
            // If header is present, return the first value
            List<String> requestHeaderList = requestHeaders.get(CORRELATION_ID);
            return requestHeaderList.stream().findFirst().get();
        } else {
            // If not present, return null
            return null;
        }
    }

    // Sets a new request header on the current request
    public ServerWebExchange setRequestHeader(ServerWebExchange exchange, String name, String value) {
        return exchange.mutate()
                .request(exchange.getRequest().mutate().header(name, value).build())
                .build();
    }

    // Specifically sets the correlation ID header
    public ServerWebExchange setCorrelationId(ServerWebExchange exchange, String correlationId) {
        return this.setRequestHeader(exchange, CORRELATION_ID, correlationId);
    }
}
```

### ✅ **Why?**

This utility ensures the correlation ID can be:

* **Read from the incoming request**
* **Set on requests** before forwarding to downstream services
* **Reused** in other filters or logs for traceability

---

## 🌐 `RequestTraceFilter.java` — **Global Pre-Filter**

```java
@Order(1) // Ensure this runs early in the filter chain
@Component
public class RequestTraceFilter implements GlobalFilter {

    private static final Logger logger = LoggerFactory.getLogger(RequestTraceFilter.class);

    @Autowired
    FilterUtility filterUtility;

    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        HttpHeaders requestHeaders = exchange.getRequest().getHeaders();

        // If a correlation ID is present, log it
        if (isCorrelationIdPresent(requestHeaders)) {
            logger.debug("eazyBank-correlation-id found in RequestTraceFilter : {}",
                    filterUtility.getCorrelationId(requestHeaders));
        } else {
            // If not, generate a new UUID and add it to the request
            String correlationID = generateCorrelationId();
            exchange = filterUtility.setCorrelationId(exchange, correlationID);
            logger.debug("eazyBank-correlation-id generated in RequestTraceFilter : {}", correlationID);
        }

        // Continue processing the request
        return chain.filter(exchange);
    }

    // Check if correlation ID is present
    private boolean isCorrelationIdPresent(HttpHeaders requestHeaders) {
        return filterUtility.getCorrelationId(requestHeaders) != null;
    }

    // Generate a unique correlation ID
    private String generateCorrelationId() {
        return java.util.UUID.randomUUID().toString();
    }
}
```

### ✅ **Why?**

* This **pre-filter** ensures that **every request** entering the system has a unique `eazybank-correlation-id`.
* Useful for **tracing requests across microservices**, especially during logging or debugging.
* Prevents missing IDs from causing errors in downstream services.

---

## 🌐 `ResponseTraceFilter.java` — **Global Post-Filter**

```java
@Configuration
public class ResponseTraceFilter {

    private static final Logger logger = LoggerFactory.getLogger(ResponseTraceFilter.class);

    @Autowired
    FilterUtility filterUtility;

    // A GlobalFilter bean that modifies the response after execution
    @Bean
    public GlobalFilter postGlobalFilter() {
        return (exchange, chain) -> {
            return chain.filter(exchange).then(Mono.fromRunnable(() -> {
                HttpHeaders requestHeaders = exchange.getRequest().getHeaders();
                String correlationId = filterUtility.getCorrelationId(requestHeaders);

                // Log and propagate correlation ID in the response
                logger.debug("Updated the correlation id to the outbound headers: {}", correlationId);
                exchange.getResponse().getHeaders().add(FilterUtility.CORRELATION_ID, correlationId);
            }));
        };
    }
}
```

### ✅ **Why?**

* This **post-filter** ensures that the correlation ID is added to the **response headers**, allowing:

  * Clients to use it for **debugging**, **monitoring**, or **troubleshooting**.
  * Better **end-to-end visibility** across the request/response lifecycle.

---

## 🔚 Summary

| Component             | Purpose                                                                |
| --------------------- | ---------------------------------------------------------------------- |
| `FilterUtility`       | Central utility to get/set correlation ID in request/response          |
| `RequestTraceFilter`  | Ensures every incoming request has a correlation ID (generates if not) |
| `ResponseTraceFilter` | Adds the correlation ID to outbound responses for traceability         |

This pattern is a **best practice** in microservices architecture to track individual requests as they pass through multiple services—especially helpful for **logging**, **error tracking**, and **distributed tracing**.

