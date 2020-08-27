# error-handler-library
An advanced mule 4 error handler library with handler overriding and extension

Design document: https://wiki.corp.mulesoft.com/display/OBD/Error+Handler+Library

# Getting Started
As per Organization needs, modify error handler library by
- Add new error types
- Modify default error message
- Modify Error processing logic

### Steps:
1. Clone the repository
2. Update library as required
3. Run ```mvn deploy``` from project root folder to Publish this library to your/customer artifact repo (Nexus, artefactory, azure repo etc). 
_You can publish to Exchange with the current configuration(Just need to update the project.groupId )_

(Make sure you have appropriate credentials configured in `settings.xml` file in local `.m2` folder.

# How to Use?
## Create new API/ Update Existing API with Error handler library

### Steps:

1. Please make sure you have user credentials in `settings.xml` file in local `.m2` folder 
2. Publish [Json logger][1] in Customer Exchange 
3. Add [json-logger][1] to project if it has not been added before and Configure json-logger global element
4. In Project pom.xml file add the below plugin in `<build>` session along with other plugins

```
<build>
....
</plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <version>${maven.dependency.plugin.version}</version>
                <executions>
                    <execution>
                        <id>unpack</id>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>unpack</goal>
                        </goals>
                        <configuration>
                            <artifactItems>

                                <artifactItem>
                                    <!-- *************************************************** -->
                                    <!-- TODO: Replace with the Published error-handling artifact library details -->
                                    <!-- *************************************************** -->
                                    <groupId>b144f004-790a-4e9b-8ff3-61a28db48356</groupId>
                                    <artifactId>error-handler-library</artifactId>
                                    <version>${replace-with-latest-version}</version>
                                    <!-- *************************************************** -->
                                    <classifier>mule-application</classifier>
                                    <overWrite>true</overWrite>
                                    <outputDirectory>src/main/mule/</outputDirectory>
                                    <includes>**/error-*.xml</includes>
                                </artifactItem>
                                <artifactItem>
                                    <!-- *************************************************** -->
                                    <!-- TODO: Replace with the Published error-handling artifact library details -->
                                    <!-- *************************************************** -->
                                    <groupId>b144f004-790a-4e9b-8ff3-61a28db48356</groupId>
                                    <artifactId>error-handler-library</artifactId>
                                    <version>1.0.0-SNAPSHOT</version>
                                    <!-- *************************************************** -->
                                    <classifier>mule-application</classifier>
                                    <overWrite>true</overWrite>
                                    <outputDirectory>src/main/resources/</outputDirectory>
                                    <includes>**/*.yaml</includes>
                                </artifactItem>
                            </artifactItems>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
...
        </plugins>
    </build>
```

4. Go to Project root folder and execute `mvn clean install` . This should pull the library files from Exchange or Artefact repo.  
5. Configure properties file (Please take this configuration for [reference][2]. This file is only for reference and won't be part of library in the API)
6. Make sure to configure http-listener response accordingly.(Please take this configuration for ([reference][2] This file is only for reference and won't be part of library in the API)
7. Add flow reference to `error-mainErrorHandlerFlow` in `On Error Propagate` or `On Error Continue` to initiate the error handler libary logic. ([reference][2]. This file is only for reference and won't be part of library in the API)


Please refer this [sample project][3] for more info

  [1]: https://blogs.mulesoft.com/dev/anypoint-platform-dev/json-logging-mule-4/
  [2]: https://github.com/mulesoft-consulting/error-handler-library/blob/master/src/main/mule/nl-common-eh.xml
  [3]: https://github.com/mulesoft-consulting/mule4-rest-api-template

