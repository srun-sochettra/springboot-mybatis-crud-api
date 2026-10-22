# Spring Boot MyBatis CRUD API

**A PostgreSQL-backed coursework API exploring annotated SQL, layered services and JWT authentication.**

Employee, product and category CRUD endpoints use MyBatis mapper interfaces rather than JPA. Authentication code registers database users, hashes passwords with BCrypt and issues signed JWTs. This is a learning project, not a production-ready employee or inventory service.

## Source-backed features

- Controller/service/mapper separation with constructor injection.
- SQL annotations, bound values and generated-key mapping.
- Transactional employee, product and category services.
- Login and registration with username, password and role data.
- JSON envelopes containing success, message and data.

The POM declares Java 17, Spring Boot 4.0.5, MyBatis starter 4.0.1, Springdoc 2.8.0 and JJWT 0.12.6. The wrapper selects Maven 3.9.14. These are declarations, not a verified compatible dependency set.

## Important: local demonstration only

The security configuration permits all `/api/v1/auth/**` requests, including `/register-admin`. That controller path registers an ADMIN and returns a token. The declared role restrictions therefore do not establish controlled administrator provisioning.

Database credentials and a JWT signing key are committed in application.properties. Rotate them if used anywhere real. Their values are not reproduced here, and this documentation does not remove them from source or history. Review [SECURITY.md](SECURITY.md) before running or publishing.

## Setup boundaries

Use JDK 17, the supplied wrapper and an isolated PostgreSQL database. The configured database name is basic-spring-boot. Review application.properties and provide private connection/signing configuration before execution; do not reuse committed values.

The mapper SQL expects employees, products, categories and users tables. The supplied script/scheme.sql and script/data.sql are empty. No executable schema, migrations or seed accounts are supplied, so this export is not a complete fresh-database setup. Determine column types, defaults, keys and constraints deliberately rather than treating model fields as a complete DDL contract.

Suggested commands from the repository root, after resolving configuration and schema prerequisites:

```powershell
.\mvnw.cmd spring-boot:run
```

POSIX shell equivalent:

```sh
sh mvnw spring-boot:run
```

Initial use may download Maven and dependencies. No server.port is set in the supplied properties. No startup or HTTP request was performed here. The old README lists Swagger paths `/swagger-ui/index.html` and `/v3/api-docs`; dependency compatibility and actual availability require local verification.

## Endpoint map

Each resource prefix—`/api/v1/employees`, `/api/v1/products`, `/api/v1/categories`—defines:

| Method | Suffix | Controller behaviour |
| --- | --- | --- |
| GET | `/all` | List records |
| GET | `/{id}` | Read, or return 404 |
| POST | `/add` | Insert and return HTTP 200 |
| PUT | `/{id}` | Update, or return 404 |
| DELETE | `/{id}` | Read then delete, or return 404 |

Authentication routes under `/api/v1/auth` are POST `/login`, `/register` and `/register-admin`. Registration success returns HTTP 200. These routes are documented as implemented, not endorsed as safe provisioning interfaces.

SecurityConfig declares public resource GETs, USER/ADMIN POST and PUT, and ADMIN-only DELETE. JwtFilter reads a Bearer token and creates role authorities from its claims. No logout, refresh-token or revocation workflow is supplied. InMemoryUserConfig lacks a configuration annotation; its sample users should not be advertised as the active database login accounts.

## Architecture and integration concerns

- [ProductRepo.java](src/main/java/com/example/basicspringboot/repository/ProductRepo.java) illustrates annotated SQL and generated IDs.
- [AuthServiceImp.java](src/main/java/com/example/basicspringboot/service/imp/AuthServiceImp.java) performs database lookup, BCrypt checks and token issuance.
- [SecurityConfig.java](src/main/java/com/example/basicspringboot/config/SecurityConfig.java) declares request permissions.
- [application.properties](src/main/resources/application.properties) contains database/JWT configuration and security TRACE logging.

AppConfig declares a productService bean while ProductServiceImp is also a service component. Two configurations declare passwordEncoder and corsConfigurationSource beans, with bean overriding enabled. Review the effective wiring rather than assuming every configuration is simultaneously active. CORS declarations also differ across configuration and controllers.

Requests bind directly to model objects without supplied field-validation annotations or a global exception handler. Salary and price use Double. No pagination, ownership checks or schema constraints are established by these model declarations.

## Checks

Suggested local commands:

```powershell
.\mvnw.cmd test
.\mvnw.cmd package
```

POSIX equivalents use `sh mvnw test` and `sh mvnw package`. The supplied test is a contextLoads smoke test, not CRUD, JWT or role-enforcement coverage. Database prerequisites and bean wiring can affect context startup.

This refresh parsed the POM and inspected source/configuration. No dependency resolution, compilation, Maven test/package, database access or server execution was performed. See [CONTRIBUTING.md](CONTRIBUTING.md) and [refresh notes](docs/repository-refresh.md).

## Licence

No root project licence file is supplied. Maven wrapper notices do not establish a licence for the application. This refresh assigns none.
