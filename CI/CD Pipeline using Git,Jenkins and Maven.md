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

![image](https://user-images.githubusercontent.com/76660222/205739011-7a355fd0-75e8-41d1-9217-61bbbd292dde.png)

![image](https://user-images.githubusercontent.com/76660222/205739131-cac2e093-739e-40d7-b7ae-c5748bbc6b87.png)

![image](https://user-images.githubusercontent.com/76660222/205739207-93e06c37-4068-4788-9e43-623d1c1c381d.png)


* Once our server is running, connect to your server via SSH by using your keypair.
* Next we need to install `Java`,`Jenkins`, `Maven` to our server.
* First switch to root user `sudo su -` and update the packages first `sudo yum update -y`

![image](https://user-images.githubusercontent.com/76660222/205739264-21dbbf8c-71fb-4c77-8190-8c1dbb667bf2.png)

![image](https://user-images.githubusercontent.com/76660222/205739529-68b9b50b-1810-4387-841c-28c906693f32.png)


```shell
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```

![image](https://user-images.githubusercontent.com/76660222/205739635-4bb01c6b-5383-46fa-b7db-bf0471d8b5cb.png)

* Then we need to install Java
``` sudo amazon-linux-extras install java-openjdk11 -y ```

![image](https://user-images.githubusercontent.com/76660222/205739944-3813c083-ef9f-404f-a75e-45645329098e.png)


* After installing Java, we can now install Jenkins and start our Jenkins server

```shell
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

![image](https://user-images.githubusercontent.com/76660222/205740398-41b976e3-bda0-4eee-8585-6d01640cec76.png)


* Connect to http://<your_server_public_DNS>:8080 from your browser. You can get `initialAdminPassword` for jenkins by running below command:

```shell
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![image](https://user-images.githubusercontent.com/76660222/205740845-ffb76faa-7f24-42c0-9080-5ca3542a8cab.png)

![image](https://user-images.githubusercontent.com/76660222/205741042-f7762eae-b02d-4bfe-8af4-8b8a95ef6c63.png)

![image](https://user-images.githubusercontent.com/76660222/205741117-8570ad49-0aeb-4e92-a274-0e0bbf9b6c02.png)

* We need to install git in our Jenkins server, run below command:

```shell
sudo yum install git
```
![image](https://user-images.githubusercontent.com/76660222/205741401-819d3d5a-e98b-41d2-92c0-79cc7c42b970.png)

* Now we can run our first Jenkins job. Go to `Dashboard` -> `New Item`

```shell
JobName: HelloWorldJob
Type: Free Style Project
Build Step: Execute shell
echo "Hello World!"
```

![image](https://user-images.githubusercontent.com/76660222/205746733-14d4c7b5-9dfb-4d4a-894c-b5487d6cb225.png)

![image](https://user-images.githubusercontent.com/76660222/205746903-de945925-b33c-4171-a993-c540a0a69e01.png)

![image](https://user-images.githubusercontent.com/76660222/205747226-9a4e8370-007c-444d-bf1d-787354fce8a3.png)


### Step2: Integrate Git with Jenkins

* We need to go to `Manage Jenkins` -> `Manage Plugins`. Here we will install `Github Integration` and `Maven Integration` plugins.
* Now we can run our Second job to check `Github integration` is working as expected. Create another FreeStyleJob as below:

```shell
SCM: Git
URL: https://github.com/rumeysakdogan/hello-world.git
Save -> Build Now
```

![image](https://user-images.githubusercontent.com/76660222/205747714-7f2416ea-479c-46ec-b35a-3e01e717d5ef.png)

![image](https://user-images.githubusercontent.com/76660222/205747914-b0d5fcf4-a00c-416f-a697-d5abedfeb7da.png)


