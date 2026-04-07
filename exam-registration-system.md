Alright — continuing:

# ✅ 3. Exam Registration System (Spring Boot – Exam Ready)

👉 Goal: **Register students for exams + View registrations**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="95kdwy"
exam-registration/
 ├── src/main/java/com/example/exam/
 │    ├── ExamApplication.java
 │    ├── Registration.java
 │    ├── RegistrationRepository.java
 │    ├── RegistrationController.java
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

```java id="u36a9l"
package com.example.exam;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ExamApplication {
    public static void main(String[] args) {
        SpringApplication.run(ExamApplication.class, args);
    }
}
```

---

# 🧾 2. Entity Class

```java id="kbq8wa"
package com.example.exam;

import jakarta.persistence.*;

@Entity
public class Registration {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String studentName;
    private String subject;

    public Registration() {}

    public Registration(String studentName, String subject) {
        this.studentName = studentName;
        this.subject = subject;
    }

    public Long getId() { return id; }
    public String getStudentName() { return studentName; }
    public String getSubject() { return subject; }

    public void setStudentName(String studentName) { this.studentName = studentName; }
    public void setSubject(String subject) { this.subject = subject; }
}
```

---

# 🗃️ 3. Repository

```java id="1er33i"
package com.example.exam;

import org.springframework.data.jpa.repository.JpaRepository;

public interface RegistrationRepository extends JpaRepository<Registration, Long> {
}
```

---

# 🎮 4. Controller

```java id="f06lgn"
package com.example.exam;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class RegistrationController {

    private final RegistrationRepository repo;

    public RegistrationController(RegistrationRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("registration", new Registration());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Registration reg) {
        repo.save(reg);
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

```html id="wy2vrl"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Exam Registration Form</h2>

    <form action="/save" method="post" th:object="${registration}">
      Student Name: <input type="text" th:field="*{studentName}" /><br /><br />
      Subject: <input type="text" th:field="*{subject}" /><br /><br />
      <button type="submit">Register</button>
    </form>

    <a href="/list">View Registrations</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="1v4x5s"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Registered Students</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Subject</th>
      </tr>

      <tr th:each="r : ${list}">
        <td th:text="${r.id}"></td>
        <td th:text="${r.studentName}"></td>
        <td th:text="${r.subject}"></td>
      </tr>
    </table>

    <a href="/">New Registration</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="o5e4rs"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

👉 Same as previous (only change artifactId if needed)

```xml id="j50v0p"
<artifactId>exam-registration</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="i2xps3"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="2g1m8s"
http://localhost:8080
```

---

# ✅ Exam Points

- Used for student exam registration
- Stores student name & subject
- MVC architecture (Model, View, Controller)
- H2 database used
- Simple CRUD operations

---

# 🚀 Next

Say **"next"** →

👉 **4. Stock Maintenance System**
