# Create an Alfresco Out-of-Process Skeleton (Hello World)

## Initial Steps
1. Create a directory on your local machine for this exercise
2. Download the *Community* and *Enterprise* folders to that directory (from this git)

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

## Define a Maven Project
1. Create a new folder called ```oop-hello-world``` in the directory created in *initial steps*.
2. In terminal *cd* into that directory.
3. To create a Maven project, run the command: ```mvn archetype:generate  -DarchetypeArtifactId=maven-archetype-quickstart```. The Maven creator will ask a series of questions. Choose the options below.
   - Group ID: ```org.alfresco```
   - Artifact ID: ```oop-hello-world```
   - Version: ```0.8```
   - Package ID: _press ENTER_
   - ```Y```
        * This will create a folder with a POM file and Java folder structure.
4. In your JDE, select **File > Open** and navigate to the POM.xml file created in the previous step. Once selected, press the **Open as Project** button on the next popup.
5. Open the POM file by selecting from the left heirarchy panel.
6. Copy the below XML code and replace the code in your POM file.
   - ```Enter code here```
8. Create a new directoryun the _main_ folder titled: ```resources```.
9. Create a new file in the _resources_ folder named: ```application.properties```.
10. Paste the following code into the _application.properties_ file.
    - ```get code from >```
11. Open the _App.java_ file located in the dir: _src > main > java > org.alfresco_.
12. Add the first spring famework import. Add the lines below.
    - ``` add first import here ```
    - You may need to add the Maven dependency. Roll over each import and choose from the actions menu. In the popup window, select **Search for Class**, then **Try updating Maven indexes**.
13. Add the next few imports below.
    - ``` add 3 imports ```
    - Add Maven dependencies if necessary.
14. 
