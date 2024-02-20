# Spring Cloud 
- Spring Cloud là một framework phát triển trên nền tảng Spring để giúp cho việc xây dựng các ứng dụng phân tán trở nên dễ dàng hơn. Nó cung cấp các tính năng và công cụ để giải quyết các vấn đề phức tạp như phân tán, khả năng mở rộng, cân bằng tải, khả năng phục hồi, giám sát và quản lý cấu hình. Spring Cloud cũng hỗ trợ các công nghệ mở như Netflix OSS (Open Source Software) và các giải pháp đám mây như Eureka, Ribbon, Hystrix, Zuul, Config Server, và nhiều hơn nữa. Sử dụng Spring Cloud giúp cho việc triển khai các ứng dụng phân tán trở nên đơn giản và dễ quản lý hơn.
# Microservices
- Một microservice là một phương pháp kỹ thuật tập trung vào việc phân tách (decomposing) ứng dụng thành các module chức năng đơn (single-function ) với các giao diện được xác định rõ ràng (well-defined interfaces), được triển khai và vận hành độc lập (Independent) bởi các nhóm nhỏ (Small Teams) có quản lý toàn bộ vòng đời (Entire Lifecycle) của dịch vụ.
- Microservices giúp gia tăng tốc độ phát triển bằng cách giảm thiểu sự giao tiếp (Minimizing Communication) và phối hợp giữa các thành viên trong nhóm, đồng thời giảm phạm vi và rủi ro của các thay đổi (The scope and risk of change) .
  - ***Decomposing*** trong ngữ cảnh của microservices nghĩa là phân tách ứng dụng thành các module chức năng đơn
  - ***Single-function*** là thuật ngữ trong kiến trúc Microservices, chỉ định rằng mỗi microservice chỉ nên chứa một chức năng cố định, thực hiện một nhiệm vụ cụ thể của hệ thống.
  - ***Well-defined interfaces*** là các giao diện được định nghĩa rõ ràng và cung cấp các quy tắc về cách các thành phần khác của hệ thống có thể tương tác với chúng.
  - ***Độc lập (independent)*** thường được hiểu là các service có thể hoạt động hoàn toàn độc lập với nhau, mà không bị phụ thuộc vào các service khác.
# Actuator
~~~
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
~~~
- Spring Boot Actuator là một sub-probject của Spring Boot. Actuator cho phép ta theo dõi, giám sát ứng dụng, thu thập số liệu, lưu lượng truy cập hay trạng thái cơ sở dữ liệu, v.v. mà không cần thêm bất kỳ dòng code nào.
- Một khi project của ta được cấu hình Spring Actuator thì mặc định ta sẽ có sẵn 16 endpoint để quản lý và theo dõi ứng dụng của ta. ví dụ endpoint /info.
- Sau đây là một số enpoint mặc định tiêu biểu:
  - ***/health***: Cho biết thông tin "sức khỏe" của ứng dụng như một trạng thái khi truy cập thông qua kết nối không xác thực, hay toàn bộ chi tiết tin message khi xác thực. Nó không nhạy cảm theo mặc định.
  - ***/info***: Nó hiển thị thông tin của ứng dụng một cách tùy ý.
  - ***/metricts***: Hiển thị thông tin "số liệu" của ứng dụng tại thời điểm hiện tại.
  - ***/trace***: Hiển thị thông tin những request HTTP cuối cùng.
  - ***/beans***: Hiển thị các bean đã được cấu hình của ứng dụng.
  - ***/loggers***: Hiển thị và thay đổi cấu hình log của ứng dụng.
  - ***/mappings***: Hiển thị danh sách toàn bộ path của ứng dụng @RequestMapping.
  - ***/shutdown***: Nó cho phép ứng dụng được shutdown một cách bình thường.
- Tài liệu đọc thêm: https://viblo.asia/p/spring-boot-actuator-GrLZDp2BZk0
# Feign Client
~~~
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>

<dependency>
  <groupId>io.github.openfeign</groupId>
  <artifactId>feign-micrometer</artifactId>
</dependency>
~~~
- Để gọi tới một REST client hoặc nhiều services khác bạn có thể dùng:
  - RestTemplate là một đối tượng trong Spring Framework cung cấp khả năng gửi các yêu cầu HTTP đến các dịch vụ REST API khác. Nó hỗ trợ nhiều phương thức HTTP như GET, POST, PUT, DELETE, PATCH, ... để gửi các yêu cầu đến các địa chỉ URL khác nhau và xử lý các phản hồi trả về từ các dịch vụ đó.
  - FeignClient là một annotation trong Spring Cloud, được sử dụng để tạo ra một client đại diện cho một RESTful service. Thay vì sử dụng RestTemplate, FeignClient sử dụng cấu hình interface và annotation để định nghĩa các method và URL endpoint cho các request. FeignClient cũng cung cấp khả năng load balancing và fault tolerance cho các service.
# Thế nào là cân bằng tải (load balancing)
- Khi một dịch vụ có nhiều hơn một phiên bản đang chạy trên các cổng khác nhau, ta cần phải cân bằng tải các yêu cầu giữa các phiên bản của dịch vụ đó.
- Khi sử dụng phương pháp "Ribbon" (mặc định), các yêu cầu sẽ được phân phối đều giữa các phiên bản của dịch vụ đó.
# Eureka Server
~~~
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
~~~
- Eureka Server là một máy chủ đăng ký dịch vụ trong hệ thống Microservices. Nó đảm nhiệm việc đặt tên cho mỗi microservice. Tại sao cần đặt tên? Bởi vì khi có nhiều microservices được triển khai và hoạt động trên nhiều instance khác nhau, không cần phải mã hóa địa chỉ IP cứng của mỗi service, thay vào đó, chúng ta có thể sử dụng tên service đã đăng ký trên Eureka Server để tìm kiếm và truy cập các dịch vụ này. Điều này giúp cho việc quản lý và mở rộng các dịch vụ một cách dễ dàng và hiệu quả hơn.
- Cấu hình Eureka Server trong application.properties:
  - spring.application.name=eureka-server
  - server.port=8761
  - ( Eureka by default will register itself as a client. So, we need to set it to false. )
  - eureka.client.register-with-eureka=false
  - eureka.client.fetch-registry=false
- Trong lớp ứng dụng chính của Spring Boot ta kích hoạt Eureka server bằng cách sử dụng chú thích @EnableEurekaServer
# EnableDiscoveryClient
~~~
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-config</artifactId>
</dependency>

<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
~~~
- Service Eureka client là một dịch vụ độc lập trong kiến trúc microservice. Nó có thể được sử dụng cho thanh toán, tài khoản, thông báo, xác thực, cấu hình, v.v.
- Cấu hình Enable Discovery Client trong application.properties:
  - spring.application.name=service01
  - server.port=8001
  - eureka.client.service-url.default-zone=http://localhost:8761/eureka
  - spring.config.import=optional:configserver:http://localhost:8888 ( Spring Cloud Config Client )
  - Trong lớp ứng dụng chính của Spring Boot ta kích hoạt Enable Discovery Client bằng cách sử dụng chú thích @EnableDiscoveryClient
# Spring Cloud Gateway
~~~
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
~~~
- Spring Cloud Gateway là một thư viện được sử dụng để xây dựng cổng API trên nền tảng Spring WebFlux. Dự án này nhằm mục đích cung cấp một cách đơn giản và hiệu quả để định tuyến đến các API và cung cấp các vấn đề liên quan đến bảo mật, giám sát/thống kê và tính chịu lỗi.
- Nó là một proxy, cổng thông tin, một lớp trung gian giữa người dùng và dịch vụ của bạn.
- Tuy nhiên, chúng ta vẫn có thể có nhiều hơn một dịch vụ (instances) đang chạy trên các cổng khác nhau:
  - Spring Cloud Gateway sẽ ánh xạ giữa một tiền tố đường dẫn, ví dụ như /service02/ và một dịch vụ Service02. Nó sử dụng Eureka server để định tuyến dịch vụ được yêu cầu.
  - Nó cân bằng tải (sử dụng Ribbon) giữa các phiên bản của dịch vụ đang chạy trên các cổng khác nhau.
  - Chúng ta có thể lọc các yêu cầu( filter requests), thêm xác thực(authentication) và nhiều hơn nữa.
- Tính năng của Spring Cloud Gateway:
  - Có thể khớp các tuyến đường với bất kỳ thuộc tính yêu cầu nào.
  - Các Predicates và Filters được chỉ định cho từng tuyến đường cụ thể.
  - Tích hợp Circuit Breaker
  - Tích hợp DiscoveryClient của Spring Cloud.
  - Dễ dàng viết Predicates và Filters.
  - Giới hạn tốc độ yêu cầu (Request Rate Limiting).
  - Chuyển đổi lại đường dẫn (Path Rewriting).
- Tài liệu đọc thêm: https://viblo.asia/p/microservices-voi-spring-boot-va-spring-cloud-phan-2-cau-hinh-du-an-ban-dau-bang-eureka-server-spring-cloud-gateway-spring-cloud-config-aNj4vz9x46r
# Zipkin
~~~
<dependency>
    <groupId>io.opentelemetry</groupId>
    <artifactId>opentelemetry-exporter-zipkin</artifactId>
</dependency>
~~~
- Zipkin là một hệ thống truy tìm phân tán. Truy tìm là một kỹ thuật để ghi lại thông tin về một yêu cầu như đường dẫn thực hiện, độ trễ, lỗi là gì và cứ thế. Điều này mang lại cho bạn là khả năng khắc phục sự cố về hiệu năng như nút cổ chai, tình trạng ứng dụng xuất phát từ đâu, nguyên nhân là gì, cung cấp cho bạn tổng quan về toàn bộ ứng dụng của bạn và cho bạn thấy sự tương tác giữa mỗi dịch vụ từ bắt đầu đến cuối mỗi yêu cầu Techinique có thể áp dụng cho bất kỳ kiến ​​trúc phần mềm nào, nhưng cực kỳ cần thiết cho một hệ thống phân tán.
# Spring Cloud Circuit Breaker
~~~
<dependency>
  <groupId>io.github.resilience4j</groupId>
  <artifactId>resilience4j-spring-boot3</artifactId>
</dependency>
~~~
- Spring Cloud Circuit Breaker trong Spring cloud là một thư viện quan trong cho phép bạn triển khai mô hình circuit breaker trong các ứng dụng microservices Springboot. Mô hình circuit breaker giúp bảo vệ ứng dụng/dịch vụ của bạn khỏi các dịch vụ phụ thuộc đang bị lỗi hoặc chậm chạp (đang quá tải).
- ***Tự động mở mạch***: Spring Cloud Circuit Breaker sẽ tự động mở mạch khi một dịch vụ phụ thuộc bị lỗi hoặc chậm chạp. Điều này giúp bảo vệ ứng dụng của bạn khỏi các lỗi tràn lan. Điều này giúp cải thiện độ tin cậy của ứng dụng của bạn.
- ***Chế độ chuyển tiếp***: Spring Cloud Circuit Breaker cung cấp một chế độ chuyển tiếp cho phép ứng dụng của bạn tiếp tục hoạt động ngay cả khi một dịch vụ phụ thuộc bị lỗi. Giúp cải thiện hiệu suất của ứng dụng của bạn bằng cách tránh gọi các dịch vụ phụ thuộc bị lỗi hoặc chậm chạp.
- ***Tích hợp với các công cụ phân tích rủi ro***: Spring Cloud Circuit Breaker có thể tích hợp với các công cụ phân tích rủi ro phổ biến, chẳng hạn như Zipkin và Jaeger. Điều này cho phép bạn xem các dữ liệu phân tích rủi ro của ứng dụng của mình trong một giao diện trực quan.
- Annotation để sử dụng circuit breaker:
  - ***@CircuitBreaker***: chỉ định rằng một phương thức được bảo vệ bởi một circuit breaker.
  - ***@Fallback***: để chỉ định rằng phương thức fallbackHello() sẽ được gọi khi circuit breaker mở mạch.
  - ***@CircuitBreakerProperties***: được sử dụng để cấu hình các thuộc tính của circuit breaker
  - ~~~
    @CircuitBreaker(name = "greetingService",
            circuitBreakerProperties = @CircuitBreakerProperties(
                    threshold = 5,
                    timeout = 1000,
                    failureRateThreshold = 0.5))
    threshold: Số lượng lỗi tối thiểu trước khi circuit breaker mở mạch.
    timeout: Thời gian tối đa để đợi phản hồi từ dịch vụ phụ thuộc.
    failureRateThreshold: Tỷ lệ lỗi tối đa trước khi circuit breaker mở mạch.
    ~~~
  - Tài liệu đọc thêm: https://viblo.asia/p/su-dung-spring-cloud-circuit-breaker-trong-microservice-java-springboot-zXRJ8bZdVGq
