---
layout: answer

title: "Chương 11"
subtitle: "Date/Time API"
exam_objectives:
  - "Thao tác date, time, duration, period, instant và time-zone object bao gồm daylight saving time bằng Date-Time API."
---

## Đáp án {#answers}
**1. Đáp án đúng là D.**

**Giải thích:**

- **A)** `LocalDate.of(2014);` 
  - Đáp án này sai. Method `LocalDate.of()` yêu cầu phải chỉ định year, month và day. Chỉ cung cấp year sẽ dẫn đến compile error.

- **B)** `LocalDate.with(2014, 1, 30);`
  - Đáp án này sai. Class `LocalDate` không có method `with()` nhận ba tham số int cho year, month và day. Method đúng để dùng là `LocalDate.of(int year, int month, int dayOfMonth)`.

- **C)** `LocalDate.of(2014, 0, 30);`
  - Đáp án này sai. Giá trị month là 0, nhưng month trong class `LocalDate` được đánh index bắt đầu từ 1. Các giá trị month hợp lệ là từ 1 đến 12, nên dùng 0 sẽ throw `DateTimeException`.

- **D)** `LocalDate.now().plusDays(5);`
  - Đáp án này đúng. Nó lấy chính xác date hiện tại bằng `LocalDate.now()` rồi cộng thêm 5 ngày bằng method `plusDays()`. Thao tác này sẽ tạo một object `LocalDate` mới biểu diễn date 5 ngày kể từ bây giờ.


**2. Đáp án đúng là C.** 

**Giải thích:**

- **A)** A `LocalDate` instance representing `2014-01-02` 
  - Đáp án này sai. Method `atTime` không trả về một `LocalDate`, mà kết hợp `LocalDate` với các tham số time được cung cấp để tạo một object `LocalDateTime`.

- **B)** A `LocalTime` instance representing `14:30:59:999999`
  - Đáp án này sai. Method `atTime` không trả về một `LocalTime`, mà kết hợp `LocalDate` với các tham số time được cung cấp để tạo một object `LocalDateTime`. Ngoài ra, `LocalTime` không có độ chính xác đến nanosecond, nên `999999` nanosecond sẽ là một `LocalTime` không hợp lệ.

- **C)** A `LocalDateTime` instance representing `2014-01-02 14:30:59:999999` 
  - Đáp án này đúng. Method `atTime` nhận một `LocalDate` và kết hợp nó với các tham số hour, minute, second và nanosecond được cung cấp để tạo một object `LocalDateTime` biểu diễn date và time đó. `LocalDateTime` thu được sẽ là `2014-01-02 14:30:59:999999`.

- **D)** An exception is thrown
  - Đáp án này sai. Các tham số được cung cấp gồm 14 cho hour, 30 cho minute, 59 cho second và 999999 cho nanosecond đều là giá trị hợp lệ cho các field tương ứng, nên kết hợp chúng với `LocalDate` sẽ không throw exception.


**3. Đáp án đúng là B và D.**

**Giải thích:**

- **A)** `YEAR`
  - Đáp án này sai. `YEAR` không phải là `ChronoUnit` hợp lệ cho `LocalTime`. `LocalTime` biểu diễn time of day mà không có bất kỳ thông tin date nào, nên các đơn vị `YEAR` không áp dụng được.

- **B)** `NANOS`
  - Đáp án này đúng. `NANOS` là `ChronoUnit` hợp lệ cho `LocalTime`. `LocalTime` có độ chính xác đến nanosecond, nên bạn có thể thực hiện các thao tác trên `LocalTime` với đơn vị `NANOS`.

- **C)** `DAY`
  - Đáp án này sai. `DAY` không phải là `ChronoUnit` hợp lệ cho `LocalTime`. Tương tự `YEAR`, `LocalTime` không có khái niệm day vì nó chỉ biểu diễn time, không biểu diễn date.

- **D)** `HALF_DAYS`
  - Đáp án này đúng. `HALF_DAYS` là `ChronoUnit` hợp lệ cho `LocalTime`. Một ngày có thể chia thành hai khoảng 12 giờ (AM và PM), nên `HALF_DAYS` có thể được dùng với `LocalTime` để biểu diễn chênh lệch hoặc cộng thêm các khối thời gian 12 giờ.


**4. Đáp án đúng là B và C.**

**Giải thích:**

- **A)** `java.time.Period` implements `java.time.temporal.Temporal`
  - Đáp án này sai. `java.time.Period` không implement interface `java.time.temporal.Temporal`. `Period` biểu diễn một khoảng thời gian giữa hai date và bản thân nó không phải là một temporal object.

- **B)** `java.time.Instant` implements `java.time.temporal.Temporal`
  - Đáp án này đúng. `java.time.Instant` thực sự implement interface `java.time.temporal.Temporal`. `Instant` biểu diễn một thời điểm trên timeline và có thể được coi là một temporal object.

- **C)** `LocalDate` and `LocalTime` are thread-safe.
  - Đáp án này đúng. `LocalDate` và `LocalTime` thực sự thread-safe. Tất cả các class cốt lõi của Java Time, bao gồm `LocalDate`, `LocalTime`, `LocalDateTime`, `Instant`, v.v., đều được thiết kế immutable và thread-safe.

- **D)** `LocalDateTime.now()` will return the current time in UTC zone
  - Đáp án này sai. `LocalDateTime.now()` trả về date và time hiện tại theo system clock ở default time zone, không nhất thiết ở UTC zone. Để lấy time hiện tại theo UTC, bạn sẽ dùng `LocalDateTime.now(ZoneOffset.UTC)` hoặc `Instant.now()`.


**5. Đáp án đúng là A.**

**Giải thích:**

- **A)** `int nanos = i.getNano();`
  - Đáp án này đúng. Class `Instant` có method `getNano()` trả về phần nanosecond của `Instant` dưới dạng `int`. Đây là cách hợp lệ để lấy nanosecond.

- **B)** `long nanos = i.get(ChronoField.NANOS);`
  - Đáp án này sai. Bạn có thể dùng method `get(TemporalField)` của `Instant` để lấy giá trị của một `ChronoField` cụ thể. Truyền `ChronoField.NANO_OF_SECOND` (không phải `ChronoField.NANO`) sẽ trả về phần nanosecond của `Instant` dưới dạng `long`.

- **C)** `long nanos = i.get(ChronoUnit.NANOS);`
  - Đáp án này sai. Mặc dù `Instant` có method `get(TemporalUnit)`, nhưng `ChronoUnit.NANOS` không phải là tham số hợp lệ cho nó. Các giá trị `ChronoUnit` được dùng cho duration và period, không dùng cho field của một temporal object.

- **D)** `int nanos = i.getEpochNano();`
  - Đáp án này sai. Class `Instant` có method `getEpochSecond()` trả về số giây kể từ Unix epoch, nhưng không có method `getEpochNano()` tương ứng.



**6. Đáp án đúng là D.**

**Giải thích:**

- **A)** `P29D`
  - Đáp án này sai. Method `Period.between` tính period giữa date thứ hai và date thứ nhất, theo thứ tự đó. Vì date thứ nhất (2025-03-20) muộn hơn date thứ hai (2025-02-20), period thu được sẽ là số âm, không phải số dương.

- **B)** `P-29D`
  - Đáp án này sai. Mặc dù period thu được sẽ âm, nó sẽ không được biểu diễn là `-29D`. Một `Period` đếm số tháng tròn trước, rồi mới đến số ngày còn lại.

- **C)** `P1M`
  - Đáp án này sai. Period thu được sẽ âm vì date thứ nhất muộn hơn date thứ hai.

- **D)** `P-1M`
  - Đáp án này đúng. Method `Period.between` lấy date thứ nhất trừ date thứ hai. Trong trường hợp này, `2025-03-20` trừ `2025-02-20` cho kết quả là period -1 tháng, được biểu diễn là `P-1M`. Class `Period` tính chênh lệch theo số tháng tròn trước, rồi đến số ngày còn lại. Vì chênh lệch đúng một tháng, kết quả là `P-1M`.



**7. Đáp án đúng là D.**

**Giải thích:**

- **A)** `PT5M`
  - Đáp án này sai. `PT5M` biểu diễn duration 5 phút, đây sẽ là kết quả nếu thời điểm thứ hai sau thời điểm thứ nhất 5 phút. Tuy nhiên, vì `LocalTime.of(18, 5)` được so sánh với một `LocalDateTime`, điều này gây ra vấn đề vì chúng không cùng type.

- **B)** `PT-5M`
  - Đáp án này sai. `PT-5M` biểu diễn duration âm 5 phút. Tương tự đáp án A, đây chỉ là trường hợp nếu thời điểm thứ hai trước thời điểm thứ nhất. Vấn đề chính là có sự không khớp type giữa `LocalDateTime` và `LocalTime`.

- **C)** `PT300S`
  - Đáp án này sai. `PT300S` biểu diễn duration 300 giây (hay 5 phút), một lần nữa đây sẽ là kết quả nếu thời điểm thứ hai sau thời điểm thứ nhất 5 phút. Tuy nhiên, điều này vẫn không giải quyết vấn đề không khớp type giữa `LocalDateTime` và `LocalTime`. 

- **D)** An exception is thrown
  - Đáp án này đúng. Exception được throw vì có sự không khớp type giữa `LocalDateTime.of(2025, 3, 20, 18, 0)` và `LocalTime.of(18, 5)`. Method `Duration.between` yêu cầu hai temporal object cùng type.


**8. Đáp án đúng là A và C.**

**Giải thích:**

- **A)** `DAY_OF_WEEK`
  - Đáp án này đúng. `DAY_OF_WEEK` là giá trị `ChronoField` hợp lệ cho `LocalDate`. Nó biểu diễn day của tuần, một số nguyên từ 1 (Monday) đến 7 (Sunday), có thể được trích xuất từ một `LocalDate`.

- **B)** `HOUR_OF_DAY`
  - Đáp án này sai. `HOUR_OF_DAY` không phải là giá trị `ChronoField` hợp lệ cho `LocalDate`. `HOUR_OF_DAY` liên quan đến `LocalTime` hoặc `LocalDateTime`, những type bao gồm thành phần time, trong khi `LocalDate` chỉ xử lý thành phần date.

- **C)** `DAY_OF_MONTH`
  - Đáp án này đúng. `DAY_OF_MONTH` là giá trị `ChronoField` hợp lệ cho `LocalDate`. Nó biểu diễn day của tháng, có thể được trích xuất từ một `LocalDate`.

- **D)** `MILLI_OF_SECOND`
  - Đáp án này sai. `MILLI_OF_SECOND` không phải là giá trị `ChronoField` hợp lệ cho `LocalDate`. `MILLI_OF_SECOND` liên quan đến thành phần time, cụ thể cho `LocalTime` hoặc `LocalDateTime`, và `LocalDate` chỉ xử lý thành phần date.



**9. Đáp án đúng là C.**

**Giải thích:**

- **A)** `ZoneId.ofHours(2);`
  - Đáp án này sai. Method `ofHours(int)` thuộc class `ZoneOffset`, không phải `ZoneId`.

- **B)** `ZoneId.of("2");`
  - Đáp án này sai. Định dạng của offset không đúng cho `ZoneId`. Nó phải là một time-zone ID hợp lệ hoặc bắt đầu bằng một dấu (`+` hoặc `-`).

- **C)** `ZoneId.of("-1");`
  - Đáp án này đúng. `ZoneId.of("-1")` hợp lệ vì nó tuân theo đúng định dạng cho time-zone offset.

- **D)** `ZoneId.of("America/Canada");`
  - Đáp án này sai. Định dạng cho zone region phải theo dạng `"Area/City"`, không phải `"Area/Country"`. Một ví dụ hợp lệ sẽ là `"America/Montreal"`.


**10. Đáp án đúng là D.**

**Giải thích:**

- **A)** `0`
  - Đáp án này sai. Method `offset.get(ChronoField.HOUR_OF_DAY)` không trả về giá trị hour của `ZoneOffset`. `ZoneOffset` biểu diễn time-zone offset so với UTC/Greenwich, và gọi `get(ChronoField.HOUR_OF_DAY)` trên nó là không phù hợp.

- **B)** `1`
  - Đáp án này sai. Tương tự đáp án A, method `get` của `ZoneOffset` với `ChronoField.HOUR_OF_DAY` không tạo ra kết quả này. Class `ZoneOffset` không được thiết kế để cung cấp trực tiếp field như vậy.

- **C)** `12:00`
  - Đáp án này sai. `12:00` không phải là kết quả hợp lệ cho lời gọi method vì nó ngụ ý một biểu diễn time, trong khi `ZoneOffset` xử lý các giá trị offset chứ không phải các giá trị time of day cụ thể.

- **D)** An exception is thrown
  - Đáp án này đúng. Exception được throw vì `ZoneOffset` không hỗ trợ field `ChronoField.HOUR_OF_DAY`. Class `ZoneOffset` cung cấp giá trị offset theo đơn vị giây thay vì các chrono field cụ thể như hour of day.


**11. Đáp án đúng là A.**

**Giải thích:**

- **A)** `05:00` 
  - Đáp án này đúng. `ZonedDateTime.of(2025, 02, 28, 5, 0, 0, 0, ZoneId.of("+05:00"))` tạo một instance `ZonedDateTime` với date, time và time zone offset +05:00 được chỉ định. Gọi `toLocalTime()` trên instance này trả về local time, tức `05:00`, vì không có chuyển đổi sang local time zone +2:00 nào được thực hiện trong đoạn code này.

- **B)** `17:00`
  - Đáp án này sai. `17:00` sẽ là time nếu code chuyển đổi time đã cho (05:00) từ time zone +05:00 sang local time zone +02:00, nhưng nó không làm vậy. 

- **C)** `02:00`
  - Đáp án này sai. `02:00` không tương ứng với bất kỳ kết quả logic nào dựa trên time và time zone offset đã cho.

- **D)** `03:00`
  - Đáp án này sai. `03:00` cũng không tương ứng với bất kỳ kết quả logic nào dựa trên time và time zone offset đã cho.


**12. Đáp án đúng là C.**

**Giải thích:**

- **A)** `2025-10-04T00:00-03:00[America/Asuncion]` 
  - Đáp án này sai. Time ban đầu là `2025-10-04T00:00-03:00[America/Asuncion]` trước khi DST bắt đầu. Khi cộng thêm 1 giờ, time sẽ dịch lên 1 giờ, nhưng vì DST bắt đầu đúng lúc này, offset sẽ thay đổi.

- **B)** `2025-10-04T01:00-03:00[America/Asuncion]` 
  - Đáp án này sai. Cộng 1 giờ vào time ban đầu `2025-10-04T00:00-03:00[America/Asuncion]` trong khi xét đến thời điểm DST bắt đầu (thường cộng 1 giờ vào local time) nghĩa là effective time sẽ được điều chỉnh bởi DST transition.

- **C)** `2025-10-04T02:00-03:00[America/Asuncion]`
  - Đáp án này đúng. Ban đầu, time là `2025-10-04T00:00-03:00[America/Asuncion]`. Khi cộng thêm 1 giờ và xét đến thời điểm DST bắt đầu lúc `2025-10-04T00:00`, time tiến tới `2025-10-04T02:00-03:00[America/Asuncion]`, vì nó thực sự bỏ qua giờ 01:00.

- **D)** `2025-10-03T23:00-03:00[America/Asuncion]`
  - Đáp án này sai. Date và time `2025-10-03T23:00-03:00[America/Asuncion]` không tương ứng đúng với việc cộng 1 giờ từ time ban đầu và không tính đến DST transition. 


**13. Đáp án đúng là B.**

**Giải thích:**

- **A)** `java.time.ZoneOffset` is a subclass of `java.time.ZoneId`.
  - Đáp án này sai. `java.time.ZoneOffset` không phải là subclass của `java.time.ZoneId`. `java.time.ZoneOffset` là một final class extends `java.time.ZoneId` nhưng nó không phải là subclass.

- **B)** `java.time.Instant` can be obtained from `java.time.ZonedDateTime`. 
  - Đáp án này đúng. `java.time.Instant` thực sự có thể được lấy từ `java.time.ZonedDateTime` bằng method `toInstant()`.

- **C)** `java.time.ZoneOffset` can manage DST.
  - Đáp án này sai. `java.time.ZoneOffset` biểu diễn một offset cố định so với UTC và không quản lý Daylight Saving Time (DST). DST được quản lý bởi `java.time.ZoneId`.

- **D)** `java.time.OffsetDateTime` represents a point in time in the UTC time zone.
  - Đáp án này sai. `java.time.OffsetDateTime` biểu diễn một date-time với offset so với UTC, nhưng nó không nhất thiết biểu diễn một thời điểm ở UTC time zone. Offset có thể là bất kỳ `ZoneOffset` hợp lệ nào.


**14. Đáp án đúng là C.**

**Giải thích:**

- **A)** `5/7/15 4:00 PM`
  - Đáp án này sai. Method `DateTimeFormatter.ofLocalizedTime(FormatStyle.SHORT)` được dùng để format chỉ phần time của một object `LocalDateTime`, và nó không bao gồm date. Do đó, output sẽ không bao gồm `5/7/15`.

- **B)** `5/7/15`
  - Đáp án này sai. Như đã đề cập trước đó, `DateTimeFormatter.ofLocalizedTime(FormatStyle.SHORT)` chỉ format phần time và không bao gồm date. Vì vậy, output `5/7/15` là không thể.

- **C)** `4:00 PM`
  - Đáp án này đúng. `DateTimeFormatter.ofLocalizedTime(FormatStyle.SHORT)` format phần time của object `LocalDateTime` theo kiểu short. Với time đầu vào `16:00`, trong `Locale.ENGLISH`, output được format là `4:00 PM`.

- **D)** `4:00:00 PM`
  - Đáp án này sai. `DateTimeFormatter.ofLocalizedTime(FormatStyle.SHORT)` format phần time mà không bao gồm second. Do đó, output sẽ không bao gồm `4:00:00 PM`.


**15. Đáp án đúng là D.**

**Giải thích:**

- **A)** The pattern `HH:mm:ss X` is invalid.
  - Đáp án này sai. Pattern `HH:mm:ss X` hợp lệ. `HH` biểu diễn hour của ngày (00-23), `mm` biểu diễn minute của giờ, `ss` biểu diễn second của phút, và `X` biểu diễn ISO 8601 time zone offset.

- **B)** An `OffsetDateTime` is created successfully. 
  - Đáp án này sai. Pattern `HH:mm:ss X` hợp lệ, nhưng method `OffsetDateTime.parse` yêu cầu một định dạng date và time cùng với offset. Vì chuỗi đầu vào `"11:50:20 Z"` không chứa phần date, điều này sẽ gây ra `DateTimeParseException`.

- **C)** `Z` is an invalid offset.
  - Đáp án này sai. `Z` là một offset hợp lệ biểu diễn UTC (Coordinated Universal Time).

- **D)** An exception is thrown at runtime.
  - Đáp án này đúng. Exception được throw at runtime vì chuỗi đầu vào `"11:50:20 Z"` không khớp với pattern mong đợi cho một `OffsetDateTime`, vốn thường bao gồm cả phần date lẫn time và offset.
