Alright — continuing:

# ✅ 11. Foreign Trading System (Spring Boot – Exam Ready)

👉 Goal: **Add + View trade records (country + product)**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="t7k2m4"
trading-system/
 ├── src/main/java/com/example/trading/
 │    ├── TradingApplication.java
 │    ├── Trade.java
 │    ├── TradeRepository.java
 │    ├── TradeController.java
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

```java id="v5p9x3"
package com.example.trading;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class TradingApplication {
    public static void main(String[] args) {
        SpringApplication.run(TradingApplication.class, args);
    }
}
```

---

# 🌍 2. Entity Class

```java id="k3n8c6"
package com.example.trading;

import jakarta.persistence.*;

@Entity
public class Trade {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String country;
    private String product;

    public Trade() {}

    public Trade(String country, String product) {
        this.country = country;
        this.product = product;
    }

    public Long getId() { return id; }
    public String getCountry() { return country; }
    public String getProduct() { return product; }

    public void setCountry(String country) { this.country = country; }
    public void setProduct(String product) { this.product = product; }
}
```

---

# 🗃️ 3. Repository

```java id="m1x9p4"
package com.example.trading;

import org.springframework.data.jpa.repository.JpaRepository;

public interface TradeRepository extends JpaRepository<Trade, Long> {
}
```

---

# 🎮 4. Controller

```java id="z9v3q7"
package com.example.trading;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class TradeController {

    private final TradeRepository repo;

    public TradeController(TradeRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("trade", new Trade());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Trade trade) {
        repo.save(trade);
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

```html id="p4m8n2"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Foreign Trade Form</h2>

    <form action="/save" method="post" th:object="${trade}">
      Country: <input type="text" th:field="*{country}" /><br /><br />
      Product: <input type="text" th:field="*{product}" /><br /><br />
      <button type="submit">Add Trade</button>
    </form>

    <a href="/list">View Trades</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="c6v2x8"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Trade Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Country</th>
        <th>Product</th>
      </tr>

      <tr th:each="t : ${list}">
        <td th:text="${t.id}"></td>
        <td th:text="${t.country}"></td>
        <td th:text="${t.product}"></td>
      </tr>
    </table>

    <a href="/">New Trade</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="n3k7m6"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml id="q2v6p9"
<artifactId>trading-system</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="z5k9d5"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="x7z1c9"
http://localhost:8080
```

---

# ✅ Exam Points

- Manages foreign trade records
- Stores country and product details
- Built using Spring Boot MVC
- H2 database used
- Simple CRUD operations

---

# 🚀 Next

Say **"next"** →

👉 **12. Conference Management System**
