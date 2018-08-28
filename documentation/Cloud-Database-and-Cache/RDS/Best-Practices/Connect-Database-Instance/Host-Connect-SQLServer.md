# 云主机相关设置
由于云数据库SQL Server是创建在VPC中，因此在没有专线连接的情况下，需要**将应用或客户端所在的云主机跟数据库实例部署在同一VPC中使用**。由于云主机在创建时，必须关联安全组，因此我们需要对云主机的安全组进行合理的设置：
1. 如果用户没有任何安全组创建的话，那么默认的安全组是开放全部端口，这这种情况下，云主机可以访问数据库，但存在安全风险，建议新建专用安全组，具体配置见后。
2. 如果用户选择了其他的安全组，那么该安全组必须配置为：**出站规则允许1433端口**

设置的具体方法如下：
1. 创建安全组可以参见下面的链接：https://www.jdcloud.com/help/detail/1486/isCateLog/1
2. 在需要访问SQL Server的云主机的安全组中，增加一个“出站规则”，在类型中选择【MSSQL】**（注意不是MYSQL）**，策略为【接受】
![通过云主机连接1](../../../image/RDS/Instance-Connection-SQLServer-1.png)

