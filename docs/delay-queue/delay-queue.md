
## camellia-delay-queue

### compile(java21)
```shell
git clone https://github.com/caojiajun/camellia-jdk21-bootstraps.git
cd camellia-jdk21-bootstraps
mvn clean package
```

### package to tar.gz and run

```shell
cd camellia-delay-queue-bootstraps/camellia-delay-queue-server-bootstrap
cp target/xxx.jar /yourdict/camellia-delay-queue/delay-queue.jar
cd /yourdict/camellia-delay-queue
jar xvf delay-queue.jar
rm -rf delay-queue.jar
touch start.sh
echo "java -XX:+UseG1GC -Xms4096m -Xmx4096m -Dio.netty.tryReflectionSetAccessible=true --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED --add-opens java.base/java.math=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAMED --add-opens java.base/java.security=ALL-UNNAMED --add-opens java.base/java.text=ALL-UNNAMED --add-opens java.base/java.time=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/jdk.internal.access=ALL-UNNAMED --add-opens java.base/jdk.internal.misc=ALL-UNNAMED --add-opens java.base/sun.net.util=ALL-UNNAMED -server org.springframework.boot.loader.launch.JarLauncher" > start.sh
chmod +x start.sh
cd ..
tar zcvf delay-queue.tar.gz ./camellia-delay-queue
```

```shell
tar xvf delay-queue.tar.gz
cd camellia-delay-queue
## modify config on ./BOOT-INF/classes, such as application.yml、logback.xml and more
./start.sh
```

#### build docker images and run

```shell
docker build -t camellia-delay-queue -f docs/delay-queue/Dockerfile .
```

```shell
docker run -d -p 8080:8080 -v /yourconfdict/application.yml:/opt/camellia-delay-queue/BOOT-INF/classes/application.yml camellia-delay-queue
```

