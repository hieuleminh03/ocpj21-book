---
layout: answer

title: "Chương 4"
subtitle: "Làm việc với dữ liệu"
exam_objectives:
  - "Sử dụng primitive và wrapper class. Đánh giá biểu thức số học và boolean, dùng Math API cùng việc áp dụng operator precedence, type conversion và casting."
  - "Thao tác text, bao gồm text block, bằng class String và StringBuilder."
---

## Đáp án {#answers}
**1. Đáp án đúng là C.**

**Giải thích:**

- **A)** Một `double` có thể được gán trực tiếp cho một `float` mà không cần casting. 
  - Đáp án này sai. Một `double` không thể được gán trực tiếp cho một `float` mà không cần casting vì `double` có range và độ chính xác (precision) lớn hơn `float`.

- **B)** Một `boolean` có thể được cast thành một `int`.
  - Đáp án này sai. Trong Java, các giá trị `boolean` không thể được cast thành `int`. Chúng không phải là các kiểu tương thích.

- **C)** Một `String` có thể được gán cho một reference variable kiểu `Object`.
  - Đáp án này đúng. `String` là một instance của class `Object`, do đó nó có thể được gán cho một reference variable kiểu `Object`.

- **D)** `char` là một reference data type. 
  - Đáp án này sai. `char` là một primitive data type, không phải reference data type.

- **E)** Một `int` có thể lưu một giá trị `long` mà không cần bất kỳ explicit casting nào.
  - Đáp án này sai. Một `int` không thể lưu một giá trị `long` mà không cần explicit casting vì `long` có range lớn hơn `int`.


**2. Đáp án đúng là A.**

**Giải thích:**

Hãy phân tích từng bước biểu thức `a + b * c / a - b` theo thứ tự thực hiện các phép toán:

1. **Phép nhân và phép chia** được thực hiện trước, từ trái sang phải:
   - `b * c` = `10 * 15` = `150`
   - `150 / a` = `150 / 5` = `30`

2. **Phép cộng và phép trừ** được thực hiện tiếp theo, từ trái sang phải:
   - `a + 30` = `5 + 30` = `35`
   - `35 - b` = `35 - 10` = `25`

Vậy giá trị của `result` là `25`, và chương trình in ra `25`.

- **A)** `25`
  - Đáp án này đúng.

- **B)** `35`
  - Đáp án này sai.

- **C)** `20` 
  - Đáp án này sai.

- **D)** `15` 
  - Đáp án này sai.


**3. Đáp án đúng là D.**

**Giải thích:**

- **A)** Các object `StringBuilder` là immutable.
  - Đáp án này sai. Các object `StringBuilder` là mutable, nghĩa là chúng có thể được thay đổi sau khi được tạo.

- **B)** Các object `String` có thể được sửa đổi sau khi chúng được tạo. 
  - Đáp án này sai. Các object `String` là immutable, nghĩa là một khi object `String` được tạo, nó không thể bị sửa đổi. Mọi thay đổi đều tạo ra một object `String` mới.

- **C)** `StringBuilder` được synchronized và thread-safe.
  - Đáp án này sai. `StringBuilder` không được synchronized và không thread-safe. Nếu cần synchronization, nên dùng `StringBuffer` thay thế.

- **D)** `StringBuilder` cung cấp các method cho một mutable sequence of characters.
  - Đáp án này đúng. `StringBuilder` cung cấp các method cho một mutable sequence of characters, cho phép sửa đổi object mà không tạo ra instance mới.

- **E)** `String` và `StringBuilder` có cùng performance characteristics khi thao tác với string.
  - Đáp án này sai. `String` và `StringBuilder` không có cùng performance characteristics khi thao tác với string. `StringBuilder` nói chung hiệu quả hơn cho các thao tác như vậy vì nó mutable và không tạo instance mới sau mỗi lần sửa đổi.


**4. Đáp án đúng là A và B.**

**Giải thích:**

- **A)** Text block có thể trải dài trên nhiều dòng mà không cần escape sequence cho ký tự xuống dòng.
  - Đáp án này đúng. Text block thực sự có thể trải dài trên nhiều dòng mà không cần escape sequence cho ký tự xuống dòng, giúp làm việc với string nhiều dòng dễ dàng hơn.


- **B)** Text block giữ nguyên định dạng chính xác, bao gồm cả whitespace, của code như khi viết.
  - Đáp án này đúng. Text block giữ nguyên định dạng chính xác, bao gồm cả whitespace, của code như khi viết. Điều này hữu ích để duy trì bố cục gốc của văn bản.


- **C)** Text block chỉ có thể được dùng bên trong method.
  - Đáp án này sai. Text block có thể được dùng ở bất kỳ đâu mà một `String` thông thường có thể được dùng, không chỉ bên trong method. Chúng có thể là một phần của class field, tham số method, v.v.


- **D)** Text block tự động cắt bỏ whitespace ở đầu và cuối mỗi dòng. 
  - Đáp án này sai. Text block không tự động cắt bỏ whitespace ở đầu và cuối mỗi dòng. Chúng giữ nguyên whitespace chính xác như khi viết trong code.

- **E)** Text block yêu cầu mức thụt lề tối thiểu là một dấu cách.
  - Đáp án này sai. Text block không yêu cầu mức thụt lề tối thiểu là một dấu cách. Phần thụt lề chung của tất cả các dòng được tự động loại bỏ, nhưng các dòng bên trong text block có thể có không hoặc nhiều dấu cách thụt lề.


**5. Đáp án đúng là D.**

**Giải thích:**

- **A)** Method `Math.round()` trả về một `double`.
  - Đáp án này sai. Method `Math.round()` trả về một `long` khi nhận đối số `double` và trả về một `int` khi nhận đối số `float`.

- **B)** Method `Math.random()` trả về một số nguyên ngẫu nhiên.
  - Đáp án này sai. Method `Math.random()` trả về một giá trị `double` trong khoảng từ 0.0 (bao gồm) đến 1.0 (không bao gồm).

- **C)** Method `Math.max()` chỉ có thể được dùng với các số nguyên.
  - Đáp án này sai. Method `Math.max()` có thể được dùng với nhiều kiểu số khác nhau, bao gồm `int`, `long`, `float` và `double`.

- **D)** Method `Math.pow()` trả về kết quả của việc lũy thừa đối số thứ nhất lên số mũ là đối số thứ hai.
  - Đáp án này đúng. Method `Math.pow()` trả về kết quả của việc lũy thừa đối số thứ nhất lên số mũ là đối số thứ hai. Cả hai đối số đều có kiểu `double`.

- **E)** Method `Math.abs()` chỉ có thể được dùng với các số dương.
  - Đáp án này sai. Method `Math.abs()` có thể được dùng với các số âm để trả về giá trị tuyệt đối của chúng, và nó hoạt động với nhiều kiểu số khác nhau bao gồm `int`, `long`, `float` và `double`.
