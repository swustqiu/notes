一.先下载解压redis，然后进入utils目录
这里写图片描述

二.打开文件redis_init_script
这里写图片描述

三.根据实际环境重新写路径，注意最后的两行蓝色注释要加上。
PIDFILE先去/var/run看看有没有redis开头的pid文件，没有的话先去redis-3.2.5/src下执行 ./redis-server ../redis.conf 手动启动redis，然后pid结尾的文件就会生成。

# chkconfig:2345 90 10
# description: Redis service
REDISPORT=6379
EXEC=/opt/kdm/redis/src/redis-server
CLIEXEC=/opt/kdm/redis/src/redis-cli

PIDFILE=/var/run/redis_6379.pid
CONF="/opt/kdm/redis/redis.conf"


修改redis.conf

################################ GENERAL  #####################################

# By default Redis does not run as a daemon. Use 'yes' if you need it.
# Note that Redis will write a pid file in /var/run/redis.pid when daemonized.
daemonize yes

# When running daemonized, Redis writes a pid file in /var/run/redis.pid by
# default. You can specify a custom pid file location here.
pidfile /var/run/redis_6379.pid

# Accept connections on the specified port, default is 6379.
# If port 0 is specified Redis will not listen on a TCP socket.
port 6379

chmod +x /etc/init.d/redis 修改读写权限



加入开机自启服务
chkconfig –add redis

开启服务自启动
chkconfig redis on


service redis start
service redis stop
