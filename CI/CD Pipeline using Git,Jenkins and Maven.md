## CI/CD Pipeline using Git,Jenkins and Maven

### Step1: Configure Jenkins Server

* First we need to launch an EC2 instance with Keypair

```shell
instanceType: t2.micro
AMI: Amazon Linux-2
Security Group: 
22, SSH
8080, Custom TCP
```

![1670268659503](image/readme/1670268659503.png)

![1670268808809](image/readme/1670268808809.png)

![1670268850416](image/readme/1670268850416.png)

* Once our server is running, connect to your server via SSH by using your keypair.
* Next we need to install `Java`,`Jenkins`, `Maven` to our server.
* First switch to root user `sudo su -` and update the packages first `sudo yum update -y`

![1670272758823](image/readme/1670272758823.png)


```shell
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```
