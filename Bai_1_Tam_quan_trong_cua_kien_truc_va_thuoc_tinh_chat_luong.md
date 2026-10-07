# BÀI TẬP 1 – TẦM QUAN TRỌNG CỦA KIẾN TRÚC & THUỘC TÍNH CHẤT LƯỢNG

## 1. Tại sao phải lựa chọn kiến trúc trước khi bắt đầu dự án?

**Kiến trúc phần mềm (Software Architecture)** là cách tổ chức hệ thống thành các thành phần, quy định trách nhiệm của từng thành phần, cách chúng giao tiếp với nhau và những nguyên tắc thiết kế quan trọng. Kiến trúc không phải là toàn bộ mã nguồn mà là các quyết định nền tảng ảnh hưởng đến quá trình xây dựng và phát triển hệ thống.

Việc lựa chọn kiến trúc ngay từ đầu rất quan trọng vì:

1. **Định hướng phát triển:** Giúp nhóm xác định các thành phần chính, luồng xử lý và cách phân chia công việc, tránh tình trạng mỗi lập trình viên triển khai theo một kiểu.
2. **Giảm chi phí thay đổi về sau:** Nếu các chức năng phụ thuộc chặt vào nhau, chỉ một thay đổi nhỏ cũng có thể ảnh hưởng đến nhiều phần khác. Một cấu trúc có ranh giới rõ ràng sẽ giúp sửa chữa, nâng cấp dễ hơn.
3. **Đáp ứng các yêu cầu chất lượng:** Kiến trúc ảnh hưởng trực tiếp đến hiệu năng, khả năng mở rộng, tính sẵn sàng, bảo mật và khả năng bảo trì.
4. **Hỗ trợ mở rộng sản phẩm:** Khi số lượng người dùng tăng, hệ thống cần có cách xử lý tải lớn hơn mà không phải viết lại toàn bộ ứng dụng.
5. **Giảm rủi ro kỹ thuật và kinh doanh:** Quyết định sai có thể khiến dự án chậm tiến độ, tốn chi phí vận hành hoặc không thể đáp ứng nhu cầu khách hàng.

**Ví dụ:** Một startup xây dựng ứng dụng bán hàng. Ban đầu ứng dụng chỉ phục vụ vài trăm người dùng, nhưng sau này có thể cần xử lý hàng chục nghìn lượt truy cập. Nếu mã nguồn của chức năng sản phẩm, đơn hàng và thanh toán phụ thuộc lẫn nhau quá nhiều, việc bổ sung tính năng hoặc xử lý khi lưu lượng tăng sẽ khó khăn.

Tuy nhiên, **chọn kiến trúc tốt không đồng nghĩa với chọn kiến trúc phức tạp nhất**. Với startup cần ra mắt sớm, một **Modular Monolith** (ứng dụng triển khai thống nhất nhưng chia thành các module nghiệp vụ rõ ràng) thường là lựa chọn hợp lý: vừa phát triển nhanh, vừa tạo nền tảng để tách dịch vụ khi thực sự cần.

## 2. Các loại kiến trúc phần mềm phổ biến

| Loại kiến trúc | Đặc điểm chính | Ưu điểm | Hạn chế |
|---|---|---|---|
| **Layered Architecture (kiến trúc phân lớp)** | Chia mã nguồn theo các tầng như Controller, Service, Repository. | Dễ hiểu, dễ học, dễ tổ chức code. | Nếu không kiểm soát, các tầng có thể phụ thuộc chặt và khó thay đổi. |
| **Monolithic Architecture (kiến trúc nguyên khối)** | Nhiều chức năng chạy và được triển khai trong một ứng dụng. | Phát triển, kiểm thử và triển khai ban đầu tương đối đơn giản. | Khi hệ thống lớn, việc thay đổi và mở rộng từng phần có thể khó khăn. |
| **Microservices Architecture** | Chia hệ thống thành nhiều dịch vụ nhỏ theo nghiệp vụ, có thể triển khai độc lập. | Mở rộng và phát hành từng dịch vụ linh hoạt. | Giao tiếp qua mạng, dữ liệu phân tán và vận hành phức tạp hơn. |
| **Event-Driven Architecture (kiến trúc hướng sự kiện)** | Các thành phần phát và nhận sự kiện như `OrderCreated`, `PaymentSucceeded`. | Giảm phụ thuộc trực tiếp, phù hợp xử lý bất đồng bộ. | Khó theo dõi luồng xử lý và quản lý tính nhất quán dữ liệu. |
| **Hexagonal Architecture (Ports & Adapters)** | Đưa logic nghiệp vụ vào trung tâm, giao tiếp với database/API qua các cổng và adapter. | Dễ thay thế công nghệ, thuận lợi cho kiểm thử nghiệp vụ. | Có thể làm tăng số lớp trừu tượng nếu ứng dụng nhỏ. |

**Lưu ý:** Các kiểu trên không hoàn toàn loại trừ nhau. Chẳng hạn, một ứng dụng Monolith vẫn có thể tổ chức code theo Layered Architecture, đồng thời áp dụng nguyên tắc Hexagonal cho một số module.

## 3. Các thuộc tính chất lượng (Quality Attributes) của phần mềm

Thuộc tính chất lượng là những tiêu chí đánh giá **hệ thống hoạt động tốt đến mức nào**, ngoài việc hệ thống có đầy đủ chức năng hay không.

| Thuộc tính | Giải thích | Ví dụ / cách đánh giá |
|---|---|---|
| **Scalability – Khả năng mở rộng** | Khả năng đáp ứng khi số lượng người dùng, yêu cầu hoặc dữ liệu tăng lên. | Có thể bổ sung máy chủ ứng dụng khi lượng truy cập tăng. |
| **Availability – Tính sẵn sàng** | Mức độ hệ thống có thể truy cập và phục vụ người dùng khi cần. | Mục tiêu uptime 99,9% trong một khoảng thời gian xác định. |
| **Performance – Hiệu năng** | Tốc độ phản hồi và khả năng xử lý công việc của hệ thống. | Phần lớn yêu cầu tìm kiếm trả kết quả dưới 500 ms. |
| **Maintainability – Khả năng bảo trì** | Mức độ dễ sửa lỗi, đọc hiểu, cải tiến và thay đổi phần mềm. | Sửa logic giảm giá mà không cần chỉnh sửa module thanh toán. |
| **Security – Bảo mật** | Khả năng bảo vệ tài khoản, dữ liệu và chức năng trước truy cập trái phép hoặc tấn công. | Xác thực, phân quyền, mã hóa đường truyền và bảo vệ dữ liệu nhạy cảm. |
| **Reliability – Độ tin cậy** | Khả năng thực hiện đúng chức năng một cách ổn định trong điều kiện xác định. | Tránh tạo hai đơn hàng khi khách nhấn thanh toán nhiều lần. |
| **Testability – Khả năng kiểm thử** | Mức độ dễ kiểm tra hệ thống đúng hay sai bằng unit test, integration test... | Kiểm thử logic tính tiền mà không cần kết nối cổng thanh toán thật. |
| **Modifiability – Khả năng thay đổi** | Khả năng điều chỉnh hoặc bổ sung chức năng với tác động hạn chế. | Thêm phương thức vận chuyển mới mà ít ảnh hưởng xử lý đơn hàng. |
| **Observability – Khả năng quan sát** | Khả năng hiểu trạng thái hoạt động từ logs, metrics và traces. | Xác định yêu cầu bị chậm tại bước truy vấn cơ sở dữ liệu. |
| **Interoperability – Khả năng tương tác** | Khả năng kết nối và trao đổi dữ liệu với hệ thống khác. | Tích hợp API của đối tác vận chuyển hoặc thanh toán. |

Các thuộc tính có thể **đánh đổi** với nhau. Ví dụ, triển khai nhiều dịch vụ giúp mở rộng từng phần tốt hơn nhưng lại tăng độ trễ giao tiếp và công sức vận hành. Vì vậy, không thể tối ưu mọi tiêu chí ở mức cao nhất với chi phí thấp nhất.

## 4. Tư vấn cho startup: nhanh ra mắt hay đầu tư dài hạn?

Theo em, startup nên **ưu tiên ra mắt phiên bản MVP đủ tốt**, nhưng vẫn cần những quyết định kiến trúc nền tảng:

- Bắt đầu bằng **Modular Monolith**, phân tách rõ các module như Người dùng, Sản phẩm, Đơn hàng, Thanh toán.
- Sử dụng cấu trúc code thống nhất (ví dụ trong Spring Boot: Controller – Service – Repository), nhưng tránh để các module truy cập tùy tiện vào logic nội bộ của nhau.
- Ưu tiên các thuộc tính cần thiết ngay từ đầu: **Security, Maintainability, Reliability**; đặt mục tiêu Performance và Availability phù hợp quy mô thực tế.
- Viết kiểm thử cho các chức năng quan trọng, bổ sung logging/monitoring và đo lường hệ thống trước khi quyết định mở rộng.
- Chỉ cân nhắc chuyển một phần sang Microservices khi có vấn đề cụ thể về tải, quy mô đội ngũ hoặc nhu cầu triển khai độc lập.

## Kết luận

**Kiến trúc tốt là kiến trúc phù hợp với mục tiêu, quy mô và nguồn lực của dự án.** Nó giúp hệ thống đáp ứng yêu cầu hiện tại mà không tạo ra rào cản quá lớn khi mở rộng trong tương lai. Ngược lại, lựa chọn kiến trúc quá sơ sài hoặc quá phức tạp đều có thể khiến startup tốn thời gian, tăng chi phí và bỏ lỡ cơ hội kinh doanh. Vì vậy, thành công của dự án không phụ thuộc vào việc dùng công nghệ “mới nhất”, mà ở việc đưa ra những quyết định kiến trúc có cơ sở và có thể điều chỉnh theo thực tế.
