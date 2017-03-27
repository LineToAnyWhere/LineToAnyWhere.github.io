# 格式转换 #
> # 命令描述 #

将DOS格式文档与linux/unix格式文档格式互转
> # 常用参数 #

* **dos2unix**  
  -k :保留该档案原本的 mtime 时间格式 (不更新档案上次内容经过修订的时间)  
  -n :保留原本的旧档，将转换后的内容输出到新档案，如： dos2unix -n old new
* **unix2dos**  
  -k :保留该档案原本的 mtime 时间格式 (不更新档案上次内容经过修订的时间)  
  -n :保留原本的旧档，将转换后的内容输出到新档案，如： dos2unix -n old new

> # 应用示例 #

```
  unix2dos -k man.config                       //将unix转为dos格式
  dos2unix -k -n man.config man.config.linux   //将dos格式转为unix，并保存为新文件
```
