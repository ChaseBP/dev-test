Alright — we’ll go **one by one**, starting with:

# ✅ 1. Passport Automation System (Spring Boot – Exam Ready)

👉 Goal: **Super simple CRUD app** (Add + View Passport records)
👉 Stack: Spring Boot + Thymeleaf + H2 DB (no setup needed → plug & play)

---

# 📁 Project Structure (minimal)

```
passport-system/
 ├── src/main/java/com/example/passport/
 │    ├── PassportApplication.java
 │    ├── Passport.java
 │    ├── PassportRepository.java
 │    ├── PassportController.java
 │
 ├── src/main/resources/templates/
 │    ├── form.html
 │    ├── list.html
 │
 ├── src/main/resources/application.properties
 ├── pom.xml (Maven)
 ├── build.gradle (Gradle)
```

---

# 🧠 1. Main Application

```java
package com.example.passport;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class PassportApplication {
    public static void main(String[] args) {
        SpringApplication.run(PassportApplication.class, args);
    }
}
```

---

# 🧾 2. Entity Class

```java
package com.example.passport;

import jakarta.persistence.*;

@Entity
public class Passport {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;
    private String nationality;

    public Passport() {}

    public Passport(String name, String nationality) {
        this.name = name;
        this.nationality = nationality;
    }

    public Long getId() { return id; }
    public String getName() { return name; }
    public String getNationality() { return nationality; }

    public void setName(String name) { this.name = name; }
    public void setNationality(String nationality) { this.nationality = nationality; }
}
```

---

# 🗃️ 3. Repository

```java
package com.example.passport;

import org.springframework.data.jpa.repository.JpaRepository;

public interface PassportRepository extends JpaRepository<Passport, Long> {
}
```

---

# 🎮 4. Controller

```java
package com.example.passport;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class PassportController {

    private final PassportRepository repo;

    public PassportController(PassportRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("passport", new Passport());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Passport passport) {
        repo.save(passport);
        return "redirect:/list";
    }

    @GetMapping("/list")
    public String list(Model model) {
        model.addAttribute("list", repo.findAll());
        return "list";
    }
}
```

---

# 🌐 5. HTML – Form (`form.html`)

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Passport Form</h2>

    <form action="/save" method="post" th:object="${passport}">
      Name: <input type="text" th:field="*{name}" /><br /><br />
      Nationality: <input type="text" th:field="*{nationality}" /><br /><br />
      <button type="submit">Submit</button>
    </form>

    <a href="/list">View All</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Passport Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Nationality</th>
      </tr>

      <tr th:each="p : ${list}">
        <td th:text="${p.id}"></td>
        <td th:text="${p.name}"></td>
        <td th:text="${p.nationality}"></td>
      </tr>
    </table>

    <a href="/">Add New</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>passport</artifactId>
    <version>1.0</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.0</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
        </dependency>
    </dependencies>
</project>
```

---

# 📦 9. Gradle (build.gradle)

```gradle
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.0'
    id 'io.spring.dependency-management' version '1.1.0'
}

group = 'com.example'
version = '1.0'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    runtimeOnly 'com.h2database:h2'
}
```

---

# ▶️ How to Run (Exam Ready Steps)

### Maven

```
mvn spring-boot:run
```

### Gradle

```
gradle bootRun
```

---

# 🌐 Open in Browser

```
http://localhost:8080
```

---

# ✅ What You Can Say in Exam (Important Points)

- Spring Boot used for rapid development
- Thymeleaf used for frontend
- H2 in-memory database (no installation needed)
- CRUD operations implemented
- MVC architecture followed

---

# 🚀 Next

Say **"go"** and I’ll give:

👉 **2. Book Bank System (same simple format)**
