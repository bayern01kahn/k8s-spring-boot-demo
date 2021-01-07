# 在 Kubernetes 中部署 SpringBoot 应用

> 在 Kubernetes 中通过yaml 配置文件预先声明部署 SpringBoot 应用

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
