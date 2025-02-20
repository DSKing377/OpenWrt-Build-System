# 默认配置

- IP: `192.168.8.8`
- 用户名: `root`
- 密码: `无`
- 插件:
```
accesscontrol-plus
adguardhome
openappfilter
argon-config
arpbind
autoreboot
ddns
ddns-go
diskman
dockerman
hd-idle
homeproxy
netdata
Openclash
PassWall
poweroff
ramfree
smartdns
usb-printer
vlmcsd
应用中心(iStore)
```

---
# 使用说明

## Fork 本项目  ==>  Actions  ==>  选择项目  ==>  Run Workflow
[![LEDE_x86_64](https://github.com/DSKing377/OpenWrt-Build-System/actions/workflows/LEDE_x86_64.yml/badge.svg)](https://github.com/DSKing377/OpenWrt-Build-System/actions/workflows/LEDE_x86_64.yml)
[![iStoreOS_x86_64_22.03](https://github.com/DSKing377/OpenWrt-Build-System/actions/workflows/istoreos_x86_64_22.03.yml/badge.svg)](https://github.com/DSKing377/OpenWrt-Build-System/actions/workflows/istoreos_x86_64_22.03.yml)
[![immortalwrt_x86_64_23.05](https://github.com/DSKing377/OpenWrt-Build-System/actions/workflows/immortalwrt_x86_64.yml/badge.svg)](https://github.com/DSKing377/OpenWrt-Build-System/actions/workflows/immortalwrt_x86_64.yml)
  
   
---

## [![Manually with SSH](https://github.com/DSKing377/OpenWrt-Build-System/actions/workflows/Manually%20with%20SSH.yml/badge.svg?branch=master&event=workflow_dispatch)](https://github.com/DSKing377/OpenWrt-Build-System/actions/workflows/Manually%20with%20SSH.yml)
#####  可用于修改编译内容或手动编译
  
   

---
# 使用SSH连接Action

#### SSH连接命令

在工作流的Setup ssh for debug步骤中会显示
```
============frpc启动成功!===========
==========以下是SSH连接命令==========
ssh root@xxx -p xxxx
```
密码为SSH_PW定义的密码,不设置则为123
   
---
#### 自定义选项(可选)
```
点击仓库的Settings  ==> Actions secrets and variables ==> Actions ==> New repository secret ==> 填写Secret 信息
```
|Name |Value说明|
|----------|--------------------------------------------------|
|SSH_PW|   用于定义ssh访问的root密码,不设置默认123|
| FRPC_CONFIG|  用于定义frpc的配置文件,不设置将自动尝试使用公共frp服务器并生成SSH连接命令|
| IYUU_TOKEN| 爱语飞飞Token,用于通知编译结果,前往[官网](https://iyuu.cn/)申请|
| SERVERCHAN_SCKEY| Server酱SendKey,用于通知编译结果,前往[官网](https://sct.ftqq.com/)申请|
###### 爱语飞飞,Server酱二选一即可
  

---
#### FRPC_CONFIG示例
##### frp.freefrp.net是个公共服务器,所以可能会与他人配置冲突,默认会随机生成端口并尝试连接
```
[common]
server_addr = frp.freefrp.net  
server_port = 7000
token = freefrp.net

[ssh2action]     
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 22222   
```
##### `备选公共服务器frp1.freefrp.net;frp2.freefrp.net;www.freefrps.com`
##### 若使用公共服务器只需要修改frpc.ini.example中  [common]  部分的内容
   
---

# 添加新项目
   

#### 配置文件说明
| 目录         |         作用        |文件名格式                   |
| ------------| --------------------| --------------------|
| config      | 放置.config配置文件   |   项目名称_编译目标.config              |
| customize   | 放置自定义脚本及文件    |   项目名称_编译目标.sh             |
| feeds       | 放置feeds源           |    项目名称_编译目标            |
| patches     | 放置补丁文件           |                |
   
---   
#### 环境变量说明
|变量 |说明|
|----------|--------------------------------------------------|
|BD_PROJECT|   项目名称|
|  BD_TARGET|  编译目标|
| REPO_URL| 项目地址|
| REPO_BRANCH|  项目分支|
| TARGET_PLATFORM|  平台架构(amd64/arm64)|
| SSH_DEBUG| 是否开启SSH功能(true/false)|
| SSH_TIME|    设置开始编译前暂停时间,可用gogogo命令提前继续工作流|
|SSH_TIME2|   设置编译报错后暂停时间,可用gogogo命令提前继续工作流|
| CACHE_CCACHE  |    是否开启ccache缓存功能,不开启则只缓存工具链(true/false)|
| CACHE_CLEAN  |    是否清除缓存(true/false)|
| UPLOAD_ARTIFACT|   是否上传到ARTIFACT(true/false)|
| UPLOAD_RELEASE|    是否上传到RELEASE(true/false)|
