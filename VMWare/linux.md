#  命令累积

## 1. 开启/关闭图形化界面

```
1.关闭图形化界面  systemctl set-default multi-user.target
2.开启图形化界面  systemctl set-default graphical.target
```

##  2. 查看文件和目录

```
查看当前所在的路径：pwd
命令格式：命令 -选项 -参数（目录）
查看当前路径下的文件：ls
-d：只看当前目录的信息
-l：看详细信息
-a：显示所有 任何一个文件前面加上“.”，表示隐藏文件
-h：显示文件大小
```

```
IPADDR="192.168.111.189"
NETMASK="255.255.255.0"
GATEWAY=192.168.111.254"
DNS1="192.168.9.35"
DNS2="192.168.9.72"
```


##  2.  NetworkManager 

```
开启 NetworkManager 

cat <<EOF >/etc/NetworkManager/nm-system-settings.conf
[main]
plugins=ifupdown,keyfile
[ifupdown]
managed=true
EOF
systemctl start NetworkManager 
systemctl enable NetworkManager

关闭 NetworkManager 
systemctl stop NetworkManager 
systemctl disable NetworkManager 
rm -rf /var/lib/NetworkManager/NetworkManager.state /etc/NetworkManager/nm-system-settings.conf
reboot

```

```
1、查看networkmanager 状态
systemctl status NetworkManager      是actice状态

2、然后关掉networkmanager
systemctl stop NetworkManager

3、在禁用
systemctl disable NetworkManager

4、然后重新启动网卡
systemctl start network.service

```


```
/etc/NetworkManager/nm-system-settings.conf 是NetworkManager的配置文件
/etc/NetworkManager/nm-system-settings.conf 是NetworkManager的状态文件
```


##  3.  ifcfg-ens33配置文件解读

```
TYPE=Ethernet                                   # 网卡类型：为以太网
PROXY_METHOD=none                               # 代理方式：关闭状态
BROWSER_ONLY=no                                 # 只是浏览器：否
BOOTPROTO=dhcp                                  # 网卡的引导协议：DHCP[中文名称: 动态主机配置协议]
DEFROUTE=yes                                    # 默认路由：是, 不明白的可以百度关键词 `默认路由` 
IPV4_FAILURE_FATAL=no                           # 是不开启IPV4致命错误检测：否
IPV6INIT=yes                                    # IPV6是否自动初始化: 是[不会有任何影响, 现在还没用到IPV6]
IPV6_AUTOCONF=yes                               # IPV6是否自动配置：是[不会有任何影响, 现在还没用到IPV6]
IPV6_DEFROUTE=yes                               # IPV6是否可以为默认路由：是[不会有任何影响, 现在还没用到IPV6]
IPV6_FAILURE_FATAL=no                           # 是不开启IPV6致命错误检测：否
IPV6_ADDR_GEN_MODE=stable-privacy               # IPV6地址生成模型：stable-privacy [这只一种生成IPV6的策略]
NAME=ens33                                      # 网卡物理设备名称
UUID=f47bde51-fa78-4f79-b68f-d5dd90cfc698       # 通用唯一识别码, 每一个网卡都会有, 不能重复, 否两台linux只有一台网卡可用
DEVICE=ens33                                    # 网卡设备名称, 必须和 `NAME` 值一样
ONBOOT=no                                       # 是否开机启动， 要想网卡开机就启动或通过 `systemctl restart network`控制网卡,必须设置为 `yes` 

```

##  4.  network

```
重启网卡
systemctl restart network

service network restart

```

## 5. ifconfig 

```
inet 192.168.111.189                局域网IP地址
netmask 255.255.255.0               子网掩码
broadcast 192.168.111.255           广播地址

```
## 6. 允许网卡访问外网主机（修改dns）----这里eno1 要提换成你要设置的那块网卡
 
```
显示当前网络连接
nmcli connection show                       

修改当前网络连接对应的DNS服务器，这里的网络连接可以用名称或者UUID来标识
nmcli con mod ens33 ipv4.dns "114.114.114.114 8.8.8.8"


将dns配置生效
nmcli con up eno1
```


## 7. 防火墙：

```
#查看默认防火墙状态（关闭后显示notrunning，开启后显示running）
firewall-cmd --state

#停止firewall
systemctl stop firewalld.service 或 systemctl stop firewalld

#禁止firewall开机启动
systemctl disable firewalld.service 或 systemctl disable firewalld


```

## 8. DNS 配置

```
vi /etc/resolv.conf 


```

## 8. linux上用route添加/删除路由

```
1. 查看
route -n

 2. 添加
route add -net 9.123.0.0 netmask 255.255.0.0 gw 9.123.0.1

 3. 删除
route del -net 9.123.0.0 netmask 255.255.0.0 gw 9.123.0.1

有些童鞋问怎么加永久路由，很简单，把 “route add -net 9.123.0.0 netmask 255.255.0.0 gw 9.123.0.1” 写到/etc/rc.local最后就行了，

或者复制编辑好执行也可以：
echo “route add -net 9.123.0.0 netmask 255.255.0.0 gw 9.123.0.1” >> /etc/rc.local

实际中发现，CentOS7.4默认环境下，rc.local中不会执行，需要赋权才可以
chmod +x /etc/rc.local
```

## 9. 关机 重启
 
```
Linux centos重启命令：
　　1、reboot   普通重启
　　2、shutdown -r now 立刻重启(root用户使用)
　　3、shutdown -r 10 过10分钟自动重启(root用户使用)
　　4、shutdown -r 20:35 在时间为20:35时候重启(root用户使用)
　　如果是通过shutdown命令设置重启的话，可以用shutdown -c命令取消重启
Linux centos关机命令：
　　1、halt 立刻关机
　　2、poweroff 立刻关机
　　3、shutdown -h now 立刻关机(root用户使用)
　　4、shutdown -h 10 10分钟后自动关机
　　如果是通过shutdown命令设置关机的话，可以用shutdown -c命令取消重启

```