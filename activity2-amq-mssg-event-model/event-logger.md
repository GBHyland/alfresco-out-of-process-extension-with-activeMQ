## ActiveMQ Messages (community vs enterprise)

### Enable Debug Logging
1. In the **application.properties** file, add the following lines:
   ```
      # Set the logging level to DEBUG
      logging.level.org.alfresco.event.sdk.integration.transformer.EventGenericTransformer=DEBUG
   ```
2. open the **App.java** file and add the following imports:
   ```
      import org.springframework.boot.SpringApplication;
      import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
      import org.springframework.boot.autoconfigure.SpringBootApplication;
      import org.springframework.boot.autoconfigure.security.servlet.SecurityAutoConfiguration;
      import org.springframework.integration.dsl.IntegrationFlow;
      import org.springframework.context.annotation.Bean;
      import org.alfresco.event.sdk.handling.filter.EventTypeFilter;
      import org.alfresco.event.sdk.handling.filter.NodeTypeFilter;
      import org.alfresco.event.sdk.integration.EventChannels;
      import org.slf4j.Logger;
      import org.slf4j.LoggerFactory;
      import org.alfresco.event.sdk.integration.EventChannels;
      import org.alfresco.event.sdk.integration.filter.IntegrationEventFilter;
   ```
3. In the class, add the following function:
   ```
      private static final Logger LOGGER = LoggerFactory.getLogger(App.class);
      @Bean
      public IntegrationFlow logTheCreationOfNodesOfTypeContent() {
        return IntegrationFlow.from(EventChannels.MAIN)
                .filter(IntegrationEventFilter.of(EventTypeFilter.NODE_CREATED
                        .and(NodeTypeFilter.of("cm:content"))))
                .handle(t -> LOGGER.info("A new node of type cm:content has been created! - Event: {}", t.getPayload().toString()))
                .get();
      }
   ```

### Run Enterprise, Build & Test Java Application
1. In your JDE, open a Terminal window and perform the following steps to package and run:
    * Create a Java package using the command: ```mvn package```.
    * Run the Java package with the command: ```java -jar target/oop-*.jar```
2. Open your browser to your alfreco environment at: ```http://localhost:8080/share```.
3. Navigate to the **shared files** section and create a text document.
    * Notice in the output Terminal window in your JDE you should see a a log from the **EventGenericTransformer** which will include the following properties:
      * **resourceReaderAuthroities** and **resourceDeniedAuthorities**.
    * This is the difference between the enterprise and community ActiveMQ messages, which provides informatioin of who has and does not have access to the node.
   
