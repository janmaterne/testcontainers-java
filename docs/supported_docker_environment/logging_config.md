# Recommended logback configuration

Testcontainers, and many of the libraries it uses, utilize SLF4J for logging. In order to see logs from Testcontainers,
your project should include a SLF4J implementation (Logback is recommended). The following example `logback-test.xml`
should be included in your classpath to show a reasonable level of log output:

```xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="info">
        <appender-ref ref="STDOUT"/>
    </root>

    <logger name="org.testcontainers" level="INFO"/>
    <logger name="com.github.dockerjava" level="WARN"/>
</configuration>
```

*Include* means having the required jars on the classpath, like this snippet in the Maven POM:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
    ...
    <dependencies>
    	<dependency>
			<groupId>ch.qos.logback</groupId>
			<artifactId>logback-classic</artifactId>
			<version>1.2.3</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
</project>
```
