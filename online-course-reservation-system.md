Alright — continuing:

# ✅ 5. Online Course Reservation System (Spring Boot – Exam Ready)

👉 Goal: **Enroll students in courses + View enrollments**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="k8v2s1"
course-system/
 ├── src/main/java/com/example/course/
 │    ├── CourseApplication.java
 │    ├── Enrollment.java
 │    ├── EnrollmentRepository.java
 │    ├── EnrollmentController.java
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

```java id="t9x3p6"
package com.example.course;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class CourseApplication {
    public static void main(String[] args) {
        SpringApplication.run(CourseApplication.class, args);
    }
}
```

---

# 🧾 2. Entity Class

```java id="v5l8d2"
package com.example.course;

import jakarta.persistence.*;

@Entity
public class Enrollment {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String studentName;
    private String courseName;

    public Enrollment() {}

    public Enrollment(String studentName, String courseName) {
        this.studentName = studentName;
        this.courseName = courseName;
    }

    public Long getId() { return id; }
    public String getStudentName() { return studentName; }
    public String getCourseName() { return courseName; }

    public void setStudentName(String studentName) { this.studentName = studentName; }
    public void setCourseName(String courseName) { this.courseName = courseName; }
}
```

---

# 🗃️ 3. Repository

```java id="n2c7r4"
package com.example.course;

import org.springframework.data.jpa.repository.JpaRepository;

public interface EnrollmentRepository extends JpaRepository<Enrollment, Long> {
}
```

---

# 🎮 4. Controller

```java id="y6h1q9"
package com.example.course;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class EnrollmentController {

    private final EnrollmentRepository repo;

    public EnrollmentController(EnrollmentRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("enrollment", new Enrollment());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Enrollment enroll) {
        repo.save(enroll);
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

```html id="w3n8b2"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Course Enrollment Form</h2>

    <form action="/save" method="post" th:object="${enrollment}">
      Student Name: <input type="text" th:field="*{studentName}" /><br /><br />
      Course Name: <input type="text" th:field="*{courseName}" /><br /><br />
      <button type="submit">Enroll</button>
    </form>

    <a href="/list">View Enrollments</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="m7z4p1"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Course Enrollments</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Student</th>
        <th>Course</th>
      </tr>

      <tr th:each="e : ${list}">
        <td th:text="${e.id}"></td>
        <td th:text="${e.studentName}"></td>
        <td th:text="${e.courseName}"></td>
      </tr>
    </table>

    <a href="/">New Enrollment</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="x1k9c6"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml id="c8v2m5"
<artifactId>course-system</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="q4t6y8"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="z5n2r7"
http://localhost:8080
```

---

# ✅ Exam Points

- Used for course registration/enrollment
- Stores student name and course name
- Built using Spring Boot MVC
- H2 database used
- Supports simple CRUD

---

# 🚀 Next

Say **"next"** →

👉 **6. Airline / Railway Reservation System**
