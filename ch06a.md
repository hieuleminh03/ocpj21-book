---
layout: answer

title: "Chương 6"
subtitle: "Mảng, Generics và Collections"
exam_objectives:
  - "Tạo array, collection List, Set, Map và Deque, rồi add, remove, update, retrieve và sort các phần tử của chúng."
---

## Đáp án {#answers}
**1. Đáp án đúng là D.**

**Giải thích:**

- **A)** 
```
0 0 0 
0 0 0 
```
  - Đáp án này sai vì các element của array được khởi tạo và thay đổi bên trong các vòng lặp. Các giá trị không phải đều bằng 0.

- **B)** 
```
0 1 2 
0 1 2 
```
  - Đáp án này sai vì mỗi hàng được khởi tạo với các giá trị tăng dần dựa trên tổng của các index, không giống nhau ở cả hai hàng.

- **C)** 
```
0 0 0 
1 1 1 
```
  - Đáp án này sai vì các giá trị phải là tổng của row index và column index, không phải toàn số 0 hay toàn số 1 ở hàng thứ hai.

- **D)** 
```
0 1 2 
1 2 3 
```
  - Đây là đáp án đúng. Mỗi element của array được gán bằng tổng hai index của nó. Vậy, `arr[0][0] = 0 + 0 = 0`, `arr[0][1] = 0 + 1 = 1`, `arr[0][2] = 0 + 2 = 2`, `arr[1][0] = 1 + 0 = 1`, `arr[1][1] = 1 + 1 = 2`, `arr[1][2] = 1 + 2 = 3`.


**2. Đáp án đúng là B.**

**Giải thích:**

- **A)** 
```java
public static T getFirstElement(T[] array) {
    return array[0];
}
```
  - Đáp án này sai vì generic type `<T>` bị thiếu trước return type `T`.

- **B)** 
```java
public static <T> T getFirstElement(T[] array) {
    return array[0];
}
```
  - Đây là đáp án đúng. Generic type `<T>` được khai báo đúng trước return type `T`.

- **C)** 
```java
public static <T> getFirstElement(T[] array) {
    return array[0];
}
```
  - Đáp án này sai vì return type `T` bị thiếu.

- **D)** 
```java
public static <T> T[] getFirstElement(T[] array) {
    return array[0];
}
```
  - Đáp án này sai vì return type là `T[]`, không khớp với return type dự định của method.


**3. Đáp án đúng là D.**

**Giải thích:**

**A)** Đoạn code compile và in ra:
```
1 2 3
1.1 2.2 3.3
one two three
```
  - Đáp án này sai. Đoạn code không compile, nên nó không thể tạo ra output nào.

**B)** Đoạn code compile và in ra:
```
1 2 3
1.1 2.2 3.3
```
  - Đáp án này sai. Mặc dù đây sẽ là output nếu dòng `printList(strings)` bị xóa, đoạn code như đã viết vẫn không compile.

**C)** Đoạn code không compile do lỗi trong method `printList`.
  - Đáp án này sai. Method `printList` được định nghĩa đúng, dùng upper bound wildcard `<? extends Number>`.

**D)** Đoạn code không compile do lỗi trong method `main`.
  - Đáp án này đúng. Đoạn code compile thất bại do lỗi trong method `main`. `printList(strings)` gây ra compilation error vì `String` không phải là subclass của `Number`.

**E)** Đoạn code compile nhưng throw runtime exception khi thực thi.
  - Đáp án này sai. Đoạn code compile thất bại nên nó không thể được thực thi.
  
  
**4. Đáp án đúng là A.** 

**Giải thích:**

- **A)** `[A, B, E, C, D]`
  - Đáp án này đúng. Method `add` với tham số index chèn element được chỉ định vào vị trí được chỉ định trong list. Mọi element sau vị trí đó được dịch sang phải. Do đó, `"E"` được chèn tại index 2, đẩy `"C"` và `"D"` sang phải.

- **B)** `[A, E, B, C, D]`
  - Đáp án này sai. Đây sẽ là kết quả nếu `"E"` được thêm tại index 1, không phải index 2.

- **C)** `[A, B, C, E, D]`
  - Đáp án này sai. Đây sẽ là kết quả nếu `"E"` được thêm tại index 3, không phải index 2.

- **D)** `[A, B, C, D, E]`
  - Đáp án này sai. Đây sẽ là kết quả nếu `"E"` được thêm vào cuối list, không phải tại index 2.

- **E)** `[A, C, B, E, D]`
  - Đáp án này sai. Chuỗi kết quả này không tuân theo hành vi đúng của method `add` với index 2. Nó có vẻ như một sự xáo trộn ngẫu nhiên và không tương ứng với cách các element được dịch khi một element mới được thêm vào.
  
  
**5. Đáp án đúng là C và D.**

**Giải thích:**

- **A)** Một `Set` cho phép các element trùng lặp.
  - Đáp án này sai. Một trong những đặc điểm chính của `Set` là nó không cho phép các element trùng lặp. Mỗi element phải là duy nhất.

- **B)** Các element trong một `Set` được duy trì theo thứ tự chúng được chèn vào.
  - Đáp án này sai. Thứ tự của các element phụ thuộc vào implementation cụ thể của interface `Set`. Ví dụ, `HashSet` không duy trì thứ tự nào, trong khi `LinkedHashSet` duy trì insertion order, và `TreeSet` duy trì thứ tự đã sắp xếp.

- **C)** Interface `Set` bao gồm các method để thêm, xóa và kiểm tra sự tồn tại của element.
  - Đáp án này đúng. Interface `Set` cung cấp các method như `add()`, `remove()` và `contains()` để quản lý các element của nó.

- **D)** Interface `Set` được implement bởi các class như `HashSet`, `LinkedHashSet` và `TreeSet`.
  - Đáp án này đúng. `HashSet`, `LinkedHashSet` và `TreeSet` đều là các implementation cụ thể của interface `Set`, mỗi loại có những đặc điểm khác nhau về thứ tự và hiệu năng.

- **E)** Một `Set` đảm bảo hiệu năng constant-time cho các thao tác cơ bản (add, remove, contains).
  - Đáp án này sai. Câu này đúng với riêng `HashSet`, vốn cung cấp hiệu năng constant-time trung bình cho các thao tác này. Tuy nhiên, nó không đúng với mọi implementation của `Set`. Ví dụ, `TreeSet` cung cấp hiệu năng logarithmic time cho các thao tác này vì nó dựa trên cây Red-Black.


**6. Đáp án đúng là C.**

**Giải thích:**

- **A)** `[A, B, C, D]`
  - Đáp án này sai. Đáp án này bỏ qua thứ tự các element được thêm vào deque. Nó chỉ liệt kê các element theo thứ tự như thể chúng được thêm vào mà không xét đến các method `addFirst` và `addLast`.

- **B)** `[C, B, A, D]`
  - Đáp án này sai. Đáp án này giả định sai rằng `"A"` được thêm sau `"B"`, tuy nhiên `addFirst("A")` đặt `"A"` ở vị trí thứ hai.

- **C)** `[C, A, B, D]`
  - Đáp án này đúng. Đây thực sự là output đúng. Method `addFirst("C")` đặt "C" ở đầu, `addFirst("A")` đặt `"A"` ở vị trí thứ hai, `addLast("B")` thêm `"B"` sau `"A"`, và `addLast("D")` thêm `"D"` vào cuối. Vậy thứ tự cuối cùng là `[C, A, B, D]`.

- **D)** `[D, B, A, C]`
  - Đáp án này sai. Đáp án này cho thấy thứ tự đảo ngược, không khớp với cách các element thực sự được thêm vào deque.

- **E)** `[A, C, B, D]`
  - Đáp án này sai. Đáp án này giả định sai rằng `"A"` được thêm trước `"C"` mặc dù `addFirst("C")` được gọi sau `addFirst("A")`.


**7. Đáp án đúng là D.**

**Giải thích:**

- **A)** `{1=A, 2=B, 3=C, 2=D}`
  - Đáp án này sai. Đáp án này cho rằng map sẽ giữ các key trùng lặp, điều không đúng với một `Map`. Một key chỉ có thể có một value gắn với nó tại một thời điểm.

- **B)** `{1=A, 2=B, 3=C}`
  - Đáp án này sai. Đáp án này bỏ qua việc value gắn với key `2` được cập nhật từ `"B"` thành `"D"`.

- **C)** `{1=A, 2=D, 3=C, 2=D}`
  - Đáp án này sai. Đáp án này một lần nữa cho rằng map có thể có các key trùng lặp, điều không thể xảy ra.

- **D)** `{1=A, 2=D, 3=C}`
  - Đáp án này đúng. Method `put` cập nhật value gắn với một key nếu key đó đã tồn tại trong map. Do đó, value gắn với key `2` được cập nhật từ `"B"` thành `"D"`.

- **E)** `{1=A, 3=C, 2=B}`
  - Đáp án này sai. Đáp án này bỏ qua việc cập nhật value gắn với key `2` từ `"B"` thành `"D"`.


**8. Đáp án đúng là C.** 

**Giải thích:**

- **A)**
```
Alice 30  
Bob 25  
Charlie 35
```
  - Đáp án này sai. Đáp án này liệt kê các element theo thứ tự ban đầu, không phải thứ tự đã sắp xếp theo age.

- **B)** 
```
Charlie 35  
Alice 30  
Bob 25
```
  - Đáp án này sai. Đáp án này liệt kê các element theo thứ tự giảm dần của age, nhưng method `compareTo` sắp xếp theo thứ tự tăng dần của age.

- **C)** 
```
Bob 25  
Alice 30  
Charlie 35
```
  - Đáp án này đúng. Method `compareTo` sắp xếp các object `Person` theo thứ tự tăng dần dựa trên age của chúng. Do đó, thứ tự đã sắp xếp là `Bob (25)`, `Alice (30)` và `Charlie (35)`.

- **D)** 
```
Bob 25  
Charlie 35  
Alice 30
```
  - Đáp án này sai. Đáp án này không tuân theo đúng thứ tự tăng dần của age.

- **E)** 
```
Alice 30  
Charlie 35  
Bob 25
```
  - Đáp án này sai. Đáp án này không tuân theo đúng thứ tự tăng dần của age.


**9. Đáp án đúng là A.**


**Giải thích:**

- **A)** 
```
Bob 25  
Alice 30  
Charlie 35
```
  - Đáp án này sai. `AgeComparator` sắp xếp các object `Person` theo thứ tự tăng dần dựa trên age của chúng. Do đó, thứ tự đã sắp xếp là `Bob (25)`, `Alice (30)` và `Charlie (35)`.

- **B)** 
```
Charlie 35  
Alice 30  
Bob 25
```
  - Đáp án này sai. Đáp án này liệt kê các element theo thứ tự giảm dần của age, nhưng `AgeComparator` sắp xếp theo thứ tự tăng dần của age.

- **C)** 
```
Alice 30  
Bob 25  
Charlie 35
```
  - Đáp án này sai. Đáp án này không tuân theo đúng thứ tự tăng dần của age.

- **D)** 
```
Bob 25  
Charlie 35  
Alice 30
```
  - Đáp án này sai. Đáp án này không tuân theo đúng thứ tự tăng dần của age.

- **E)** 
```
Alice 30  
Charlie 35  
Bob 25
```
  - Đáp án này sai. Đáp án này không tuân theo đúng thứ tự tăng dần của age.

