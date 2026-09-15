---
layout: answer

title: "Chương 12"
subtitle: "File I/O và Serialization"
exam_objectives:
  - "Read and write console and file data using I/O streams."
  - "Serialize and de-serialize Java objects."
  - "Construct, traverse, create, read, and write Path objects and their properties using the java.nio.file API."
---

## Đáp án {#answers}
**1. Đáp án đúng là D.**

**Giải thích:**

- **A)** `/home/user`
  - Đáp án này sai vì method `resolve` nối path đã cho vào base path. Nó không trả về riêng base path.

- **B)** `/home/user/documents` 
  - Đáp án này sai vì method `resolve` bao gồm toàn bộ relative path được truyền vào làm tham số, không chỉ một phần của nó.

- **C)** `/documents/notes.txt`
  - Đáp án này sai vì method `resolve` kết hợp base path với relative path đã cho; nó không thay thế base path bằng relative path.

- **D)** `/home/user/documents/notes.txt`
  - Đáp án này đúng vì method `resolve` nối relative path vào base path, cho kết quả là `/home/user/documents/notes.txt`.



**2. Đáp án đúng là C.**

**Giải thích:**

- **A)** `/home/user/../documents/./notes.txt` 
  - Đáp án này sai vì method `normalize` loại bỏ các phần tử `.` và `..` dư thừa, nên nó sẽ không giữ nguyên path như vậy.

- **B)** `/home/user/documents/notes.txt`
  - Đáp án này sai vì dù `.` đã bị loại bỏ, `..` lại đi lên một directory, dẫn đến final path không đúng.

- **C)** `/home/documents/notes.txt`
  - Đáp án này đúng vì method `normalize` xử lý path bằng cách loại bỏ `.` và đi lên một directory do `..`, cho kết quả là `/home/documents/notes.txt`.

- **D)** `/documents/notes.txt`
  - Đáp án này sai vì method `normalize` không loại bỏ hoàn toàn phần đầu của path cho đến tận `documents`. Nó chỉ xử lý các phần tử `.` và `..`.



**3. Đáp án đúng là B.**

**Giải thích:**

- **A)** `FileOutputStream`
  - Đáp án này sai vì `FileOutputStream` được dùng để ghi dữ liệu nhị phân vào file, không dùng để đọc character stream.

- **B)** `FileReader`
  - Đáp án này đúng vì `FileReader` được thiết kế để đọc character stream từ file, khiến nó trở thành class phù hợp cho mục đích này.

- **C)** `BufferedOutputStream`
  - Đáp án này sai vì `BufferedOutputStream` được dùng để ghi dữ liệu nhị phân vào một output stream, buffer dữ liệu để ghi hiệu quả. Nó không được dùng để đọc character stream.

- **D)** `ObjectInputStream`
  - Đáp án này sai vì `ObjectInputStream` được dùng để deserialize object từ một input stream, không dùng để đọc character stream.



**4. Đáp án đúng là C.**

**Giải thích:**

- **A)** 
```java
Path source = Paths.get("source.txt");
Path target = Paths.get("target.txt");
Files.copy(source, target, StandardCopyOption.ATOMIC_MOVE);
```
  - Đáp án này sai vì `StandardCopyOption.ATOMIC_MOVE` được dùng để di chuyển file một cách atomic, không dùng để copy. Nó không đảm bảo rằng file đã tồn tại sẽ bị ghi đè.

- **B)** 
```java
Path source = Paths.get("source.txt");
Path target = Paths.get("target.txt");
Files.move(source, target, StandardCopyOption.REPLACE_EXISTING);
```
  - Đáp án này sai vì `Files.move` được dùng để di chuyển hoặc đổi tên file, không phải để copy nó. `StandardCopyOption.REPLACE_EXISTING` đảm bảo file đích bị ghi đè trong thao tác move, chứ không phải trong thao tác copy.

- **C)** 
```java
Path source = Paths.get("source.txt");
Path target = Paths.get("target.txt");
Files.copy(source, target, StandardCopyOption.REPLACE_EXISTING);
```
  - Đáp án này đúng vì `Files.copy` với `StandardCopyOption.REPLACE_EXISTING` đảm bảo file đích bị ghi đè nếu nó tồn tại, đây là cách đúng để copy file kèm ghi đè.

- **D)** 
```java
Path source = Paths.get("source.txt");
Path target = Paths.get("target.txt");
Files.copy(source, target, StandardCopyOption.APPEND);
```
  - Đáp án này sai vì `StandardCopyOption.APPEND` không tồn tại trong enum `StandardCopyOption`, khiến đoạn code này không hợp lệ.



**5. Đáp án đúng là D.**

**Giải thích:**

- **A)** 
```java
Path path = Paths.get("file.txt");
List<String> lines = Files.readAllBytes(path);
```
  - Đáp án này sai vì `Files.readAllBytes(path)` trả về một byte array, không phải một `List<String>`.

- **B)** 
```java
Path path = Paths.get("file.txt");
List<String> lines = Files.readString(path);
```
  - Đáp án này sai vì `Files.readString(path)` trả về một `String` duy nhất chứa toàn bộ nội dung của file, không phải một `List<String>`.

- **C)** 
```java
Path path = Paths.get("file.txt");
List<String> lines = Files.lines(path);
```
  - Đáp án này sai vì `Files.lines(path)` trả về một `Stream<String>`, không phải một `List<String>`. Nó cung cấp một stream các dòng được load lazy.

- **D)** 
```java
Path path = Paths.get("file.txt");
List<String> lines = Files.readAllLines(path);
```
  - Đáp án này đúng vì `Files.readAllLines(path)` đọc tất cả các dòng từ file và trả về chúng dưới dạng một `List<String>`, đây chính là hành vi mong muốn.



**6. Đáp án đúng là A.**

**Giải thích:**

- **A)** 
```java
Path path = Paths.get("output.txt");
List<String> lines = Arrays.asList("line1", "line2", "line3");
Files.write(path, lines);
```
  - Đáp án này đúng vì `Files.write(path, lines)` ghi danh sách string đã cho vào file tại path được chỉ định, tạo file nếu nó chưa tồn tại.

- **B)** 
```java
Path path = Paths.get("output.txt");
List<String> lines = Arrays.asList("line1", "line2", "line3");
Files.writeString(path, lines);
```
  - Đáp án này sai vì `Files.writeString(path, lines)` không tồn tại. `Files.writeString` yêu cầu tham số thứ hai là một `String` duy nhất, không phải một `List<String>`.

- **C)** 
```java
Path path = Paths.get("output.txt");
List<String> lines = Arrays.asList("line1", "line2", "line3");
Files.writeLines(path, lines);
```
  - Đáp án này sai vì `Files.writeLines(path, lines)` không tồn tại. Không có method nào như vậy trong class `Files`.

- **D)** 
```java
Path path = Paths.get("output.txt");
List<String> lines = Arrays.asList("line1", "line2", "line3");
Files.write(path, lines, StandardOpenOption.READ);
```
  - Đáp án này sai vì `StandardOpenOption.READ` không phải là option hợp lệ để ghi file. Nó được dùng để đọc file.



**7. Đáp án đúng là B.**

**Giải thích:**

- **A)** 
```java
BasicFileAttributes attrs = Files.readAttributes(path, BasicFileAttributes.class);
attrs.lastModifiedTime();
```
  - Đáp án này sai vì `attrs.lastModifiedTime()` lấy thời gian sửa đổi lần cuối của file, không phải thời gian tạo.

- **B)** 
```java
BasicFileAttributes attrs = Files.readAttributes(path, BasicFileAttributes.class);
attrs.creationTime();
```
  - Đáp án này đúng vì `attrs.creationTime()` lấy thời gian tạo của file, đây là method đúng của `BasicFileAttributes` cho mục đích này.

- **C)** 
```java
BasicFileAttributes attrs = Files.readAttributes(path, BasicFileAttributes.class);
attrs.lastAccessTime();
```
  - Đáp án này sai vì `attrs.lastAccessTime()` lấy thời gian truy cập lần cuối của file, không phải thời gian tạo.

- **D)** 
```java
BasicFileAttributes attrs = Files.readAttributes(path, BasicFileAttributes.class);
attrs.size();
```
  - Đáp án này sai vì `attrs.size()` lấy kích thước của file, không phải thời gian tạo.


**8. Đáp án đúng là D.**

**Giải thích:**

- **A)** 
```java
Path start = Paths.get("start_directory");
Files.walkFileTree(start, new SimpleFileVisitor<Path>() {
    @Override
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) throws IOException {
        return FileVisitResult.SKIP_SUBTREE;
    }
});
```
  - Đáp án này sai vì `FileVisitResult.SKIP_SUBTREE` sẽ bỏ qua việc duyệt toàn bộ subtree, không cho phép duyệt hoàn toàn cây directory.

- **B)** 
```java
Path start = Paths.get("start_directory");
Files.walkFileTree(start, new SimpleFileVisitor<Path>() {
    @Override
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) throws IOException {
        throw new IOException("Error visiting file");
    }
});
```
  - Đáp án này sai vì việc throw một `IOException` bên trong `visitFile` sẽ dừng quá trình duyệt do exception không được xử lý.

- **C)** 
```java
Path start = Paths.get("start_directory");
Files.walkFileTree(start, new SimpleFileVisitor<Path>() {
    @Override
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) throws IOException {
        System.out.println("Visited file: " + file);
        return FileVisitResult.TERMINATE;
    }
});
```
  - Đáp án này sai vì việc dùng `FileVisitResult.TERMINATE` sẽ dừng quá trình duyệt sau khi thăm file đầu tiên, không cho phép duyệt hoàn toàn cây directory.

- **D)** 
```java
Path start = Paths.get("start_directory");
Files.walkFileTree(start, EnumSet.noneOf(FileVisitOption.class), Integer.MAX_VALUE, new SimpleFileVisitor<Path>() {
    @Override
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) throws IOException {
        System.out.println("Visited file: " + file);
        return FileVisitResult.CONTINUE;
    }

    @Override
    public FileVisitResult preVisitDirectory(Path dir, BasicFileAttributes attrs) throws IOException {
        return FileVisitResult.CONTINUE;
    }

    @Override
    public FileVisitResult visitFileFailed(Path file, IOException exc) throws IOException {
        return FileVisitResult.CONTINUE;
    }

    @Override
    public FileVisitResult postVisitDirectory(Path dir, IOException exc) throws IOException {
        return FileVisitResult.CONTINUE;
    }
});
```
  - Đáp án này đúng vì nó dùng `Files.walkFileTree` với `SimpleFileVisitor`, chỉ định không có `FileVisitOption` đặc biệt và đặt độ sâu tối đa là `Integer.MAX_VALUE`, đảm bảo duyệt đầy đủ cây directory. Ngoài ra, nó còn xử lý đúng các sự kiện pre-visit directory, visit file, visit file thất bại và post-visit directory.



**9. Đáp án đúng là B.**

**Giải thích:**

- **A)** 

    ```java
    class Animal implements Serializable {
        private static final long serialVersionUID = 1L;
        private String species;
        private int age;

        public Animal(String species, int age) {
            this.species = species;
            this.age = age;
        }
    }

    Animal animal = new Animal("Lion", 5);
    try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("animal.ser"))) {
        ois.writeObject(animal);
    } catch (IOException e) {
        e.printStackTrace();
    }
    ```
  - Đáp án này sai vì `ObjectInputStream` được dùng để deserialization (đọc object từ stream), không phải serialization. Nó nên là `ObjectOutputStream`.

- **B)** 

    ```java
    class Animal implements Serializable {
        private static final long serialVersionUID = 1L;
        private String species;
        private int age;

        public Animal(String species, int age) {
            this.species = species;
            this.age = age;
        }
    }

    Animal animal = new Animal("Lion", 5);
    try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("animal.ser"))) {
        oos.writeObject(animal);
    } catch (IOException e) {
        e.printStackTrace();
    }
    ```
  - Đáp án này đúng vì `ObjectOutputStream` được dùng để serialize một object ra file, và đoạn code này làm điều đó một cách chính xác.

- **C)** 

    ```java
    class Animal {
        private String species;
        private int age;

        public Animal(String species, int age) {
            this.species = species;
            this.age = age;
        }
    }

    Animal animal = new Animal("Lion", 5);
    try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("animal.ser"))) {
        oos.writeObject(animal);
    } catch (IOException e) {
        e.printStackTrace();
    }
    ```
  - Đáp án này sai vì class `Animal` không implements `Serializable`, nên nó không thể được serialize bằng `ObjectOutputStream`.

- **D)** 

    ```java
    class Animal implements Serializable {
        private static final long serialVersionUID = 1L;
        private String species;
        private int age;

        public Animal(String species, int age) {
            this.species = species;
            this.age = age;
        }
    }

    Animal animal = new Animal("Lion", 5);
    try (BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("animal.ser"))) {
        bos.write(animal);
    } catch (IOException e) {
        e.printStackTrace();
    }
    ```
  - Đáp án này sai vì `BufferedOutputStream` không thể được dùng để ghi object trực tiếp; nên dùng `ObjectOutputStream` để serialization.
