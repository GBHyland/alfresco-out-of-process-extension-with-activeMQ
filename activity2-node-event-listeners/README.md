# Create a Node Event Listener Project

## Initial Steps
For this activity, you must use **your environment from the end state of activity 1 from this git project** or **download and extract the _finished-state.zip_ project linked here: https://github.com/GBHyland/alfresco-out-of-process-extension-with-activeMQ/blob/main/activity1-helloworld-oop-skeleton/completed-state.zip**.
* If using the zip file, complete the next section _(Steps to start from zip file)_ steps.

### Steps to start from the zip file.
* Download and extract the zip archive linked above to an accessible location.
* In your JDE, select **File > Open** and navigate to the POM.xml file created in the previous step. Once selected, press the **Open as Project** button on the next popup.
* When the project is opened and any dependency errors are resolved, continue to the next section _(Create a _NodeUpdatedHandler_ Java Class)_.

## Create a _NodeUpdatedHandler_ Java Class
### Imports and Implements
* Create a new Java class file titled ```NodeUpdatedHandler``` in the following path: _src > main > java > org.alfresco > handler_.
* Add the following import:
  ```
      
  ```
* Change the class function to this:
  ```

  ```
* You may need to implement the methods for this class by holding the mouse cursoer over the implement statement and select _Implement methods_ from the popup (implement the handle event).
* Add ```@Component``` just before the class statement.

### Create a LOGGER
* Add the following line of code to the class:
  ```

  ```
* NEED IMPORTS?
* 

* Add the following script to the _handleEvent_ function:
  ```
      final NodeResource nodeResource = (NodeResource) event.getData().getResource();
  ```
* Add the following _if statement_ to single out events that contain content.
  ```

  ```
* 
