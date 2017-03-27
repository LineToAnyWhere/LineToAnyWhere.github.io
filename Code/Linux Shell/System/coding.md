# 编码转换 #
> # 命令描述 #

将文档格式转换为不同编码
> # 常用参数 #

* **iconv**  
  --list ：列出 iconv 支持的语系数据  
  -f ：from ，原来的编码格式  
  -t ：to ，要转换的编码格式  
  -o file ：如果要保留原本的档案，那么使用 -o 新档名，可以建立新编码档案  

> # 应用示例 #

```
  iconv -f big5 -t utf8 vi.big5 -o vi.utf8    //将vi.big5从big5转为utf8，并生成新文件vi.utf8
```
