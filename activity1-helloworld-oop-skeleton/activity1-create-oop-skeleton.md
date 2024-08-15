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

8. 
