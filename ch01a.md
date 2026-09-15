---
layout: answer

title: "Chương 1"
subtitle: "Sử dụng lập trình hướng đối tượng trong Java - Phần 1"
exam_objectives:
  - "Declare and instantiate Java objects including nested class objects, and explain the object life-cycle including creation, reassigning references, and garbage collection."
  - "Create classes and records, and define and use instance and static fields and methods, constructors, and instance and static initializers."
  - "Implement overloading, including var-arg methods."
---

## Đáp án {#answers}

**1. Đáp án đúng là B.**

**Giải thích:**

- **A)** Cả `sb1` và `sb2` đều đủ điều kiện bị garbage collection.
  - Đáp án này sai vì `sb2` vẫn giữ reference tới object `StringBuilder` mà nó được gán ban đầu. Do đó, nó không đủ điều kiện bị garbage collection.

- **B)** Chỉ object `StringBuilder` được `sb1` reference ban đầu là đủ điều kiện bị garbage collection.
  - Đáp án này đúng. Sau khi `sb1` được gán lại để reference cùng object với `sb2`, object `StringBuilder` gốc được tạo bằng `new StringBuilder("Java")` và được `sb1` reference ban đầu không còn truy cập được nữa. Vì không còn reference nào trỏ tới nó, nó trở nên đủ điều kiện bị garbage collection.

- **C)** Chỉ object `StringBuilder` được `sb2` reference ban đầu là đủ điều kiện bị garbage collection.
  - Đáp án này sai vì sau phép gán `sb1 = sb2;`, cả `sb1` và `sb2` đều reference cùng một object (`new StringBuilder("Python")`). Object này vẫn truy cập được qua `sb2` (và giờ cả `sb1` nữa), nên nó không đủ điều kiện bị garbage collection.

- **D)** Không object `StringBuilder` nào đủ điều kiện bị garbage collection.
  - Đáp án này sai vì, như đã giải thích, object được `sb1` reference ban đầu trở nên đủ điều kiện bị garbage collection sau khi `sb1` được gán lại cho `sb2`.



**2. Đáp án đúng là C và D.**

**Giải thích:**

- **A)** `implement` sai. Keyword đúng để implement một interface trong Java là `implements`.

- **B)** `array` sai. Java không có reserved keyword nào tên là `array`. Array được khai báo bằng dấu ngoặc vuông `[ ]`.

- **C)** `volatile` đúng. `volatile` là một reserved keyword được dùng để chỉ ra rằng giá trị của một biến sẽ bị thay đổi bởi các thread khác nhau.

- **D)** `extends` đúng. `extends` là reserved keyword được dùng trong khai báo class để kế thừa từ một superclass.



**3. Đáp án đúng là A và E.**

**Giải thích:**

- **A)** Dòng 1 là ví dụ của single-line comment.
  - Đáp án này đúng. Dòng 1 dùng `//` để bắt đầu single-line comment, một cách phổ biến để thêm ghi chú hoặc giải thích một phần code mà không ảnh hưởng đến việc thực thi.

- **B)** Dòng 3-7 minh họa việc dùng javadoc comment.
  - Đáp án này sai. Dòng 3-7 dùng block comment. Javadoc comment bắt đầu bằng `/**` và kết thúc bằng `*/`.

- **C)** Dòng 9 dùng javadoc comment để giải thích method `add`.
  - Đáp án này sai. Dòng 9 là single-line comment, không phải javadoc comment. Javadoc comment trong Java được định nghĩa với `/**` ở đầu và `*/` ở cuối, và được dùng riêng để mô tả class, method và field.

- **D)** Dòng 12 dùng comment `TODO` đặc biệt, khác với single-line comment.
  - Đáp án này sai. Dòng 12 dùng comment `TODO`, một quy ước nhiều developer tuân theo để đánh dấu những phần code cần phát triển hoặc chú ý thêm, nhưng nó vẫn là single-line comment.

- **E)** Dòng 3-7 là block comment được dùng như thể nó là javadoc comment.
  - Đáp án này đúng. Dòng 3-7 dùng block comment, vốn không được các công cụ javadoc xử lý và do đó không phù hợp để tạo tài liệu chính thức.



**4. Đáp án đúng là B và D.** 

**Giải thích:**

- **A)** Câu lệnh `import` trong `Application.java` là không cần thiết vì cả hai class nằm trong cùng thư mục.
  - Đáp án này sai. Trong Java, câu lệnh `import` được dùng để đưa một class hoặc cả một package vào phạm vi hiển thị, và sự cần thiết của nó được quyết định bởi package chứa các class, không phải vị trí thư mục của chúng. Kể cả khi các class nằm trong cùng thư mục, nếu chúng thuộc các package khác nhau, câu lệnh `import` là bắt buộc để dùng class này trong class kia.

- **B)** Câu lệnh `import` trong `Application.java` là cần thiết để dùng class `Calculator` vì chúng thuộc các package khác nhau.
  - Đây là đáp án đúng. Class `Calculator` nằm trong package `math`, và class `Application` nằm trong package `app`. Dù ở cùng thư mục, các package khác nhau đòi hỏi phải có câu lệnh `import` để dùng `Calculator` trong `Application`.

- **C)** Class `Calculator` sẽ không truy cập được trong `Application.java` do nằm ở thư mục khác.
  - Đáp án này sai. Kiểm soát truy cập của Java không dựa trên cấu trúc thư mục mà dựa trên khai báo `package` và `import`. Miễn là các class được đóng gói và import đúng, chúng có thể được truy cập xuyên qua các thư mục khác nhau.

- **D)** Xóa câu lệnh `package` khỏi cả hai file sẽ cho phép `Application.java` dùng `Calculator` mà không cần câu lệnh `import`, bất kể cấu trúc thư mục.
  - Đáp án này đúng. Xóa câu lệnh `package` khỏi cả hai file sẽ đặt chúng vào default package, và chúng có thể truy cập lẫn nhau mà không cần câu lệnh `import`. Tuy nhiên, điều này không được khuyến khích cho bất cứ thứ gì ngoài code rất đơn giản hoặc tạm thời, do các vấn đề về quản lý namespace và khả năng đọc hiểu.



**5. Đáp án đúng là A, B và C.** 

**Giải thích:**

- **A)** Một class hoặc member `public` có thể được truy cập bởi bất kỳ class nào khác trong cùng package hoặc trong bất kỳ package nào khác.
  - Điều này đúng. Modifier `public` cấp mức truy cập cao nhất. Một class hoặc member `public` có thể truy cập được từ bất kỳ class nào khác, bất kể chúng thuộc package nào.

- **B)** Một member `protected` có thể được truy cập bởi bất kỳ class nào trong package của nó, nhưng từ bên ngoài package, chỉ bởi các class extend class chứa member protected đó.
  - Điều này đúng. Mức truy cập `protected` cho phép một member được truy cập trong package của nó và bởi các subclass ở bất kỳ package nào. Nó cung cấp mức truy cập hạn chế hơn so với `public`.

- **C)** Một member với mức truy cập `default` (không có modifier) có thể được truy cập bởi bất kỳ class nào trong cùng package nhưng không từ một class ở package khác.
  - Điều này đúng. Nếu không có access modifier nào được chỉ định (còn gọi là mức truy cập `default`), member chỉ truy cập được trong các class cùng package. Mức này hạn chế hơn `protected` và `public`.

- **D)** Một member `private` chỉ có thể được truy cập bởi các method là member của cùng class hoặc trong cùng file.
  - Đáp án này sai vì member `private` chỉ có thể được truy cập trong cùng class. Không phải chuyện nằm trong cùng file, vì Java chỉ cho phép một public top-level class mỗi file.

- **E)** Một member `protected` có thể được truy cập bởi bất kỳ class nào trong chương trình Java, bất kể package.
  - Điều này sai. Truy cập `protected` không cấp quyền truy cập phổ quát cho mọi class trong chương trình. Truy cập từ ngoài package chỉ giới hạn cho các subclass.



**6. Đáp án đúng là D:** 

**Giải thích:**

- **A)** `class public Vehicle { }`
  - Đáp án này sai vì cú pháp sai. Thứ tự đúng là access modifier, tiếp theo là keyword `class`, rồi đến tên class.

- **B)** `public class vehicle { }`
  - Đáp án này sai chủ yếu do quy ước đặt tên class. Trong Java, tên class nên bắt đầu bằng chữ hoa, nên `vehicle` phải là `Vehicle`.

- **C)** `Public class Vehicle { }`
  - Đáp án này sai vì `Public` viết hoa không đúng. Java phân biệt chữ hoa chữ thường, và keyword đúng là `public`.

- **D)** `public class Vehicle { }`
  - Đây là đáp án đúng. Cú pháp theo đúng thứ tự: access modifier (`public`), tiếp theo là keyword `class`, rồi đến tên class (`Vehicle`), bắt đầu bằng chữ hoa đúng theo quy ước đặt tên của Java.

- **E)** `classVehicle public { }`
  - Đáp án này sai vì nhiều lý do: thứ tự cú pháp sai, không có dấu cách giữa `class` và tên class, và vị trí của access modifier không đúng.



**7. Đáp án đúng là A, C và D.** 

**Giải thích:**

- **A)** Biến `COUNT` có thể được truy cập trực tiếp bằng tên class mà không cần tạo instance của `Counter`.
  - Đáp án này đúng. Static variable thuộc về class và có thể được truy cập trực tiếp bằng tên class, như `Counter.COUNT`, mà không cần khởi tạo class.

- **B)** Method `getCount()` là ví dụ của static method vì nó trả về giá trị của một static variable.
  - Đáp án này sai. Dù `getCount()` trả về giá trị của một static variable, nó không được định nghĩa là static method. Static method được khai báo bằng modifier `static`. Bản chất instance hay non-static của method không thay đổi dựa trên các biến mà nó truy cập hay trả về.

- **C)** Mỗi khi một instance mới của `Counter` được tạo, biến `COUNT` được tăng lên.
  - Đáp án này đúng. Constructor tăng biến `COUNT` thêm 1 mỗi khi instance mới của `Counter` được tạo, minh họa tính chất chia sẻ của static variable giữa tất cả instance.

- **D)** Method `resetCount()` đặt lại biến `COUNT` về 0 cho tất cả instance của `Counter`.
  - Đáp án này đúng. Static method `resetCount()` đặt biến `COUNT` về 0. Vì `COUNT` là static, thay đổi này ảnh hưởng đến tất cả instance của class, do chỉ có một biến `COUNT` duy nhất được chia sẻ giữa chúng.



**8. Đáp án đúng là A, C và D.**

**Giải thích:**

- **A)** `int _age;` đúng. Identifier trong Java có thể bắt đầu bằng chữ cái, dấu gạch dưới (_) hoặc dấu đô la ($). Do đó, `_age` là identifier hợp lệ.

- **B)** `double 2ndValue;` sai. Identifier không thể bắt đầu bằng chữ số. Định dạng đúng là bắt đầu bằng chữ cái hoặc ký tự không phải chữ số như dấu gạch dưới hay dấu đô la.

- **C)** `boolean is_valid;` đúng. Tương tự `_age`, `is_valid` là identifier hợp lệ vì nó bắt đầu bằng chữ cái và có thể chứa dấu gạch dưới.

- **D)** `String $name;` đúng. Identifier cũng có thể bắt đầu bằng dấu đô la ($), khiến `$name` là identifier hợp lệ.

- **E)** `char #char;` sai. Ký tự hash (#) không được phép làm ký tự bắt đầu của identifier. Identifier chỉ có thể bắt đầu bằng chữ cái, `$` hoặc `_`.



**9. Đáp án đúng là B.** 

**Giải thích:**

- **A)** `int public static final computeSum(int num1, int num2)  { return num1 + num2 }` sai vì return type trong khai báo method nằm ngay trước tên method, không phải ở đầu.

- **B)** `private void updateRecord(int id) throws IOException {}` đúng. Khai báo method này đúng cú pháp trong Java. Nó dùng access modifier `private`, chỉ định return type (`void`), bao gồm một exception (`IOException`) mà method này có thể throw, và định nghĩa parameter list đúng cách.

- **C)** `synchronized boolean checkStatus [int status] { return status == 1; }` Cú pháp đúng yêu cầu dấu ngoặc đơn cho parameter list, kể cả khi không có parameter nào, nên khai báo đúng là `synchronized boolean checkStatus(int status)`.

- **D)** `float calculateArea() {}` sai vì method trả về `float` không thể có thân method rỗng.



**10. Đáp án đúng là (A và B) và (C và D).**

**Giải thích:**

Trong Java, method signature bao gồm tên method và parameter list. Return type, access modifier và exception list không được coi là một phần của method signature.

- **A)** (`public void update(int id, String value)`) 
- **B)** (`private void update(int identifier, String data)`) 
  - Hai đáp án trên có cùng method signature (`update(int, String)`) vì cả hai đều có cùng tên method và parameter list (một `int` và một `String`, theo thứ tự đó). Sự khác biệt về tên parameter (`id` so với `identifier` và `value` so với `data`) không ảnh hưởng đến method signature.

- **C)** `public boolean update(String value, int id)` 
- **D)** `void update(String value, int id)`
  - Đáp án này có cùng method signature (`update(String, int)`) với C vì cả hai đều có cùng tên method và parameter list (một `String` và một `int`, theo thứ tự đó). Access modifier và return type khác nhau không ảnh hưởng đến method signature.

- **E)** `protected void update(int id, int value) throws IOException`
  - Đáp án này cũng có parameter list khác (`update(int, int)`).



**11. Đáp án đúng là C và D.** 

**Giải thích:**

- **A)** Method `resetAccountPassword` có thể được truy cập từ bất kỳ class nào trong cùng package nhưng không từ một class ở package khác.
  - Đáp án này sai. Method `resetAccountPassword` có truy cập `private`, nghĩa là nó chỉ truy cập được trong chính class `AccountManager`, không từ bất kỳ class nào, kể cả trong cùng package. Phát biểu ban đầu hơi sai khi ngụ ý mức truy cập cấp package cho một method `private`.

- **B)** Method `auditTrail` có thể được truy cập từ bất kỳ class nào trong cùng package và từ các subclass ở package khác.
  - Đáp án này sai vì method `auditTrail` có truy cập package-private (không có access modifier), nghĩa là nó truy cập được từ bất kỳ class nào trong cùng package nhưng không từ các subclass ở package khác trừ khi chúng cũng nằm trong cùng package.

- **C)** Method `notifyAccountChanges` có thể được truy cập từ bất kỳ class nào trong cùng package và từ các subclass ở package khác.
  - Đáp án này đúng. Method `notifyAccountChanges` có truy cập `protected`, nghĩa là nó có thể được truy cập trong cùng package và bởi các subclass, kể cả khi các subclass ở package khác.

- **D)** Method `updateAccountInformation` có thể được truy cập từ bất kỳ class nào, bất kể package của nó.
  - Đáp án này đúng. Method `updateAccountInformation` là `public`, nên nó có thể được truy cập từ bất kỳ class nào, bất kể package mà nó thuộc về.



**12. Đáp án đúng là B.**

**Giải thích:**

Java hoàn toàn là pass-by-value. Điều này có nghĩa là khi truyền một biến vào method, Java truyền một bản sao giá trị của biến, không truyền chính biến đó. Thay đổi parameter bên trong method không ảnh hưởng đến biến gốc.

- **A)** 
```
Before calling changeValue: 10  
After calling changeValue: 20  
 ```
  - Đáp án này sai vì dù method `changeValue` đổi parameter `value` thành 20, thay đổi này không ảnh hưởng đến biến gốc `originalValue` bên ngoài method. Thay đổi trên `value` được thực hiện trên bản sao của nó, không phải trên chính `originalValue`.

- **B)** 
```
Before calling changeValue: 10  
After calling changeValue: 10  
```
  - Đây là đáp án đúng. `originalValue` được truyền theo giá trị (passed by value) vào method `changeValue`. Do đó, các thay đổi trên `value` bên trong `changeValue` không ảnh hưởng đến `originalValue`. Output xác nhận rằng `originalValue` không đổi sau lời gọi method.

- **C)**
```
Before calling changeValue: 20  
After calling changeValue: 20  
```
- **D)** 
```
Before calling changeValue: 20  
After calling changeValue: 10  
```
  - Các đáp án này sai vì chúng cho rằng thay đổi method parameter có thể ảnh hưởng đến biến gốc, điều không đúng với cách hoạt động của pass-by-value semantics trong Java.



**13. Đáp án đúng là B.**

**Giải thích:**

- **A)** `Object`
  - Đáp án này sai vì Java dùng method cụ thể nhất có thể áp dụng cho các parameter. Trong trường hợp này, `String` cụ thể hơn `Object`, nên method `print(String s)` được gọi.

- **B)** `String`
  - Đáp án này đúng. Dù `null` có thể được gán cho bất kỳ reference type nào, Java ưu tiên method cụ thể nhất có thể áp dụng cho method parameter. Vì `String` là type cụ thể hơn `Object`, method `print(String s)` được chọn thay vì method `print(Object o)`.

- **C)** Compilation fails
  - Compilation không thất bại vì cả hai method `print` đều được định nghĩa đúng và đều có khả năng khớp với lời gọi `print(null)`. Cơ chế method overloading của Java cho phép đoạn code này compile mà không gặp vấn đề gì.

- **D)** A runtime exception is thrown
  - Không có runtime exception nào bị throw vì lời gọi method `print` được resolve thành công thành method `print(String s)` tại compile time. Vì method được gọi đúng và không có code nào khác có thể gây runtime exception, chương trình này chạy thành công.



**14. Đáp án đúng là B và D.**

**Giải thích:**

- **A)** `public void print(String... messages, int count)`
  - Đáp án này sai vì varargs (variable arguments) phải là parameter cuối cùng trong parameter list của method. Việc đặt `int count` sau `String... messages` vi phạm quy tắc này.

- **B)** `public void print(int count, String... messages)`
  - Đáp án này đúng. Nó đặt parameter varargs `String... messages` ở cuối parameter list của method, đúng cú pháp bắt buộc khi dùng varargs.

- **C)** `public void print(String messages...)`
  - Đáp án này sai vì cú pháp `String messages...` không hợp lệ. Cú pháp đúng cho varargs là đặt dấu ellipsis (`...`) sau type và trước tên biến, như `String... messages`.

- **D)** `public void print(String[]... messages)`
  - Đáp án này đúng. Nó minh họa việc dùng varargs với array type, điều được cho phép. Ở đây, mỗi argument truyền cho `messages` có thể tự nó là một array các `String`, và `messages` sẽ được xử lý như một array của các array (`String[][]`).

- **E)** `public void print(String... messages, String lastMessage)`
  - Đáp án này sai, tương tự đáp án A, vì varargs phải là parameter cuối cùng trong parameter list của method. Không được phép có parameter khác sau parameter varargs.



**15. Đáp án đúng là A.** 

**Giải thích:**

- **A)** Class `Vehicle` minh họa constructor overloading bằng cách có nhiều constructor với parameter list khác nhau.
  - Đáp án này đúng. Constructor overloading trong Java là kỹ thuật có nhiều hơn một constructor với parameter list khác nhau trong cùng một class. Nó cho phép object của class được khởi tạo theo nhiều cách khác nhau. Class `Vehicle` có hai constructor, một constructor nhận `String` (cho vehicle type) và một constructor nhận `int` (cho max speed), đây là ví dụ hoàn hảo của constructor overloading.

- **B)** Class `Vehicle` sẽ compile với lỗi vì nó không cung cấp default constructor.
  - Đáp án này sai. Java không yêu cầu default constructor tường minh nếu class cung cấp bất kỳ constructor nào khác. Việc thiếu default constructor (constructor không nhận argument nào) không phải là compile error; nó chỉ có nghĩa là lập trình viên không thể khởi tạo class bằng no-argument constructor trừ khi constructor đó được định nghĩa tường minh.

- **C)** Có thể tạo một instance của `Vehicle` với cả `type` và `maxSpeed` được đặt thành giá trị cụ thể thông qua một lời gọi constructor duy nhất.
  - Đáp án này sai vì không constructor nào hiện có nhận cả parameter `String` lẫn `int`. Mỗi constructor chỉ đặt một field thành giá trị do caller chỉ định; field còn lại giữ default value (`null` hoặc `0`).

- **D)** Gọi một trong hai constructor sẽ khởi tạo cả hai field `type` và `maxSpeed` của class `Vehicle`.
  - Đáp án này sai. Gọi một trong hai constructor chỉ khởi tạo parameter được truyền cho nó. Constructor đầu tiên khởi tạo `type`, constructor thứ hai khởi tạo `maxSpeed`. Nếu không có thêm code, chẳng hạn constructor nhận cả hai parameter hoặc setter method, thì không cách nào để chỉ một constructor khởi tạo cả hai field.



**16. Đáp án đúng là A và D.** 

**Giải thích:**

- **A)** Instance initializer block được thực thi trước constructor, khởi tạo list `books` và thêm hai cuốn sách vào đó.
  - Đáp án này đúng. Instance initializer block được thực thi mỗi khi một instance của class được tạo, trước khi code của constructor chạy. Nó khởi tạo list `books` và thêm hai cuốn sách vào đó.

- **B)** Instance initializer block thay thế nhu cầu về constructor trong class `Library`.
  - Đáp án này sai. Instance initializer block không thay thế nhu cầu về constructor. Nó được dùng cùng với constructor, thường để khởi tạo những phần chung của nhiều constructor khác nhau trong một class.

- **C)** Instance initializer block không thể khởi tạo instance variable như `books`. 
  - Đáp án này sai. Instance initializer block thực sự có thể khởi tạo instance variable. Trong trường hợp này, list `books` là một instance variable được khởi tạo và thêm phần tử bên trong instance initializer block.

- **D)** Nếu nhiều instance của `Library` được tạo, instance initializer block sẽ thực thi mỗi lần trước constructor, đảm bảo list `books` được khởi tạo và thêm phần tử cho mỗi object.
  - Đáp án này đúng. Với mỗi instance mới của class `Library`, instance initializer block chạy trước khi constructor được gọi. Điều này đảm bảo list `books` được khởi tạo và thêm `"Book 1"` cùng `"Book 2"` cho mọi object `Library` được tạo.



**17. Đáp án đúng là A.** 

**Giải thích:**

- **A)** Static initializer block chỉ được thực thi một lần khi class được load vào bộ nhớ lần đầu, khởi tạo map `settings` với các default value.
  - Đáp án này đúng. Static initializer block được thực thi một lần duy nhất, khi class được load vào bộ nhớ JVM lần đầu. Trong trường hợp này, nó khởi tạo map `settings` với các giá trị cấu hình mặc định.

- **B)** Static initializer block cho phép instance method thay đổi map `settings` mà không cần tạo instance của class `Configuration`.
  - Đáp án này gây nhầm lẫn. Mặc dù static method như `getSetting` có thể truy cập và thay đổi static field như `settings` mà không cần instance của class, khả năng này không phải nhờ static initializer block mà là do bản chất của static field và static method.

- **C)** Static initializer block được thực thi mỗi khi một instance mới của class `Configuration` được tạo.
  - Đáp án này sai. Static initializer block không được thực thi mỗi khi instance mới của class được tạo. Chúng chỉ được thực thi một lần: khi class được load lần đầu.

- **D)** Static initializer block được thực thi trước mọi instance initializer block hoặc constructor, khi một instance của class được tạo.
  - Phát biểu này đúng một phần ở chỗ static initializer block được thực thi trước mọi instance initializer block hoặc constructor, nhưng nó gây nhầm lẫn vì ngụ ý một trình tự gắn với việc tạo instance. Điểm mấu chốt là static initializer block chạy một lần khi class được load, bất kể việc tạo instance.



**18. Đáp án đúng là B.** 

**Giải thích:**

Trong Java, thứ tự khởi tạo khi một class được load và một instance của class đó được tạo ra như sau:

1. **Static field và static initializer** được xử lý theo thứ tự chúng xuất hiện trong định nghĩa class. Đầu tiên, static initializer block in ra `"1. Static initializer"`. Sau đó, static field `staticValue` được khởi tạo bằng cách gọi `initializeStaticValue()`, in ra `"2. Static value initializer".`

2. **Instance field và instance initializer** được xử lý theo thứ tự chúng xuất hiện khi một instance của class được tạo. Đầu tiên, instance field `instanceValue` được khởi tạo bằng cách gọi `initializeInstanceValue()`, in ra `"3. Instance value initializer"`. Sau đó, instance initializer block in ra `"3. Instance initializer"`.

3. **Constructor** được thực thi sau khi tất cả field và instance initializer đã được xử lý. Constructor trong trường hợp này in ra `"4. Constructor"`.

Cách đánh số của output cho `"3. Instance initializer"` và `"3. Instance value initializer"` trong câu hỏi có thể khiến bạn nghĩ rằng chúng được thực thi đồng thời hoặc không theo thứ tự, nhưng điều quan trọng cần nhớ là instance field và instance initializer thực thi theo thứ tự chúng xuất hiện trong class, trước khi constructor được thực thi. Việc đánh số trùng nhau có nghĩa là instance field initializer chạy trước, tiếp theo là instance initializer, và cuối cùng, constructor chạy.

- **A)**
```
1. Static initializer
2. Static value initializer
3. Instance initializer
3. Instance value initializer
4. Constructor 
```
  - Đáp án này sai.

- **B)** 
```
1. Static initializer
2. Static value initializer
3. Instance value initializer
3. Instance initializer
4. Constructor
```
  - Đáp án này đúng.

- **C)** 
```
1. Static initializer
3. Instance initializer
2. Static value initializer
3. Instance value initializer
4. Constructor
``` 
  - Đáp án này sai. 

- **D)** 
```
2. Static value initializer
1. Static initializer
3. Instance value initializer
3. Instance initializer
4. Constructor 
```
  - Đáp án này sai.



**19. Đáp án đúng là A và C.** 

**Giải thích:**

- **A)** Gọi `toString()` trên một instance của `CustomObject` sẽ trả về một `String` bao gồm tên class, theo sau là ký hiệu `@` và hashcode của object.
  - Đáp án này đúng. Method `toString()` trong `java.lang.Object` trả về một string bao gồm tên class, ký hiệu `@` và hashcode của object ở dạng thập lục phân. Nếu `CustomObject` không override `toString()`, định dạng mặc định này được dùng.

- **B)** Gọi `equals(Object obj)` trên hai instance khác nhau của `CustomObject` có nội dung giống hệt nhau sẽ trả về `true` vì chúng là instance của cùng một class. 
  - Đáp án này sai. Implementation mặc định của `equals(Object obj)` trong `java.lang.Object` kiểm tra reference equality, nghĩa là nó chỉ trả về `true` nếu cả hai reference trỏ đến đúng cùng một object. Nếu không override `equals`, hai instance khác nhau của `CustomObject`, dù nội dung giống hệt nhau, cũng không được coi là bằng nhau.

- **C)** Dùng `hashCode()` trên bất kỳ instance nào của `CustomObject` sẽ tạo ra một số nguyên duy nhất, nhất quán qua nhiều lần gọi trong cùng một lần thực thi chương trình.  
  - Đáp án này đúng. Method `hashCode()` được thiết kế để trả về biểu diễn số nguyên của địa chỉ bộ nhớ của object hoặc một giá trị dẫn xuất từ đó. Mặc dù implementation chính xác không được quy định cụ thể và có thể khác nhau, nó vẫn nhất quán trong suốt quá trình thực thi chương trình đối với bất kỳ object nào.

- **D)** Method `clone()` có thể được dùng để tạo shallow copy của một instance `CustomObject` mà không cần `CustomObject` implement interface `Cloneable`. 
  - Đáp án này sai. Method `clone()` trong `java.lang.Object` là protected, và nó throw `CloneNotSupportedException` trừ khi class implement interface `Cloneable`. Nếu `CustomObject` không implement tường minh `Cloneable` và không override `clone()` để biến nó thành `public`, method này không thể dùng để clone instance của `CustomObject`.



**20. Đáp án đúng là B.**

**Giải thích:**

- **A)** Một static nested class có thể truy cập trực tiếp cả static lẫn non-static member của enclosing class. 
  - Đáp án này sai vì static nested class không thể truy cập trực tiếp non-static member của enclosing class. Nó chỉ có thể truy cập trực tiếp static member.

- **B)** Instance của static nested class có thể tồn tại mà không cần instance của enclosing class.
  - Đây là đáp án đúng. Static nested class gắn với outer class của nó, và không giống inner class, nó không cần instance của outer class để được khởi tạo. Điều này khiến nó hữu ích để nhóm các class sẽ được dùng trong static context.

- **C)** Static nested class chỉ có thể được khởi tạo bên trong static method của enclosing class.
  - Đáp án này sai. Static nested class có thể được khởi tạo từ bất kỳ context nào (static hoặc non-static) miễn là nó truy cập được (tức là visibility cho phép).

- **D)** Static nested class không được coi là member của enclosing class và không thể truy cập bất kỳ member nào của enclosing class.
  - Đáp án này sai. Static nested class thực sự được coi là member của enclosing class và có thể truy cập static member cùng static method của nó. Tuy nhiên, chúng không có quyền truy cập non-static member của enclosing class trừ khi chúng khởi tạo enclosing class.



**21. Đáp án đúng là A.** 

**Giải thích:**

- **A)** Một non-static nested class có thể truy cập trực tiếp cả static lẫn non-static member của enclosing class
  - Đáp án này đúng. Non-static nested class, hay inner class, có quyền truy cập tất cả member (bao gồm cả static lẫn non-static) của enclosing class, như được minh họa trong đoạn code nơi `InnerClass` truy cập field non-static `message` của `OuterClass`.

- **B)** Instance của non-static nested class có thể tồn tại độc lập với instance của enclosing class. 
  - Đáp án này sai. Instance của non-static nested class (inner class) được gắn ngầm với một instance của enclosing class. Do đó, chúng không thể tồn tại độc lập với instance của enclosing class. Trong đoạn code được cung cấp, instance `InnerClass` được tạo thông qua một instance của `OuterClass`.

- **C)** Non-static nested class không thể truy cập trực tiếp non-static member của enclosing class.
  - Đáp án này sai. Như đã nói ở trên, inner class có thể truy cập trực tiếp cả static lẫn non-static member của enclosing class.

- **D)** Non-static nested class phải được khai báo static để truy cập static member của enclosing class.
  - Đáp án này sai. Non-static nested class (inner class) được thiết kế để truy cập trực tiếp member của enclosing class mà không cần khai báo static. Khai báo một nested class là static sẽ biến nó thành static nested class, vốn có các thuộc tính truy cập khác với inner class.



**22. Đáp án đúng là A và D.** 

**Giải thích:**

- **A)** Local class có thể được khai báo trong bất kỳ block nào đứng trước một statement.
  - Đáp án này đúng. Local class trong Java thực sự có thể được khai báo trong bất kỳ block nào đứng trước một statement, chẳng hạn thân method, vòng lặp `for` hay câu lệnh `if`.

- **B)** Instance của local class có thể được tạo và dùng bên ngoài block nơi local class được định nghĩa.
  - Đáp án này sai. Instance của local class không thể được tạo và dùng bên ngoài block nơi chúng được định nghĩa. Scope của chúng chỉ giới hạn trong block mà chúng được khai báo.

- **C)** Local class là một loại static nested class và có thể truy cập trực tiếp cả static lẫn non-static member của enclosing class.
  - Đáp án này sai. Local class không phải static; chúng gắn với một instance của enclosing class và có quyền truy cập instance member của nó. Chúng không có static context như static nested class, và do đó chúng có thể truy cập cả static lẫn non-static member của enclosing class.

- **D)** Local class có thể truy cập local variable và parameter của enclosing block chỉ khi chúng được khai báo `final` hoặc effectively final.
  - Điều này đúng. Local class có thể truy cập local variable và parameter của method (hoặc bất kỳ enclosing block nào) nơi chúng được định nghĩa, nhưng những biến đó phải được khai báo `final` hoặc effectively final (nghĩa là giá trị của chúng không thay đổi sau khi được khởi tạo).



**23. Đáp án đúng là A.** 

**Giải thích:**

- **A)** Anonymous class có thể implement interface và extend class mà không cần khai báo một class có tên.
  - Đáp án này đúng. Anonymous class là cách extend class hoặc implement interface ngay tại chỗ mà không cần khai báo class chính thức. Điều này khiến chúng hữu ích để tạo các implementation nhanh, dùng một lần.

- **B)** Anonymous class phải override tất cả method trong superclass hoặc interface mà nó khai báo là đang implement hoặc extend.
  - Đáp án này sai. Anonymous class chỉ cần override các abstract method của superclass hoặc interface mà nó extend hoặc implement. Nếu superclass hoặc interface không có abstract method nào, thì anonymous class không cần override method nào cả.

- **C)** Anonymous class có thể có constructor như các class có tên.
  - Đáp án này sai. Anonymous class không có constructor có tên vì bản thân chúng không có tên. Thay vào đó, mọi khởi tạo được thực hiện qua instance initializer block.

- **D)** Instance của anonymous class không thể được truyền làm argument cho method.
  - Đáp án này sai. Instance của anonymous class thực sự có thể được truyền làm argument cho method. Chúng hữu ích để tạo implementation ngay lập tức cho interface hoặc subclass cần thiết cho một lời gọi method.



**24. Đáp án đúng là C.** 

**Giải thích:**

- **A)** Một source file có thể chứa nhiều public class.
  - Đáp án này sai. Một source file Java không thể chứa nhiều hơn một class `public`. Nếu một class được khai báo `public`, nó phải là class `public` duy nhất trong file, và tên file phải khớp với tên class.

- **B)** Private class có thể được khai báo ở top level trong một source file.
  - Đáp án này sai. Java không cho phép khai báo class là `private` ở top level. Chỉ class `public` hoặc package-private (không có access modifier) mới có thể được định nghĩa ở top level. Inner class có thể là `private`.

- **C)** Một class `public` phải được khai báo trong source file có cùng tên với class.
  - Điều này đúng. Theo quy tắc của Java, nếu một class được khai báo `public`, source file chứa nó phải có cùng tên với class, theo sau là phần mở rộng `.java`. Đây là quy tắc nghiêm ngặt giúp Java compiler dễ dàng tìm thấy source file.

- **D)** Nếu một source file chứa nhiều hơn một class, không class nào có thể là `public`.
  - Điều này sai. Dù đúng là nếu một source file chứa một class `public`, source file phải được đặt tên theo class `public` đó, nhưng không đúng khi nói rằng không class nào có thể là `public` nếu source file chứa nhiều hơn một class. Một source file có thể chứa nhiều class, nhưng chỉ một trong số đó có thể là `public`, và source file phải được đặt tên theo class `public` đó. Phát biểu này có thể ngụ ý rằng nhiều non-public top-level class là kịch bản phổ biến mà bỏ qua ngữ cảnh của quy tắc đặt tên class `public`.
