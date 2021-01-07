# 在 Kubernetes 中部署 SpringBoot 应用

> 在 Kubernetes 中通过yaml 配置文件预先声明部署 SpringBoot 应用

## 创建 SpringBoot 应用

- 添加 Dockerfile
```dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
ARG JAR_FILE
ADD ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom", "-Duser.timezone=GMT+08", "-jar","/app.jar"]
```

- 编译打包
```bash
./gradlew clean build -x test
```

- 本地docker run (项目目录下) 
```bash
docker build --build-arg JAR_FILE=./build/libs/k8s-service-0.0.1-SNAPSHOT.jar -t k8s-service:demo .
```

## 在  Kubernetes 中添加服务
- 创建服务
```
kubectl apply -f k8s-service.yaml
```

- 等待服务启动之后访问 `127.0.0.1:30002`，会返回 `Hello Kubernetes`，部署完成
