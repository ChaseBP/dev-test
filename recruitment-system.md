Alright — continuing:

# ✅ 10. Recruitment System (Spring Boot – Exam Ready)

👉 Goal: **Add + View job applicants (name + position)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="r7k2m4"
recruitment-system/
 ├── src/main/java/com/example/recruitment/
 │    ├── RecruitmentApplication.java
 │    ├── Applicant.java
 │    ├── ApplicantRepository.java
 │    ├── ApplicantController.java
 │
 ├── src/main/resources/templates/
 │    ├── form.html
 │    ├── list.html
 │
 ├── src/main/resources/application.properties
 ├── pom.xml
 ├── build.gradle
```

---

# 🧠 1. Main Application

```java id="t5v9p3"
package com.example.recruitment;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class RecruitmentApplication {
    public static void main(String[] args) {
        SpringApplication.run(RecruitmentApplication.class, args);
    }
}
```

---

# 👤 2. Entity Class

```java id="k3n7c6"
package com.example.recruitment;

import jakarta.persistence.*;

@Entity
public class Applicant {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;
    private String position;

    public Applicant() {}

    public Applicant(String name, String position) {
        this.name = name;
        this.position = position;
    }

    public Long getId() { return id; }
    public String getName() { return name; }
    public String getPosition() { return position; }

    public void setName(String name) { this.name = name; }
    public void setPosition(String position) { this.position = position; }
}
```

---

# 🗃️ 3. Repository

```java id="v1x8p4"
package com.example.recruitment;

import org.springframework.data.jpa.repository.JpaRepository;

public interface ApplicantRepository extends JpaRepository<Applicant, Long> {
}
```

---

# 🎮 4. Controller

```java id="m9v3z7"
package com.example.recruitment;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class ApplicantController {

    private final ApplicantRepository repo;

    public ApplicantController(ApplicantRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("applicant", new Applicant());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Applicant applicant) {
        repo.save(applicant);
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

```html id="p4m8n1"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Recruitment Form</h2>

    <form action="/save" method="post" th:object="${applicant}">
      Name: <input type="text" th:field="*{name}" /><br /><br />
      Position: <input type="text" th:field="*{position}" /><br /><br />
      <button type="submit">Apply</button>
    </form>

    <a href="/list">View Applicants</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="c6v2x9"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Applicant Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Position</th>
      </tr>

      <tr th:each="a : ${list}">
        <td th:text="${a.id}"></td>
        <td th:text="${a.name}"></td>
        <td th:text="${a.position}"></td>
      </tr>
    </table>

    <a href="/">New Application</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="n3k7m5"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml id="q2v6p8"
<artifactId>recruitment-system</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="z5k9d4"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="x7z1c8"
http://localhost:8080
```

---

# ✅ Exam Points

- Manages job applicants
- Stores name and position applied
- Built using Spring Boot MVC
- H2 database used
- Simple CRUD operations

---

# 🚀 Next

Say **"next"** →

👉 **11. Foreign Trading System**
