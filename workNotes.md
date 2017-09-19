## 零碎 
* git 版本回退   

> git log 获取版本号  
  git reset --hard 版本号
 
* git分支

> git branch 查看分支  
  git branch -a  
  git branch dev  创建一个dev分支  
  git branch -d dev 删除dev分支  
  git checkout dev  
  git checkout -b dev  创建并切换到dev分支  
  git pull origin dev  本地分支关联远程分支  
  git checkout -b dev origin/dev 创建并切换到dev分支并且关联到远程dev  
  git push origin dev 将本地分支推送到远程
 
* merge冲突（pod）  

> 删除冲突标记后，pod update。还是无法解决的话直接删除pod和pod.lock文件，然后pod update

* 命令

> open .   打开当前的文件夹.

* 允许Http请求

> NSAppTransportSecurity

>![](ImageSource/allowHttp.png)  

## ios文件系统 -- 8/31
### 文件夹层级  
![](ImageSource/directoryHierarchy.png)  

 * Documents  
 
> Only documents and other data that is user-generated, or that cannot  otherwise be recreated by your application, should be stored in the <Application_Home>/Documents directory and will be automatically backed up by iCloud.  
  
* Library/Caches  
      
>   Data that can be downloaded again or regenerated should be stored >in the <Application_Home>/Library/Caches directory. Examples of files you should put in the Caches directory include database cache files and downloadable content  
     
 * Library/Preferences  
 
 * tmp  
 
> Data that is used only temporarily should be stored in the <Application_Home>/tmp directory. Although these files are not backed up to iCloud, remember to delete those files when you are done with them so that they do not continue to consume space on the user’s device.

* 总结
  
> iCloud includes Backup, which automatically backs up a user’s iOS device daily over Wi-Fi. Everything in your app’s home directory is backed up, with the exception of the application bundle itself, the caches directory, and temp directory.（除了caches，tmp，其他文件夹都会通过icloud备份。其中，document存放由用户生成，不可有app再创建的文件（例如用户写的笔记）。tmp存放临时文件，用完要删除（例如从服务器下载的图片））。 

### 获取文件夹路径  
* NSHomeDirectory()  

> 获取到的是该app的根目录,  
  /Users/xxx/Library/Developer/CoreSimulator/Devices/21726890-8224-43EF-8B25-D002B2EC979B/data/Containers/Data/Application/A3C63249-C349-4C00-AEAC-B29F589F66B1
 
 *  NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);

> 返回的是一个路径数组，但符合传入的参数条件的路径只有一个，所以数组只有一个元素。
  /Users/xxx/Library/Developer/CoreSimulator/Devices/21726890-8224-43EF-8B25-D002B2EC979B/data/Containers/Data/Application/A3C63249-C349-4C00-AEAC-B29F589F66B1/Documents  
    
> NSDocumentDirectory : Document文件夹  
  NSLibraryDirectory :   
  NSCachesDirectory  
  
### 原生对象存储到本地
* writeToFile

> This method recursively validates （递归验证）that all the contained objects are property list objects 
(instances of NSData, NSDate, NSNumber, NSString, NSArray, or NSDictionary) before writing out the file,
 and returns NO if all the objects are not property list objects, since the resultant file would not be a valid property list.
 
 writeToFile会生成一个plist文件，所以那些不是property list objects不能直接调用writeToFile来写入文件。  
 例如装有10个字符串的数组可以直接调用writeToFile，但装有10个自定义person类的实例直接调用writeToFile会写入失败。
 
 * dataWithContentsOfFile / dictionaryWithContentsOfFile / arrayWithContentsOfFile  
 
> writeToFile的相反操作。从文件中读出相应的数据。

* NSData  NSDictionary 互相转换

> NSDictionary *obj = [NSJSONSerialization JSONObjectWithData:jsonData options:(NSJSONReadingMutableContainers) error:nil];   
 
> NSData *data =    [NSJSONSerialization dataWithJSONObject:dic options:NSJSONWritingPrettyPrinted error:nil]


### 自定义对象存储到本地（NSFileManager、NSKeyedArchiver）

## yymodel
## UIImagePickerController
  
  
  
  