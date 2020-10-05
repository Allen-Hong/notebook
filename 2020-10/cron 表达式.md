cron 表达式

unix 系统内置指令

用法： 分	时	日	月	星

*每一

，并列

-连续

/整除

```shell
* * * * * echo >> `date` $HOME/date.txt #每分钟输出当前日期到当前用户home目录的date.text文件
```



