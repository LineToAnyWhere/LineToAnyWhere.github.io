# date #
> # 命令描述 #

用于显示Linux的系统时间。
> # 常用参数 #

* **[+FORMAT]**  
  格式化输出日期，常用的格式化有：%Y、%m、%d、%H、%M、%S，分别代表年月日，时分秒。

> # 应用示例 #

```
  date +%Y/%m/%d
  date +%H:%M
  date "+%Y-%m-%d %H:%M:%S"
//AIX取昨天数据需要更改时区，不支持-d参数
  delname=`TZ=aaa24 date +%Y%m%d`
//昨天：
  date -d '-1 day' +'%Y%m%d'
  date -d "1 days ago" +%Y%m%d
  date --date='yesterday' '+%Y%m%d'
//前天
  date -d '-2 day' +'%Y%m%d'
  date -d "2 days ago" +%Y%m%d
//大前天
  date -d '-3 day' +'%Y%m%d'
  date -d "3 days ago" +%Y%m%d
//明天
  date -d '+1 day' +'%Y%m%d'
  date -d "1 days next" +%Y%m%d
  date --date='tomorrow' '+%Y%m%d'
```
