JAVA_Calendar_类获取指定年月的第一天日期和最后一天的日期

icecoola_ 2020-12-23 16:27:50   534   收藏 1
分类专栏： JAVA 文章标签： Calendar 获取第一天 最后一天 当前月 当前年 java
版权
JAVA_Calendar日历,日期,时间取值判断是否在某段时间内

获取某年的第一天

public static Date getYearFirstDay(int year, int month) {
//获取Calendar类的实例
Calendar c = Calendar.getInstance();
c.clear();
c.set(Calendar.YEAR, year);
return c.getTime();
}
}
1
2
3
4
5
6
7
8
获取某年的最后一天

public static Date getYearLastDay(int year, int month) {
//获取Calendar类的实例
Calendar c = Calendar.getInstance();
c.clear();
c.set(Calendar.YEAR, year);
c.set(Calendar.DAY_OF_Year, -1);
return c.getTime();
}
}
1
2
3
4
5
6
7
8
9
获取某月第一天

public static Date getMonthFirstDay(int year, int month) {
//获取Calendar类的实例
Calendar c = Calendar.getInstance();
//设置年份
c.set(Calendar.YEAR, year);
//设置月份，因为月份从0开始，所以用month - 1
c.set(Calendar.MONTH, month - 1);
//获取当前时间下，该月的最小日期的数字
int firstDay = c.getActualMinimum(Calendar.DAY_OF_MONTH);
//将获取的最小日期数设置为Calendar实例的日期数
c.set(Calendar.DAY_OF_MONTH, firstDay);
//获取当前月第一天c.set(Calendar.DAY_OF_MONTH, lastDay);
return c.getTime();
}
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
获取某月最后一天

public static Date getMonthLastDay(int year, int month) {
//获取Calendar类的实例
Calendar c = Calendar.getInstance();
//设置年份
c.set(Calendar.YEAR, year);
//设置月份，因为月份从0开始，所以用month - 1
c.set(Calendar.MONTH, month - 1);
//获取当前时间下，该月的最大日期的数字
int lastDay = c.getActualMaximum(Calendar.DAY_OF_MONTH);
//将获取的最大日期数设置为Calendar实例的日期数
c.set(Calendar.DAY_OF_MONTH, lastDay);
//获取当前月第一天c.set(Calendar.DAY_OF_MONTH, lastDay);
return c.getTime();
}
}
————————————————
版权声明：本文为CSDN博主「icecoola_」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/icecoola_/article/details/111592881