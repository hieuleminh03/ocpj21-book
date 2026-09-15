---
layout: answer

title: "Chương 7"
subtitle: "Xử lý lỗi và Exceptions"
exam_objectives:
  - "Handle exceptions using try/catch/finally, try-with-resources, and multi-catch blocks, including custom exceptions."
---

## Đáp án {#answers}
**1. Đáp án đúng là B.**

**Giải thích:**

- **A.** Checked exception là một loại exception kế thừa từ class `java.lang.RuntimeException`.
  - Đáp án này sai. Checked exception không kế thừa từ `java.lang.RuntimeException`. Checked exception là subclass của `java.lang.Exception` nhưng không phải của `java.lang.RuntimeException`.

- **B.** Checked exception phải được catch hoặc khai báo trong method signature bằng keyword `throws`.
  - Đáp án này đúng. Checked exception phải được catch bằng block `try-catch` hoặc khai báo trong method signature bằng keyword `throws`. Điều này nhằm đảm bảo exception được xử lý đúng cách tại một thời điểm nào đó trong code.

- **C.** Checked exception là một error thường do môi trường mà application đang chạy gây ra, và application không thể xử lý được.
  - Đáp án này sai. Nó mô tả error chính xác hơn là checked exception. Error thường do môi trường gây ra và không được kỳ vọng là application phải xử lý.

- **D.** Checked exception có thể được Java Virtual Machine throw khi xảy ra error nghiêm trọng, chẳng hạn lỗi out-of-memory.
  - Đáp án này sai. Nó mô tả error chứ không phải checked exception. Những error như lỗi out-of-memory được JVM throw và trong hầu hết trường hợp không nhằm để application catch hay xử lý.


**2. Đáp án đúng là A.**

**Giải thích:**

- **A.** Đoạn code này định nghĩa một custom checked exception và throw cũng như xử lý nó một cách chính xác.
  - Đáp án này đúng. Đoạn code định nghĩa một custom checked exception bằng cách extends `Exception`. Method `methodThatThrowsException` throw custom exception này, sau đó nó được catch và xử lý trong method `main`.

- **B.** Đoạn code này định nghĩa một custom unchecked exception. 
  - Đáp án này sai. Đoạn code extends `Exception`, không phải `RuntimeException`, khiến nó là checked exception chứ không phải unchecked.

- **C.** Đoạn code này sẽ không compile vì custom exception không được khai báo đúng trong method signature.
  - Đáp án này sai. Custom exception được khai báo đúng trong method signature của `methodThatThrowsException`, nên nó sẽ compile không vấn đề gì.

- **D.** Đoạn code này sẽ compile nhưng sẽ không throw custom exception tại runtime.
  - Đáp án này sai. Đoạn code sẽ throw custom exception tại runtime như mong đợi, và nó sẽ được catch và xử lý trong block `catch`.


**3. Đáp án đúng là B.**

**Giải thích:**

- **A.** `1`
  - Đáp án này sai. Mặc dù block `catch` trả về `1`, block `finally` sẽ ghi đè giá trị return này bằng `2`.

- **B.** `2`
  - Đáp án này đúng. Block `finally` luôn được thực thi và giá trị return của nó ghi đè giá trị return từ block `catch`, dẫn đến `2` được in ra.

- **C.** Compile thất bại
  - Đáp án này sai. Đoạn code compile mà không có lỗi nào.

- **D.** Một exception xảy ra tại runtime
  - Đáp án này sai. Dù một `RuntimeException` được throw trong block `try`, nó được catch bởi block `catch`, và không có exception nào lan truyền để gây runtime error.


**4. Đáp án đúng là D.**

**Giải thích:**

- **A.** Đoạn code không compile đúng.
  - Đáp án này sai. Đoạn code compile đúng. Một block `try` có thể được theo sau bởi block `finally` mà không cần block `catch`.

- **B.** Đoạn code sẽ compile đúng nếu chúng ta thêm một block `catch`.
  - Đáp án này sai. Dù việc thêm block `catch` là hợp lệ, nó không cần thiết để đoạn code compile. Block `try` có thể được dùng chỉ với block `finally`.

- **C.** Đoạn code sẽ compile đúng nếu chúng ta bỏ block `finally`.
  - Đáp án này sai. Việc bỏ block `finally` không cần thiết để đoạn code compile. Đoạn code hợp lệ khi có block `finally`.

- **D.** Đoạn code compile đúng như hiện tại.
  - Đáp án này đúng. Đoạn code compile đúng như hiện tại. Một block `try` phải được theo sau bởi block `catch`, block `finally`, hoặc cả hai. 


**5. Đáp án đúng là C và D.**

**Giải thích:**

- **A.** Trong `try-with-resources`, block `catch` là bắt buộc.
  - Đáp án này sai. Trong câu lệnh `try-with-resources`, block catch là tùy chọn. Mục đích chính của `try-with-resources` là đảm bảo mỗi resource được đóng ở cuối câu lệnh, bất kể exception có được throw hay không.

- **B.** Keyword `throws` được dùng để throw một exception. 
  - Đáp án này sai. Keyword `throws` được dùng trong khai báo method để chỉ ra rằng method có thể throw một exception, chứ không phải để throw exception. Keyword `throw` được dùng để thực sự throw một exception.

- **C.** Trong block `try-with-resources`, nếu bạn khai báo nhiều hơn một resource, chúng phải được phân tách bằng dấu chấm phẩy.
  - Đáp án này đúng. Trong block `try-with-resources`, nếu bạn khai báo nhiều hơn một resource, chúng phải được phân tách bằng dấu chấm phẩy.

- **D.** Nếu một block `catch` được định nghĩa cho exception mà code trong block `try` không thể throw, một compile-time error sẽ được tạo ra.
  - Đáp án này đúng. Nếu một block `catch` được định nghĩa cho exception mà code trong block `try` không thể throw, compiler sẽ tạo ra error vì block `catch` là unreachable.


**6. Đáp án đúng là E.**

**Giải thích:**

- **A.** `Close Exception`
  - Đáp án này sai. Dù `IOException` từ `close()` sẽ xảy ra, nó sẽ bị suppressed bởi `RuntimeException`.

- **B.** `RuntimeException`
  - Đáp án này sai. Exception chính là `RuntimeException`, nhưng nó sẽ không in message của nó trực tiếp vì block catch không xử lý nó.

- **C.** `RuntimeException` rồi sau đó `CloseException` 
  - Đáp án này sai. Dù cả hai exception đều xảy ra, `RuntimeException` là exception chính, và `IOException` bị suppressed. Cả hai message không được in tuần tự.

- **D.** Compile thất bại
  - Đáp án này sai. Đoạn code compile mà không có lỗi nào.

- **E.** Stack trace của một exception không được catch sẽ được in ra.
  - Đáp án này đúng. `RuntimeException` được throw trong block try không được catch bởi block `catch (IOException e)`. Do đó, stack trace của `RuntimeException` được in ra.


**7. Đáp án đúng là B và C.**

**Giải thích:**

- **A.** `java.io.FileNotFoundException` sai. Nó là subclass của `java.io.IOException`, và `java.io.IOException` lại là subclass của `java.lang.Exception`, khiến nó là checked exception.

- **B.** `java.lang.ArithmeticException` đúng. Nó là subclass trực tiếp của `java.lang.RuntimeException` và đại diện cho các arithmetic error như chia cho 0.

- **C.** `java.lang.ClassCastException` đúng. Nó là subclass trực tiếp của `java.lang.RuntimeException` và biểu thị một thao tác cast không hợp lệ.

- **D.** `java.lang.InterruptedException` sai. Nó là subclass trực tiếp của `java.lang.Exception`, khiến nó là checked exception. Nó biểu thị rằng một thread đã bị interrupted.


**8. Đáp án đúng là D.**

**Giải thích:**

- **A.** Chỉ `"Try Block Exception"` được in ra.
  - Đáp án này sai. `Try Block Exception` là exception chính và không được in trực tiếp vì block `catch` kiểm tra suppressed exception trước.

- **B.** Chỉ `"Close Exception"` được in ra.
  - Đáp án này sai. `Close Exception` không được in trực tiếp; nó bị suppressed và được truy cập qua method `getSuppressed`.

- **C.** Cả `"Try Block Exception"` và `"Close Exception"` đều được in ra.
  - Đáp án này sai. Đoạn code chỉ in các suppressed exception, không in trực tiếp message của exception chính.

- **D.** `"Suppressed: Close Exception"` được in ra.
  - Đáp án này đúng. `RuntimeException` được throw trong block `try` là exception chính, và `RuntimeException` từ method `close` bị suppressed. Block `catch` in ra message của suppressed exception, `"Suppressed: Close Exception"`.
