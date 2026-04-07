Alright — continuing:

# ✅ 13. BPO Management System (Spring Boot – Exam Ready)

👉 Goal: **Store employee work details (name + process)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="b1p2o3"
bpo-system/
 ├── src/main/java/com/example/bpo/
 │    ├── BpoApplication.java
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

```java id="bpo1"
package com.example.bpo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class BpoApplication {
    public static void main(String[] args) {
        SpringApplication.run(BpoApplication.class, args);
    }
}
```

---

# 👨‍💼 2. Entity Class

```java id="bpo2"
package com.example.bpo;

import jakarta.persistence.*;

@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;
    private String process;

    public Employee() {}

    public Employee(String name, String process) {
        this.name = name;
        this.process = process;
    }

    public Long getId() { return id; }
    public String getName() { return name; }
    public String getProcess() { return process; }

    public void setName(String name) { this.name = name; }
    public void setProcess(String process) { this.process = process; }
}
```

---

# 🗃️ 3. Repository

```java id="bpo3"
package com.example.bpo;

import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {
}
```

---

# 🎮 4. Controller

```java id="bpo4"
package com.example.bpo;

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
    public String save(@ModelAttribute Employee e) {
        repo.save(e);
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

```html id="bpo5"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>BPO Employee Entry</h2>

    <form action="/save" method="post" th:object="${employee}">
      Name: <input type="text" th:field="*{name}" /><br /><br />
      Process: <input type="text" th:field="*{process}" /><br /><br />
      <button type="submit">Save</button>
    </form>

    <a href="/list">View Employees</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="bpo6"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Employee Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Process</th>
      </tr>

      <tr th:each="e : ${list}">
        <td th:text="${e.id}"></td>
        <td th:text="${e.name}"></td>
        <td th:text="${e.process}"></td>
      </tr>
    </table>

    <a href="/">Add Employee</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="bpo7"
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

```bash id="bpo8"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="bpo9"
http://localhost:8080
```

---

# ✅ Exam Points

- Manages BPO employee details
- Stores employee name and process assigned
- Built using Spring Boot MVC
- Uses H2 database
- Simple CRUD application

---

# 🚀 Next

Say **"next"** →

👉 **14. Library Management System**
