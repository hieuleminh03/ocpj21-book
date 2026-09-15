---
layout: answer

title: "Chương 8"
subtitle: "Functional Interface và biểu thức Lambda"
exam_objectives:
  - "Sử dụng Stream cho object và primitive, bao gồm biểu thức lambda triển khai functional interface, để tạo, filter, transform, process và sort dữ liệu."
---

## Đáp án {#answers}
**1. Đáp án đúng là B và D.**

**Giải thích:**

- **A)** Một functional interface có thể có nhiều method `abstract`.
  - Đáp án này sai. Một functional interface chỉ có thể có một abstract method. Việc có nhiều abstract method sẽ khiến nó không còn đủ điều kiện là một functional interface.

- **B)** Một functional interface có thể có default method và method `static`.
  - Đáp án này đúng. Một functional interface được phép có default method và static method, những method này không bị tính là abstract method.

- **C)** Annotation `@FunctionalInterface` là bắt buộc để khai báo một functional interface. 
  - Đáp án này sai. Annotation `@FunctionalInterface` không bắt buộc; nó chỉ là một marker để chỉ ra rằng interface này được dự định là một functional interface. Một interface vẫn có thể là functional interface mà không cần annotation này miễn là nó có đúng một abstract method.

- **D)** Biểu thức lambda có thể được dùng để khởi tạo functional interface.
  - Đáp án này đúng. Biểu thức lambda được dùng để cung cấp implementation cho abstract method duy nhất của một functional interface, khiến chúng trở thành một tính năng then chốt cho lập trình hàm (functional programming) trong Java.


**2. Đáp án đúng là A.**

**Giải thích:**

- **A)** `(s1, s2) -> s1.compareTo(s2)`
  - Đáp án này đúng. Biểu thức lambda này implement đúng interface `Comparator<String>`. Nó dùng cú pháp đúng cho một biểu thức lambda, với các parameter được bao trong dấu ngoặc đơn và một biểu thức duy nhất cho phần body.

- **B)** `(String s1, s2) -> s1.compareTo(s2)`
  - Đáp án này sai. Cú pháp không hợp lệ vì nếu bạn chỉ định type của một parameter, bạn phải chỉ định type cho tất cả các parameter. Đúng ra phải là `(String s1, String s2)`.

- **C)** `s1, s2 -> s1.compareTo(s2)`
  - Đáp án này sai. Các parameter phải được bao trong dấu ngoặc đơn. Cú pháp đúng là `(s1, s2)`.

- **D)** `(s1, s2) -> return s1.compareTo(s2);`
  - Đáp án này sai. Khi dùng câu lệnh return, bạn cũng phải thêm dấu ngoặc nhọn.

- **E)** `(s1, s2) -> { s1.compareTo(s2); }`
  - Đáp án này sai. Khi dùng dấu ngoặc nhọn, bạn phải thêm câu lệnh return cho những biểu thức trả về giá trị. Cú pháp đúng phải là `(s1, s2) -> { return s1.compareTo(s2); }`.


**3. Đáp án đúng là B.**

**Giải thích:**

- **A)** `java.util.function.Function`
  - Đáp án này sai. `Function` biểu diễn một function nhận một argument và tạo ra một kết quả.

- **B)** `java.util.function.BiFunction`
  - Đáp án này đúng. `BiFunction` biểu diễn một function nhận hai argument và tạo ra một kết quả.

- **C)** `java.util.function.Supplier`
  - Đáp án này sai. `Supplier` biểu diễn một function không nhận argument nào và tạo ra một kết quả.

- **D)** `java.util.function.Consumer`
  - Đáp án này sai. `Consumer` biểu diễn một function nhận một argument và không tạo ra kết quả.

- **E)** `java.util.function.Predicate`
  - Đáp án này sai. `Predicate` biểu diễn một function nhận một argument và trả về một giá trị `boolean`.


**4. Đáp án đúng là A.**

**Giải thích:**

- **A)** `13`
  - Đáp án này đúng. `combinedFunction` đầu tiên nhân 5 với 2 để được 10, sau đó cộng 3, cho kết quả là 13.

- **B)** `16`
  - Đáp án này sai. Nó giả định sai rằng 5 được cộng vào sau khi nhân đôi và nhân đôi lần nữa.

- **C)** `10`
  - Đáp án này sai. Nó chỉ thể hiện kết quả của function đầu tiên mà không áp dụng function thứ hai.

- **D)** `11`
  - Đáp án này sai. Có vẻ nó thể hiện nhầm phép tính 5 cộng với function đầu tiên (double).

- **E)** `8`
  - Đáp án này sai. Có vẻ nó thể hiện sai giá trị input được nhân đôi mà không cộng thêm 3.



**5. Đáp án đúng là C.**

**Giải thích:**

- **A)** `String::valueOf` 
  - Đáp án này sai. `String::valueOf` chuyển một integer thành một string, chứ không phải chuyển một string thành một integer.

- **B)** `Integer::valueOf`
  - Đáp án này sai. `Integer::valueOf` trả về một object `Integer`, trong khi lambda trả về một `int`.

- **C)** `Integer::parseInt`
  - Đáp án này đúng. `Integer::parseInt` là một method reference khớp với biểu thức lambda `str -> Integer.parseInt(str)`, tức là chuyển một string thành một integer.

- **D)** `String::parseInt`
  - Đáp án này sai. Class `String` không có method `parseInt`.

- **E)** `Integer::toString`
  - Đáp án này sai. `Integer::toString` chuyển một integer thành một string, chứ không phải chuyển một string thành một integer.

