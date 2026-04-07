Alright — continuing:

# ✅ 8. Credit Card Processing System (Spring Boot – Exam Ready)

👉 Goal: **Store simple payment details (name + amount)**
👉 ⚠️ For exam: _No real payment logic_ (just simulation)
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="m4k9x2"
credit-system/
 ├── src/main/java/com/example/credit/
 │    ├── CreditApplication.java
 │    ├── Payment.java
 │    ├── PaymentRepository.java
 │    ├── PaymentController.java
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

```java id="a7p2c6"
package com.example.credit;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class CreditApplication {
    public static void main(String[] args) {
        SpringApplication.run(CreditApplication.class, args);
    }
}
```

---

# 💳 2. Entity Class

```java id="t8v3n5"
package com.example.credit;

import jakarta.persistence.*;

@Entity
public class Payment {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String cardHolderName;
    private double amount;

    public Payment() {}

    public Payment(String cardHolderName, double amount) {
        this.cardHolderName = cardHolderName;
        this.amount = amount;
    }

    public Long getId() { return id; }
    public String getCardHolderName() { return cardHolderName; }
    public double getAmount() { return amount; }

    public void setCardHolderName(String cardHolderName) { this.cardHolderName = cardHolderName; }
    public void setAmount(double amount) { this.amount = amount; }
}
```

---

# 🗃️ 3. Repository

```java id="p6x9k1"
package com.example.credit;

import org.springframework.data.jpa.repository.JpaRepository;

public interface PaymentRepository extends JpaRepository<Payment, Long> {
}
```

---

# 🎮 4. Controller

```java id="z3q7w2"
package com.example.credit;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class PaymentController {

    private final PaymentRepository repo;

    public PaymentController(PaymentRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("payment", new Payment());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Payment payment) {
        repo.save(payment);
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

```html id="k1c8m4"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Credit Card Payment</h2>

    <form action="/save" method="post" th:object="${payment}">
      Card Holder Name:
      <input type="text" th:field="*{cardHolderName}" /><br /><br />
      Amount:
      <input type="number" step="0.01" th:field="*{amount}" /><br /><br />
      <button type="submit">Pay</button>
    </form>

    <a href="/list">View Payments</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="x9m2p7"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Payment Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Amount</th>
      </tr>

      <tr th:each="p : ${list}">
        <td th:text="${p.id}"></td>
        <td th:text="${p.cardHolderName}"></td>
        <td th:text="${p.amount}"></td>
      </tr>
    </table>

    <a href="/">New Payment</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="c5v2x9"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml id="m8p3k6"
<artifactId>credit-system</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="v2k9d4"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="z7n4r1"
http://localhost:8080
```

---

# ✅ Exam Points

- Simulates credit card payment system
- Stores card holder name and amount
- No real transaction (for academic purpose)
- Built using Spring Boot MVC
- H2 database used

---

# 🚀 Next

Say **"next"** →

👉 **9. E-Book Management System**
