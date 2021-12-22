### Useful Linux Commands.

#### Find files. 
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
