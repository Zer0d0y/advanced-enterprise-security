##### 所有服务器

## Cleanup Rules First!
##--------------------
/sbin/iptables  -P INPUT ACCEPT
/sbin/iptables  -P FORWARD ACCEPT
/sbin/iptables  -P OUTPUT ACCEPT
/sbin/iptables  -F
/sbin/iptables  -X
/sbin/iptables  -t nat -F
/sbin/iptables  -t nat -X
/sbin/iptables  -t mangle -F
/sbin/iptables  -t mangle -X
##--------------------

## Create Filter Rules
##---------------------

# 接受本机连接
/sbin/iptables  -A INPUT -i lo -j ACCEPT
/sbin/iptables  -A OUTPUT -o lo -j ACCEPT

# 连接跟踪（位置很重要）
/sbin/iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# 内网IP段 & SSH
/sbin/iptables  -A INPUT -s 192.168.2.0/24 -j ACCEPT
#/sbin/iptables -A INPUT -s 192.168.2.0/24 -p tcp -m tcp --dport 10022 -j ACCEPT

# SSH 白名单
/sbin/iptables  -A INPUT -s 123.123.151.0/24 -p tcp -m tcp --dport 10022 -j ACCEPT
/sbin/iptables  -A INPUT -s 123.123.142.0/24 -p tcp -m tcp --dport 10022 -j ACCEPT
/sbin/iptables  -A INPUT -s 123.123.189.0/24 -p tcp -m tcp --dport 10022 -j ACCEPT
/sbin/iptables  -A INPUT -s 123.123.181.0/24 -p tcp -m tcp --dport 10022 -j ACCEPT
/sbin/iptables  -A INPUT -s 123.123.182.0/24 -p tcp -m tcp --dport 10022 -j ACCEPT
/sbin/iptables  -A INPUT -p tcp -m tcp --dport 10022 -j DROP

#### Allow ICMP/Ping
iptables -A INPUT -p icmp --icmp-type 8 -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT

## Default Policies 默认策略DROP
##--------------------
/sbin/iptables  -P INPUT DROP
##--------------------


