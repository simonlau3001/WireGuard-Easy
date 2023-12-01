curl -sSL https://get.docker.com | sh
报错
[root@ip-172-31-29-153 ec2-user]# curl -sSL https://get.docker.com | sh
# Executing docker install script, commit: e5543d473431b782227f8908005543bb4389b8de

ERROR: Unsupported distribution 'amzn'

用中文
看起

為了解決這個問題，您可以嘗試以下替代方法在Amazon Linux上安裝Docker：

bash
Copy code

sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user

這種方法使用了amazon-linux-extras工具來在Amazon Linux上安裝Docker。安裝完畢後，啟動Docker服務，並將ec2-user添加到docker組中，以便您可以無需sudo運行Docker命令。

執行這些命令後，您可能需要退出並重新登錄以應用組更改。

請注意，這些信息基於我在2022年1月的最後一次訓練，具體情況可能已經發生變化。始終參考官方的Docker文檔或Amazon Linux文檔以獲取最新的指令。

报错+1

[root@ip-172-31-29-153 ec2-user]# sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user
sudo: amazon-linux-extras: command not found
Redirecting to /bin/systemctl start docker.service
Failed to start docker.service: Unit docker.service not found.
usermod: group 'docker' does not exist

看起來 amazon-linux-extras 命令未找到，而 Docker 服务也未能正常启动。这可能是由于 Amazon Linux 2 的特定配置或更新引起的问题。

在 Amazon Linux 2 上，您可以使用 yum 包管理器来安装 Docker。请尝试以下步骤：

bash
Copy code

sudo yum update -y
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user

这将先更新系统，然后使用 amazon-linux-extras 安装 Docker，接着启动 Docker 服务，并将 ec2-user 添加到 docker 组。最后，您可能需要退出并重新登录以应用组更改。

如果您还是遇到问题，请查看 Amazon Linux 文档或 Docker 官方文档，以确保您使用了最新的指令和适用于您系统的方法。

[root@ip-172-31-29-153 ec2-user]# sudo yum update -y
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user
Last metadata expiration check: 0:38:10 ago on Fri Dec  1 08:17:55 2023.
Dependencies resolved.
Nothing to do.
Complete!
sudo: amazon-linux-extras: command not found
Redirecting to /bin/systemctl start docker.service
Failed to start docker.service: Unit docker.service not found.
usermod: group 'docker' does not exist

报错

看起來 amazon-linux-extras 命令仍然未被找到，而 Docker 服务也未能正常启动。这可能是由于您使用的 Amazon Linux 版本或 AMI 配置的不同导致的。

在这种情况下，您可以尝试直接使用 yum 安装 Docker：

bash
Copy code

sudo yum install docker -y
sudo service docker start
sudo usermod -aG docker ec2-user

这将通过 yum 安装 Docker，启动 Docker 服务，并将 ec2-user 添加到 docker 组。最后，您可能需要退出并重新登录以应用组更改。

如果您仍然遇到问题，您可能需要检查您的系统配置，确保您使用的是与您 AMI 版本兼容的 Docker 安装方法。此外，您还可以查看 Amazon Linux 和 Docker 的官方文档以获取最新的指令和建议。

Installed:
  containerd-1.7.2-1.amzn2023.0.4.x86_64         docker-24.0.5-1.amzn2023.0.2.x86_64                        iptables-libs-1.8.8-3.amzn2023.0.2.x86_64         iptables-nft-1.8.8-3.amzn2023.0.2.x86_64        
  libcgroup-3.0-1.amzn2023.0.1.x86_64            libnetfilter_conntrack-1.0.8-2.amzn2023.0.2.x86_64         libnfnetlink-1.0.1-19.amzn2023.0.2.x86_64         libnftnl-1.2.2-2.amzn2023.0.2.x86_64            
  pigz-2.5-1.amzn2023.0.3.x86_64                 runc-1.1.7-1.amzn2023.0.3.x86_64                          

Complete!
Redirecting to /bin/systemctl start docker.service


看起来您已经成功地安装了 Docker 和相关的组件。接下来，您可以尝试运行 Docker 命令来验证安装是否正常。例如，您可以运行以下命令：

bash
Copy code
docker --version
docker info
这将显示 Docker 的版本信息以及有关 Docker 安装的其他详细信息。如果您成功看到输出，那么 Docker 已经安装并运行在您的 Amazon Linux 系统上了。

如果您需要使用 Docker 命令而无需使用 sudo，您可能需要注销并重新登录，以便应用 docker 组的更改：

bash
Copy code
sudo usermod -aG docker ec2-user
然后注销并重新登录。之后，您应该能够以非管理员用户身份运行 Docker 命令。

请随时告诉我如果您遇到任何其他问题，我将尽力帮助您。
