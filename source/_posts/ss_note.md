---
title: shadowsocks配置 
date: 2019-08-28 19:23:11
tags:
---

### 一键安装脚本
```bash
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

### 端口
```bash
开关端口权限
$ /sbin/iptables -I INPUT -p tcp --dport 8381 -j ACCEPT 
$ /sbin/iptables -I INPUT -p tcp --dport 8381 -j DROP   
查看是否生效
$ /sbin/iptables -L -n
```

### config.json
#### server
```json
{
    "server":"0.0.0.0",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
        "8381": "password1",
        "8384": "pd2",
        "8385": "pd3"
        },
    "timeout":300,
    "method":"rc4-md5",
    "fast_open":true
}
```
开启server
```bash
$ ssserver -c /etc/shadowsocks-python/config.json -d restart
```
#### client
```json

```
### shadowsocks开机自启动脚本
```
#/etc/init.d/sslocal
name=sslocal
BIN=/usr/local/bin/sslocal
conf=/etc/shadowsocks/config.json

start(){
    $BIN -c $conf -d start
    RETVAL=$?
    if [ "$RETVAL" = "0" ]; then
        echo "$name start success"
    else
        echo "$name start failed"
    fi
}

stop(){
    pid=`ps -ef | grep -v grep | grep -i "${BIN}" | awk '{print $2}'`
    if [[ ! -z $pid ]]; then
        $BIN -c $conf -d stop
        RETVAL=$?
        if [ "$RETVAL" = "0" ]; then
            echo "$name stop success"
        else
            echo "$name stop failed"
        fi
    else
        echo "$name is not running"
        RETVAL=1
    fi
}

status(){
    pid=`ps -ef | grep -v grep | grep -i "${BIN}" | awk '{print $2}'`
    if [[ -z $pid ]]; then
        echo "$name is not running"
        RETVAL=1
    else
        echo "$name is running with PID $pid"
        RETVAL=0
    fi
}

case "$1" in
'start')
    start
    ;;
'stop')
    stop
    ;;
'status')
    status
    ;;
'restart')
    stop
    start
    RETVAL=$?
    ;;
*)
    echo "Usage: $0 { start | stop | restart | status }"
    RETVAL=1
    ;;
esac
exit $RETVAL
```


