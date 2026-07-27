# 1. 使用包含 Maven 和 Java 的官方镜像进行构建
FROM maven:3.8.4-openjdk-17 AS build
WORKDIR /app
# 把项目所有文件复制到镜像里
COPY . .
# 执行打包命令
RUN mvn clean package -DskipTests

# 2. 使用纯净的 Java 运行环境
FROM openjdk:17-jdk-slim
WORKDIR /app
# 从上面的构建阶段，把打好的 jar 包复制过来
COPY --from=build /app/sky-server/target/*.jar app.jar

# 3. 暴露端口并启动
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]