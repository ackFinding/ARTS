看到一个有意思的拷贝u盘的程序，自己写了下。如果存在u盘目录，则循环拷贝u盘中的新文件到指定路径下。
这里把u盘路径写死了
```python
 # -*-coding:utf-8-*-                                                                                  
from time import sleep                                                                                
import os, shutil                                                                                     
                                                                                                      
usb_path = 'I:\\'                                                                                     
save_path = 'F:\\test\\'                                                                              
if os.path.exists(usb_path):                                                                          
    content = os.listdir(save_path)                                                                   
    while True:                                                                                       
        new_content = os.listdir(usb_path)                                                            
        if new_content == content:                                                                    
            sleep(3)                                                                                  
        else:                                                                                         
            x = [item for item in new_content if item not in content]                                 
            if x:                                                                                     
                shutil.copytree(os.path.join(usb_path, x[0]), os.path.join(save_path, x[0]))          
```
