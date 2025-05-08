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

