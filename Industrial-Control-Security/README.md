# Zapp公共电力公司网络架构图

![image](https://github.com/KevinPro1/Blockchain-Security-Portfolio/blob/main/Picture2.png)

在此次演练中，我们是“玩家一”，并已被提供 VPN 凭证。


# 🔌 工业控制系统安全应急响应响应变电站VPN凭证填充攻击导致的断电事件  

## 技术架构

A[攻击者] --> B(VPN接入点)
B --> C{防火墙 pfSense}
C --> D[HMI系统]
D --> E[物理开关]

## 技术流程
A[VPN异常登录] --> B[日志分析]
B --> C{时间戳关联}
C --> D[定位泄露账户]
D --> E[密钥重置]
E --> F[系统恢复]


首先我开始分析日志以识别被攻破的账户，先打开网页浏览器，进入防火墙管理界面（通过 pfSense 网站），
输入以下凭证：“用户名：playerone，密码：password123”，并在“Status > System Logs > System > General”路径下找到系统日志，
为了进一步识别可疑活动，我前往“Status > Monitoring”页面，发现停电时间为5月12日19:55。

![image](https://github.com/KevinPro1/Blockchain-Security-Portfolio/blob/main/status%20monitoring%20interface.png)


之后我发现了预共享密钥以及疑似用户名的信息，
![image](https://github.com/KevinPro1/Blockchain-Security-Portfolio/blob/main/preshared%20keys%E5%85%B1%E4%BA%AB%E5%AF%86%E9%92%A5.png)

随后导航至防火墙日志，并筛选出目标为已知 HMI 系统（IP 地址为 192.168.30.16）的连接记录，
我识别出一个可疑的内部 IP 地址：192.168.31.171

![image](https://github.com/KevinPro1/Blockchain-Security-Portfolio/blob/main/Firewall-Log-Entries.png)


在确认系统宕机时间附近的 IPSec 日志中，我注意到一条日志显示，其中一个预共享密钥列表中的用户名被分配到了相同的 IP 地址。
我由此判断该账户已被攻破。
![image](https://github.com/KevinPro1/Blockchain-Security-Portfolio/blob/main/Ipsec%20Logs.png)







