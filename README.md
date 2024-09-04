## Alfresco Out-of-Process Extension Project with ActiveMQ Messaging

### Necessary for this Project
1. Quay.io Alfresco account (to pull enterprise images)
   * If you do not have a Quay.io account, obtain trial credentials by following these steps:
     * Visit the following url and submit the form. Provide an email address you can access. Quay.io trial credentials will be emailed to the address you provide.
         ```
           https://www.hyland.com/en/resources/alfresco-ecm-download
         ```
3. IntelliJ Software (JDE Environment) - (https://www.jetbrains.com/idea/download)
4. Java installed on your machine: 
   * https://www.oracle.com/java/technologies/downloads/?er=221886#jdk22-mac
5. Maven installed on your machine:
   * Steps to install Maven:
     1. In terminal window enter the following command:
        ```
          /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
        ```
    2. in the feedback of the Brew installation find the two commands under the **Next Steps:** header and enter each one of those commands into Terminal.
    3. Enter the final command to install Maven:
    ```
      brew install maven
    ```
    4. To check that Maven is installed, enter the following command:
    ```
      mvn -version
    ```
