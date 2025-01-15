# Docker-install

##安装必要的依赖包

	sudo apt install apt-transport-https ca-certificates curl software-properties-common

##添加 Docker 的官方 GPG 密钥

	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

##添加 Docker 仓库

	echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

	sudo apt update

##安装 Docker

	sudo apt install docker-ce

##启动并启用 Docker 服务

	sudo systemctl start docker

	sudo systemctl enable docker

#配置镜像源

	{
    	"registry-mirrors": [
        	"https://hub.docker.com/",
        	"https://registry.docker-cn.com/"
    		]
	}

 ##配置守护进程的网络代理[https://docs.docker.com/engine/daemon/proxy/#daemon-configuration](url)

 	sudo mkdir -p /etc/systemd/system/docker.service.d

  	nano /etc/systemd/system/docker.service.d/http-proxy.conf

   添加以下内容
   
	[Service]
	Environment="HTTP_PROXY=http://127.0.0.1:7890"
	Environment="HTTPS_PROXY=http://127.0.0.1:7890"
