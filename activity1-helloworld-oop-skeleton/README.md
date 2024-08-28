# Create an Alfresco Out-of-Process Skeleton (Hello World)

## Initial Steps
1. Create a directory on your local machine for this exercise.
2. Download the *Community* and *Enterprise* folders to that directory (above).

## Create a Community Edition environment
1. In Terminal, navigate to the *community* folder downloaded from initial steps.
   - The folder should have a _compose.yaml_ file. Use ```ls``` command to ensure file is present. 
3. Run docker command ```docker compose up```
   - Docker will created containers and download all necessary images.
   - First time running this command may take a few moments.
4. Test alfresco is running by opening a browser window at address: ```http://localhost:8080/alfresco```
5. Connect to ActiveMQ using browser at address: ```http://localhost:8161```
6. Stop the alfresco environment with command by entering CTRL+C in Terminal.
7. Use docker command ```docker compose down``` to remove containers.

## Create an Enterprise Edition environment
1. In Terminal, navigate to the *enterprise* folder downloaded from initial steps.
   - The folder should have a _compose.yaml_ file. Use ```ls``` command to ensure file is present. 
3. Run docker command ```docker compose up```
   - Docker will created containers and download all necessary images.
   - First time running this command may take a few moments.
   - *Note:* You may see some errors in terminal due to indexing component being removed from the yaml file (not necessary for this activity).
4. Test alfresco is running by opening a browser window at address: ```http://localhost:8080/alfresco```
5. Connect to ActiveMQ using browser at address: ```http://localhost:8161```
6. Stop the alfresco environment with command by entering CTRL+C in Terminal.
7. Use docker command ```docker compose down``` to remove containers.

## Create a Maven Project
1. Create a new folder called ```oop-hello-world``` in the directory created in *initial steps*.
2. In terminal *cd* into that directory.
3. To create a Maven project, run the command:
   ```
         mvn archetype:generate  -DarchetypeArtifactId=maven-archetype-quickstart
   ```
   - The Maven creator will ask a series of questions. Choose the options below:
   - Group ID: ```org.alfresco```
   - Artifact ID: ```oop-hello-world```
   - Version: ```0.8```
   - Package ID: _press ENTER_
   - ```Y```
        * This will create a folder with a POM file and Java folder structure.
5. In your JDE, select **File > Open** and navigate to the POM.xml file created in the previous step. Once selected, press the **Open as Project** button on the next popup.
6. Delete the **App.Test** file located at: _src > test > java > org.alfresco_.
7. Open the POM file by selecting from the left heirarchy panel.
8. Delete all of the file contents.
9. Add the following line of code:
   ```
         <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
         
         
         
         </project>
   ```
10. Add the project name, groupId, artifactId, version and modelVersion **inside** the <project> tag.
   ```
         <name>oop-hello-world</name>
         <groupId>org.alfresco</groupId>
         <artifactId>oop-hello-world</artifactId>
         <version>0.8</version>
         <modelVersion>4.0.0</modelVersion>
   ```
11. Specify the packaging type inside the <project> tag:
   ```
         <packaging>jar</packaging>
         <url>http://maven.apache.org</url>
   ```
11. Specify the parent artifact that you will inherit properties necessary to the module.
    ```
         <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>3.2.8</version>
            <relativePath/>
         </parent>
    ```
12. Specify the properties that need to be defined for this project.
    ```
         <properties>
            <maven.compiler.source>17</maven.compiler.source>
            <maven.compiler.target>17</maven.compiler.target>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
         </properties>
    ```
13. Add repositories that your project needs to download required artifacts from.
    ```
         <repositories>
            <repository>
               <id>alfresco-public</id>
               <url>https://artifacts.alfresco.com/nexus/content/groups/public</url>
            </repository>
         </repositories>
    ```
14. Declare any dependencies that your project needs to fetch external libraries from.
    ```
         <dependencies>
            <dependency>
               <groupId>org.alfresco</groupId>
               <artifactId>alfresco-java-event-api-spring-boot-starter</artifactId>
               <version>6.2.0</version>
            </dependency>
            <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter</artifactId>
            </dependency>
         </dependencies>
    ```
15. Specify the plugins used in the build section that Maven needs to build the project.
    ```
         <build>
            <plugins>
               <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-compiler-plugin</artifactId>
               </plugin>
               <plugin>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-maven-plugin</artifactId>
               </plugin>
            </plugins>
         </build>
    ```
   * Save the pom file. Right-click the POM.xml file in the left heirarchy and select ```Maven > Reload project```. This should get rid of any errors in your pom file.
16. Create a new directory in the _main_ folder titled: ```resources```.
17. Create a new file in the _resources_ folder named: ```application.properties```.
18. Paste the following code into the _application.properties_ file.
      ```
         # Application.properties defines configuration which is required to run the application in a different environment.
         # Each environment will have a different properties needing to be defines.
         
         # Specify where the Alfresco Active MQ JMS Broker is running
         spring.activemq.brokerUrl=tcp://localhost:61616
         
         # This property is required if you want Spring Boot to auto-define the ActiveMQConnectionFactory.
         # otherwise you can define that bean in Spring config
         spring.jms.cache.enabled=false
         
         # Enable Spring Integration based event handlers
         alfresco.events.enableSpringIntegration=true
         
         # Turn off plain Java event handlers
         alfresco.events.enableHandlers=true
      ```
19. Open the _App.java_ file located in the dir: _src > main > java > org.alfresco_.
20. Add the first spring famework import. Add the lines below.
    - ```import org.springframework.boot.SpringApplication;```
    - You may need to add the Maven dependency. Roll over each import and choose from the actions menu. In the popup window, select **Search for Class**, then **Try updating Maven indexes**.
21. Add the next few imports below.
      ```
         import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
         import org.springframework.boot.autoconfigure.SpringBootApplication;
         import org.springframework.boot.autoconfigure.security.servlet.SecurityAutoConfiguration;
      ```
    - Add Maven dependencies if necessary.
22. Add the following lines to your *App.jva* file before the class.
       ```
         @SpringBootApplication
         @EnableAutoConfiguration(exclude={SecurityAutoConfiguration.class})
       ```
23. Inside the class function, paste the following code over the default code:
       ```
         public static void main( String[] args )
          {
              SpringApplication.run(App.class, args);
          }
       ```
24. Create the _NodeCreatedHandler_.
    * Create a new package called **handler** at the following location: _src > java > org.alfresco > handler_ using the right-click menu and selecting "new package".
    * Create a new Java file titled ```NodeCreatedHandler``` inside the following _handler_ directory.
25. Paste the following code into the **NodeCreatedHandler** java file:
       ```
         package org.alfresco.handler;

         import org.alfresco.event.sdk.handling.handler.OnNodeCreatedEventHandler;
         import org.alfresco.repo.event.v1.model.*;
         import org.springframework.stereotype.Component;
         
         @Component
         public class NodeCreatedHandler implements OnNodeCreatedEventHandler {
             @Override
             public void handleEvent(RepoEvent<DataAttributes<Resource>> event) {
                 final NodeResource nodeResource = (NodeResource) event.getData().getResource();
                 System.out.println("Hello World! "+nodeResource.getName());
             }
         }

       ```
26. Save all edited files. The skeleton environment is now ready to test.
27. In Terminal, start your alfresco environment using the docker command: ```docker compose up```.
28. In your JDE, open a Terminal window and perform the following steps to package and run:
    * Create a Java package using the command: ```mvn package```.
    * Run the Java package with the command: ```java -jar target/oop-*.jar```
29. Open your browser to your alfreco environment at: ```http://localhost:8080/share```.
30. Navigate to the **shared files** section and create a text document.
    * Watch the output Terminal window in your JDE which should print the messsage: ```Hello World! [your_file_name]```.
    
