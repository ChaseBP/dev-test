Alright — continuing:

# ✅ 7. Software Personnel Management System (Spring Boot – Exam Ready)

👉 Goal: **Add + View employee details (name + role)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="p8z2m4"
personnel-system/
 ├── src/main/java/com/example/personnel/
 │    ├── PersonnelApplication.java
 │    ├── Employee.java
 │    ├── EmployeeRepository.java
 │    ├── EmployeeController.java
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

```java id="y3x6k9"
package com.example.personnel;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class PersonnelApplication {
    public static void main(String[] args) {
        SpringApplication.run(PersonnelApplication.class, args);
    }
}
```

---

# 👨‍💻 2. Entity Class

```java id="m2n7v5"
package com.example.personnel;

import jakarta.persistence.*;

@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;
    private String role;

    public Employee() {}

    public Employee(String name, String role) {
        this.name = name;
        this.role = role;
    }

    public Long getId() { return id; }
    public String getName() { return name; }
    public String getRole() { return role; }

    public void setName(String name) { this.name = name; }
    public void setRole(String role) { this.role = role; }
}
```

---

# 🗃️ 3. Repository

```java id="d6k1r8"
package com.example.personnel;

import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {
}
```

---

# 🎮 4. Controller

```java id="t5q9p2"
package com.example.personnel;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class EmployeeController {

    private final EmployeeRepository repo;

    public EmployeeController(EmployeeRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("employee", new Employee());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Employee emp) {
        repo.save(emp);
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

```html id="k4c8v1"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Employee Form</h2>

    <form action="/save" method="post" th:object="${employee}">
      Name: <input type="text" th:field="*{name}" /><br /><br />
      Role: <input type="text" th:field="*{role}" /><br /><br />
      <button type="submit">Add Employee</button>
    </form>

    <a href="/list">View Employees</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="p9r2x7"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Employee Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Role</th>
      </tr>

      <tr th:each="e : ${list}">
        <td th:text="${e.id}"></td>
        <td th:text="${e.name}"></td>
        <td th:text="${e.role}"></td>
      </tr>
    </table>

    <a href="/">Add New Employee</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="z1v5m3"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml id="c3x7k2"
<artifactId>personnel-system</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="w6n8q4"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="h2m9p6"
http://localhost:8080
```

---

# ✅ Exam Points

- Manages employee/personnel data
- Stores employee name and role
- Built using Spring Boot MVC
- H2 database used
- Simple CRUD operations

---

# 🚀 Next

Say **"next"** →

👉 **8. Credit Card Processing System**
