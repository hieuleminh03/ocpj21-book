---
layout: answer

title: "Chương 10"
subtitle: "Concurrency và Multithreading"
exam_objectives:
  - "Tạo cả platform thread lẫn virtual thread. Sử dụng cả Runnable lẫn Callable object, quản lý thread lifecycle, và dùng các Executor service khác nhau cùng concurrent API để chạy task."
  - "Phát triển code thread-safe, dùng cơ chế locking và concurrent API."
  - "Xử lý Java collection đồng thời và tận dụng parallel stream."
---

## Đáp án {#answers}
**1. Đáp án đúng là C.**

**Giải thích:**

- **A)** `Thread thread = Thread.ofVirtual(); thread.start(task);`
  - Đáp án này sai vì `Thread.ofVirtual()` trả về một `Thread.Builder`, không phải một `Thread`. Method `start()` trên `Thread.Builder` nhận một `Runnable`, nhưng cú pháp này là không đúng.

- **B)** `Thread thread = Thread.ofVirtual().unstarted(task).run();`
  - Đáp án này sai vì gọi trực tiếp `run()` không khởi động một thread mới. Nó thực thi task trên thread hiện tại.

- **C)** `Thread thread = Thread.ofVirtual().start(task);`
  - Đáp án này đúng. Nó dùng thread builder API mới trong Java 21 để tạo và khởi động một virtual thread chỉ trong một bước.

- **D)** `Thread thread = Thread.ofVirtual(); task.run();`
  - Đáp án này sai vì nó không thực sự khởi động một thread mới. Nó tạo một thread builder nhưng không sử dụng, rồi chạy task trên thread hiện tại.

- **E)** `Thread thread = Thread.start(task);`
  - Đáp án này sai vì `Thread.start(task)` không phải là một static method hợp lệ trong Java 21.


**2. Đáp án đúng là B.**

**Giải thích:**
- **A)** `synchronized (this) { counter++; }`
  - Đáp án này sai vì `this` không thể được dùng trong ngữ cảnh static. Trong method `main`, `this` không khả dụng. Với một static field như `counter`, bạn cần đồng bộ hóa trên một static object hoặc class.

- **B)** `synchronized (Main.class) { counter++; }`
  - Đáp án này đúng vì đồng bộ hóa trên `Main.class` đảm bảo chỉ một thread có thể vào block synchronized tại một thời điểm cho tất cả các instance của `Main`, điều này phù hợp để bảo vệ các static field như `counter`.

- **C)** `synchronized (task) { counter++; }`
  - Đáp án này sai vì `task` là một object `Runnable`, và đồng bộ hóa trên nó không kiểm soát hiệu quả việc truy cập vào static field chia sẻ `counter`.

- **D)** `synchronized (counter) { counter++; }`
  - Đáp án này sai vì `counter` là một primitive type (`int`), và bạn không thể đồng bộ hóa trên một primitive type. Đồng bộ hóa đòi hỏi một object.

- **E)** `synchronized (System.out) { counter++; }`
  - Đáp án này sai vì đồng bộ hóa trên `System.out` không liên quan đến việc kiểm soát truy cập vào `counter`. Nó cũng sẽ gây ảnh hưởng đến những chỗ sử dụng `System.out` khác.


**3. Đáp án đúng là B và C.**   

**Giải thích:**

- **A)** `AtomicInteger` là một phần của package `java.util.concurrent.atomic`, nhưng nó không cung cấp các atomic operation cho việc tăng và giảm.
  - Phát biểu này sai. `AtomicInteger` cung cấp các atomic operation cho việc tăng và giảm, chẳng hạn như `incrementAndGet()` và `decrementAndGet()`.

- **B)** `AtomicReference` chỉ có thể được dùng với reference type, không dùng với primitive type.
  - Phát biểu này đúng. `AtomicReference` được thiết kế để làm việc với reference type và không thể dùng trực tiếp với primitive type.

- **C)** `AtomicLong` hỗ trợ các atomic operation trên giá trị `long`, bao gồm các method `getAndIncrement()` và `compareAndSet()`. 
  - Phát biểu này đúng. `AtomicLong` cung cấp các atomic operation trên giá trị `long`, bao gồm các method `getAndIncrement()` và `compareAndSet()`.

- **D)** `AtomicBoolean` có thể được dùng để thực hiện các phép toán số học atomic trên giá trị `boolean`.
  - Phát biểu này sai. `AtomicBoolean` được dùng cho các cập nhật atomic trên giá trị `boolean`, nhưng nó không hỗ trợ các phép toán số học atomic.



**4. Đáp án đúng là A.**

**Giải thích:**

- **A)** 
```java
lock.lock();
try {
    count++;
} finally {
    lock.unlock();
}
```
  - Đáp án này đúng. Nó lấy lock trước khi sửa đổi tài nguyên chia sẻ và đảm bảo lock được giải phóng trong block `finally`, đây là cách dùng đúng interface `Lock`.

- **B)** 
```java
lock.lock();
count++;
lock.unlock();
```
  - Đáp án này sai vì nếu một exception xảy ra giữa `lock.lock()` và `lock.unlock()`, lock sẽ không được giải phóng, có thể gây ra deadlock.

- **C)** 
```java
try {
    lock.lock(() -> {
        count++;
    });
} finally {
    lock.unlock();
}
```
  - Đáp án này sai vì đó không phải là một lệnh gọi `lock.lock()` hợp lệ.

- **D)** 
```java
synchronized(lock) {
    count++;
}
```
  - Đáp án này sai vì block `synchronized` được dùng với chính object `lock`, đây không phải cách dùng đúng interface `Lock` và không mang lại chức năng như mong muốn.



**5. Đáp án đúng là A.**

**Giải thích:**

- **A)** 
```java
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> System.out.println("Task executed"));
}
```
  - Đáp án này đúng. Nó dùng block `try-with-resources` với method `Executors.newVirtualThreadPerTaskExecutor()` mới được giới thiệu trong Java 21. `ExecutorService` sẽ tự động được đóng khi block `try` kết thúc, loại bỏ nhu cầu gọi shutdown tường minh.

- **B)** 
```java
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> System.out.println("Task executed"));
} finally {
    executor.shutdown();
}
```
  - Đáp án này sai vì nó gọi `shutdown()` không cần thiết trong block finally. Với `try-with-resources`, `ExecutorService` tự động được đóng, khiến lệnh gọi `shutdown()` tường minh trở nên thừa và có thể gây hại.

- **C)** 
```java
ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor();
try {
    executor.submit(() -> System.out.println("Task executed"));
} finally {
    executor.close();
}
```
  - Đáp án này sai vì nó không dùng cú pháp `try-with-resources`. Mặc dù nó đóng `ExecutorService` đúng cách, nó không tận dụng việc quản lý tài nguyên tự động mà `try-with-resources` mang lại.

- **D)** 
```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> System.out.println("Task executed"));
    executor.awaitTermination(1, TimeUnit.SECONDS);
}
```
  - Đáp án này sai vì nó gọi `awaitTermination()` không cần thiết. Trong block `try-with-resources`, `ExecutorService` tự động được đóng khi block kết thúc, khiến việc chờ termination tường minh trở nên không cần thiết và có thể khiến thread bị block trong 1 giây.



**6. Đáp án đúng là D.**

**Giải thích:**

- **A)** 
```java
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    Future<Integer> future = executor.submit(task);
    System.out.println(future.get());
}
```
  - Đáp án này sai vì nó không xử lý `InterruptedException` và `ExecutionException` tiềm ẩn mà `future.get()` có thể throw.

- **B)**
```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    Future<Integer> future = executor.submit(task);
    Integer result = future.get(1, TimeUnit.SECONDS);
    System.out.println(result);
}
```
  - Đáp án này sai vì nó không xử lý các exception tiềm ẩn (`InterruptedException`, `ExecutionException` và `TimeoutException`) mà `future.get(long, TimeUnit)` có thể throw.

- **C)**
```java
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    Future<Integer> future = executor.submit(task);
    executor.shutdown();
    System.out.println(future.get());
}
```
  - Đáp án này sai vì nó gọi `executor.shutdown()` không cần thiết. Trong block `try-with-resources`, `ExecutorService` tự động được đóng khi block kết thúc. Ngoài ra, nó không xử lý các exception tiềm ẩn từ `future.get()`.

- **D)**
```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    Future<Integer> future = executor.submit(task);
    try {
        Integer result = future.get();
        System.out.println(result);
    } catch (InterruptedException | ExecutionException e) {
        e.printStackTrace();
    }
}
```
  - Đáp án này đúng. Nó dùng `try-with-resources` để tự động đóng `ExecutorService`, submit task `Callable` đúng cách, lấy kết quả bằng `Future.get()`, và xử lý `InterruptedException` cùng `ExecutionException` tiềm ẩn có thể được throw.



**7. Đáp án đúng là A.**

**Giải thích:**

- **A)** `ConcurrentHashMap` cho phép các operation đọc và ghi đồng thời, và các operation truy xuất không bị block ngay cả khi đang có các cập nhật.
  - Phát biểu này đúng. `ConcurrentHashMap` được thiết kế để xử lý truy cập đồng thời, cho phép nhiều thread đọc và ghi cùng lúc mà không block các operation đọc trong khi cập nhật.

- **B)** `CopyOnWriteArrayList` được tối ưu cho các tình huống có số lượng operation ghi lớn hơn so với operation đọc. 
  - Phát biểu này sai. `CopyOnWriteArrayList` được tối ưu cho các tình huống mà operation đọc diễn ra thường xuyên hơn nhiều so với operation ghi, vì nó tạo một bản sao mới của array trên mỗi lần ghi, điều này có thể tốn kém nếu việc ghi diễn ra thường xuyên.

- **C)** `ConcurrentSkipListSet` không giữ các phần tử được sắp xếp.
  - Phát biểu này sai. `ConcurrentSkipListSet` giữ các phần tử theo natural ordering của chúng, hoặc theo một `Comparator` được cung cấp tại thời điểm tạo set.

- **D)** Các implementation của `BlockingQueue` như `LinkedBlockingQueue` cho phép thêm và xóa phần tử đồng thời mà không cần bất kỳ cơ chế khóa nội bộ nào.
  - Phát biểu này sai. Các implementation của `BlockingQueue` như `LinkedBlockingQueue` có sử dụng cơ chế khóa nội bộ để xử lý truy cập đồng thời một cách an toàn.



**8. Đáp án đúng là B.**

**Giải thích:**

- **A)** Parallel stream luôn cải thiện hiệu năng của chương trình nhờ tận dụng nhiều thread.
  - Phát biểu này sai vì parallel stream không phải lúc nào cũng cải thiện hiệu năng. Chi phí quản lý nhiều thread đôi khi có thể lớn hơn lợi ích, đặc biệt với dataset nhỏ hoặc các operation đơn giản.

- **B)** Parallel stream có thể dẫn đến kết quả sai nếu các operation được thực hiện không thread-safe.
  - Phát biểu này đúng. Khi dùng parallel stream, phải cẩn thận đảm bảo các operation thực hiện trên các phần tử là thread-safe. Nếu không, có thể dẫn đến race condition và kết quả sai.

- **C)** Thứ tự các phần tử trong parallel stream luôn được giữ nguyên so với stream gốc.
  - Phát biểu này sai. Thứ tự các phần tử trong parallel stream không được đảm bảo giống với stream gốc trừ khi có biện pháp đặc biệt để giữ thứ tự, chẳng hạn dùng các stream operation có thứ tự.

- **D)** Dùng parallel stream đảm bảo rằng các operation trên các phần tử sẽ thực thi theo một thứ tự cố định.
  - Phát biểu này sai vì parallel stream không đảm bảo thứ tự thực thi các operation trên các phần tử. Các operation có thể thực thi theo thứ tự không xác định do tính chất đồng thời của xử lý song song.



**9. Đáp án đúng là B.**

**Giải thích:**

- **A)** 
```java
int sum = numbers.parallelStream().reduce(1, Integer::sum);
System.out.println(sum);
```
  - Đáp án này sai vì nó dùng `1` làm identity value. Identity value cho phép tính tổng phải là `0`, vì đó là phần tử trung hòa (neutral element) của phép cộng. Bắt đầu reduction với `1` sẽ cho kết quả tổng sai, bị cộng thêm `1`.

- **B)** 
```java
int sum = numbers.parallelStream().reduce(0, Integer::sum).collect();
System.out.println(sum);
```
  - Đáp án này đúng. Nó dùng đúng `parallelStream()` để tạo một parallel stream và method `reduce` với identity value `0` cùng method reference `Integer::sum` để tính tổng các phần tử.

- **C)** 
```java
int sum = numbers.stream().reduce(0, Integer::sum);
System.out.println(sum);
```
  - Đáp án này sai vì nó dùng stream tuần tự (`stream()`) thay vì parallel stream. Mặc dù nó tính tổng các phần tử đúng, nó không minh họa việc dùng parallel stream như câu hỏi yêu cầu.

- **D)** 
```java
int sum = numbers.parallelStream().collect(reduce(0, Integer::sum));
System.out.println(sum);
```
  - Đáp án này sai vì nó cố dùng method `collect()` kết hợp với `reduce()`, đây không phải cú pháp đúng. Method `collect()` được dùng cho mutable reduction và thường dùng với collector, không phải trực tiếp với operation `reduce()`.
