---
layout: answer

title: "Chương 5"
subtitle: "Điều khiển luồng chương trình"
exam_objectives:
  - "Tạo các cấu trúc điều khiển luồng chương trình gồm if/else, switch statement và switch expression, loop, cùng break và continue."
  - "Triển khai inheritance, bao gồm abstract type, sealed type cũng như record class. Override method, kể cả method của class Object. Triển khai polymorphism và phân biệt object type với reference type. Thực hiện reference type casting, nhận diện object type bằng toán tử instanceof, và pattern matching với toán tử instanceof cùng cấu trúc switch."
---

## Đáp án {#answers}
**1. Đáp án đúng là A.**

**Giải thích:**

- **A)** `x is between 5 and 20`
  - Đáp án này đúng. Giá trị của `x` là 10, thỏa mãn cả hai điều kiện trong các câu lệnh `if` lồng nhau (`x > 5` và `x < 20`). Do đó, chương trình in ra `"x is between 5 and 20"`.

- **B)** `x is 5 or less` 
  - Đáp án này sai. Giá trị của `x` là 10, không thỏa mãn điều kiện `x <= 5` trong block `else`. Do đó, message này sẽ không được in.

- **C)** `x is greater than 20`
  - Đáp án này sai. Giá trị của `x` là 10, không thỏa mãn điều kiện `x > 20`. Do đó, message này sẽ không được in.

- **D)** Chương trình không compile 
  - Đáp án này sai. Chương trình compile thành công mà không có lỗi nào.

- **E)** Chương trình compile nhưng không tạo ra output nào
  - Đáp án này sai. Chương trình tạo ra output vì giá trị của `x` thỏa mãn các điều kiện trong các câu lệnh `if` lồng nhau, dẫn đến output `"x is between 5 and 20"`.
  

**2. Đáp án đúng là D.**

**Giải thích:**

- **A)** 
```java
if (emp instanceof Employee) {
    var (id, Person(name, age)) = emp;
    System.out.println(name + " is " + age + " years old.");
}
```
  - Đáp án này sai. Mặc dù nó cố gắng dùng destructuring, cú pháp này không hợp lệ trong Java. Java không hỗ trợ destructuring assignment theo cách này.

- **B)** 
```java
if (emp instanceof Employee(_, Person(var name, var age))) {
    System.out.println(name + " is " + age + " years old.");
}
```
  - Đáp án này sai. Nó dùng dấu gạch dưới (`_`) để bỏ qua field `id`, đây không phải là một kỹ thuật hợp lệ trong Java 21.

- **C)**
```java
if (emp instanceof Employee e) {
    System.out.println(e.person().name() + " is " + e.person().age() + " years old.");
}
```
  - Đáp án này sai. Nó dùng `instanceof` truyền thống mà không có pattern matching, dựa vào các accessor method để trích xuất dữ liệu.

- **D)**
```java
if (emp instanceof Employee(var id, Person(var name, var age))) {
    System.out.println(name + " is " + age + " years old.");
}
```
  - Đáp án này đúng. Nó dùng nested record pattern matching để trích xuất cả dữ liệu `Employee` và `Person` chỉ trong một bước. Nó dùng `var` cho type inference và đặt tên các biến `name` và `age` chính xác như yêu cầu.

- **E)** 
```java
if (emp instanceof Employee(var id, var person)) {
    System.out.println(person.name() + " is " + person.age() + " years old.");
}
```
  - Đáp án này sai. Mặc dù nó dùng pattern matching cho record `Employee`, nó không lồng pattern matching cho record `Person`, nên vẫn cần gọi các accessor method trên `person`.



**3. Đáp án đúng là C.**



**Giải thích:**

- **A)** Code snippet 1
  - Đáp án này sai. Biến `y` được khai báo bên trong câu lệnh `if` đầu tiên và không thể truy cập từ bên ngoài block của nó. Do đó, việc cố in `y` ra ngoài scope của nó dẫn đến compilation error.

- **B)** Code snippet 2
  - Đáp án này sai. Biến `z` được khai báo bên trong câu lệnh `if` thứ hai và không thể truy cập từ bên ngoài block của nó. Do đó, việc cố dùng `z` ra ngoài scope của nó dẫn đến compilation error.

- **C)** Code snippet 3
  - Đáp án này đúng. Biến `a` được khai báo bên ngoài câu lệnh `if`, nên nó có thể truy cập cả bên trong lẫn bên ngoài block `if`. Việc gán lại `a` bên trong block `if` là hợp lệ.

- **D)** Không có đáp án nào ở trên
  - Đáp án này sai. Mặc dù đúng là các code snippet 1, 2 và 4 sẽ không compile, nhưng code snippet 3 compile mà không có lỗi nào. Do đó, đáp án không thể là "none of the above".


**4. Đáp án đúng là C.**

**Giải thích:**

- **A)** `Weekend` 
  - Đáp án này sai. Giá trị của `dayOfWeek` là 3, không khớp với case 1 hoặc 7, nên nó không in ra `"Weekend"`.

- **B)** `Invalid day`
  - Đáp án này sai. Case `default` không được thực thi vì giá trị của `dayOfWeek` khớp với một trong các case cụ thể (2, 3, 4, 5, hoặc 6).

- **C)** `Weekday`
  - Đáp án này đúng. Giá trị của `dayOfWeek` là 3, khớp với case 3. Do đó, biến `dayType` được gán giá trị `"Weekday"`, và giá trị này được in ra.

- **D)** Chương trình không compile
  - Đáp án này sai. Chương trình compile mà không có lỗi.

- **E)** Chương trình compile nhưng không tạo ra output nào
  - Đáp án này sai. Chương trình compile và tạo ra output, đó là `"Weekday"` dựa trên giá trị `dayOfWeek` đã cho.


**5. Đáp án đúng là B.**

**Giải thích:**

- **A)** `A`
  - Đáp án này sai. Giá trị của `score` là 85, không khớp với các case 90 hoặc 100. Do đó, nó không in ra `"A"`.

- **B)** `F`
  - Đáp án này đúng. Case `default` được thực thi vì giá trị của `score` không khớp với bất kỳ câu lệnh `case` nào khác.

- **C)** Chương trình không compile 
  - Đáp án này sai. Chương trình dùng `switch` expression một cách chính xác, compile mà không có lỗi.

- **D)** `B`
  - Đáp án này sai. Giá trị của `score` là 85, không khớp với case 80 hoặc 89.

- **E)** Chương trình compile nhưng không tạo ra output nào
  - Đáp án này sai. Chương trình compile và tạo ra output, đó là `"F"` dựa trên giá trị `score` đã cho.


**6. Đáp án đúng là A.**

**Giải thích:**

- **A)** 
```java
case CarType.SEDAN, CarType.HATCHBACK -> System.out.println("Compact vehicle");
case CarType.SUV -> System.out.println("Large vehicle");
case CarType.CONVERTIBLE -> System.out.println("Open-top vehicle");
```
  - Đáp án này đúng. Trong Java 21, bạn có thể dùng fully qualified name của các enum constant trong switch statement, ngay cả khi selector expression có kiểu assignment-compatible với enum type (trong trường hợp này, `Vehicle` assignment-compatible với `CarType`).

- **B)** 
```java
case SEDAN, HATCHBACK -> System.out.println("Compact vehicle");
case SUV -> System.out.println("Large vehicle");
case CONVERTIBLE -> System.out.println("Open-top vehicle");
```
  - Đáp án này sai. Khi dùng một interface type (`Vehicle`) làm selector expression, bạn phải dùng fully qualified name cho các enum constant. Dùng tên không đầy đủ (`SEDAN`, `HATCHBACK`, v.v.) sẽ dẫn đến compilation error.

- **C)** 
```java
case CarType.SEDAN || CarType.HATCHBACK -> System.out.println("Compact vehicle");
case CarType.SUV -> System.out.println("Large vehicle");
case CarType.CONVERTIBLE -> System.out.println("Open-top vehicle");
```
  - Đáp án này sai. Nó cố dùng toán tử logical OR (`||`) trong case label, đây không phải cú pháp hợp lệ cho switch statement. Nhiều case label phải được phân tách bằng dấu phẩy, không phải các toán tử logic.

- **D)** 
```java
case Vehicle.SEDAN, Vehicle.HATCHBACK -> System.out.println("Compact vehicle");
case Vehicle.SUV -> System.out.println("Large vehicle");
case Vehicle.CONVERTIBLE -> System.out.println("Open-top vehicle");
```
  - Đáp án này sai. Mặc dù nó dùng fully qualified name, nó lại thêm tiền tố `Vehicle` thay vì `CarType` cho các enum constant. Các enum constant thuộc enum `CarType`, không phải interface `Vehicle`, nên điều này sẽ dẫn đến compilation error.


**7. Đáp án đúng là D.**

**Giải thích:**

- **A)** 
```java
case Circle c -> Math.PI * c.radius() * c.radius();
case Square s -> s.side() * s.side();
case null -> 0;
```
  - Đáp án này sai. Nó không compile vì `switch` expression không exhaustive, nó không bao quát tất cả các giá trị `Shape` có thể có.

- **B)** 
```java
default -> 0;
case Circle c -> Math.PI * c.radius() * c.radius();
case Square s -> s.side() * s.side();
case Triangle t -> 0.5 * t.base() * t.height();
```
   - Đáp án này sai. Nó không compile vì case `default` (không cần thiết) xuất hiện trước các câu lệnh `case` còn lại.

- **C)** 
```java
case Shape s when s instanceof Circle ->
        Math.PI * ((Circle)s).radius() * ((Circle)s).radius();
case Shape s when s instanceof Square ->
        ((Square)s).side() * ((Square)s).side();
case Shape s when s instanceof Triangle ->
        0.5 * ((Triangle)s).base() * ((Triangle)s).height();
```
  - Đáp án này sai. Nó không compile vì không exhaustive. Do dùng các kiểm tra `instanceof` dài dòng thay vì tận dụng pattern matching, nó thiếu một nhánh `default`.

- **D)** 
```java
case Circle c -> Math.PI * c.radius() * c.radius();
case Square s -> s.side() * s.side();
case Triangle t -> 0.5 * t.base() * t.height();
``` 
- Đáp án này đúng. Nó bao quát tất cả các subtype có thể có của interface `Shape` được sealed mà không cần case `default` không cần thiết.


**8. Đáp án đúng là B.**

**Giải thích:**

- **A)** `2`
  - Đáp án này sai. Giá trị của `count` được tăng cho đến khi nó đạt 3. Câu lệnh labeled `break` thoát khỏi vòng lặp ngoài khi `count` bằng 3.

- **B)** `3`
  - Đáp án này đúng. Giá trị của `count` được tăng bên trong vòng lặp `while` bên trong. Khi `count` đạt 3, câu lệnh labeled `break` (`break outerLoop`) được thực thi, khiến luồng điều khiển thoát khỏi vòng lặp ngoài. Do đó, `count` là 3 khi được in ra.

- **C)** `4`
  - Đáp án này sai. Vòng lặp không tiếp tục tăng `count` lên 4 vì câu lệnh labeled `break` thoát khỏi vòng lặp khi `count` là 3.

- **D)** `5`
  - Đáp án này sai. Vòng lặp không tiếp tục tăng `count` lên 5 vì câu lệnh labeled `break` thoát khỏi vòng lặp khi `count` là 3.

- **E)** Chương trình không compile
  - Đáp án này sai. Chương trình compile thành công và chạy mà không có lỗi.


**9. Đáp án đúng là C.**

**Giải thích:**

- **A)** `5`
  - Đáp án này sai. Giá trị 5 chỉ là giới hạn trên của vòng lặp, không phải tổng của các số nguyên từ 1 đến 5.

- **B)** `10`
  - Đáp án này sai. Giá trị 10 nhỏ hơn tổng của các số nguyên từ 1 đến 5.

- **C)** `15`
  - Đáp án này đúng. Vòng lặp lặp từ 1 đến 5, cộng từng giá trị của `i` vào `sum`. Các phép tính như sau: 1 + 2 + 3 + 4 + 5 = 15.

- **D)** `20`
  - Đáp án này sai. Giá trị 20 lớn hơn tổng của các số nguyên từ 1 đến 5.

- **E)** Chương trình không compile
  - Đáp án này sai. Chương trình compile thành công và chạy mà không có lỗi.


**10. Đáp án đúng là A.**

**Giải thích:**

- **A)** `9`
  - Đáp án này đúng. Câu lệnh `continue` bỏ qua lần lặp hiện tại khi số đó là số chẵn (`num % 2 == 0`). Các số lẻ trong array là 1, 3, và 5. Tổng của chúng là 1 + 3 + 5 = 9.

- **B)** `10`
  - Đáp án này sai. Tổng của các số lẻ (1, 3, và 5) là 9, không phải 10.

- **C)** `12`
  - Đáp án này sai. Tổng của các số lẻ (1, 3, và 5) là 9, không phải 12.

- **D)** `15`
  - Đáp án này sai. Tổng của tất cả các số trong array (1 + 2 + 3 + 4 + 5) là 15, nhưng câu lệnh `continue` khiến vòng lặp bỏ qua việc cộng các số chẵn.

- **E)** Chương trình không compile
  - Đáp án này sai. Chương trình compile thành công và chạy mà không có lỗi.

