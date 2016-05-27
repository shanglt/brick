# Nginx定时切割日志
## 说明

以下两脚本定时移动nginx日志，重启nginx日志进程(通过向nginx发送USR1信号，重新生成nginx日志，不会影响nginx服务。日志会有极小部分损失，估计是移动日志或重启时日志文件锁住造成的丢失)，实现按天切割，按小时切割nginx日志。


### 一.按天自动切割nginx日志
##### vim /usr/local/sbin/nginx_log_day.sh，添加以下内容
	#!/bin/bash
	logs_path="/var/log/nginx/"
	mv ${logs_path}nginx_access.log ${logs_path}nginx_access_$(date -d "yesterday" +"%Y%m%d").log
	kill -USR1 `cat /usr/local/webserver/nginx/nginx.pid`

##### crontab -e，添加以下内容，指定每天0点执行日志切割脚本
	00 00 * * * /bin/bash  /usr/local/sbin/nginx_log_day.sh
	
	
### 二.按小时自动切割nginx日志
##### vim /usr/local/sbin/nginx_log_hour.sh，添加以下内容
	#!/bin/bash
	log_dir="/var/log/nginx/"
	date_dir=`date +%Y%m%d`
	#收下这句用于判断，当时间为凌晨00：00时，将date_dri设为昨天
	if [ "`date +%H`" = "00" ]; then
  		date_dir=`date -d "yesterday" +%Y%m%d`
	fi
	#将当前小时减一，因为记录的是之前的访问数据
	tag=`date +%Y%m%d%H --date="-1 hour"`
	/bin/mkdir -p ${log_dir}${date_dir}
	mv ${log_dir}wx_lxh_access.log ${log_dir}${date_dir}/wx_lxh_access_${tag}.log
	kill -USR1 `cat /usr/local/webserver/nginx/nginx.pid`


##### crontab -e，添加以下内容，指定每小时执行日志切割脚本
	00 */1 * * * /bin/bash  /usr/local/sbin/nginx_log_hour.sh
