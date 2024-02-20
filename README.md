# Cấu hình POM.XML cho từng Service, Eureka, Gateway
~~~
<build>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
      <configuration>
        <image>
          <name>phuctapcode/mmv3-${project.artifactId}:${project.version}</name>
        </image>
        <pullPolicy>IF_NOT_PRESENT</pullPolicy>
      </configuration>
    </plugin>
  </plugins>
</build>
~~~
# Lệnh build image
~~~
mvn spring-boot:build-image -DskipTests
~~~
# Chạy Docker run cho từng service
~~~
docker run --network mynet -p 8761:8761 --name naming-server in28min/mmv3-naming-server:0.0.1-SNAPSHOT
docker run --network mynet -e eureka.client.serviceUrl.defaultZone=http://naming-server:8761/eureka/ -e MANAGEMENT.ZIPKIN.TRACING.ENDPOINT=http://zipkin-server:9411/api/v2/spans -p 8000:8000 --name currency-exchange in28min/mmv3-currency-exchange-service:0.0.1-SNAPSHOT
docker run --network mynet -e eureka.client.serviceUrl.defaultZone=http://naming-server:8761/eureka/ -e MANAGEMENT.ZIPKIN.TRACING.ENDPOINT=http://zipkin-server:9411/api/v2/spans -p 8100:8100 --name currency-conversion in28min/mmv3-currency-conversion-service:0.0.1-SNAPSHOT
docker run --network mynet -p 9411:9411 --name openzipkin/zipkin:2.23
~~~
# Chạy Docker Compose trong project
~~~
docker-compose up ( đẩy container và run )
docker-compose down ( xoá container )
~~~
# Đưa lên Docker Hub
~~~
docker push phuctapcode/mmv3-currency-exchange-service:0.0.1-SNAPSHOT
~~~
