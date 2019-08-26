# Organize-files
### Python - This python code is written to organise files under a directory based on their file format. When you run this code, it will fetch the current working directory and will check the files under that directory then it will create a new directory based on their file format and finally will move it to the newly created directory.  If the directory already exists, then it wont create a new directory and it will just move the files to the respective directories. Also, if there is files with file type not specified then it will move to a common directory.

```python
import subprocess
import os

location = os.getcwd()

for item in os.walk(location):
   
    curDir,subDirs,subFiles = item
    
    for subFile in subFiles:
        
        fetch_format = subFile.split('.')
        
        if len(fetch_format) == 1:
        
            cmd = 'mkdir {}/other-files; mv {} {}/other-files/'.format(location,fetch_format[0],location)
        
            subprocess.call(cmd, shell = True)
            
        else:
                
            full_file = os.path.join(location,subFile)
        
            for directory in subDirs:
            
                if os.path.exists(directory.endswith(fetch_format[-1])) in subDirs:
            
                   try:
                    
                        cmd = 'mv {} {}/test-{}/'.format(full_file,location,fetch_format[-1])
        
                        subprocess.call(cmd, shell = True)
            
                   except:
                    
                        break
                    
                else:
        
                    try:
            
                        cmd = 'mkdir test-{}; mv {} {}/test-{}/'.format(fetch_format[-1],full_file,location,fetch_format[-1])
        
                        subprocess.call(cmd, shell = True)
            
                    except:
            
                        break
```

### The sample output of this code will looks like as follows.

- drwxrwxr-x 10 ubuntu ubuntu 4096 Aug 26 06:04 ./

- drwxr-xr-x 28 ubuntu ubuntu 4096 Aug 26 06:03 ../

- drwxrwxr-x  2 ubuntu ubuntu 4096 Aug 26 06:04 other-files/

- drwxrwxr-x  3 ubuntu ubuntu 4096 Aug 26 05:58 test-bz/

- drwxrwxr-x  2 ubuntu ubuntu 4096 Aug 26 05:58 test-conf/

- drwxrwxr-x  2 ubuntu ubuntu 4096 Aug 26 05:58 test-gz/

- drwxrwxr-x  2 ubuntu ubuntu 4096 Aug 26 06:04 test-ipynb/

- drwxrwxr-x  2 ubuntu ubuntu 4096 Aug 26 05:58 test-mp3/

- drwxrwxr-x  3 ubuntu ubuntu 4096 Aug 26 06:04 test-py/

- drwxrwxr-x  2 ubuntu ubuntu 4096 Aug 26 05:58 test-txt/

