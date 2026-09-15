---
layout: answer

title: "Chương 3"
subtitle: "Làm việc với Records và Enums"
exam_objectives:
  - "Tạo class và record, định nghĩa và sử dụng instance field, static field, method, constructor cùng instance initializer và static initializer."
  - "Tạo và sử dụng enum type với field, method và constructor."
---

## Đáp án {#answers}

**1. Đáp án đúng là C.**

**Giải thích:**

- **A)** Record `Employee` định nghĩa tường minh một public constructor để khởi tạo các field của nó.
  - Đáp án này sai vì record `Employee` không định nghĩa tường minh một constructor `public`. Record tự động sinh ra một constructor `public` với cùng các tham số như trong khai báo của record.

- **B)** Các field `name` và `age` có thể được gán lại giá trị mới sau khi một object `Employee` được tạo ra.
  - Đáp án này sai vì các field trong record là `final`, nghĩa là chúng không thể được gán lại giá trị mới sau khi object `Employee` đã được tạo. Tính bất biến (immutability) này là một trong những đặc điểm quan trọng của record.

- **C)** Record `Employee` ngầm tạo ra một constructor `public` cùng các field `private` `final` cho `name` và `age`.
  - Đây là đáp án đúng. Record ngầm tạo ra một public constructor cho các field của record và cũng biến các field này thành `private` và `final`. Nghĩa là bạn không phải tự tay viết code boilerplate cho constructor, getter hay để đảm bảo tính bất biến.

- **D)** Việc định nghĩa getter cho các field `name` và `age` trong record `Employee` là bắt buộc.
  - Đáp án này sai vì record tự động sinh ra các public method để truy cập field, gọi là accessor method, về bản chất đóng vai trò như getter. Do đó, việc định nghĩa getter riêng cho các field là không bắt buộc (thậm chí là không thể).



**2. Đáp án đúng là B.**

**Giải thích:**

- **A)** Field `balance` có thể bị sửa đổi bằng một public setter method bên trong record `Account`.
  - Đáp án này sai vì record trong Java không hỗ trợ public setter method cho các field của chúng. Các field của record là `final` và không thể bị sửa đổi sau khi object được khởi tạo, đây là một khía cạnh then chốt trong thiết kế của chúng để thực thi tính bất biến.

- **B)** Sau khi object `Account` được tạo, `id` và `balance` của nó không thể bị thay đổi.
  - Đây là đáp án đúng. Record bất biến theo thiết kế, nghĩa là khi một record object đã được tạo, giá trị các field của nó (`id` và `balance` trong trường hợp này) không thể thay đổi. Tính bất biến này được đảm bảo bằng cách để các field là `private` và `final`, và không cung cấp setter method.

- **C)** Tính bất biến của record có thể bị vượt qua nếu bạn định nghĩa setter method tùy chỉnh cho các field `id` và `balance`.
  - Đáp án này sai. Không thể định nghĩa setter method tùy chỉnh cho các field của record vì record không cho phép định nghĩa mutator cho các component của nó.

- **D)** Record cho phép sửa đổi giá trị field nếu được truy cập trực tiếp, không dùng setter method.
  - Đáp án này sai vì các field trong record ngầm định là `final` và private, nghĩa là chúng không thể bị sửa đổi trực tiếp hay thông qua setter method. Thiết kế của record thực thi tính bất biến này để đảm bảo các instance của record thực sự là những data carrier bất biến.


**3. Đáp án đúng là D.**

**Giải thích:**

- **A)** `Product p = new Product();`
  - Đáp án này sai vì constructor mặc định không tham số không tồn tại đối với record trong Java. Record yêu cầu tất cả field của nó phải được chỉ định tại thời điểm khởi tạo.

- **B)** `Product p = Product(101, "Coffee", 15.99);`
  - Đáp án này sai vì cú pháp dùng ở đây không hợp lệ để tạo một instance mới của record trong Java. Cú pháp đúng để khởi tạo một record là dùng keyword `new` theo sau là tên record và các tham số trong ngoặc đơn.

- **C)** `Product p = {101, "Coffee", 15.99};`
  - Đáp án này sai vì nó nhầm với cú pháp khởi tạo array. Trong Java, object, bao gồm record, không thể được khởi tạo bằng cặp ngoặc nhọn mà không có keyword `new` và constructor phù hợp.

- **D)** `Product p = new Product(101, "Coffee", 15.99);`
  - Đây là đáp án đúng. Record trong Java được khởi tạo bằng keyword `new` theo sau là constructor của record, đòi hỏi phải truyền tất cả field được định nghĩa trong record. Cú pháp này tạo đúng một record `Product` mới với `id`, `name` và `price` đã cho.


**4. Đáp án đúng là B.**

**Giải thích:**

- **A)** Record không thể implement interface vì chúng là `final` và bất biến theo thiết kế, điều này ngăn cản mọi hình thức tùy biến hành vi.
  - Đáp án này sai. Record trong Java có thể implement interface. Tính final và bất biến của record không ngăn chúng implement interface, vốn có thể được dùng để thêm hành vi hoặc ràng buộc hợp đồng cho một record.

- **B)** Record này implement đúng interface `Comparable`, cho phép các object `Item` được sắp xếp dựa trên `price` của chúng.
  - Đây là đáp án đúng. Định nghĩa record được cho implement đúng interface `Comparable<Item>` bằng cách override method `compareTo`. Việc tùy biến này cho phép các instance của record `Item` được sắp xếp dựa trên field `price`, cho thấy record thực sự có thể implement interface và override method khi cần.

- **C)** Việc implement interface trong record chỉ được giới hạn cho functional interface do bản chất bất biến của chúng.
  - Đáp án này sai. Không có giới hạn nào như vậy khiến record chỉ được implement functional interface. Record có thể implement bất kỳ interface nào, kể cả những interface có nhiều abstract method, miễn là record cung cấp phần triển khai cho các abstract method được định nghĩa trong interface đó.

- **D)** Method `compareTo` không thể bị override trong record vì method overriding không được hỗ trợ trong record type.
  - Đáp án này sai. Record có thể override các method từ interface mà chúng implement, bao gồm method `compareTo` từ interface `Comparable` trong ví dụ này. Method overriding là một khía cạnh then chốt của việc implement interface và được record type trong Java hỗ trợ đầy đủ.


**5. Đáp án đúng là A và D.**

**Giải thích:**

- **A)** 
```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```
  - Đáp án này đúng. Nó minh họa một khai báo enum hợp lệ trong Java. Enum được dùng để định nghĩa một tập các hằng số có tên, và cú pháp này là cách chuẩn để khai báo chúng. Access modifier `public` khiến enum này có thể được truy cập từ bất kỳ class nào khác.

- **B)** 
```java
enum Month {
    private JANUARY, FEBRUARY, MARCH, APRIL, MAY, JUNE, JULY, AUGUST, SEPTEMBER, OCTOBER, NOVEMBER, DECEMBER;
}
```
  - Đáp án này sai. Enum không thể có access modifier `private` cho các hằng số của nó. Enum constant ngầm định là `public`, `static` và `final` và phải được khai báo mà không có access modifier.

- **C)** 
```java
protected enum Season {
    WINTER, SPRING, SUMMER, FALL
}
```
  - Đáp án này sai vì enum không thể được khai báo với mức truy cập `protected` hoặc `private`. Enum ngầm định là `public` nếu chúng được định nghĩa bên ngoài một class. Nếu được định nghĩa bên trong một class, chúng có thể có bất kỳ mức truy cập nào, nhưng keyword `protected` không thể được dùng ở cấp độ của chính enum.

- **D)** 
```java
enum Status {
    ACTIVE, INACTIVE, DELETED;

    public void printStatus() {
        System.out.println("Current status: " + this);
    }
}
```
  - Đáp án này đúng. Nó cho thấy một enum `Status` với method `printStatus()`. Enum trong Java có thể chứa method, field, constructor và implement interface. Điều này minh họa khả năng có method của enum, khiến khai báo này hợp lệ.


**6. Đáp án đúng là A.**

**Giải thích:**

- **A)** `1`
   - Đáp án này đúng. Method `ordinal()` trả về ordinal của enum constant này (vị trí của nó trong khai báo enum, trong đó hằng số đầu tiên có ordinal bằng 0). Vì `GREEN` là enum constant thứ hai được khai báo trong enum `Color`, giá trị ordinal của nó là 1.

- **B)** `2`
  - Đáp án này sai. Giá trị ordinal của `BLUE` mới là 2, không phải `GREEN`, vì `BLUE` là hằng số được khai báo thứ ba trong enum `Color`.

- **C)** `0`
  - Đáp án này sai. Giá trị ordinal của `RED` là 0, vì nó là hằng số được khai báo đầu tiên trong enum `Color`.

- **D)** `Color.GREEN`
  - Đáp án này sai. Method `ordinal()` trả về một số nguyên biểu thị vị trí của enum constant trong khai báo, chứ không phải chính enum constant.


**7. Đáp án đúng là D.**

**Giải thích:**

- **A)** 
```java
public enum Size {
    SMALL, MEDIUM, LARGE;
    public static void printSize() {
        System.out.println("The size is " + this.name());
    }
}
```
  - Đáp án này sai vì method `printSize()` được định nghĩa là `static`, nghĩa là nó không thể truy cập tham chiếu `this`. Static method trong enum không thể truy cập trực tiếp các enum constant mà không chỉ định rõ hằng số hoặc được truyền tham chiếu.

- **B)** 
```java
enum Flavor {
    CHOCOLATE, VANILLA, STRAWBERRY;
    void printFlavor() {
        System.out.println("Flavor: " + Flavor.name);
    }
}
```
  - Đáp án này sai vì thuộc tính `name` của một enum constant là `private`. Bạn chỉ có thể truy cập nó thông qua tham chiếu `this` và method `name()` (`this.name()`).

- **C)** 
```java
protected enum Direction {
    NORTH, SOUTH, EAST, WEST;
    private printDirection() {
        System.out.println("Going " + this.toString());
    }
}
```
  - Đáp án này sai vì hai lý do. Thứ nhất, `protected` không phải là access modifier hợp lệ cho top-level enum, top-level enum chỉ có thể là `public` hoặc package-private (không có modifier). Thứ hai, method `printDirection()` thiếu kiểu giá trị trả về (ví dụ `void`).

- **D)** 
```java
public enum Season {
    WINTER, SPRING, SUMMER, FALL;
    public void printSeason() {
        System.out.println("The season is " + this.name());
    }
}
```
  - Đây là đáp án đúng. Method `printSeason()` được định nghĩa đúng chuẩn: nó là `public`, non-static và dùng tham chiếu `this` để truy cập tên của enum constant hiện tại. Method này cung cấp đúng hành vi tùy chỉnh cho mỗi enum constant, cho phép in ra thông báo thể hiện mùa hiện tại.
