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
   ```
3. In the class, add the following function:
   ```
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
1. Visit the following url and submit the form. Provide an email address you can access. Quay.io trial credentials will be emailed to the address you provide.
   ```
     https://www.hyland.com/en/resources/alfresco-ecm-download
   ```
   
