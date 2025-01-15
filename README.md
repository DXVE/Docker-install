# [1、安装 Docker （基于Ubuntu 24.04.1 LTS）](https://www.docker.com/)

## 安装必要的依赖包

	sudo apt install apt-transport-https ca-certificates curl software-properties-common

## 添加 Docker 的官方 GPG 密钥

	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

## 添加 Docker 仓库

	echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
</br>

	sudo apt update

## 安装 Docker

	sudo apt install docker-ce

## 启动并启用 Docker 服务

	sudo systemctl start docker
</br>

	sudo systemctl enable docker

# [2、配置镜像源](https://hub.docker.com/)

	sudo nano /etc/docker/daemon.json
添加以下内容 </br>
 
	{
    	"registry-mirrors": [
        	"https://hub.docker.com/",
        	"https://registry.docker-cn.com/"
    		]
	}

 # 3、[配置守护进程的网络代理](https://docs.docker.com/engine/daemon/proxy/#daemon-configuration)

 	sudo mkdir -p /etc/systemd/system/docker.service.d
</br>

  	sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf

   添加以下内容
   
	[Service]
	Environment="HTTP_PROXY=http://127.0.0.1:7890"
	Environment="HTTPS_PROXY=http://127.0.0.1:7890"
</br>

> [!WARNING]
官方文档中 “HTTPS_PROXY” 的配置值为 Environment="HTTPS_PROXY=https://proxy.example.com:3129" ；</br></br>修改后测试在拉取镜像时会提示 EOF 错误 ；</br></br>把 “https://xxxx” 修改成 “http://xxxx” 即可成功代理

</br>

	sudo systemctl daemon-reload
 </br>
 
 	sudo systemctl restart docker
