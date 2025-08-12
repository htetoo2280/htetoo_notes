---
id: 4zh1449ulgovce5t7xdp0lc
title: Import_os
desc: ''
updated: 1753328976821
created: 1753327507699
---


```bash
import os

print(os.getcwd())  # current working directory

# if want to change working directory
os.chdir('D:\\htetoo')

# check all dir 
os.listdir()
file_dir = os.listdir()
print(file_dir)

# create dir
os.mkdir()  # top lvl directory 
os.mkdirs('Java\\OOP\\gg') # create all sub dir

# to remove 
os.rmdir() # top lvl directory remove (empty only)
os.rmdirs('Java\\OOP\\gg') # remove all sub dir (**** not use)

```

## changing working dir 
```bash
import os

# print(os.getcwd())
# os.chdir('D:\\htetoo')
# print(os.getcwd())


path = os.getcwd()  ## check the dir with tree directory  , will return (currentpath , dirname , file) , datatype Truple

# tuple unpack
# str , list , list
for dirpath , dirname , file in os.walk(path):   # use when a dir or file is finding in all dir
    print()
    print(dirpath)
    print(dirname)
    print(file)
    print()

```

## checking env
```bash
import os
tmp = os.environ.get('tmp')
print (tmp)
```


# file path joining
```bash
import os

os.chdir('D:\\htetoo')
path = os.getcwd()

print(path )
secondpath = 'spark'

final_path = os.path.join(path, secondpath)
print(f'this is final path {final_path} ')
```




## the last final component of path 
```bash
import os
aa = os.getcwd()
print(aa)
print(os.path.basename(aa)) # return the last file componant of a dir 
print(os.path.dirname(aa)) # return the last dir componant of a path

print(os.path.exists(aa + 'bb')) # finding the file in dir

print(os.path.isdir('D:\\htetoo\\spark'))  # is the spark is folder

print(os.path.isfile('D:\\htetoo\\spark\\os_env.py'))  # is the os_env.py is file

print(os.path.splitext('D:\\htetoo\\spark\\os_env.py')) # split with "."
```

