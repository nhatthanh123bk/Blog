## Create group for file 

### Create group
- command create 1 group
    ```Shell Script
    groupadd name_group
    ```
- add 1 count into group
    ```Shell Script
    usermod -aG name_group name_user
     ```    
- Change the group owner of the file/folder to name_group
    ```Shell Script
    chgrp name_file/name_folder name_group
    ```
- set read/write access for the group members
    ```Shell Script
    chmod 771 name_file/name_folder
    ```
- Command show all groups in system.
    ```Shell Script
    getent group
    ```    
- Command show all user in system:
    ```Shell Script
    getent passwd    
    ```   
- Command delete 1 user from group:
    ```Shell Script
    gpasswd -d name_user name_group
    ```     
 (nhatthanhg)  