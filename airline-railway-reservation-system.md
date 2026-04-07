Alright — continuing:

# ✅ 6. Airline / Railway Reservation System (Spring Boot – Exam Ready)

👉 Goal: **Book tickets (Passenger + Destination) + View bookings**
👉 Stack: Spring Boot + Thymeleaf + H2 DB (plug & play)

---

# 📁 Project Structure

```id="k2d8p1"
reservation-system/
 ├── src/main/java/com/example/reservation/
 │    ├── ReservationApplication.java
 │    ├── Booking.java
 │    ├── BookingRepository.java
 │    ├── BookingController.java
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

```java id="a9x4c7"
package com.example.reservation;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ReservationApplication {
    public static void main(String[] args) {
        SpringApplication.run(ReservationApplication.class, args);
    }
}
```

---

# 🎫 2. Entity Class

```java id="m5q2v8"
package com.example.reservation;

import jakarta.persistence.*;

@Entity
public class Booking {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String passengerName;
    private String destination;

    public Booking() {}

    public Booking(String passengerName, String destination) {
        this.passengerName = passengerName;
        this.destination = destination;
    }

    public Long getId() { return id; }
    public String getPassengerName() { return passengerName; }
    public String getDestination() { return destination; }

    public void setPassengerName(String passengerName) { this.passengerName = passengerName; }
    public void setDestination(String destination) { this.destination = destination; }
}
```

---

# 🗃️ 3. Repository

```java id="b7n3k1"
package com.example.reservation;

import org.springframework.data.jpa.repository.JpaRepository;

public interface BookingRepository extends JpaRepository<Booking, Long> {
}
```

---

# 🎮 4. Controller

```java id="q1r6z9"
package com.example.reservation;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class BookingController {

    private final BookingRepository repo;

    public BookingController(BookingRepository repo) {
        this.repo = repo;
    }

    @GetMapping("/")
    public String form(Model model) {
        model.addAttribute("booking", new Booking());
        return "form";
    }

    @PostMapping("/save")
    public String save(@ModelAttribute Booking booking) {
        repo.save(booking);
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

```html id="t4y8p3"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Ticket Booking Form</h2>

    <form action="/save" method="post" th:object="${booking}">
      Passenger Name:
      <input type="text" th:field="*{passengerName}" /><br /><br />
      Destination: <input type="text" th:field="*{destination}" /><br /><br />
      <button type="submit">Book Ticket</button>
    </form>

    <a href="/list">View Bookings</a>
  </body>
</html>
```

---

# 📋 6. HTML – List (`list.html`)

```html id="v2m6n1"
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <body>
    <h2>Booking Records</h2>

    <table border="1">
      <tr>
        <th>ID</th>
        <th>Passenger</th>
        <th>Destination</th>
      </tr>

      <tr th:each="b : ${list}">
        <td th:text="${b.id}"></td>
        <td th:text="${b.passengerName}"></td>
        <td th:text="${b.destination}"></td>
      </tr>
    </table>

    <a href="/">New Booking</a>
  </body>
</html>
```

---

# ⚙️ 7. application.properties

```properties id="n8c3z5"
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=update
spring.thymeleaf.cache=false
```

---

# 📦 8. Maven (pom.xml)

```xml id="u7w1x4"
<artifactId>reservation-system</artifactId>
```

---

# 📦 9. Gradle (build.gradle)

👉 Same as previous

---

# ▶️ Run

```bash id="f9p2k6"
mvn spring-boot:run
# OR
gradle bootRun
```

---

# 🌐 Open

```id="s3d7h8"
http://localhost:8080
```

---

# ✅ Exam Points

- Used for airline/railway ticket booking
- Stores passenger name and destination
- Simple reservation system
- Built using Spring Boot MVC
- H2 database used

---

# 🚀 Next

Say **"next"** →

👉 **7. Software Personnel Management System**
