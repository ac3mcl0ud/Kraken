### The Find Command.

* Find with non-root user
  
  ```find / -type f -name user.txt 2> /dev/null``` 
  
* Find root suid files
  
  ```find / -type f -user root -perm -u=s 2>/dev/null```
  
* Find with root user
 
  ``` find / -type f -name root.txt```
  
* Find a particukar file or folder 
  
  ```find / -name '.ssh' 2>/dev/null```
  
* Find all files whose name ends with ```.xml```

    ```find /``` to search for items in the root directory
    
    ```-type f``` to filter for files
    
    ```-name "*.xml"``` to filter for items with a ```.xml``` as a suffix

    ```find / -type f -name "*.xml"```  
* Find all files in the /home directory (recursive) whose name is ```user.txt``` (case insensitive)

    ```find /home``` to search for items in the /home directory
    
    ```-type f``` to filter for files
    
    ```-iname user.txt``` to filter for case insensitive name pattern of ```user.txt```

   ```find /home -type f -iname user.txt```

* Find all directories whose name contains the word exploits:

    ```find /``` to search for items in the root directory
    
    ```-type d``` to filter for directories
    
    ```-name "*exploits*"``` to filter for items with ```exploits``` substring in their name

   ```find / -type d -name "*exploits*"```
   
* Know exactly what you're looking for. Find all files owned by the user kittycat

    ```find /``` to search for items in the root directory
    
    ```-type f``` to filter for files
    
    ```-user kittycat``` to filter for items owned by the user ```kittycat```

   ```find / -type f -user kittycat```
   
* Find all files in the /usr/bin directory (recursive) that are owned by root and have at least the SUID permission (use symbolic format)

    ```find /usr/bin``` to search for items in the ```/usr/bin``` directory
    
    ```-type f``` to filter for files
    
    ```-user root``` to filter for items owned by the user ```root```
    
    ```-perm -u=s``` (symbolic format) to filter for items that have at least the SUID permission

   ```find /usr/bin -type f -user root -perm -u=s```  
   
