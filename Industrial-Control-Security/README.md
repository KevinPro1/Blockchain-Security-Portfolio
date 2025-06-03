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
```mermaid
graph TD
    A[VPN异常登录] --> B[日志分析]
    B --> C{时间戳关联}
    C --> D[定位泄露账户]
    D --> E[密钥重置]
    E --> F[系统恢复]
