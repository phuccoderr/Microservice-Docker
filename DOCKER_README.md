# Docker
- Docker là một nền tảng cho developers và sysadmin để develop, deploy và run application với container. Nó cho phép tạo các môi trường độc lập và tách biệt để khởi chạy và phát triển ứng dụng và môi trường này được gọi là container. Khi cần deploy lên bất kỳ server nào chỉ cần run container của Docker thì application của bạn sẽ được khởi chạy ngay lập tức.
# Lợi ích của Docker
- Không như máy ảo Docker start và stop chỉ trong vài giây.
- Bạn có thể khởi chạy container trên mỗi hệ thống mà bạn muốn.
- Container có thể build và loại bỏ nhanh hơn máy ảo.
- Dễ dàng thiết lập môi trường làm việc. Chỉ cần config 1 lần duy nhất và không bao giờ phải cài đặt lại các dependencies. Nếu bạn thay đổi máy hoặc có người mới tham gia vào project thì bạn chỉ cần lấy config đó và đưa cho họ.
- Nó giữ cho word-space của bạn sạch sẽ hơn khi bạn xóa môi trường mà ảnh hưởng đến các phần khác.
# Một số khái niệm
![docker](https://github.com/phuccoderr/Microservice-Docker/assets/124669538/9c0c11cd-a85b-4df4-93b8-99bcd751fbcd)
- ***Docker Client***: là cách mà bạn tương tác với docker thông qua command trong terminal. Docker Client sẽ sử dụng API gửi lệnh tới Docker Daemon.
- ***Docker Daemon***: là server Docker cho yêu cầu từ Docker API. Nó quản lý images, containers, networks và volume.
- ***Docker Volume***s: là cách tốt nhất để lưu trữ dữ liệu liên tục cho việc sử dụng và tạo apps.
- ***Docker Registry***: là nơi lưu trữ riêng của Docker Images. Images được push vào registry và client sẽ pull images từ registry. Có thể sử dụng registry của riêng bạn hoặc registry của nhà cung cấp như : AWS, Google Cloud, Microsoft Azure.
- ***Docker Hub***: là Registry lớn nhất của Docker Images ( mặc định). Có thể tìm thấy images và lưu trữ images của riêng bạn trên Docker Hub ( miễn phí).
- ***Docker Repository***: là tập hợp các Docker Images cùng tên nhưng khác tags. VD: golang:1.11-alpine.
- ***Docker Networking***: cho phép kết nối các container lại với nhau. Kết nối này có thể trên 1 host hoặc nhiều host.
- ***Docker Compose***: là công cụ cho phép run app với nhiều Docker containers 1 cách dễ dàng hơn. Docker Compose cho phép bạn config các command trong file docker-compose.yml để sử dụng lại. Có sẵn khi cài Docker.
- ***Docker Swarm***: để phối hợp triển khai container.
- ***Docker Services***: là các containers trong production. 1 service chỉ run 1 image nhưng nó mã hoá cách thức để run image — sử dụng port nào, bao nhiêu bản sao container run để service có hiệu năng cần thiết và ngay lập tức.
# Dockerfile
- ***FROM*** — chỉ định image gốc: python, unbutu, alpine…
- ***LABEL*** — cung cấp metadata cho image. Có thể sử dụng để add thông tin maintainer. Để xem các label của images, dùng lệnh docker inspect.
- ***ENV*** — thiết lập một biến môi trường.
- ***RUN*** — Có thể tạo một lệnh khi build image. Được sử dụng để cài đặt các package vào container.
- ***COPY*** — Sao chép các file và thư mục vào container.
- ***ADD*** — Sao chép các file và thư mục vào container.
- ***CMD*** — Cung cấp một lệnh và đối số cho container thực thi. Các tham số có thể được ghi đè và chỉ có một CMD.
- ***WORKDIR*** — Thiết lập thư mục đang làm việc cho các chỉ thị khác như: RUN, CMD, ENTRYPOINT, COPY, ADD,…
- ***ARG*** — Định nghĩa giá trị biến được dùng trong lúc build image.
- ***ENTRYPOINT*** — cung cấp lệnh và đối số cho một container thực thi.
- ***EXPOSE*** — khai báo port lắng nghe của image.
- ***VOLUME*** — tạo một điểm gắn thư mục để truy cập và lưu trữ data.
# Các câu lệnh thông dụng thường dùng trong docker
~~~
docker ps
docker image ls
docker pull your_name_dockerhub
docker build -t your_name_container
docker run image_name
docker logs --follow your_name_container
docker volume ls ( Lệnh này dùng để liệt kê ra các volumn mà các container sử dụng, volume là một cơ chế dùng để lưu trữ dữ liệu sinh ra và sử dụng bởi Docker )
docker rm <list_container_name_or_id> ( Lệnh này dùng để xóa một hoặc nhiều container. )
docker rmi <list_image_id> ( Lệnh này dùng để xóa một hoặc nhiều images. )
docker stop <list_container_name_or_id> ( Lệnh này dùng để stop một hoặc nhiều container. )
~~~
# Các option thường dùng với docker run:
- ***--detach, -d*** : container sẽ được chạy ngầm vì vậy mọi output, lỗi sẽ không hiển thị.
- ***--entrypoint*** : Thiết lập hoặc ghi đè các lệnh mặc định khi chạy images
- ***--env, -e*** : Thiết lập biến môi trường sử dụng cặp (key=value). Nếu ta có biến môi trường trong file ta có thể truyền nó vào file bằng tùy chọn --env-file.
- ***--ip*** : Khai báo địa chỉ IP cho container
- ***--name*** : Gắn tên cho container
- ***--publish, -p | --publish-all, -P*** : Để mở các cổng của network các container và ánh xạ nó với cổng của máy host ta sử dụng tùy chọn --publish, -p. Hoặc sử dụng --publish-all, -P sẽ mở tất cả các cổng của container.'
~~~
docker run --publish 80:80 <image_name> bash
~~~
- ***--rm*** : Tự động xóa container khi nó thoát.
- ***--volume, -v*** : Gắn một volume vào một container, cho phép chúng ta thao tác ở container nhưng dữ liệu vẫn được lưu trữ ở máy chủ.
~~~
docker run --volume /volume_name <image_name> bash
~~~
- ***--workdir, -w*** : Chỉ định thư mục sẽ làm việc bên trong container. Giả sử ta sẽ làm việc với thư mục app trong docker
~~~
docker run --workdir /app <image_name> bash
~~~
- ***--tty, -t*** : Cấp một terminal ảo cho container.



