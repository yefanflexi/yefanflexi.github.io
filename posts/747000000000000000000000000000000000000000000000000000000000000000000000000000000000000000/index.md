# Docker安装oracle19c


&lt;!--more--&gt;
* docker 安装 oracle19c
 
docker pull registry.cn-hangzhou.aliyuncs.com/zhuyijun/oracle:19c
 
安装 Oracle
```bash
 &gt; docker run -d -it --name orcl19c_03 -p 1521:1521 -p 5500:5500 -e ORACLE_SID=orcl -e ORACLE_PDB=orclPDB1 -e ORACLE_PWD=123456 -e ORACLE_EDITION=standard -e ORACLE_CHARACTERSET=AL32UTF8 -v /data/oracle/oracleData:/opt/myData/oracle/oracleData registry.cn-hangzhou.aliyuncs.com/zhuyijun/oracle:19c   
```
上面执行的命令中，备注：  
ORACLE_SID=orcl 是服务名，安装后连接Oracle 时用的服务名，CDB数据库的  
ORACLE_PWD=123456 是安装后 dba 用户的密码，即：123456  
ORACLE_PDB=orclPDB1 是安装后的PDB数据库，想更明白一点，可以往下看6.3.1创建用户的两种方式，一个是在CDB库下，一个是下PDB库下
         
```bash
docker run -d -it --name orcl19c_03 -p 1521:1521 -p 5500:5500 -e ORACLE_SID=orcl -e ORACLE_PDB=orclPDB1 -e ORACLE_PWD=123456 -e ORACLE_EDITION=standard -e ORACLE_CHARACTERSET=AL32UTF8 -v /data/oracle/oracleData:/opt/myData/oracle/oracleData registry.cn-hangzhou.aliyuncs.com/zhuyijun/oracle:19c
 ```
docker启动oracle数据库
       
### Docker 常用命令
 
#### 1. Docker 基础命令  
- **查看 Docker 版本：**  
```bash  
docker --version  
```
 
- **启动 Docker 服务：**  
```bash  
sudo systemctl start docker  
```
 
- **停止 Docker 服务：**  
```bash  
sudo systemctl stop docker  
```
 
- **查看 Docker 服务状态：**  
```bash  
sudo systemctl status docker  
```
 
- **启动 Docker 容器：**  
```bash  
docker start &lt;容器ID或名称&gt;  
```
 
- **停止 Docker 容器：**  
```bash  
docker stop &lt;容器ID或名称&gt;  
```
 
- **删除 Docker 容器：**  
```bash  
docker rm &lt;容器ID或名称&gt;  
```
 
- **删除 Docker 镜像：**  
```bash  
docker rmi &lt;镜像ID或名称&gt;  
```
 
- **列出所有正在运行的容器：**  
```bash  
docker ps  
```
 
- **列出所有容器（包括停止的）：**  
```bash  
docker ps -a  
```
 
- **列出所有镜像：**  
```bash  
docker images  
```
 
#### 2. Docker 镜像操作命令  
- **拉取镜像：**  
```bash  
docker pull &lt;镜像名称&gt;:&lt;标签&gt;  
```
 
- **构建镜像：**  
```bash  
docker build -t &lt;镜像名称&gt;:&lt;标签&gt; .  
```
 
- **查看镜像详情：**  
```bash  
docker inspect &lt;镜像ID或名称&gt;  
```
 
#### 3. Docker 容器操作命令  
- **运行容器：**  
```bash  
docker run -d --name &lt;容器名称&gt; &lt;镜像名称&gt;  
```
 
- **进入正在运行的容器：**  
```bash  
docker exec -it &lt;容器ID或名称&gt; /bin/bash  
```
 
- **导出容器为一个文件：**  
```bash  
docker export &lt;容器ID&gt; &gt; &lt;文件名&gt;.tar  
```
 
- **从文件中导入容器：**  
```bash  
docker import &lt;文件名&gt;.tar  
```
 
#### 4. Docker 网络操作命令  
- **列出所有网络：**  
```bash  
docker network ls  
```
 
- **创建自定义网络：**  
```bash  
docker network create &lt;网络名称&gt;  
```
 
- **将容器连接到网络：**  
```bash  
docker network connect &lt;网络名称&gt; &lt;容器名称&gt;  
```
 
### Docker 安装步骤
 
#### 1. 安装前准备  
- 更新系统包：  
```bash  
sudo apt-get update  
```
 
#### 2. 安装 Docker  
##### 对于 Ubuntu 系统：
 
1. **安装依赖：**  
```bash  
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common  
```
 
2. **添加 Docker 的 GPG 密钥：**  
```bash  
curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) | sudo apt-key add -  
```
 
3. **添加 Docker 的仓库：**  
```bash  
sudo add-apt-repository &#34;deb [arch=amd64] [https://download.docker.com/linux/ubuntu](https://download.docker.com/linux/ubuntu) $(lsb_release -cs) stable&#34;  
```
 
4. **更新软件包并安装 Docker：**  
```bash  
sudo apt-get update  
sudo apt-get install docker-ce  
```
 
5. **验证 Docker 安装：**  
```bash  
sudo docker --version  
```
 
#### 3. 启动 Docker 并设置开机自启动  
- **启动 Docker：**  
```bash  
sudo systemctl start docker  
```
 
- **设置 Docker 开机自启动：**  
```bash  
sudo systemctl enable docker  
```
 
#### 4. 运行 Docker 测试  
- 运行一个简单的 Docker 容器来测试安装：  
```bash  
sudo docker run hello-world  
```
 
这将下载并运行一个测试容器，确保 Docker 安装正确。

 ==配置 docker 镜像加速==
 
编辑 daemon.json ：vim /etc/docker/daemon.json
 
添加下面的内容：
 
{  
&#34;registry-mirrors&#34;: [  
&#34;[https://mirror.ccs.tencentyun.com](https://mirror.ccs.tencentyun.com)&#34;  
]  
}
 
重载所有修改过的配置文件
 
systemctl daemon-reload
 
重启服务
 
systemctl restart docker


---

> 作者:   
> URL: http://localhost:1313/posts/747000000000000000000000000000000000000000000000000000000000000000000000000000000000000000/  

