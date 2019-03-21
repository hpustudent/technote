### mvn -DskipTests=true  package

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-jar-plugin</artifactId>
            <version>2.6</version>
            <configuration>
                <archive>
                    <manifest>
                        <addClasspath>true</addClasspath>
                        <classpathPrefix>lib/</classpathPrefix>
                        <mainClass>com.xx.xxx.start.Application</mainClass> <!-- 运行jar的main class  -->
                    </manifest>
                    <!-- 添加本地的jar -->
                    <manifestEntries>
                        <Class-Path>lib/class-util-1.0.jar lib/pool-executor-1.0.jar</Class-Path> <!-- 这个>lib/class-util-1.0.jar 路径是已经被打包到target/lib里的,多个包用空格隔开就可以了 -->
                    </manifestEntries>
                </archive>
            </configuration>
        </plugin>
