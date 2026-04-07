Alright — final one 🎯

# ✅ 15. Student Information System (Spring Boot – Exam Ready)

👉 Goal: **Store student details (name + department)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="s1t2u3"
student-system/
 ├── src/main/java/com/example/student/
 │    ├── StudentApplication.java
 │    ├── Student.java
 │    ├── StudentRepository.java
 │    ├── StudentController.java
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

```java id="stu1"
package com.example.student;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class StudentApplication {
    public static void main(String[] args) {
        SpringApplication.run(StudentApplication.class, args);
    }
}
```

---

# 🎓 2. Entity Class

```java id="stu2"
package com.example.student;

import jakarta.persistence.*;

@Entity
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;
    private String department;

    public Student() {}

    public Student(String name, String department) {
        this.name = name;
        this.department = department;
    }

    public Long getId() { return id; }
    public String getName() { return name; }
    public String getDepartment() { return department; }

    public void setName(String name) { this.name = name; }
    public void setDepartment(String department) { this.department = department; }
}
```

---

# 🗃️ 3. Repository

```java id="stu3"
package com.example.student;

import org.springframework.data.jpa.repository.JpaRepository;

public interface StudentRepository extends JpaRepository<Student, Long> {
}
```

---

# 🎮 4. Controller

```java id="stu4"
package com.example.student;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class StudentController {

    private final StudentRepository repo;

    public StudentController(StudentRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("student", new Student());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Student s) {
        repo.save(s);
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

```html id="stu5"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Student Entry</h2>

    <form action="/save" method="post" th:object="${student}">
      Name: <input type="text" th:field="*{name}" /><br /><br />
      Department: <input type="text" th:field="*{department}" /><br /><br />
      <button type="submit">Save</button>
    </form>

    <a href="/list">View Students</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="stu6"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Student Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Department</th>
      </tr>

      <tr th:each="s : ${list}">
        <td th:text="${s.id}"></td>
        <td th:text="${s.name}"></td>
        <td th:text="${s.department}"></td>
      </tr>
    </table>

    <a href="/">Add Student</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="stu7"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

👉 Use same dependencies:

- spring-boot-starter-web
- spring-boot-starter-thymeleaf
- spring-boot-starter-data-jpa
- h2

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="stu8"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="stu9"
http://localhost:8080
```

---

# ✅ Exam Points

- Manages student records
- Stores name and department
- Built using Spring Boot MVC
- Uses H2 in-memory database
- Simple CRUD application

---
