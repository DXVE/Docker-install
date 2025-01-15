# Docker-install

安装必要的依赖包

	`sudo apt install apt-transport-https ca-certificates curl software-properties-common`

添加Docker 的官方 GPG 密钥

	```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg```

添加 Docker 仓库

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

安装 Docker

sudo apt install docker-ce

启动并启用 Docker 服务

sudo systemctl start docker

sudo systemctl enable docker
