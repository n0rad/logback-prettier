Pretty logback output for sysout/syserr with custum color (and bold) text by level

Maven dependency :

    <dependency>
      <groupId>fr.norad.logback.prettier</groupId>
      <artifactId>logback-prettier</artifactId>
      <version>0.5</version>
    </dependency>

Sample logback.xml :

    <configuration scan="true" scanPeriod="30 seconds">
        <conversionRule conversionWord="colorlevel"
            converterClass="fr.norad.logback.prettier.ColorLevelCompositeConverter" />
        <conversionRule conversionWord="bold"
            converterClass="fr.norad.logback.prettier.BoldCompositeConverter" />
    
        <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
            <target>System.out</target>
            <withJansi>true</withJansi>
            <encoder>
                <pattern><![CDATA[%blue(%d{HH:mm:ss.SSS}) [%-10.10thread] %colorlevel(%-5level) %-45.45(%41C{41}:%L) - %msg%n]]></pattern>
            </encoder>
            <filter class="fr.norad.logback.prettier.OutFilter" />
        </appender>
        <appender name="STDERR" class="ch.qos.logback.core.ConsoleAppender">
            <target>System.err</target>
            <withJansi>true</withJansi>
            <encoder>
                <pattern><![CDATA[%boldBlue(%d{HH:mm:ss.SSS}) %bold([%-10.10thread]) %colorlevel(%-5level) %bold(%-45.45(%41C{41}:%L)) - %colorlevel(%msg) %n]]></pattern>
            </encoder>
            <filter class="fr.norad.logback.prettier.ErrFilter" />
        </appender>
    
        <root>
            <level value="DEBUG" />
            <appender-ref ref="STDOUT" />
            <appender-ref ref="STDERR" />
        </root>
    </configuration>

Will result in : 

![alt screenshot](https://raw.github.com/n0rad/logback-prettier/master/screenshot.png)
