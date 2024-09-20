# Create a Node Event Listener Project

## Initial Steps
For this activity, you must use **your environment from the end state of activity 1 from this git project** or **download and extract the _finished-state.zip_ project linked here: https://github.com/GBHyland/alfresco-out-of-process-extension-with-activeMQ/blob/main/activity1-helloworld-oop-skeleton/completed-state.zip**.
* If using the zip file, complete the next section _(Steps to start from zip file)_ steps.

### Steps to start from the zip file.
* Download and extract the zip archive linked above to an accessible location.
* In your JDE, select **File > Open** and navigate to the POM.xml file created in the previous step. Once selected, press the **Open as Project** button on the next popup.
* When the project is opened and any dependency errors are resolved, continue to the next section _(Create a _NodeUpdatedHandler_ Java Class)_.

## Create a _NodeUpdatedHandler_ Java Class

### Dependencies
* Add the following dependency to your **pom.xml** in the main dependency tag:
  ```
    <dependency>
      <groupId>org.alfresco</groupId>
      <artifactId>alfresco-acs-java-rest-api-spring-boot-starter</artifactId>
      <version>6.2.0</version>
    </dependency>
  ```
* Save the pom.xml file and **Reload project** using the right-click menu on the pm.xml file in the left panel.

### Build NodeUpdatedHandler Java Class
* Create a new Java class file titled ```NodeUpdatedHandler``` in the following path: _src > main > java > org.alfresco > handler_.
* Remove **all** of the code within the file and paste the following code into the file:
  ```
    package org.alfresco.handler;

    import org.alfresco.core.handler.CommentsApi;
    import org.alfresco.core.model.CommentBody;
    import org.alfresco.event.sdk.handling.filter.EventFilter;
    import org.alfresco.event.sdk.handling.filter.IsFileFilter;
    import org.alfresco.event.sdk.handling.handler.OnNodeUpdatedEventHandler;
    import org.alfresco.repo.event.v1.model.*;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Component;
    import java.util.Set;
    
    @Component
    public class NodeUpdatedHandler implements OnNodeUpdatedEventHandler {
    
        private static final Logger LOGGER = LoggerFactory.getLogger(NodeUpdatedHandler.class);
        @Autowired
        CommentsApi commentsApi;
    
        @Override
        public void handleEvent(RepoEvent<DataAttributes<Resource>> event) {
            
        }
    
        @Override
        public EventFilter getEventFilter() {
            return IsFileFilter.get();
        }
    
        // https://github.com/Alfresco/alfresco-java-sdk/blob/develop/samples/event-api-handlers/src/main/java/org/alfresco/sdk/sample/event/handler/MultipleEventTypeHandler.java
        @Override
        public Set<EventType> getHandledEventTypes() {
            return OnNodeUpdatedEventHandler.super.getHandledEventTypes();
        }
    }

  ```
* Declare a NodeResource variable inside of the **handleEvent** function:
  ```
    final NodeResource nodeResource = (NodeResource) event.getData().getResource();
  ```
* Add a Logger command to the _handleEvent_ just after the _nodeResource_ variable:
  ```
    LOGGER.info("\n\n ** DATA: "+event.getData());
  ```
* Add the following _if statement_ to single out events that contain content.
  ```
    if (((NodeResource) event.getData().getResourceBefore()).getContent() != null) {

    }
  ```
* **Note:** A document node in ACS has associated nodes that will update when a change is made to the document, causing the Updated handler event to execute mutliple times. By ensuring that the _getContent_ attribute of the _getResourceBefore_ attribute of the edited node is **not** null, we can single out responses that are referring to the content node.
* Add the following line of code inside the if statement:
  ```
    System.out.println("This content has been modified. ");
  ```

### Deploy the Java App and test the EventHandler 
* With your alfresco environment running, execute both of these commands in your Terminal window to run your java application:
  ```
    mvn package
  ```
  ```
    java -jar target/oop-*.jar
  ```
* In your Alfresco environment, **log in as an Admin** and create a Site if you do not have one already (There may be a sample site already created - use that one if so). 
* Create a plain text file in the Document Library of your site titled: ```Created by Admin```.
* Edit the file's content within Share.
* Go back to your Terminal window in your JDE to view the printed results.
    * **Note:** You should see each returned data block from the _LOGGER_ command that is printing the event data, however only one of those blocks should be followed by the _"This content has been modified."_ system print comment added within the "if" statement.
* Stop the Java application by using ```CTRL+C``` inside the Terminal window.

### Apply conditional logic that checks if a document was edited by someone other than creator
* Add the following "if" statement nested inside of your current "if" statement:
  ```
    if (!nodeResource.getModifiedByUser().getId().equals(nodeResource.getCreatedByUser().getId()))
    {

    }
  ```
* **Note:** The above "if" statement compares the _CreatedBy_ user ID to the _ModifiedBy_ user ID to determine if the ID's are **not** the same. This will allow you to perform logic against content nodes (documents) that have been edited by a user other than the creator.
*  Add the following "print" command inside the new "if" statement to print a message to the Terminal:
  ```
    System.out.println("This doc was modified by someone other than creator!");
  ```

### Deploy the Java App and test the conditional logic 
* With your alfresco environment running, execute both of these commands in your Terminal window to run your java application:
  ```
    mvn package
  ```
  ```
    java -jar target/oop-*.jar
  ```
* In your Alfresco environment create a new user and add that user to the Site you're using to test.
* Log out and log back in as this new user.
* Navigate to the _Created by Admin_ document created earlier and edit the document adding a line to the body: ```Edited by other user.```.
* Go back to the Terminal window in your JDE. You should see response blocks from the _LOGGER_ command as before, and that one of them contains the added text from the "if" statements: _"This content has been modified."_ and _"This doc was modified by someone other than creator!"_.
* Stop the Java application by using ```CTRL+C``` inside the Terminal window.


### Apply a Comment action to documents edited by users other than their creator
* Open the _aaplication.properties_ file and add the following lines of code:
  ```
    # Location of the server and API endpoints
    content.service.url=http://localhost:8080
    
    # HTTP Basic Authentication that will be used by the API
    content.service.security.basicAuth.username=admin
    content.service.security.basicAuth.password=admin
  ```
* Inside of the second, nested "if" statement, add the following lines of code:
  ```
    CommentBody commentBody = new CommentBody();
    commentBody.setContent("Edited by user: "+nodeResource.getModifiedByUser().getId());
    commentsApi.createComment(nodeResource.getId(), commentBody, null);
  ```
* **Note:** The actions here will create a new comment on the document with the following text: _"edited by user: [user name]"_.

### Deploy the Java App and test the Comment action execution 
*  Add the following "print" command inside the new "if" statement to print a message to the Terminal:
  ```
    System.out.println("This doc was modified by someone other than creator!");
  ```
* With your alfresco environment running, execute both of these commands in your Terminal window to run your java application:
  ```
    mvn package
  ```
  ```
    java -jar target/oop-*.jar
  ```
* Log in as the new user created earlier.
* Navigate to the _Created by Admin_ document created earlier and edit the document adding a line to the body: ```Edited by other user.```.
* Refresh the document page and look below the document at the comments section. You should see a new comment with the _"Edited by user: [user name]"_ comment.
* Stop the Java application by using ```CTRL+C``` inside the Terminal window.
