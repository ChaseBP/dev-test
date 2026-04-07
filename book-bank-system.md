Alright — next one:

# ✅ 2. Book Bank System (Spring Boot – Exam Ready)

👉 Goal: **Add + View Books (Book Bank records)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (same → plug & play)

---

# 📁 Project Structure

```
bookbank/
 ├── src/main/java/com/example/bookbank/
 │    ├── BookBankApplication.java
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

```java
package com.example.bookbank;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class BookBankApplication {
    public static void main(String[] args) {
        SpringApplication.run(BookBankApplication.class, args);
    }
}
```

---

# 📚 2. Entity Class

```java
package com.example.bookbank;

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

```java
package com.example.bookbank;

import org.springframework.data.jpa.repository.JpaRepository;

public interface BookRepository extends JpaRepository<Book, Long> {
}
```

---

# 🎮 4. Controller

```java
package com.example.bookbank;

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
    public String save(@ModelAttribute Book book) {
        repo.save(book);
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
    <h2>Book Bank Form</h2>

    <form action="/save" method="post" th:object="${book}">
      Title: <input type="text" th:field="*{title}" /><br /><br />
      Author: <input type="text" th:field="*{author}" /><br /><br />
      <button type="submit">Add Book</button>
    </form>

    <a href="/list">View Books</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Book Bank Records</h2>

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

    <a href="/">Add New Book</a>
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

(Same as previous — just change artifactId if needed)

```xml
<artifactId>bookbank</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

(Same as previous — no change needed)

---

# ▶️ Run

```bash
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```
http://localhost:8080
```

---

# ✅ Exam Points

- Book Bank system stores book details
- Uses Spring Boot MVC architecture
- Thymeleaf for UI
- H2 database for storage
- Simple CRUD (Create + Read)

---

# 🚀 Next

Say **"next"** →

👉 **3. Exam Registration System**
