---
layout: answer

title: "Chương 9"
subtitle: "Streams"
exam_objectives:
  - "Use Java object and primitive Streams, including lambda expressions implementing functional interfaces, to create, filter, transform, process, and sort data."
  - "Perform decomposition, concatenation, and reduction, and grouping and partitioning on sequential and parallel streams."
---

## Đáp án {#answers}
**1. Đáp án đúng là C.**

**Giải thích:**

- **A)** `Optional<String> optional = new Optional<>(value);`
  - Đáp án này sai vì `Optional` không có public constructor. Thay vào đó, nên dùng các static factory method như `of` và `ofNullable`.

- **B)** `Optional<String> optional = Optional.of(value);`
  - Đáp án này sai vì `Optional.of(value)` sẽ throw một `NullPointerException` nếu `value` là `null`. Trong tình huống này, vì `getValue()` có thể trả về `null`, dòng code này có thể dẫn đến exception.

- **C)** `Optional<String> optional = Optional.ofNullable(value);`
  - Đáp án này đúng vì `Optional.ofNullable(value)` sẽ trả về một `Optional` mô tả giá trị được chỉ định nếu nó khác null, hoặc một `Optional` rỗng nếu giá trị là `null`. Đây là cách phù hợp để xử lý một giá trị có thể là `null`.

- **D)** `Optional<String> optional = Optional.empty(value);`
  - Đáp án này sai vì `Optional.empty()` không nhận bất kỳ argument nào. Nó chỉ đơn giản trả về một `Optional` rỗng.

- **E)** `Optional<String> optional = Optional.nullable(value);`
  - Đáp án này sai vì không có method `nullable` trong class `Optional`. Method đúng cho mục đích này là `ofNullable`. 


**2. Đáp án đúng là E.**

**Giải thích:**

- **A)** `stream.filter(s -> s.contains("A"));` 
  - Đáp án này sai vì `filter` là một intermediate operation. Nó trả về một stream mới chứa các phần tử khớp với predicate đã cho.

- **B)** `stream.map(String::toLowerCase);`
  - Đáp án này sai vì `map` là một intermediate operation. Nó trả về một stream mới với các phần tử là kết quả của việc áp dụng function đã cho.

- **C)** `stream.distinct();`
  - Đáp án này sai vì `distinct` là một intermediate operation. Nó trả về một stream mới chỉ chứa các phần tử không trùng lặp.

- **D)** `stream.limit(2);`
  - Đáp án này sai vì `limit` là một intermediate operation. Nó trả về một stream mới được cắt ngắn để không dài hơn kích thước đã cho.

- **E)** `stream.collect(Collectors.toList());`
  - Đáp án này đúng vì `collect` là một terminal operation. Nó kích hoạt việc xử lý stream và thu thập các phần tử vào một `List`.


**3. Đáp án đúng là D.**

**Giải thích:**

- **A)** `int sum = numbers.stream().sum();` 
  - Đáp án này sai vì array không có method `stream` trực tiếp trên nó. Bạn cần dùng một method từ một utility class như `IntStream` để tạo stream.

- **B)** `int sum = IntStream.range(0, numbers.length).sum();` 
  - Đáp án này sai vì `IntStream.range(0, numbers.length)` tạo ra một stream các số nguyên từ 0 đến độ dài của array, chứ không phải các phần tử của array.

- **C)** `int sum = IntStream.from(numbers).sum();`
  - Đáp án này sai vì `IntStream` không có method `from`. Method đúng là `of`.

- **D)** `int sum = IntStream.of(numbers).sum();`
  - Đáp án này đúng vì `IntStream.of(numbers).sum()` tạo đúng một `IntStream` từ array và tính tổng các phần tử của nó.

- **E)** `int sum = IntStream.range(numbers).sum();`
  - Đáp án này sai vì `IntStream.range` yêu cầu hai argument (index bắt đầu và index kết thúc) và được dùng để tạo một stream các số trong một khoảng, chứ không phải để tính tổng một array.


**4. Đáp án đúng là A.**

**Giải thích:**

- **A)** `Stream<String> filteredStream = stream.filter(s -> s.length() > 3);`  
  - Đáp án này đúng vì `filter` là intermediate operation đúng để áp dụng một predicate lên từng phần tử của stream và trả về một stream mới chỉ chứa các phần tử khớp với predicate.

- **B)** `Stream<String> filteredStream = stream.map(s -> s.length() > 3);` 
  - Đáp án này sai vì `map` được dùng để biến đổi các phần tử của stream chứ không filter chúng. Kết quả sẽ là một stream các giá trị `Boolean` thay vì các string ban đầu.

- **C)** `Stream<String> filteredStream = stream.collect(Collectors.filtering(s -> s.length() > 3));` 
  - Đáp án này sai vì `Collectors.filtering` không phải là một method hợp lệ. Việc filter được thực hiện thông qua method `filter` trên chính stream, chứ không phải thông qua collectors.

- **D)** `Stream<String> filteredStream = stream.filtering(s -> s.length() > 3);` 
  - Đáp án này sai vì không có method `filtering` trên stream. Method đúng là `filter`.

- **E)** `Stream<String> filteredStream = stream.filterByLength(3);`
  - Đáp án này sai vì không có method `filterByLength` trên stream. Method đúng cần dùng là `filter`.


**5. Đáp án đúng là C.**

**Giải thích:**

- **A)** `Stream<String> lengthStream = stream.map(s -> s.length());`
  - Đáp án này sai vì method `map` sẽ biến đổi các phần tử thành `Integer`, không phải `String`. Kiểu đúng cho stream kết quả phải là `Stream<Integer>`.

- **B)** `Stream<String> lengthStream = stream.mapToInt(s -> s.length());`
  - Đáp án này sai vì `mapToInt` tạo ra một `IntStream`, không phải một `Stream<String>`. Ngoài ra, kiểu của stream kết quả cũng không phải `Stream<String>`.

- **C)** `Stream<Integer> lengthStream = stream.map(s -> s.length());`
  - Đáp án này đúng vì `map` biến đổi mỗi string trong stream thành độ dài của nó, tạo ra một `Stream<Integer>`.

- **D)** `IntStream lengthStream = stream.map(s -> s.length());` 
  - Đáp án này sai vì `map` tạo ra một `Stream<R>`, không phải một `IntStream`. Method đúng để tạo ra một `IntStream` sẽ là `mapToInt`.

- **E)** `Stream<String> lengthStream = stream.flatMap(s -> Stream.of(s.length()));`
  - Đáp án này sai vì `flatMap` được dùng để làm phẳng các stream lồng nhau chứ không chỉ đơn thuần map sang một kiểu khác. Ngoài ra, kiểu của stream kết quả cũng không phải `Stream<String>`.


**6. Đáp án đúng là A.**

**Giải thích:**

- **A)** `Stream<String> resultStream = stream.skip(2).limit(3);`
  - Đáp án này đúng vì `skip(2)` bỏ qua 2 phần tử đầu tiên của stream, và `limit(3)` giới hạn stream còn 3 phần tử tiếp theo. Do đó, stream kết quả sẽ chứa phần tử thứ 3, 4 và 5 của list ban đầu.

- **B)** `Stream<String> resultStream = stream.limit(3).skip(2);`
  - Đáp án này sai vì `limit(3)` trước tiên giới hạn stream còn 3 phần tử đầu tiên, và sau đó `skip(2)` bỏ qua 2 trong số các phần tử đó, kết quả là một stream chỉ còn phần tử thứ 3.

- **C)** `Stream<String> resultStream = stream.skip(3).limit(2);`
  - Đáp án này sai vì `skip(3)` bỏ qua 3 phần tử đầu tiên, và `limit(2)` sau đó giới hạn stream còn 2 phần tử tiếp theo, kết quả là một stream chứa phần tử thứ 4 và 5.

- **D)** `Stream<String> resultStream = stream.limit(2).skip(3);`
  - Đáp án này sai vì `limit(2)` trước tiên giới hạn stream còn 2 phần tử đầu tiên, và sau đó `skip(3)` sẽ cố bỏ qua nhiều phần tử hơn số hiện có, kết quả là một stream rỗng.

- **E)** `Stream<String> resultStream = stream.slice(2, 5);`
  - Đáp án này sai vì không có method `slice` trong Stream API. Các method đúng để đạt được kết quả mong muốn là `skip` và `limit`.


**7. Đáp án đúng là B.**

**Giải thích:**

- **A)** `Stream<String> resultStream = Stream.concat(stream1, stream2.collect(Collectors.toList()));`
  - Đáp án này sai vì `Stream.concat` mong đợi hai stream làm argument. `stream2.collect(Collectors.toList())` chuyển `stream2` thành một `List`, không phải một `Stream`.

- **B)** `Stream<String> resultStream = Stream.concat(stream1, stream2);`
  - Đáp án này đúng vì `Stream.concat(stream1, stream2)` nối đúng hai stream thành một stream duy nhất chứa tất cả phần tử từ cả hai stream.

- **C)** `Stream<String> resultStream = stream1.concat(stream2);`
  - Đáp án này sai vì `Stream` không có instance method `concat`. Method `concat` là một static method của class `Stream`.

- **D)** `Stream<String> resultStream = stream1.merge(stream2);`
  - Đáp án này sai vì không có method `merge` trong `Stream` API. Method đúng để nối các stream là `Stream.concat`.

- **E)** `Stream<String> resultStream = Stream.of(stream1, stream2);`
  - Đáp án này sai vì `Stream.of(stream1, stream2)` tạo ra một stream của các stream, kết quả là `Stream<Stream<String>>` thay vì một `Stream<String>` đã được nối duy nhất.


**8. Đáp án đúng là E.**

**Giải thích:**

- **A)** `int product = stream.reduce(1, (a, b) -> a + b);`
  - Đáp án này sai vì phép reduction đang dùng phép cộng thay vì phép nhân. Phép toán đúng để tính tích phải là `(a, b) -> a * b`.

- **B)** `int product = stream.reduce((a, b) -> a * b);`
  - Đáp án này sai vì nó không cung cấp identity value, vốn cần thiết cho phép reduction khi gặp một stream rỗng. Không có identity value, kết quả là một `Optional<Integer>` thay vì một `int`.

- **C)** `int product = stream.reduce(0, (a, b) -> a * b);`
  - Đáp án này sai vì identity value cho phép nhân phải là `1`, không phải `0`. Dùng `0` làm identity value sẽ cho kết quả tích bằng `0` bất kể các phần tử của stream là gì.

- **D)** `Optional<Integer> product = stream.reduce(1, (a, b) -> a * b);`
  - Đáp án này sai vì cách dùng đúng của method `reduce` với một identity value không trả về `Optional`. Nó phải trả về kết quả trực tiếp dưới dạng `int`.

- **E)** `int product = stream.reduce(1, (a, b) -> a * b, (a, b) -> a * b);`
  - Đáp án này đúng vì nó dùng đúng method `reduce` với identity value là `1` và một combiner function nhân các kết quả lại. Dạng `reduce` này cũng phù hợp cho xử lý song song, đảm bảo tích được tính đúng trên nhiều đoạn khác nhau của stream.


**9. Đáp án đúng là B.**

**Giải thích:**

- **A)** `Set<String> resultSet = stream.collect(Collectors.toSet());` 
  - Đáp án này sai vì `Collectors.toSet()` không đảm bảo thứ tự của các phần tử. Implementation mà collector này trả về không giữ nguyên thứ tự chèn.

- **B)** `Set<String> resultSet = stream.collect(Collectors.toCollection(LinkedHashSet::new));`
  - Đáp án này đúng vì `Collectors.toCollection(LinkedHashSet::new)` thu thập các phần tử vào một `LinkedHashSet`, vốn giữ nguyên thứ tự chèn.

- **C)** `Set<String> resultSet = stream.collect(Collectors.toCollection(TreeSet::new));` 
  - Đáp án này sai vì `TreeSet` sắp xếp các phần tử theo natural ordering của chúng (hoặc theo một comparator nếu được cung cấp). Điều này không nhất thiết giữ nguyên thứ tự ban đầu của các phần tử trong stream.

- **D)** `Set<String> resultSet = stream.collect(Collectors.toList());` 
  - Đáp án này sai vì `Collectors.toList()` thu thập các phần tử vào một `List`, không phải một `Set`.

- **E)** `Set<String> resultSet = stream.collect(Collectors.toMap());`
  - Đáp án này sai vì `Collectors.toMap()` được dùng để thu thập các phần tử vào một `Map`, không phải một `Set`.
