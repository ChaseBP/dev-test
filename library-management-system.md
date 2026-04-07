Alright — continuing:

# ✅ 14. Library Management System (Spring Boot – Exam Ready)

👉 Goal: **Store book details (title + author)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="l1i2b3"
library-system/
 ├── src/main/java/com/example/library/
 │    ├── LibraryApplication.java
 │    ├── Book.java
 │    ├── BookRepository.java
 │    ├── BookController.java
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

```java id="lib1"
package com.example.library;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class LibraryApplication {
    public static void main(String[] args) {
        SpringApplication.run(LibraryApplication.class, args);
    }
}
```

---

# 📚 2. Entity Class

```java id="lib2"
package com.example.library;

import jakarta.persistence.*;

@Entity
public class Book {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String title;
    private String author;

    public Book() {}

    public Book(String title, String author) {
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

```java id="lib3"
package com.example.library;

import org.springframework.data.jpa.repository.JpaRepository;

public interface BookRepository extends JpaRepository<Book, Long> {
}
```

---

# 🎮 4. Controller

```java id="lib4"
package com.example.library;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class BookController {

    private final BookRepository repo;

    public BookController(BookRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("book", new Book());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Book b) {
        repo.save(b);
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

```html id="lib5"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Library Book Entry</h2>

    <form action="/save" method="post" th:object="${book}">
      Title: <input type="text" th:field="*{title}" /><br /><br />
      Author: <input type="text" th:field="*{author}" /><br /><br />
      <button type="submit">Save</button>
    </form>

    <a href="/list">View Books</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="lib6"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Book Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Title</th>
        <th>Author</th>
      </tr>

      <tr th:each="b : ${list}">
        <td th:text="${b.id}"></td>
        <td th:text="${b.title}"></td>
        <td th:text="${b.author}"></td>
      </tr>
    </table>

    <a href="/">Add Book</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="lib7"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

👉 Same as previous (Spring Boot + Web + JPA + Thymeleaf + H2)

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="lib8"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="lib9"
http://localhost:8080
```

---

# ✅ Exam Points

- Manages library book records
- Stores book title and author
- Built using Spring Boot MVC
- Uses H2 database
- Simple CRUD system

---

# 🚀 Final One Left

Say **"next"** →

👉 **15. Student Information System (LAST)**
