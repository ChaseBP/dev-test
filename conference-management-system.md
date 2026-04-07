Alright — continuing:

# ✅ 12. Conference Management System (Spring Boot – Exam Ready)

👉 Goal: **Register participants for conference (name + topic)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="c9k2m4"
conference-system/
 ├── src/main/java/com/example/conference/
 │    ├── ConferenceApplication.java
 │    ├── Participant.java
 │    ├── ParticipantRepository.java
 │    ├── ParticipantController.java
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

```java id="v6p9x3"
package com.example.conference;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ConferenceApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConferenceApplication.class, args);
    }
}
```

---

# 👥 2. Entity Class

```java id="k4n8c6"
package com.example.conference;

import jakarta.persistence.*;

@Entity
public class Participant {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;
    private String topic;

    public Participant() {}

    public Participant(String name, String topic) {
        this.name = name;
        this.topic = topic;
    }

    public Long getId() { return id; }
    public String getName() { return name; }
    public String getTopic() { return topic; }

    public void setName(String name) { this.name = name; }
    public void setTopic(String topic) { this.topic = topic; }
}
```

---

# 🗃️ 3. Repository

```java id="m2x9p4"
package com.example.conference;

import org.springframework.data.jpa.repository.JpaRepository;

public interface ParticipantRepository extends JpaRepository<Participant, Long> {
}
```

---

# 🎮 4. Controller

```java id="z8v3q7"
package com.example.conference;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class ParticipantController {

    private final ParticipantRepository repo;

    public ParticipantController(ParticipantRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("participant", new Participant());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Participant p) {
        repo.save(p);
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

```html id="p4m8n3"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Conference Registration</h2>

    <form action="/save" method="post" th:object="${participant}">
      Name: <input type="text" th:field="*{name}" /><br /><br />
      Topic: <input type="text" th:field="*{topic}" /><br /><br />
      <button type="submit">Register</button>
    </form>

    <a href="/list">View Participants</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="c6v2x7"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Participant Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Topic</th>
      </tr>

      <tr th:each="p : ${list}">
        <td th:text="${p.id}"></td>
        <td th:text="${p.name}"></td>
        <td th:text="${p.topic}"></td>
      </tr>
    </table>

    <a href="/">New Registration</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="n3k7m7"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml id="q2v6p7"
<artifactId>conference-system</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="z5k9d6"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="x7z1c7"
http://localhost:8080
```

---

# ✅ Exam Points

- Manages conference participants
- Stores participant name and topic
- Built using Spring Boot MVC
- H2 database used
- Simple CRUD operations

---

# 🚀 Next

Say **"next"** →

👉 **13. BPO Management System**
