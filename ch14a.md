---
layout: answer

title: "Chương 14"
subtitle: "Localization"
exam_objectives:
  - "Triển khai localization bằng locale và resource bundle. Parse và format message, date, time và number, bao gồm giá trị currency và percentage."
---

## Đáp án {#answers}
**1. Đáp án đúng là C.**

**Giải thích:**

- **A)** 
```
true
true
true
French (Canada)
French (Canada)
French (Canada)
```
  - Đáp án này sai vì nó không tính đến những khác biệt do variant trong `locale2` gây ra.

- **B)** 
```
false
true
false
French (Canada)
French (Canada, UNIX2024)
French (Canada)
```
  - Đáp án này sai vì nó không biểu diễn đúng display name của `Locale.CANADA_FRENCH`.

- **C)** 
```
false
true
false
French (Canada)
French (Canada, UNIX2024)
Canadian French
```
  - Đáp án này đúng. Hãy phân tích chi tiết:

    1. `locale1.equals(locale2)` là `false` vì `locale2` có variant (`"UNIX2024"`) còn `locale1` thì không.
    2. `locale1.equals(locale3)` là `true` vì `Locale.CANADA_FRENCH` tương đương với `new Locale("fr", "CA")`.
    3. `locale2.equals(locale3)` là `false` vì `locale2` có variant còn `locale3` thì không.
    4. `locale1.getDisplayName(Locale.ENGLISH)` trả về `"French (Canada)"`.
    5. `locale2.getDisplayName(Locale.ENGLISH)` trả về `"French (Canada, UNIX2024)"`, bao gồm cả variant.
    6. `locale3.getDisplayName(Locale.ENGLISH)` trả về `"Canadian French"`, đây là display name đặc biệt của constant này.

- **D)** 
```
false
false
false
French (Canada)
French (Canada, UNIX2024)
Canadian French
```
  - Đáp án này sai vì nó cho rằng `locale1` và `locale3` không bằng nhau, trong khi thực tế chúng bằng nhau.

- **E)** Đoạn code sẽ throw `IllegalArgumentException` vì `UNIX2024` không phải là variant hợp lệ.
  - Đáp án này sai. Mặc dù `UNIX2024` không phải là variant code chuẩn của ISO 639, constructor của `Locale` vẫn chấp nhận bất kỳ string nào làm variant mà không throw exception.


**2. Đáp án đúng là D.**

**Giải thích:**

- **A)** Enum `Locale.Category` có ba giá trị: `DISPLAY`, `FORMAT` và `LANGUAGE`.
  - Đáp án này sai. Enum `Locale.Category` chỉ có hai giá trị: `DISPLAY` và `FORMAT`. Không có category `LANGUAGE`.

- **B)** Method `Locale.setDefault(Locale.Category, Locale)` chỉ có thể set default locale cho category `FORMAT`.
  - Đáp án này sai. Method `Locale.setDefault(Locale.Category, Locale)` có thể set default locale cho cả hai category `DISPLAY` và `FORMAT`, không chỉ `FORMAT`.

- **C)** Dùng `Locale.getDefault(Locale.Category)` luôn trả về cùng một locale bất kể category được chỉ định.
  - Đáp án này sai. `Locale.getDefault(Locale.Category)` có thể trả về các locale khác nhau tùy theo category được chỉ định. Hai category `DISPLAY` và `FORMAT` có thể có default locale khác nhau.

- **D)** Category `DISPLAY` ảnh hưởng đến ngôn ngữ dùng để hiển thị các thành phần user interface, còn category `FORMAT` ảnh hưởng đến việc format number, date và currency.
  - Đáp án này đúng. Category `DISPLAY` thực sự ảnh hưởng đến ngôn ngữ dùng để hiển thị các thành phần user interface (như error message hay label của GUI), còn category `FORMAT` ảnh hưởng đến cách format number, date, currency và các dữ liệu phụ thuộc locale khác.

- **E)** Locale category được giới thiệu trong Java 8 để thay thế các method `Locale` cũ.
  - Đáp án này sai. Locale category được thêm vào để cung cấp khả năng kiểm soát chi tiết hơn các khía cạnh localization, bổ sung (chứ không thay thế) các method `Locale` hiện có.


**3. Đáp án đúng là D.**

**Giải thích:**

- **A)** Resource bundle chỉ có thể được lưu trong các file `.properties`.
  - Đáp án này sai. Mặc dù file `.properties` thường được dùng cho resource bundle, Java cũng hỗ trợ resource bundle dạng class-based. Đó là các Java class extends `ResourceBundle` và cung cấp resource đã localized bằng code.

- **B)** Method `ResourceBundle.getBundle()` luôn throw `MissingResourceException` nếu bundle được yêu cầu không được tìm thấy.
  - Đáp án này sai. Method `ResourceBundle.getBundle()` không phải lúc nào cũng throw `MissingResourceException` nếu bundle được yêu cầu không được tìm thấy. Nó tuân theo cơ chế fallback, cố gắng tìm bundle cụ thể nhất, rồi fallback về các bundle tổng quát hơn, và cuối cùng là bundle mặc định.

- **C)** Khi tìm kiếm một resource bundle, Java chỉ xem xét locale được chỉ định và language của nó.
  - Đáp án này sai. Khi tìm kiếm một resource bundle, Java không chỉ xem xét locale được chỉ định và language của nó mà còn cả country, variant và thậm chí cả default locale. Nó tuân theo một lookup procedure được định nghĩa rõ ràng để tìm bundle phù hợp nhất.

- **D)** Nếu một key không được tìm thấy trong resource bundle của một locale cụ thể, Java sẽ tìm nó trong bundle của parent locale.
  - Đáp án này đúng. Java implement cơ chế fallback theo parent chain cho resource bundle. Nếu một key không được tìm thấy trong bundle của locale cụ thể, nó sẽ tìm trong bundle của parent locale. Ví dụ, nếu một key không được tìm thấy trong bundle `fr_FR` (tiếng Pháp - Pháp), nó sẽ tìm trong bundle `fr` (tiếng Pháp), và sau đó là bundle mặc định.

- **E)** Resource bundle được load dynamically tại runtime, nên các thay đổi trong file `.properties` được phản ánh ngay lập tức trong application đang chạy.
  - Đáp án này sai. Resource bundle thường được load khi `ResourceBundle.getBundle()` được gọi và sau đó được cache. Các thay đổi trong file .properties không được phản ánh ngay lập tức trong application đang chạy. Application thường cần được restart hoặc clear cache của resource bundle để thay đổi có hiệu lực.


**4. Đáp án đúng là A.**

**Giải thích:**

- **A)** 
```
red
blue
```
  - Đáp án này đúng. Hãy phân tích từng bước thực thi của code:
      1. Properties được set và store vào file `config.properties`.
      2. `props.clear()` xóa tất cả property khỏi object `props`.
      3. `System.out.println(props.getProperty("color", "red"))` in ra `red` vì các property đã bị xóa, nên nó dùng giá trị mặc định.
      4. Properties được load từ file.
      5. `System.out.println(props.getProperty("color", "red"))` giờ in ra `blue` vì nó được load từ file.

- **B)** 
```
blue
blue
```
  - Đáp án này sai. Nó không tính đến lời gọi method `clear()` vốn xóa sạch các property trước câu lệnh print đầu tiên.

- **C)** 
```
red
red
```
  - Đáp án này sai. Nó không tính đến việc properties được load thành công từ file trước câu lệnh print thứ hai.

- **D)** Đoạn code sẽ throw `FileNotFoundException`.
  - Đáp án này sai. Đoạn code tạo file trong block `try-with-resources` đầu tiên, nên file phải tồn tại để block thứ hai đọc từ nó.

- **E)** 
```
null
blue
```
  - Đáp án này sai. `getProperty()` trả về giá trị mặc định `red` khi property không được tìm thấy, chứ không phải `null`.


**5. Đáp án đúng là B.**

**Giải thích:**

- **A)** Đoạn code sẽ throw `IllegalArgumentException` vì format date không hợp lệ. 
  - Đáp án này sai. Format date `"long"` hợp lệ trong `MessageFormat` và sẽ không throw exception.

- **B)** Output sẽ bao gồm date ở long format, tên `"Alice"`, số 3, từ `"apples"` và giá theo format currency của US.
  - Đáp án này đúng. `MessageFormat` sẽ format từng parameter theo pattern được chỉ định:
   - `{0, date, long}` sẽ format `Date` theo long format (`"June 1, 2023"`)
   - `{1}` sẽ chỉ đơn giản chèn `"Alice"`
   - `{2,number,integer}` sẽ format 3 dưới dạng integer
   - `{3}` sẽ chèn "apples"
   - `{4,number,currency}` sẽ format 19.99 dưới dạng currency theo locale US (`"$19.99"`)


- **C)** Format `{2,number,integer}` sẽ hiển thị 3 là `"3.0"`.
  - Đáp án này sai. Format `{2,number,integer}` sẽ hiển thị 3 là `"3"`, không phải `"3.0"`. Format integer không bao gồm phần thập phân.

- **D)** Đoạn code sẽ không compile vì `MessageFormat` không nhận `Locale` trong constructor của nó.
  - Đáp án này sai. `MessageFormat` thực sự có constructor nhận `Locale`. Đoạn code sẽ compile thành công.

- **E)** Format `{4,number,currency}` sẽ luôn hiển thị giá bằng USD, bất kể `Locale`.
  - Đáp án này sai. Format currency sẽ dùng locale được chỉ định trong constructor của `MessageFormat`, trong trường hợp này là `Locale.US`. Nếu dùng locale khác, ký hiệu currency và cách format có thể thay đổi.


**6. Đáp án đúng là A.**

**Giải thích:**

- **A)** Method `NumberFormat.getCurrencyInstance()` trả về một formatter có thể format số tiền theo quy ước của locale được chỉ định.
  - Đáp án này đúng. Method `getCurrencyInstance()` của `NumberFormat` trả về một currency formatter cho locale được chỉ định (hoặc default locale nếu không chỉ định locale nào). Formatter này áp dụng ký hiệu currency, grouping chữ số và dấu thập phân phù hợp theo quy ước của locale.

- **B)** `NumberFormat` là concrete class có thể được khởi tạo trực tiếp bằng constructor của nó.
  - Đáp án này sai. `NumberFormat` là một abstract class và không thể được khởi tạo trực tiếp. Thay vào đó, bạn lấy instance thông qua các static factory method như `getInstance()`, `getCurrencyInstance()` hoặc `getPercentInstance()`.

- **C)** Method `setMaximumFractionDigits()` trong `NumberFormat` chỉ chấp nhận các giá trị từ 0 đến 3.
  - Đáp án này sai. Method `setMaximumFractionDigits()` không bị giới hạn trong khoảng 0 đến 3.

- **D)** Khi parse string, `NumberFormat` luôn throw `ParseException` nếu input không khớp chính xác với format mong đợi.
  - Đáp án này sai. `NumberFormat` nói chung khá dễ dãi khi parse. Nó sẽ cố parse càng nhiều phần của string mà nó nhận ra là number càng tốt, và chỉ throw `ParseException` nếu không thể parse bất kỳ phần nào của string thành number.

- **E)** Class `NumberFormat` chỉ có thể format và parse giá trị integer, không hỗ trợ số floating-point.
  - Đáp án này sai. `NumberFormat` có thể format và parse cả số integer lẫn floating-point. Nó cung cấp các method như `setMaximumFractionDigits()` và `setMinimumFractionDigits()` dành riêng cho việc xử lý phần thập phân của số floating-point.


**7. Đáp án đúng là A.**

**Giải thích:**

- **A)** 
```
2023-06-15 10:30 EDT America/New_York
2023-06-15 23:30 JST Asia/Tokyo
```
  - Đáp án này đúng. Hãy phân tích pattern của formatter:
       - `"yyyy-MM-dd HH:mm"` format date và time
       - `"z"` xuất short name của zone, như EDT hoặc JST
       - `"VV"` xuất full time zone ID, như `America/New_York` hoặc `Asia/Tokyo`
       Dòng thứ hai hiển thị đúng thời gian ở Tokyo, tức nhanh hơn New York 13 giờ.

- **B)** 
```
2023-06-15 10:30 EDT New_York
2023-06-15 23:30 JST Tokyo
```
  - Đáp án này sai. Pattern `"VV"` xuất full time zone ID, không chỉ tên thành phố.

- **C)** 
```
2023-06-15 10:30 -04:00 America/New_York
2023-06-15 23:30 +09:00 Asia/Tokyo
```
  - Đáp án này sai. Pattern `"z"` xuất short name của zone (EDT, JST), không phải offset.

- **D)** 
```
2023-06-15 10:30 America/New_York
2023-06-15 23:30 Asia/Tokyo
```
  - Đáp án này sai. Nó thiếu short zone name (EDT, JST) mà pattern `"z"` phải xuất.

- **E)** Đoạn code sẽ throw `DateTimeException` vì pattern của formatter không hợp lệ.
  - Đáp án này sai. Pattern của formatter hợp lệ và sẽ không throw exception.
