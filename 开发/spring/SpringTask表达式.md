# SpringTask之Cron表达式



Cron Expressions

Cron表达式是一个字符串，字符串以5或6个空格隔开，分为6或7个域，每一个域代表一个含义，Cron有如下两种语法格式： 

1、Seconds Minutes Hours DayofMonth Month DayofWeek Year

2、Seconds Minutes Hours DayofMonth Month DayofWeek

例  "0 0 12 ? * WED" 在每星期三下午12:00 执行,

个别子表达式可以包含范围, 例如，在前面的例子里("WED")可以替换成 "MON-FRI", "MON, WED, FRI"甚至"MON-WED,SAT".

每一个字段都有一套可以指定有效值，如

Seconds (秒)         ：可以用数字0－59 表示，

Minutes(分)          ：可以用数字0－59 表示，

Hours(时)             ：可以用数字0-23表示,

Day-of-Month(天) ：可以用数字1-31 中的任一一个值，但要注意一些特别的月份

Month(月)            ：可以用0-11 或用字符串  “JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV and DEC” 表示

Day-of-Week(每周)：可以用数字1-7表示（1 ＝ 星期日）或用字符口串“SUN, MON, TUE, WED, THU, FRI and SAT”表示

●星号(*)：可用在所有字段中，表示对应时间域的每一个时刻，例如，*在分钟字段时，表示“每分钟”；

●问号（?）：该字符只在日期和星期字段中使用，虽然我现在不知道它的值是多少，但是它的值是唯一的，通过日期可以推出星期，通过本周是周几也可以推出日期。

●减号(-)：表达一个范围，如在小时字段中使用“10-12”，则表示从10到12点，即10,11,12；

●逗号(,)：表达一个列表值，如在星期字段中使用“MON,WED,FRI”，则表示星期一，星期三和星期五；

●斜杠(/)：x/y表达一个等步长序列，x为起始值，y为增量步长值。如在分钟字段中使用0/15，则表示为0,15,30和45秒，而5/15在分钟字段中表示5,20,35,50，你也可以使用*/y，它等同于0/y；

●L：该字符只在日期和星期字段中使用，代表“Last”的意思，但它在两个字段中意思不同。L在日期字段中，表示这个月份的最后一天，如一月的31号，非闰年二月的28号；如果L用在星期中，则表示星期六，等同于7。但是，如果L出现在星期字段里，而且在前面有一个数值 X，则表示“这个月的最后X天”，例如，6L表示该月的最后星期五；

●W：该字符只能出现在日期字段里，是对前导日期的修饰，表示离该日期最近的工作日。例如15W表示离该月15号最近的工作日，如果该月15号是星期六，则匹配14号星期五；如果15日是星期日，则匹配16号星期一；如果15号是星期二，那结果就是15号星期二。但必须注意关联的匹配日期不能够跨月，如你指定1W，如果1号是星期六，结果匹配的是3号星期一，而非上个月最后的那天。W字符串只能指定单一日期，而不能指定日期范围；

●LW组合：在日期字段可以组合使用LW，它的意思是当月的最后一个工作日；

●井号(#)：该字符只能在星期字段中使用，表示当月某个工作日。如6#3表示当月的第三个星期五(6表示星期五，#3表示当前的第三个)，而4#5表示当月的第五个星期三，假设当月没有第五个星期三，忽略不触发；

● C：该字符只在日期和星期字段中使用，代表“Calendar”的意思。它的意思是计划所关联的日期，如果日期没有被关联，则相当于日历中所有日期。例如5C在日期字段中就相当于日历5日以后的第一天。1C在星期字段中相当于星期日后的第一天。

1）Cron表达式的格式：秒 分 时 日 月 周 年(可选)。

               字段名                 允许的值                        允许的特殊字符  
               秒                         0-59                               , - * /  
               分                         0-59                               , - * /  
               小时                     0-23                               , - * /  
               日                         1-31                               , - * ? / L W C  
               月                         1-12 or JAN-DEC         , - * /  
               周几                     1-7 or SUN-SAT           , - * ? / L C #  
               年 (可选字段)     empty, 1970-2099      , - * / 

2）Cron表达式范例：

                 每隔5秒执行一次：*/5 * * * * ?

                 每隔1分钟执行一次：0 */1 * * * ?

                 每天23点执行一次：0 0 23 * * ?

                 每天凌晨1点执行一次：0 0 1 * * ?

                 每月1号凌晨1点执行一次：0 0 1 1 * ?

                 每月最后一天23点执行一次：0 0 23 L * ?

                 每周星期天凌晨1点实行一次：0 0 1 ? * L

                 在26分、29分、33分执行一次：0 26,29,33 * * * ?

                 每天的0点、13点、18点、21点都执行一次：0 0 0,13,18,21 * * ?


####更多参考例子

```
0 0 10,14,16 * * ? 每天上午10点，下午2点，4点 0 0/30 9-17 * * ? 朝九晚五工作时间内每半小时 0 0 12 ? * WED 表示每个星期三中午12点 "0 0 12 * * ?" 每天中午12点触发 "0 15 10 ? * *" 每天上午10:15触发 "0 15 10 * * ?" 每天上午10:15触发 "0 15 10 * * ? *" 每天上午10:15触发 "0 15 10 * * ? 2005" 2005年的每天上午10:15触发 "0 * 14 * * ?" 在每天下午2点到下午2:59期间的每1分钟触发 "0 0/5 14 * * ?" 在每天下午2点到下午2:55期间的每5分钟触发 "0 0/5 14,18 * * ?" 在每天下午2点到2:55期间和下午6点到6:55期间的每5分钟触发 "0 0-5 14 * * ?" 在每天下午2点到下午2:05期间的每1分钟触发 "0 10,44 14 ? 3 WED" 每年三月的星期三的下午2:10和2:44触发 "0 15 10 ? * MON-FRI" 周一至周五的上午10:15触发 "0 15 10 15 * ?" 每月15日上午10:15触发 "0 15 10 L * ?" 每月最后一日的上午10:15触发 "0 15 10 ? * 6L" 每月的最后一个星期五上午10:15触发 "0 15 10 ? * 6L 2002-2005" 2002年至2005年的每月的最后一个星期五上午10:15触发 "0 15 10 ? * 6#3" 每月的第三个星期五上午10:15触发
```


<!--
create time: 2018-01-14 18:25:49
Author: Alfred

This file is created by Marboo<http://marboo.io> template file $MARBOO_HOME/.media/starts/default.md
本文件由 Marboo<http://marboo.io> 模板文件 $MARBOO_HOME/.media/starts/default.md 创建
-->

