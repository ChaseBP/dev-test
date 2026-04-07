Alright — continuing:

# ✅ 9. E-Book Management System (Spring Boot – Exam Ready)

👉 Goal: **Add + View e-books (title + author)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="e8k2v4"
ebook-system/
 ├── src/main/java/com/example/ebook/
 │    ├── EbookApplication.java
 │    ├── Ebook.java
 │    ├── EbookRepository.java
 │    ├── EbookController.java
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

```java id="a5v9p2"
package com.example.ebook;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class EbookApplication {
    public static void main(String[] args) {
        SpringApplication.run(EbookApplication.class, args);
    }
}
```

---

# 📚 2. Entity Class

```java id="r2n7c6"
package com.example.ebook;

import jakarta.persistence.*;

@Entity
public class Ebook {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String title;
    private String author;

    public Ebook() {}

    public Ebook(String title, String author) {
        this.title = title;
        this.author = author;
    }

    public Long getId() { return id; }
    public String getTitle() { return title; }
    public String getAuthor() { return author; }

    public void setTitle(String title) { this.title = title; }
    public void setAuthor(String author) { this.author = author; }
}
```

---

# 🗃️ 3. Repository

```java id="m1x8p4"
package com.example.ebook;

import org.springframework.data.jpa.repository.JpaRepository;

public interface EbookRepository extends JpaRepository<Ebook, Long> {
}
```

---

# 🎮 4. Controller

```java id="k9v3z7"
package com.example.ebook;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class EbookController {

    private final EbookRepository repo;

    public EbookController(EbookRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("ebook", new Ebook());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Ebook ebook) {
        repo.save(ebook);
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

```html id="t4m8n1"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>E-Book Form</h2>

    <form action="/save" method="post" th:object="${ebook}">
      Title: <input type="text" th:field="*{title}" /><br /><br />
      Author: <input type="text" th:field="*{author}" /><br /><br />
      <button type="submit">Add E-Book</button>
    </form>

    <a href="/list">View E-Books</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="p6c2v9"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>E-Book Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Title</th>
        <th>Author</th>
      </tr>

      <tr th:each="e : ${list}">
        <td th:text="${e.id}"></td>
        <td th:text="${e.title}"></td>
        <td th:text="${e.author}"></td>
      </tr>
    </table>

    <a href="/">Add New E-Book</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="z3x7m5"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml id="q1v6p8"
<artifactId>ebook-system</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="n2k9d4"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="m7z1c8"
http://localhost:8080
```

---

# ✅ Exam Points

- Manages e-book records
- Stores title and author
- Built using Spring Boot MVC
- H2 database used
- Simple CRUD operations

---

# 🚀 Next

Say **"next"** →

👉 **10. Recruitment System**
