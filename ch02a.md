---
layout: answer

title: "Chương 2"
subtitle: "Sử dụng lập trình hướng đối tượng trong Java - Phần 2"
exam_objectives:
  - "Hiểu scope của biến, áp dụng encapsulation và tạo immutable object. Sử dụng local variable type inference."
  - "Triển khai inheritance, bao gồm abstract type, sealed type cũng như record class. Override method, kể cả method của class Object. Triển khai polymorphism và phân biệt object type với reference type. Thực hiện reference type casting, nhận diện object type bằng toán tử instanceof, và pattern matching với toán tử instanceof cùng cấu trúc switch."
  - "Tạo và sử dụng interface, nhận diện functional interface, và tận dụng private method, static method và default method trong interface."
---

## Đáp án {#answers}

**1. Đáp án đúng là C.**

**Giải thích:**

- **A)** Đoạn code compile và in ra `3` theo sau là `1`.
  - Đáp án này sai vì, mặc dù đoạn code in ra `3` theo sau là `1` do `x` nằm trong scope, việc cố truy cập `y` bên ngoài block khai báo của nó (block `if`) sẽ gây ra compile-time error.

- **B)** Đoạn code compile và in ra `3` theo sau là `1` cùng một giá trị không xác định cho `y`.
  - Đáp án này sai vì Java không cho phép truy cập các local variable (`y` trong trường hợp này) bên ngoài scope của chúng. Khái niệm "giá trị không xác định cho `y`" không áp dụng ở đây; compiler sẽ đơn giản là không compile đoạn code này.

- **C)** Đoạn code không compile vì `y` được truy cập bên ngoài scope của nó.
  - Đây là đáp án đúng. Local variable `y` được khai báo bên trong block `if`, do đó nó chỉ có thể truy cập được bên trong block đó. Cố truy cập nó bên ngoài scope, như thực hiện ở dòng `System.out.println(y);` cuối cùng, gây ra compile-time error, cụ thể là báo rằng không thể tìm thấy `y`.

- **D)** Đoạn code compile nhưng throw runtime exception khi cố in `y`.
  - Đáp án này sai vì vấn đề của đoạn code nằm ở compile time, không phải runtime. Compiler sẽ không cho đoạn code compile do vi phạm scope của local variable `y`, nên runtime exception liên quan đến `y` là điều không thể xảy ra.



**2. Đáp án đúng là C và D.**

**Giải thích:**

- **A)** `double x, double y;`
  - Đáp án này sai vì khi khai báo nhiều biến cùng kiểu trong một câu lệnh, bạn không lặp lại kiểu trước mỗi biến. Cú pháp đúng sẽ là `double x, y;`.

- **B)** `int i = 0, String s = "hello";`
  - Đáp án này sai vì lý do tương tự A; bạn không thể khai báo các biến thuộc kiểu khác nhau (`int` và `String` trong trường hợp này) trong một câu lệnh.

- **C)** `float f1 = 3.14, f2 = 6.28f;`
  - Đáp án này đúng. Bạn có thể khai báo nhiều biến cùng kiểu (`float` trong trường hợp này) trong một câu lệnh, và cũng hoàn toàn ổn khi khởi tạo chúng với giá trị ngay trong cùng câu lệnh đó.

- **D)** `char a = 'A', b, c = 'C';`
  - Đáp án này đúng. Việc khai báo nhiều biến cùng kiểu (`char` trong trường hợp này) và khởi tạo một số, tất cả hoặc không biến nào trong cùng một câu lệnh là hợp lệ.



**3. Đáp án đúng là B và D.**

**Giải thích:**

- **A)** `var` có thể được dùng để khai báo cả local variable bên trong method lẫn instance variable bên trong class.
  - Đáp án này sai vì `var` không thể được dùng để khai báo instance variable. Nó bị giới hạn cụ thể cho local variable bên trong method, constructor hoặc initializer block, vì dùng `var` cho field sẽ làm giảm độ rõ ràng của public API của class.

- **B)** Việc dùng `var` bị giới hạn cho local variable bên trong method, constructor hoặc initializer block.
  - Đáp án này đúng. `var` được thiết kế cho local variable type inference, giúp giảm đáng kể sự dài dòng của code Java trong những tình huống mà compiler có thể dễ dàng xác định kiểu của local variable từ initializer của nó. Việc sử dụng nó bị giới hạn để đảm bảo tính rõ ràng và tránh nhập nhằng trong những cấu trúc phức tạp hơn như class field hay method parameter.

- **C)** `var` có thể được dùng để khai báo method parameter.
  - Đáp án này sai. Ví dụ đã cho thấy rõ ràng rằng `var` không thể được dùng để khai báo method parameter. Hạn chế này đảm bảo rằng chữ ký method luôn thể hiện rõ yêu cầu về kiểu của chúng, một khía cạnh quan trọng trong contract của class với người gọi nó.

- **D)** `var` tăng tính dễ đọc bằng cách suy luận kiểu ở nơi ngữ cảnh đã rõ ràng, nhưng nó không được phép trong method signature để duy trì sự rõ ràng.
  - Đáp án này đúng. Trong khi `var` chủ yếu được dùng để cải thiện tính dễ đọc của code bằng cách giảm nhu cầu khai báo kiểu tường minh ở nơi có thể suy luận kiểu từ ngữ cảnh, nó không được phép trong method signature. Hạn chế này đảm bảo rằng kiểu của parameter trong method luôn được định nghĩa tường minh, hỗ trợ tính dễ đọc và khả năng bảo trì của public API.

- **E)** `var` có thể được dùng để khai báo class (static) variable.
  - Đáp án này sai. Tương tự instance variable, `var` không được phép dùng để khai báo class (`static`) variable. Lý do đằng sau hạn chế này khớp với mục tiêu duy trì khai báo kiểu tường minh trong cấu trúc của class, đảm bảo thiết kế của class vẫn rõ ràng và không nhập nhằng với cả compiler lẫn developer.


**4. Đáp án đúng là A và C.**

**Giải thích:**

- **A)** Subclass có thể truy cập trực tiếp các member `public` và `protected` của superclass, và các member package-private khi chúng nằm trong cùng package.
  - Đáp án này đúng. Subclass có thể dùng trực tiếp các member `public` và `protected` của superclass. Các member package-private cũng dùng được, nhưng chỉ khi subclass nằm trong cùng package. Các member `private` vẫn bị chặn, nên superclass phải expose chúng thông qua accessor.

- **B)** Trong Java, một class có thể extend nhiều class để đạt được multiple inheritance.
  - Đáp án này sai. Java không hỗ trợ multiple inheritance đối với class. Một class trong Java chỉ có thể extend một class khác, ngăn chặn những phức tạp như diamond problem và sự rối rắm đi kèm với multiple inheritance.

- **C)** Keyword `extends` được dùng trong Java để tạo subclass kế thừa từ một superclass.
  - Đáp án này đúng. `extends` tạo ra một subclass kế thừa field và method của một superclass duy nhất, tạo quan hệ is-a giữa chúng.

- **D)** Subclass trong Java có thể truy cập trực tiếp các member `private` của superclass.
  - Đáp án này sai. Subclass không thể truy cập trực tiếp các member `private` của superclass. Thay vào đó, nó có thể truy cập chúng thông qua các accessor `public` hoặc `protected` mà superclass cung cấp. Nguyên lý encapsulation này đảm bảo sự tương tác có kiểm soát với state của superclass.


**5. Đáp án đúng là A và C.**

**Giải thích:**

- **A)** Đoạn code sẽ compile và in ra `"Dog eats"` khi chạy.
  - Đáp án này đúng. Class `Dog` đã cung cấp implementation cho method `eat`, vốn là abstract trong superclass `Animal`. Vì `myAnimal` có kiểu `Animal` nhưng được instantiate như một `Dog`, nó sẽ gọi method `eat` đã override trong class `Dog`, in ra `"Dog eats"`.

- **B)** Class `Animal` có thể được instantiate.
  - Đáp án này sai. Class `Animal` là abstract và không thể được instantiate. Cố tạo instance của `Animal` trực tiếp (`new Animal()`) sẽ dẫn đến compilation error.

- **C)** Xóa method `eat` khỏi class `Dog` sẽ gây ra compilation error.
  - Đáp án này đúng. Vì `Dog` extends abstract class `Animal` và `Animal` có abstract method `eat`, `Dog` phải cung cấp implementation cho `eat`. Không làm được điều đó sẽ khiến đoạn code không compile vì `Dog` cũng sẽ bị coi là abstract.

- **D)** Class `Cat` là cần thiết để đoạn code compile và chạy.
  - Đáp án này sai. Class `Cat` không được tham chiếu trong method `main` hay bất kỳ đâu khác trong đoạn code đã cho. Do đó, nó không cần thiết cho việc compile và thực thi đoạn code này.


**6. Đáp án đúng là B và C.**

**Giải thích:**

- **A)** Class `Person` phải override method `getSpeed`.
  - Đáp án này sai. Class `Person` không bắt buộc phải override method `getSpeed` vì đây là default method trong interface `Runnable`. Default method cung cấp một implementation có thể được dùng hoặc override bởi các class implement nó, nhưng việc override không bắt buộc.

- **B)** Biến `distance` trong interface `Walkable` mặc nhiên là `public`, `static` và `final`.
  - Đáp án này đúng. Trong Java, mọi biến được khai báo trong interface đều mặc nhiên là `public`, `static` và `final`. Điều này có nghĩa biến `distance` trong interface `Walkable` là một constant và phải được khởi tạo tại điểm khai báo. Nó có thể được truy cập bằng tên interface, như `Walkable.distance`.

- **C)** Một object `Person` có thể gọi method `getSpeed` mà không cần bất kỳ implementation nào trong class `Person`.
  - Đáp án này đúng. Vì interface `Runnable` cung cấp default implementation cho method `getSpeed`, một object `Person` có thể gọi method `getSpeed` mà không cần thêm implementation nào trong chính class `Person`. Implementation mặc định từ interface sẽ được dùng.

- **D)** Interface `Runnable` gây ra compilation error do xung đột tên với `java.lang.Runnable`.
  - Đáp án này sai vì Java hỗ trợ đầy đủ việc phân giải namespace. Interface `Runnable` được khai báo trong đoạn code và `java.lang.Runnable` tồn tại trong các package khác nhau. Không có compilation error trừ khi có nỗ lực import cả hai trong cùng một file mà không dùng fully qualified name. Ngoài ra, tình huống này không liên quan trực tiếp đến chức năng hay khai báo của interface theo trọng tâm của kỳ thi.



**7. Đáp án đúng là A.**

**Giải thích:**

- **A)** Class `Shape` được định nghĩa đúng là sealed class, chỉ cho phép các class được chỉ định extend nó.
  - Đáp án này đúng. Class `Shape` được khai báo là sealed class, nghĩa là nó chỉ có thể được extend bởi những class mà nó cho phép tường minh thông qua mệnh đề `permits`. Trong trường hợp này, `Shape` cho phép `Circle` và `Square` extend nó, và cả hai class đều được định nghĩa đúng là các permitted subclass.

- **B)** Class `Square` không extend class `Shape` đúng cách vì nó không được đánh dấu là `final`.
  - Đáp án này sai. Không có yêu cầu nào buộc những class extend một sealed class phải được đánh dấu là `final` nếu chúng là non-sealed. Keyword `non-sealed` cho phép tường minh class `Square` extend sealed class `Shape` mà không cần final, cho thấy nó có thể được extend tiếp.

- **C)** Class `Circle` có thể được extend tiếp bởi các class khác.
  - Đáp án này sai. Class `Circle` được khai báo là `final`, nghĩa là nó không thể được extend tiếp, phù hợp với ràng buộc khi extend một sealed class rằng permitted subclass có thể là final, sealed hoặc non-sealed.

- **D)** Method `area` trong class `Shape` phải cung cấp một default implementation.
  - Đáp án này sai. Các abstract class như `Shape` không bắt buộc phải cung cấp implementation cho các abstract method của chúng. Mục đích của abstract class là định nghĩa một template mà các subclass sẽ tuân theo, bao gồm việc implement mọi abstract method được khai báo trong abstract class.


**8. Đáp án đúng là D.**

**Giải thích:**

- **A)** Một tham chiếu đến static context của class, cho phép truy cập static method và field.
  - Đáp án này sai. Keyword `this` không tham chiếu đến static context của class. Nó tham chiếu cụ thể đến instance hiện tại của class. Static method và field thuộc về chính class và không thuộc instance nào, nên chúng không thể được truy cập thông qua `this`.

- **B)** Một biến đặc biệt lưu giá trị trả về của method.
  - Đáp án này sai. Keyword `this` không lưu giá trị trả về của method. Nó được dùng bên trong instance method hoặc constructor để tham chiếu đến object hiện tại mà method hay constructor đang được gọi trên đó.

- **C)** Một keyword tùy chọn có thể luôn được lược bỏ mà không ảnh hưởng đến chức năng của code.
  - Đáp án này sai. Mặc dù đúng là trong một số trường hợp `this` có thể được lược bỏ (ví dụ, khi truy cập instance field hoặc method mà không có xung đột tên), việc dùng nó là cần thiết trong những tình huống như constructor chaining (lời gọi `this()`) hoặc khi tên tham số của method che khuất tên instance field. Trong những tình huống đó, `this` làm rõ code đang tham chiếu đến biến nào.

- **D)** Một tham chiếu đến object hiện tại, mà instance variable của nó đang được gọi.
  - Đáp án này đúng. Keyword `this` trong Java được dùng để tham chiếu đến object hiện tại—object mà instance variable, method hoặc constructor của nó đang được gọi. Bạn có thể thấy cách dùng nó ở dòng 5 để gọi một constructor khác trong cùng class, ở dòng 14 để phân biệt tham số method `size` với instance variable `size`, và trong method `updateWidget` để truy cập instance variable `size`. Cách dùng này minh họa `this` như một cách để tham chiếu tường minh đến thuộc tính hoặc method của object hiện tại.


**9. Đáp án đúng là A và B.**

**Giải thích:**

- **A)** Keyword `super` được dùng trong constructor của `Dog` để gọi constructor của superclass.
  - Đáp án này đúng. Trong constructor `Dog`, `super(name);` được dùng để gọi constructor của superclass (`Animal`) với tham số `name`. Điều này cần thiết để khởi tạo field `name` kế thừa từ class `Animal` trong instance `Dog`.

- **B)** Method `eat` trong class `Dog` dùng `super` để gọi method `eat` của superclass.
  - Đáp án này đúng. Method `eat` trong class `Dog` gọi `super.eat();` để gọi method `eat` được định nghĩa trong superclass (`Animal`). Điều này cho phép class `Dog` mở rộng chức năng của method `eat` vượt ra ngoài những gì được định nghĩa trong superclass, minh họa method overriding và việc dùng `super` để truy cập method bị override.

- **C)** Xóa lời gọi `super.eat();` trong method `eat` của class `Dog` sẽ khiến class `Dog` không compile.
  - Đáp án này sai. Xóa lời gọi `super.eat();` khỏi method `eat` của class `Dog` sẽ không khiến class này không compile. Nó chỉ đơn giản có nghĩa là method `eat` của class `Dog` không còn gọi method `eat` của superclass, làm thay đổi hành vi của chương trình nhưng không ảnh hưởng đến khả năng compile.

- **D)** Keyword `super` có thể được dùng bên trong một `static` method của class `Dog` để truy cập các member của `Animal`.
  - Đáp án này sai. `super` tham chiếu đến instance hiện tại được nhìn nhận như kiểu của superclass, nên nó chỉ có thể xuất hiện ở nơi `this` khả dụng. Bên trong `static` method, `static` initializer hay bất kỳ static context nào khác, không có instance, và mọi cách dùng `super` sẽ dẫn đến compile-time error.



**10. Đáp án đúng là C.**

**Giải thích:**

- **A)** Đoạn code compile và in ra `"Car driving at speed: 60"`.
  - Đáp án này sai vì method `drive` trong class `Car` có kiểu tham số khác (`long`) so với method trong class `Vehicle` (`int`). Do khác biệt về kiểu tham số, method `drive` của class `Car` không override mà overload method `drive` của class `Vehicle`. Vì method được gọi trên tham chiếu `Vehicle`, method `drive` của class `Vehicle` được gọi.

- **B)** Đoạn code không compile vì method `drive` không thể được gọi bằng tham chiếu `Vehicle`.
  - Đáp án này sai vì `Vehicle` định nghĩa method `drive` đúng cách.

- **C)** Đoạn code không compile vì method `drive` trong class `Car` không override đúng method `drive` trong class `Vehicle`.
  - Đáp án này đúng. Annotation `@Override` cho compiler biết tường minh rằng method được annotate nhằm override một method từ superclass. Tuy nhiên, method `drive` trong class `Car` có tham số kiểu `long`, còn method `drive` trong class `Vehicle` có tham số kiểu `int`. Vì kiểu tham số khác nhau, method của `Car` không override method của `Vehicle`, đó là một overload. Compiler thực thi contract `@Override` một cách nghiêm ngặt, nên nó tạo ra error như: `method does not override or implement a method from a supertype`. Kết quả là đoạn code không compile.
  
- **D)** Đoạn code compile và in ra `"Vehicle driving at speed: 60"` vì method `drive` trong class `Car` là overload, không phải override.
  - Đáp án này sai. Nó xác định đúng rằng method của `Car` là overload chứ không phải override, nhưng kết luận sai rằng đoạn code compile. Annotation `@Override` ngăn việc compile vì method được annotate thực ra không override bất cứ thứ gì (xem đáp án C). Nếu annotation `@Override` bị xóa, thì đáp án này sẽ mô tả hành vi đúng. Nhưng khi annotation còn đó, đoạn code không compile.


**11. Đáp án đúng là E.**

**Giải thích:**

- **A)** Đoạn code compile và in ra `"Apple flavor"` theo sau là `"Red"`.
  - Đáp án này sai vì, mặc dù method `flavor` thực sự sẽ in `"Apple flavor"` nhờ polymorphism (class `Apple` override method `flavor` của `Fruit`), đoạn code sẽ không compile nếu method `color()` được gọi trên tham chiếu `Fruit`. Điều này là vì method `color` không thuộc interface của class `Fruit`.

- **B)** Đoạn code compile và in ra `"Fruit flavor"`.
  - Đáp án này sai vì lý do tương tự A. Method `flavor` sẽ in `"Apple flavor"` do method bị override trong class `Apple`, không phải `"Fruit flavor"`. Tuy nhiên, sự hiện diện của lời gọi method `color()` vẫn sẽ ngăn việc compile.

- **C)** Đoạn code compile nhưng throw runtime exception khi cố gọi `color()`.
  - Đáp án này sai vì vấn đề xảy ra ở compile time, không phải runtime. Compiler Java sẽ không cho phép gọi một method trên reference type nếu method đó không được định nghĩa trong class của reference type hay hệ thống phân cấp superclass của nó.

- **D)** Đoạn code không compile vì `Apple` không phải là kiểu hợp lệ của `Fruit`.
  - Đáp án này sai. `Apple` là kiểu hợp lệ của `Fruit` nhờ inheritance (`Apple extends Fruit`). Mối quan hệ này cho phép một object `Apple` được tham chiếu bởi một biến `Fruit`.

- **E)** Đoạn code không compile vì method `color` không được định nghĩa trong class `Fruit`.
  - Đáp án này đúng. Method `color` chỉ được định nghĩa trong class `Apple` và không có trong class `Fruit`. Vì reference type của `myFruit` là `Fruit`, vốn không có method `color`, việc cố gọi `myFruit.color()` sẽ dẫn đến compilation error. Điều này minh họa một nguyên lý quan trọng của polymorphism: kiểu của tham chiếu (không phải object) quyết định những method nào có thể được gọi.


**12. Đáp án đúng là B và D.**

**Giải thích:**

- **A)** `((Dog)anotherAnimal).bark();`
  - Đáp án này sai vì nó cố cast `anotherAnimal` sang `Dog` mà không kiểm tra kiểu thực tế của nó trước. Vì `anotherAnimal` là instance của `Animal` (không phải `Dog`), việc cố cast này sẽ compile, nhưng nó sẽ gây ra `ClassCastException` lúc runtime.

- **B)** `if (anotherAnimal instanceof Dog) ((Dog)anotherAnimal).bark();`
  - Đáp án này đúng. Nó dùng `instanceof` để kiểm tra liệu `anotherAnimal` có phải là instance của `Dog` trước khi cố cast và gọi `bark()`. Trong trường hợp này, vì `anotherAnimal` không phải instance của `Dog`, kiểm tra này ngăn việc cast và gọi method, tránh một `ClassCastException`.

- **C)** `((Cat)animal).meow();`
  - Đáp án này sai vì nó cast `animal` sang `Cat` và cố gọi `meow()`. Vì `animal` thực ra là instance của `Dog`, việc cast này sẽ compile nhưng sẽ dẫn đến `ClassCastException` lúc runtime.

- **D)** `if (anotherAnimal instanceof Cat) ((Cat)anotherAnimal).meow();`
  - Đáp án này đúng. Nó kiểm tra liệu `anotherAnimal` có phải instance của `Cat` trước khi cast nó sang `Cat` và gọi `meow()`.


**13. Đáp án đúng là A.**

**Giải thích:**

- **A)** Đoạn code compile và in ra `"String with Java: Hello Java!"` theo sau là `"Integer greater than 10: 15"`.
  - Đáp án này đúng. Đoạn code minh họa hiệu quả việc dùng pattern matching với toán tử `instanceof` cho cả kiểu `String` lẫn `Integer`. Tính năng pattern matching kiểm tra liệu `input` có phải instance của `String` hay `Integer` và bind nó vào một biến (`s` cho `String` và `i` cho `Integer`) trong scope của block `if` và `else if`. Toán tử logic `&&` được dùng đúng cách để kiểm tra thêm có điều kiện các thuộc tính của biến (`s.contains("Java")` và `i > 10`). Nhờ đó, method `process` in ra output cho những input lần lượt là một `String` chứa `"Java"` và một `Integer` lớn hơn `10`.

- **B)** Đoạn code compile nhưng chỉ in ra `"String with Java: Hello Java!"` vì integer không được hỗ trợ với pattern matching.
  - Đáp án này sai vì pattern matching hoạt động với mọi reference type, bao gồm `Integer`. Đoạn code có hỗ trợ integer và thực hiện các kiểm tra bổ sung bằng pattern matching một cách đúng đắn.

- **C)** Đoạn code không compile vì pattern matching trong `instanceof` không thể được kết hợp với các toán tử logic như `&&`.
  - Đáp án này sai. Đoạn code sẽ compile và chạy như mong đợi. Pattern matching trong `instanceof` thật sự có thể được kết hợp với các toán tử logic như `&&` để kiểm tra bổ sung trong cùng một câu lệnh điều kiện, như minh họa trong đoạn code.

- **D)** Đoạn code compile nhưng in ra cả bốn dòng do dùng pattern matching sai cách khiến nó luôn đánh giá thành `true`.
  - Đáp án này sai vì cách dùng pattern matching trong đoạn code được cung cấp là đúng và không luôn đánh giá thành `true`. Đoạn code in đúng các message cụ thể chỉ cho những input khớp với các điều kiện đã cho.


**14. Đáp án đúng là E.**

**Giải thích:**

- **A)** Biến các method `setName`, `setPrice` và `setStock` thành public sẽ tăng cường encapsulation của class.
  - Đáp án này sai. Biến các setter thành public thực ra sẽ làm giảm encapsulation của class bằng cách cho phép các class bên ngoài sửa đổi field không giới hạn, có thể bỏ qua mọi logic validation chứa trong setter.

- **B)** Class không được encapsulated vì các field của class `Product` là `private`.
  - Đáp án này sai. Việc dùng các field `private` là một khía cạnh nền tảng của encapsulation. Nó ngăn các class bên ngoài truy cập và sửa trực tiếp state của object, từ đó thực thi encapsulation.

- **C)** Encapsulation bị suy yếu vì constructor cho phép đặt field trực tiếp mà không có validation.
  - Đáp án này sai. Constructor không làm suy yếu encapsulation; thay vào đó, nó dùng các setter `private` có chứa logic validation. Điều này đảm bảo state của object được quản lý và validate đúng cách khi object được tạo.

- **D)** Class `Product` nên có các getter package-private để cải thiện encapsulation.
  - Đáp án này sai. Biến các getter thành package-private sẽ giới hạn khả năng sử dụng của class và không tự nó cải thiện encapsulation. Getter public là cần thiết để các class bên ngoài xem (nhưng không sửa) state của object.

- **E)** Class được encapsulated đúng cách nhờ cung cấp getter public cho mọi field và setter private có validation, đảm bảo kiểm soát state của các object của nó.
  - Đáp án này đúng. Class `Product` minh họa thực hành encapsulation đúng đắn bằng cách để field `private` và kiểm soát truy cập qua getter `public` và setter `private`. Các setter bao gồm logic validation, đảm bảo chỉ những state hợp lệ được gán cho field. Design pattern này đảm bảo state nội bộ của các instance `Product` vừa được bảo vệ vừa được quản lý đúng cách.


**15. Đáp án đúng là A và E.**

**Giải thích:**

- **A)** Class `SavingsAccount` không thể truy cập trực tiếp field `balance` do access modifier `private` của nó trong class `Account`.
  - Đáp án này đúng. Thiết kế này chủ đích hạn chế truy cập trực tiếp vào field `balance` để duy trì encapsulation.

- **B)** Method `getBalance` nên là `public` để cho phép `SavingsAccount` truy cập số dư tài khoản.
  - Đáp án này sai. Biến `getBalance` thành `public` sẽ tăng visibility của nó một cách không cần thiết. `protected` là đủ để subclass truy cập, và thay đổi này không cần thiết để `SavingsAccount` hoạt động đúng, nên phát biểu này sai.

- **C)** Method `deposit` trong class `Account` nên được đánh dấu là `final` để ngăn override.
  - Đáp án này sai. Đánh dấu `deposit` là `final` sẽ ngăn nó bị override trong subclass, điều không phải là yêu cầu hay gợi ý được chỉ ra bởi đoạn code đã cho. Quyết định để một method là `final` nên dựa trên nhu cầu thiết kế cụ thể thay vì một nguyên tắc chung của encapsulation.

- **D)** Field `interestRate` trong class `SavingsAccount` vi phạm nguyên lý encapsulation vì là `private`.
  - Đáp án này sai. Dùng access modifier `private` cho `interestRate` trong `SavingsAccount` là ví dụ của encapsulation đúng cách. Nó hạn chế truy cập field từ bên ngoài class, phù hợp với nguyên lý encapsulation, nên đáp án này sai.

- **E)** Class `Account` encapsulated field `balance` đúng cách, và `SavingsAccount` tuân thủ encapsulation bằng cách truy cập `balance` thông qua `getBalance` và `deposit`.
  - Đáp án này đúng. Class `Account` dùng access `private` cho field `balance` để đóng gói state của nó, cung cấp các method `protected` và package-private (`getBalance` và `deposit`) cho việc truy cập và sửa đổi có kiểm soát. `SavingsAccount` tôn trọng encapsulation này bằng cách dùng các method đó để tương tác với field `balance`, thể hiện hiểu biết và áp dụng đúng nguyên lý encapsulation. Thiết kế này cho phép `SavingsAccount` tận dụng chức năng do `Account` cung cấp mà không phá vỡ encapsulation, một mục tiêu then chốt trong thiết kế hướng đối tượng.


**16. Đáp án đúng là C.**

**Giải thích:**

- **A)** Object `Contact` là mutable vì class `Address` không phải `final`.
  - Đáp án này sai vì class `Address` không ảnh hưởng trực tiếp đến tính immutable của object `Contact`. Class `Contact` đảm bảo tính immutable của nó bằng cách không cung cấp setter và bằng cách tạo deep copy của các mutable object, như `Address`, cả trong constructor lẫn getter.

- **B)** Object `Contact` là immutable, nhưng chỉ vì nó không cung cấp setter.
  - Đáp án này sai. Mặc dù đúng là nó không cung cấp setter, đáp án này không nắm bắt đầy đủ bản chất của tính immutability. Do đó, nó không nêu bật thực tế rằng mọi field trong `Contact` đều là `final` cùng chiến lược defensive copying.

- **C)** Object `Contact` là immutable, và nó ngăn rò rỉ mutable internal state đúng cách thông qua defensive copying.
  - Đây là đáp án đúng. Class `Contact` là immutable vì nó thỏa mãn mọi tiêu chí của tính immutability: class được khai báo là `final` (ngăn subclassing), mọi field của nó là `private` và `final`, và nó không cung cấp setter nào. Ngoài ra, nó triển khai defensive copying cho mutable field `Address` để đảm bảo state nội bộ không thể bị thay đổi bởi các thay đổi bên ngoài đối với object `Address` được truyền vào hoặc trả về. Điều này ngăn rò rỉ mutable internal state của nó.

- **D)** Object `Contact` là mutable vì object `Address` có thể bị thay đổi thông qua method `getAddress`.
  - Đáp án này sai vì tính immutable của object `Contact` được duy trì nhờ defensive copying. Method `getAddress` trả về một instance `Address` mới mỗi lần được gọi, đảm bảo state của object `Address` gốc không thể bị thay đổi từ bên ngoài object `Contact`.

- **E)** Object `Contact` là immutable nhưng không ngăn được truy cập vào mutable internal state của nó.
  - Đáp án này sai vì object `Contact` có triển khai một chiến lược để ngăn truy cập vào mutable internal state của nó: nó dùng defensive copying cho object `Address` trong cả constructor lẫn getter, đảm bảo state nội bộ không đổi trước các sửa đổi từ bên ngoài.

