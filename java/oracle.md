# oracle

Oracle中默认的用户名bai和密码如下表格：
用户名 / 密码 登录身份 说明
sys/change_on_install SYSDBA 或 SYSOPER 不能以 NORMAL 登录，可作为默认的系统管理员
system/manager SYSDBA 或 NORMAL 不能以 SYSOPER 登录，可作为默认的系统管理员
sysman/oem_temp sysman 为 oms 的用户名
scott/tiger NORMAL 普通用户
aqadm /aqadm SYSDBA 或 NORMAL 高级队列管理员
Dbsnmp/dbsnmp SYSDBA 或 NORMAL 复制管理员sysman 为 oms 的用户名
scott/tiger NORMAL 普通用户
aqadm /aqadm SYSDBA 或 NORMAL 高级队列管理员
Dbsnmp/dbsnmp SYSDBA 或 NORMAL 复制管理员





创建用户

 create user java identified by java; 

并给用户赋予权限 

grant connect,resource,dba to java;

