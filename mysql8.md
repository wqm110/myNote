 GRANT ALL PRIVILEGES ON *.* TO 'spider'@'%'  WITH GRANT OPTION;

 	路由表设置
	>
	 # Firewall configuration written by system-config-firewall
	# Manual customization of this file is not recommended.
	*filter
	:INPUT ACCEPT [0:0]
	:FORWARD ACCEPT [0:0]
	:OUTPUT ACCEPT [0:0]
	-A INPUT -p tcp -m tcp --dport 10100:10180 -j ACCEPT
	-A INPUT -p tcp -m tcp --dport 21 -j ACCEPT
	-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
	-A INPUT -p tcp -m tcp --dport 3306 -j ACCEPT
	-A INPUT -p tcp -m tcp --dport 3306 -j ACCEPT
	-A INPUT -j REJECT –reject-with icmp-host-prohibited
	-A FORWARD -j REJECT –reject-with icmp-host-prohibited
	COMMIT
 防火前设置
```SHELL
	firewall-cmd --add-port=80/tcp --permanent #永久添加80端口例外(全局)
	firewall-cmd --remove-port=80/tcp --permanent #永久删除80端口例外(全局)
	firewall-cmd --add-port=65001-65010/tcp --permanent #永久增加65001-65010例外(全局)
	firewall-cmd --zone=public --add-port=80/tcp --permanent #永久添加80端口例外(区域public)
	firewall-cmd --zone=public --remove-port=80/tcp --permanent #永久删除80端口例外(区域public)
	firewall-cmd --zone=public --add-port=65001-65010/tcp --permanent #永久增加65001-65010例外(区域public)
	firewall-cmd --zone=public --add-port=3306/tcp --permanent #永久增加mysql例外(区域public)
	firewall-cmd  --add-port=3306/tcp --permanent #永久增加mysql例外(区域 全局)

	firewall-cmd --reload #重启防火墙(修改配置后要重启防火墙)
```

show variables like "%case%";
用ROOT登录，修改/etc/my.cnf
在[mysqld]下加入一行：lower_case_table_names=1


set global time_zone='+8:00';
