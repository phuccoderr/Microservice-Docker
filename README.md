# Spring Cloud 
Spring Cloud là một framework phát triển trên nền tảng Spring để giúp cho việc xây dựng các ứng dụng phân tán trở nên dễ dàng hơn. Nó cung cấp các tính năng và công cụ để giải quyết các vấn đề phức tạp như phân tán, khả năng mở rộng, cân bằng tải, khả năng phục hồi, giám sát và quản lý cấu hình. Spring Cloud cũng hỗ trợ các công nghệ mở như Netflix OSS (Open Source Software) và các giải pháp đám mây như Eureka, Ribbon, Hystrix, Zuul, Config Server, và nhiều hơn nữa. Sử dụng Spring Cloud giúp cho việc triển khai các ứng dụng phân tán trở nên đơn giản và dễ quản lý hơn.
# Microservices
- Một microservice là một phương pháp kỹ thuật tập trung vào việc phân tách (decomposing) ứng dụng thành các module chức năng đơn (single-function ) với các giao diện được xác định rõ ràng (well-defined interfaces), được triển khai và vận hành độc lập (Independent) bởi các nhóm nhỏ (Small Teams) có quản lý toàn bộ vòng đời (Entire Lifecycle) của dịch vụ.
- Microservices giúp gia tăng tốc độ phát triển bằng cách giảm thiểu sự giao tiếp (Minimizing Communication) và phối hợp giữa các thành viên trong nhóm, đồng thời giảm phạm vi và rủi ro của các thay đổi (The scope and risk of change) .
  - Decomposing trong ngữ cảnh của microservices nghĩa là phân tách ứng dụng thành các module chức năng đơn
  - Single-function là thuật ngữ trong kiến trúc Microservices, chỉ định rằng mỗi microservice chỉ nên chứa một chức năng cố định, thực hiện một nhiệm vụ cụ thể của hệ thống.
  - Well-defined interfaces là các giao diện được định nghĩa rõ ràng và cung cấp các quy tắc về cách các thành phần khác của hệ thống có thể tương tác với chúng.
  - Trong ngữ cảnh của microservices, độc lập (independent) thường được hiểu là các service có thể hoạt động hoàn toàn độc lập với nhau, mà không bị phụ thuộc vào các service khác.
# Actuator
- Spring Boot Actuator là một sub-probject của Spring Boot. Actuator cho phép ta theo dõi, giám sát ứng dụng, thu thập số liệu, lưu lượng truy cập hay trạng thái cơ sở dữ liệu, v.v. mà không cần thêm bất kỳ dòng code nào.
- Một khi project của ta được cấu hình Spring Actuator thì mặc định ta sẽ có sẵn 16 endpoint để quản lý và theo dõi ứng dụng của ta. ví dụ endpoint /info.
- Sau đây là một số enpoint mặc định tiêu biểu:
  - /health: Cho biết thông tin "sức khỏe" của ứng dụng như một trạng thái khi truy cập thông qua kết nối không xác thực, hay toàn bộ chi tiết tin message khi xác thực. Nó không nhạy cảm theo mặc định.
  - /info: Nó hiển thị thông tin của ứng dụng một cách tùy ý.
  - /metricts: Hiển thị thông tin "số liệu" của ứng dụng tại thời điểm hiện tại.
  - /trace: Hiển thị thông tin những request HTTP cuối cùng.
  - /beans: Hiển thị các bean đã được cấu hình của ứng dụng.
  - /loggers: Hiển thị và thay đổi cấu hình log của ứng dụng.
  - /mappings: Hiển thị danh sách toàn bộ path của ứng dụng @RequestMapping.
  - /shutdown: Nó cho phép ứng dụng được shutdown một cách bình thường.
- Tài liệu đọc thêm: https://viblo.asia/p/spring-boot-actuator-GrLZDp2BZk0
# Eureka Server
- Eureka Server là một máy chủ đăng ký dịch vụ trong hệ thống Microservices. Nó đảm nhiệm việc đặt tên cho mỗi microservice. Tại sao cần đặt tên? Bởi vì khi có nhiều microservices được triển khai và hoạt động trên nhiều instance khác nhau, không cần phải mã hóa địa chỉ IP cứng của mỗi service, thay vào đó, chúng ta có thể sử dụng tên service đã đăng ký trên Eureka Server để tìm kiếm và truy cập các dịch vụ này. Điều này giúp cho việc quản lý và mở rộng các dịch vụ một cách dễ dàng và hiệu quả hơn.
- Cấu hình Eureka Server trong application.properties:
  - spring.application.name=eureka-server
  - server.port=8761
  - ( Eureka by default will register itself as a client. So, we need to set it to false. )
  - eureka.client.register-with-eureka=false
  - eureka.client.fetch-registry=false
- Trong lớp ứng dụng chính của Spring Boot ta kích hoạt Eureka server bằng cách sử dụng chú thích @EnableEurekaServer
# EnableDiscoveryClient
- Service Eureka client là một dịch vụ độc lập trong kiến trúc microservice. Nó có thể được sử dụng cho thanh toán, tài khoản, thông báo, xác thực, cấu hình, v.v.
- Cấu hình Enable Discovery Client trong application.properties:
  - spring.application.name=service01
  - server.port=8001
  - eureka.client.service-url.default-zone=http://localhost:8761/eureka
  - spring.config.import=optional:configserver:http://localhost:8888 ( Spring Cloud Config Client )
  Trong lớp ứng dụng chính của Spring Boot ta kích hoạt Enable Discovery Client bằng cách sử dụng chú thích @EnableDiscoveryClient
