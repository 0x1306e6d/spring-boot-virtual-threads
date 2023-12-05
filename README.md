# spring-boot-virtual-threads

Spring Boot enabling virtual threads

## Enable virtual threads

You can enable virtual threads by setting the property `spring.threads.virtual.enabled` to `true`.

## Check virtual threads

You can check virtual threads by the name of the current `Thread` serving the `HelloController`.

```
$ curl http://localhost:8080/hello
Hello, world! by tomcat-handler-0

$ curl http://localhost:8080/hello
Hello, world! by tomcat-handler-1

$ curl http://localhost:8080/hello
Hello, world! by tomcat-handler-2

$ curl http://localhost:8080/hello
Hello, world! by tomcat-handler-3
```

Tomcat's `VirtualThreadExecutor` creates virtual threads on every request.
This is as same as:

```java
final OfVirtual threadBuilder = Thread.ofVirtual().name("tomcat-handler-", 0);
// on every request
threadBuilder.start(command);
```
