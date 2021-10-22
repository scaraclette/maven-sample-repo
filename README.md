## Maven Starter
This repo gives an example on how to compile Java projects using Maven.

## Creating this repo
1. The base of this project was created via VSCode's Maven project generator. More information can be found here: https://code.visualstudio.com/docs/java/java-build (download the extension bundle)
2. After downloading the extension, what I did to create the base project was using the command palette (command + shift + p, for Mac) and choosing:
    > Create Java Project -> Maven -> maven-archetype-quickstart
3. Insert the groupId (company name), artifactId (projectName), and just do 1.0 if it asks for version etc.
4. To add dependencies, go to pom.xml and add it. For example, adding GSON, you would need to add:
```
<!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.8</version>
</dependency>
``` 
5. What I didn't know before was we needed to add Maven Assembly Plugin to combine external dependencies into a single JAR file. We add this by adding the plugin in pom.xml for plugins (bottom). I've attached it already. Note that you need to change the mainClass tag to point to your main class! In this example, my groupId was example.com, but my main class is App (found in src/main/java/com/example):
http://maven.apache.org/plugins/maven-assembly-plugin/
```
         <plugin>
          <artifactId>maven-assembly-plugin</artifactId>
          <configuration>
            <archive>
              <manifest>
                <mainClass>example.com.App</mainClass>
              </manifest>
            </archive>
            <descriptorRefs>
              <descriptorRef>jar-with-dependencies</descriptorRef>
            </descriptorRefs>
          </configuration>
        </plugin>
```
6. To compile Maven projects, we do something like `mvn package`, but since we're using a plugin that bundles the libraries, run the following: `mvn compile assembly:single`
7. A jar file should be created in target folder. Run that jar file by doing `java -jar target/demo-1.0-jar-with-dependencies.jar`. I've created a shell script so that you can compile and run right away within this project.
