# spring-rest-sakila

Sakila REST API Service (Sample Project)

![Gradle Build](https://github.com/codejsha/spring-rest-sakila/actions/workflows/gradle.yml/badge.svg)

[English](README.md) | [Korean](README_ko-KR.md)

This REST API service provides access to the [Sakila database](https://dev.mysql.com/doc/sakila/en/), which is a sample database provided by MySQL for learning and testing purposes. The Sakila database models a DVD rental store company, includes data about films, actors, customers, rentals, and more.

This service provides a simple way to perform CRUD(Create, Read, Update, Delete) operations on the Sakila database. It also provides endpoints to perform more complex queries.

Microservices version is go to: https://github.com/codejsha/sakila-microservices

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Libraries and Plugins](#libraries-and-plugins)
  - [External MySQL database](#external-mysql-database)
- [Installation](#installation)
  - [Clone Repository](#clone-repository)
  - [Configure Database Connection Settings](#configure-database-connection-settings)
  - [Configure Application Settings](#configure-application-settings)
  - [Build Project](#build-project)
  - [Run Application](#run-application)
- [API Documentation](#api-documentation)
  - [Endpoints](#endpoints)
  - [References](#references)
  - [OpenAPI/Swagger](#openapiswagger)
  - [Postman](#postman)
- [Observability](#observability)
- [Sample Data](#sample-data)

## Getting Started

### Requirements

- Java 17
- Gradle 7
- MySQL 8

### Libraries and Plugins

For a complete list, see the `gradle/libs.versions.toml` file.

- Spring Boot Web
- Spring Data JPA
- Spring HATEOAS
- Spring REST Docs
- Lombok
- Querydsl
- MapStruct

### External MySQL database

An external MySQL database is required to run the application. The external database can be run as a [MySQL docker](https://hub.docker.com/_/mysql) container or as on-premises process ([MySQL Community Downloads](https://dev.mysql.com/downloads/)). After installation, follow the [Sakila database](https://dev.mysql.com/doc/sakila/en/) official guide to create the database structure and populate the data. See the link for examples of configuring your environment: https://github.com/codejsha/infrastructure-examples/tree/main/mysql

## Installation

### Clone Repository

```bash
# GitHub CLI
gh repo clone codejsha/spring-rest-sakila
# Git CLI
git clone https://github.com/codejsha/spring-rest-sakila.git
```

### Configure Database Connection Settings

Before you can use the Sakila REST API Service, you need to configure the database connection settings. The database connection settings are defined in the `application.yaml` file. The default settings are as follows:

```yaml
# application.yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/sakila
    username: sakila
    password: sakila
```

### Configure Application Settings

The default URL settings for the application API endpoint are as follows:

```yaml
# application.yaml
server:
  port: 8080
  servlet:
    context-path: /api/v1
...

app:
  uri:
    scheme: http
    host: localhost
    port: ${server.port}
```

```kotlin
// build.gradle.kts
openapi3 {
    this.setServer("http://localhost:8080/api/v1")
    // ...
}

postman {
    baseUrl = "http://localhost:8080/api/v1"
    // ...
}
```

### Build Project

```bash
cd spring-rest-sakila
bash ./gradlew build
```

### Run Application

```bash
bash ./gradlew bootRun
```

## API Documentation

### Endpoints

The Sakila REST API Service exposes the following some endpoints. Each endpoint supports CRUD operations.

- Actors: `/api/v1/actors`
- Customers: `/api/v1/customers`
- Films: `/api/v1/films`
- Payments: `/api/v1/payments`
- Rentals: `/api/v1/rentals`
- Reports: `/api/v1/reports`
- Staffs: `/api/v1/staffs`
- Stores: `/api/v1/stores`

### References

API references are generated by Asciidoctor in Spring REST Docs.

### OpenAPI/Swagger

The OpenAPI specification file `openapi3.yaml` can be rendered using the Swagger UI. The specification is generated by Spring REST Docs.

### Postman

The Postman collection file `postman-collection.json` contains the endpoints and examples of requests and responses. The collection is generated by Spring REST Docs.

## Observability

The application provides observability features using Spring Boot Actuator and Micrometer.

- Actuator: `/api/v1/actuator`
- Prometheus: `/api/v1/actuator/prometheus`

```yaml
# application.yaml
management:
  endpoints:
    web:
      exposure:
        include: "health,prometheus"
    jmx:
      exposure:
        exclude: "*"
```

## Sample Data

The sample data is from [MySQL Sakila sample database](https://dev.mysql.com/doc/sakila/en/). It is a relational database model for a DVD rental store which contains data related to films, actors, customers, rentals, and more. The database also serves views, stored procedures, and triggers.
