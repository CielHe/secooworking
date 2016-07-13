## SELECT A TEMPLATE TO START WITH:

#### **Simple Book**

#### **Science Book**

#### **Exercises Book**

#### **Quizzes Book**

Open...

Quit

* **0.** secoo工作笔记
  * **0.1.** Git基础
    * **0.1.1.** 取得项目的git仓库
      * 

    * **0.1.2.** 纪录每次更新到仓库
      * 

    * **0.1.3.** 查看提交历史
      * 

    * **0.1.4.** 撤销操作
      * 

    * **0.1.5.** 远程仓库的使用
      * 

    * **0.1.6.** 打标签
      * 

    * **0.1.7.** Git分支
      * 

    * **0.1.8.** 工作常用git
      * 


  * **0.2.** 工作账号
    * 

  * **0.3.** NSDate
    * 

  * **0.4.** iOS清理缓存功能
    * 

  * **0.5.** shareSDK
    * 

  * **0.6.** 二维码扫描
    * 

  * **0.7.** React
    * 

  * **0.8.** UIWebView
    * 

  * **0.9.** 安装包瘦身
    * 

  * **0.10.** UI
    * **0.10.1.** scrollview
      * 

    * **0.10.2.**CAShapeLayer复杂view遮罩
      * 

    * **0.10.3.**UIBlurEffect
      * 


  * **0.11.** DEMO
    * 

  * **0.12.** 面试经
    * 



H1H2H3H4

\# iOS清理缓存功能

移动应用在处理网络资源时，一般都会做离线缓存处理，其中以

图片缓存最为典型，其中很流行的离线缓存框架为SDWebImage。

但是，离线缓存会占用手机存储空间，所以缓存清理功能基本成

为资讯、购物、阅读类app的标配功能。

今天介绍的离线缓存功能的实现，主要分为缓存文件大小的获取

、删除缓存文件的实现。

获取缓存文件的大小

由于缓存文件存在沙箱中，我们可以通过NSFileManager

API来实现对缓存文件大小的计算。

计算单个文件大小

\`\`\`

+\(float\)fileSizeAtPath:\(NSString \*\)path{

 NSFileManager \*fileManager=\[NSFileManager

defaultManager\];

 if\(\[fileManager fileExistsAtPath:path\]\){

 long long size=\[fileManager

attributesOfItemAtPath:path error:nil\].fileSize;

 return size\/1024.0\/1024.0;

 }

 return 0;

PREVIEW

# **iOS清理缓存功能**

移动应用在处理网络资源时，一般都会做离线缓存处理，其中以图片缓存最为典型，其中很流行的离线缓存框架为SDWebImage。

但是，离线缓存会占用手机存储空间，所以缓存清理功能基本成为资讯、购物、阅读类app的标配功能。

今天介绍的离线缓存功能的实现，主要分为缓存文件大小的获取、删除缓存文件的实现。

获取缓存文件的大小

由于缓存文件存在沙箱中，我们可以通过NSFileManager API来实现对缓存文件大小的计算。

计算单个文件大小

```
+(float)fileSizeAtPath:(NSString *)path{
    NSFileManager *fileManager=[NSFileManager defaultManager];
    if([fileManager fileExistsAtPath:path]){
        long long size=[fileManager attributesOfItemAtPath:path error:nil].fileSize;
        return size/1024.0/1024.0;
    }
    return 0;
}

```

计算目录大小

```
+(float)folderSizeAtPath:(NSString *)path{
    NSFileManager *fileManager=[NSFileManager defaultManager];
    float folderSize;
    if ([fileManager fileExistsAtPath:path]) {
        NSArray *childerFiles=[fileManager subpathsAtPath:path];
        for (NSString *fileName in childerFiles) {
            NSString *absolutePath=[path stringByAppendingPathComponent:fileName];
            folderSize +=[FileService fileSizeAtPath:absolutePath];
        }
　　　　　//SDWebImage框架自身计算缓存的实现
        folderSize+=[[SDImageCache sharedImageCache] getSize]/1024.0/1024.0;
        return folderSize;
    }
    return 0;
}

```

清理缓存文件

同样也是利用NSFileManager API进行文件操作，SDWebImage框架自己实现了清理缓存操作，我们可以直接调用。

```
+(void)clearCache:(NSString *)path{
    NSFileManager *fileManager=[NSFileManager defaultManager];
    if ([fileManager fileExistsAtPath:path]) {
        NSArray *childerFiles=[fileManager subpathsAtPath:path];
        for (NSString *fileName in childerFiles) {
            //如有需要，加入条件，过滤掉不想删除的文件
            NSString *absolutePath=[path stringByAppendingPathComponent:fileName];
            [fileManager removeItemAtPath:absolutePath error:nil];
        }
    }
    [[SDImageCache sharedImageCache] cleanDisk];
}

```

实现效果：

