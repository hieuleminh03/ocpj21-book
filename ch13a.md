---
layout: answer

title: "Chương 13"
subtitle: "Java Platform Module System"
exam_objectives:
  - "Định nghĩa module và expose nội dung module, bao gồm qua reflection, khai báo module dependency, định nghĩa service, provider và consumer."
  - "Compile Java code, tạo modular jar và non-modular jar, runtime image, và triển khai migration sang module bằng unnamed module và automatic module."
---

## Đáp án {#answers}
**1. Đáp án đúng là A và C.** 

**Giải thích:**

- **A)** Automatic module
  - Đáp án này đúng. Automatic module được tạo từ một file JAR được đặt trên module path nhưng không có module descriptor (`module-info.java`). Module system suy ra tên module từ tên file JAR và export tất cả package trong JAR.

- **B)** Default module
  - Đáp án này sai. Không có khái niệm "default module" trong JPMS. Thuật ngữ này có thể bị nhầm với unnamed module hoặc các kiểu cấu hình khác, nhưng nó không phải là một loại module được công nhận.

- **C)** Unnamed module
  - Đáp án này đúng. Unnamed module là một module đặc biệt chứa tất cả class trên classpath. Nó không có module descriptor và có thể truy cập các unnamed module khác nhưng không thể được require bởi named module.

- **D)** Core module
  - Đáp án này sai. Không có loại cụ thể nào gọi là "core module" trong JPMS. JPMS không phân loại module theo cách này.

- **E)** Primary module
  - Đáp án này sai. Tương tự "core module", không có loại nào gọi là "primary module" trong JPMS.



**2. Đáp án đúng là D.**

**Giải thích:**

- **A)** `module com.example { export com.example.api; }`
  - Đáp án này sai. Trong trường hợp này, `exports` bị thiếu chữ "s". Cú pháp đúng để export một package sẽ là `exports com.example.api;`.

- **B)** `declare module com.example { }`
  - Đáp án này sai. Không có keyword `declare` nào được dùng trong JPMS để định nghĩa module.

- **C)** `create module com.example { requires java.base; }`
  - Đáp án này sai. Cú pháp đúng không dùng keyword `create` để khai báo module.

- **D)** `module com.example { }`
  - Đáp án này đúng. Đây là cách đúng để khai báo một module tên `com.example` mà không có requires bổ sung nào.

- **E)** `module com.example requires java.base;`
  - Đáp án này sai. Cú pháp không hợp lệ vì thiếu dấu ngoặc nhọn `{ }` để định nghĩa phần thân module.



**3. Đáp án đúng là A.**

**Giải thích:**

- **A)** `module com.example { exports com.example.internal to com.example.client; }`
  - Đáp án này đúng. Directive `exports` với mệnh đề `to` giới hạn việc export package `com.example.internal` chỉ cho module `com.example.client` được chỉ định.

- **B)** `module com.example { opens com.example.internal to com.example.client; }`
  - Đáp án này sai. Directive `opens` được dùng cho mục đích reflection, không phải để kiểm soát truy cập tại compile-time.

- **C)** `module com.example { requires com.example.internal; }`
  - Đáp án này sai. Directive `requires` được dùng để chỉ định dependency giữa các module, không phải để kiểm soát khả năng truy cập package.

- **D)** `module com.example { provides com.example.internal to com.example.client; }`
  - Đáp án này sai. Directive `provides` được dùng để chỉ định service provider trong module system, không phải để hạn chế quyền truy cập package.

- **E)** `module com.example { uses com.example.internal; }`
  - Đáp án này sai. Directive `uses` được dùng để chỉ định service consumer trong module system, không phải để hạn chế quyền truy cập package.



**4. Đáp án đúng là B.**

**Giải thích:**

- **A)** Module `com.example.client` có thể truy cập package `com.example.api` để deep reflection.
  - Đáp án này sai. Package `com.example.api` được export, không phải được open, nghĩa là nó khả dụng để sử dụng nhưng không dành cho deep reflection bởi các module khác.

- **B)** Module `com.example.client` không thể truy cập package `com.example.api` để deep reflection.
  - Đáp án này đúng. Package `com.example.api` không được open cho deep reflection; nó chỉ được export để các module khác sử dụng.

- **C)** Package `com.example.api` được open cho tất cả module để deep reflection.
  - Đáp án này sai. Package `com.example.api` được export cho tất cả module, nhưng nó không được open cho deep reflection với bất kỳ module nào.

- **D)** Package `com.example.internal` được export cho module `com.example.client`.
  - Đáp án này sai. Package `com.example.internal` được open cho `com.example.client` để deep reflection nhưng không được export.

- **E)** Package `com.example.api` được export cho module `com.example.client` để deep reflection.
  - Đáp án này sai. Package `com.example.api` được export cho module `com.example.client`, nhưng việc export không bao gồm khả năng deep reflection.



**5. Đáp án đúng là D.**

**Giải thích:**

- **A)** Module `java.base` cung cấp các thư viện Swing và AWT để xây dựng giao diện đồ họa.
  - Đáp án này sai. Module `java.base` không cung cấp các thư viện Swing và AWT. Những thư viện này được cung cấp bởi module `java.desktop`.

- **B)** Module `java.logging` chịu trách nhiệm xử lý collection, bao gồm list, set và map.
  - Đáp án này sai. Module `java.logging` chịu trách nhiệm về logging framework trong Java, không phải xử lý collection. Collections framework là một phần của module `java.base`.

- **C)** Module `java.desktop` cung cấp các class để implement standard input và output stream.
  - Đáp án này sai. Module `java.desktop` chứa các class để xây dựng giao diện đồ họa (Swing và AWT), không phải cho standard input và output stream. Standard I/O là một phần của module `java.base`.

- **D)** Module `java.xml` chứa các class để xử lý tài liệu XML.
  - Đáp án này đúng. Module `java.xml` chứa các class để xử lý tài liệu XML, chẳng hạn các class parse và transform XML bằng những API như DOM, SAX và StAX.

- **E)** Module `java.naming` cung cấp API để truy cập và xử lý annotation.
  - Đáp án này sai. Module `java.naming` cung cấp API để truy cập naming và directory service (JNDI), không phải để xử lý annotation. Annotation là một phần của module `java.base`.



**6. Đáp án đúng là C.**

**Giải thích:**

- **A)** `javac -d out src/com.example/module-info.java src/com.example/com/example/*.java`
  - Đáp án này sai. Mặc dù nó chỉ định đúng output directory và các source file, nó không dùng option `--module-source-path` và không chỉ định tên module bằng `-m`.

- **B)** `javac -sourcepath src -d out com.example/module-info.java com.example/com/example/*.java`
  - Đáp án này sai. Option `-sourcepath` không được dùng để compile module. Option đúng phải là `--module-source-path`.

- **C)** `javac -d out --module-source-path src -m com.example`
  - Đáp án này đúng. Lệnh `javac -d out --module-source-path src -m com.example` compile đúng module `com.example` nằm trong directory `src` và xuất các compiled class ra directory `out`.

- **D)** `javac -modulepath out -d src src/com.example/module-info.java src/com.example/com/example/*.java`
  - Đáp án này sai. Option `-modulepath` được đặt sai vị trí, và directory nguồn với directory đích bị hoán đổi cho nhau.

- **E)** `javac --module-path src --module com.example -d out`
  - Đáp án này sai. Lệnh dùng sai `--module-path` thay vì `--module-source-path` và tên module được chỉ định bằng `--module` thay vì `-m`.



**7. Đáp án đúng là A.**

**Giải thích:**

- **A)** `javac --module-source-path src -d out $(find src -name "*.java")`
  - Đáp án này đúng. Lệnh `javac --module-source-path src -d out $(find src -name "*.java")` compile đúng cả hai module bằng cách chỉ định module source path và tìm tất cả file Java trong directory nguồn.

- **B)** `javac -d out --module com.foo,com.bar --module-source-path src`
  - Đáp án này sai. Option `--module` không chấp nhận nhiều module phân tách bằng dấu phẩy trong ngữ cảnh này.

- **C)** `javac -sourcepath src -d out src/com.foo/module-info.java src/com.foo/com/foo/*.java src/com.bar/module-info.java src/com.bar/com/bar/*.java`
  - Đáp án này sai. Mặc dù nó chỉ định các source file, nó không dùng option `--module-source-path` và dài dòng không cần thiết.

- **D)** `javac -modulepath src -d out src/com.foo/*.java src/com.bar/*.java`
  - Đáp án này sai. Option `-modulepath` bị dùng sai, và path phải trỏ đến directory chứa source code của module.

- **E)** `javac --module-source-path src/com.foo,src/com.bar -d out`
  - Đáp án này sai. Option `--module-source-path` phải trỏ đến directory gốc (`src`), không phải từng directory module riêng lẻ.



**8. Đáp án đúng là C.**

**Giải thích:**

- **A)** `requires com.example.Service with com.provider.ServiceImpl;`
  - Đáp án này sai. Keyword `requires` được dùng để khai báo dependency lên các module khác, không phải để chỉ định service provider.

- **B)** `exports com.example.Service with com.provider.ServiceImpl;`
  - Đáp án này sai. Keyword `exports` được dùng để cho phép các module khác truy cập package, không phải để chỉ định service provider.

- **C)** `provides com.example.Service with com.provider.ServiceImpl;`
  - Đáp án này đúng. Câu lệnh `provides com.example.Service with com.provider.ServiceImpl;` chỉ định đúng rằng module `com.provider` cung cấp một implementation của `com.example.Service`.

- **D)** `uses com.example.Service with com.provider.ServiceImpl;`
  - Đáp án này sai. Keyword `uses` được dùng để khai báo rằng module phụ thuộc vào một service nhưng không cung cấp implementation.



**9. Đáp án đúng là D.**

**Giải thích:**

- **A)** `java --describe-module com.example/module-info.java`
  - Đáp án này sai. Option `--describe-module` không được dùng với một đường dẫn file cụ thể như `module-info.java`; nó yêu cầu tên module.

- **B)** `javac --describe-module com.example`
  - Đáp án này sai. Option `--describe-module` không hợp lệ với lệnh `javac`; nó được dùng với lệnh `java`.

- **C)** `jar --describe-module com.example`
  - Đáp án này sai. Option `--describe-module` không hợp lệ với lệnh `jar`; nó được dùng với lệnh `java`.

- **D)** `java --describe-module com.example`
  - Đáp án này đúng. Lệnh `java --describe-module com.example` mô tả đúng module `com.example` bằng option `--describe-module`.



**10. Đáp án đúng là B và C.**

**Giải thích:**

- **A)** `jdeps --list-deps example.jar` 
  - Đáp án này sai. Option `--list-deps` không tồn tại trong `jdeps`.

- **B)** `jdeps -verbose example.jar`
  - Đáp án này đúng. Mặc dù `-verbose` là một option hợp lệ, nó cung cấp nhiều thông tin hơn.

- **C)** `jdeps -s example.jar`
  - Đáp án này đúng. Option `-s` với `jdeps` cung cấp bản tóm tắt các dependency của file `example.jar`.

- **D)** `jdeps --check example.jar`
  - Đáp án này sai. Option `--check` không tồn tại trong `jdeps`.



**11. Đáp án đúng là A.**

**Giải thích:**

- **A)** `jmod create --class-path mods/com.example --output com.example.jmod`
  - Đáp án này đúng. Nó dùng đúng cú pháp của lệnh `jmod` để tạo file JMOD. Operation `create` được chỉ định, theo sau là option `--class-path` để chỉ directory nguồn, và cuối cùng là tên file JMOD output. Lệnh này sẽ tạo một file JMOD tên `com.example.jmod` từ nội dung của directory `mods/com.example`.

- **B)** `jmod --create --class-path mods/com.example --output com.example.jmod`
  - Đáp án này sai. Operation `create` trong lệnh `jmod` không nên có tiền tố `--`. Định dạng đúng là `jmod create`, không phải `jmod --create`. Phần còn lại của lệnh đúng, nhưng lỗi cú pháp này khiến toàn bộ lệnh không hợp lệ.

- **C)** `jmod --create --dir mods/com.example --output com.example.jmod`
  - Đáp án này sai. Thứ nhất, giống option B, nó dùng sai `--create` thay vì `create`. Thứ hai, nó dùng option `--dir`, vốn không được dùng để tạo file JMOD mà để chỉ định output directory khi extract file từ một JMOD. Khi tạo file JMOD, chúng ta dùng `--class-path` để chỉ định directory nguồn. Option `--output` cũng không phải option hợp lệ của lệnh `jmod`.

- **D)** `jmod create --dir mods/com.example --output com.example.jmod`
  - Đáp án này sai. Nó dùng option `--dir` thay vì `--class-path` để chỉ định directory nguồn, và nó còn bao gồm một option `--output` không hợp lệ với lệnh `jmod`. Khi tạo file JMOD, tên file output chỉ đơn giản được chỉ định như argument cuối cùng, không dùng option `--output`.



**12. Đáp án đúng là B.**

**Giải thích:**

- **A)** `jlink --module-path java.base:com.example --output myimage`
  - Đáp án này sai. Option `--module-path` phải chỉ định directory chứa các module, không phải chỉ định trực tiếp tên module.

- **B)** `jlink --module-path mods --add-modules java.base,com.example --output myimage`
  - Đáp án này đúng. Lệnh `jlink --module-path mods --add-modules java.base,com.example --output myimage` chỉ định đúng module path và thêm các module cần thiết, xuất custom runtime image ra directory `myimage`.

- **C)** `jlink --add-modules java.base,com.example --image myimage` 
  - Đáp án này sai. Option `--image` không hợp lệ; option đúng là `--output`.

- **D)** `jlink --modules java.base,com.example --dir myimage`
  - Đáp án này sai. Option `--modules` không đúng; option đúng là `--add-modules`, và `--dir` phải là `--output`.



**13. Đáp án đúng là D.**

**Giải thích:**

- **A)** Một unnamed module có thể phụ thuộc vào named module và các unnamed module khác.
  - Đáp án này sai. Unnamed module có thể phụ thuộc vào named module, điều này đúng. Tuy nhiên, unnamed module không thể phụ thuộc vào các unnamed module khác. Unnamed module được tạo khi class được load từ classpath, và chúng không thể đọc các unnamed module khác. Chúng chỉ có thể đọc các named module của platform và các module khác được thêm tường minh vào module path.

- **B)** Automatic module phải có file `module-info.java` để được đặt trên module path.
  - Đáp án này sai. Automatic module không yêu cầu file `module-info.java`. Tên module của chúng được suy ra từ tên file JAR.

- **C)** Unnamed module có thể export package của nó cho named module bằng `module-info.java`. 
  - Đáp án này sai. Unnamed module không thể export package vì chúng không dùng `module-info.java`.

- **D)** Một automatic module được tạo khi một file JAR không có `module-info.java` được đặt trên module path, và nó có thể đọc tất cả các module khác.
  - Đáp án này đúng. Automatic module được tạo bằng cách đặt một file JAR không có `module-info.java` lên module path. Automatic module này có thể đọc tất cả các module khác, cả named lẫn unnamed.
