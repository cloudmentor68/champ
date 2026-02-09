## jenkins agent setup



### 1. jenkins-agent-setup

1. Launch an EC2 instance, named "Jenkins-master".

2. Connect it with terminal.

3. Install Java and Jenkins on the master instance. Refer this Installation Of Java and Jenkins.


```
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
java -version
```

```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins -y
```


4. Now login to Jenkins using <Your_Public_IP:8080> via browser.

5. You can find the Admin password

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

### 2. Launch another instance, named "Jenkins-agent"


Connect it with terminal and install Java on this terminal.

```
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
java -version
```


```
sudo apt install docker.io -y
```

```
sudo usermod -aG docker $USER
```

```
sudo reboot
```

```
sudo chmod 666 /var/run/docker.sock
```


### 3. Now Go to Your Jenkins and click on "Manage Jenkins"


Click on "Security"

Under Security, Go to "Agents" and in TCP port, Select "Random" and save the configuration.

Now, In "Manage Jenkins", Go to "Nodes".

Click on "New Node".

Now give the name of your node(agentnode) and select "Permanent Agent".

Remote root directory = /home/ubuntu/jenkins

usages = as much as possible

You can see, we have our node and it is offline as of now, Click on your agent, you will see the below page.

Run from agent command line: (Unix) :- On Jenkins-agent instance just paste the commands

```
curl -sO http://3.110.193.96:8080/jnlpJars/agent.jar
java -jar agent.jar -url http://3.110.193.96:8080/ -secret 18b28f502c243429443b12e2b1f8340794465f48a2210759a5d894392835e7fb -name agentnode -webSocket -workDir "/home/ubuntu/jenkins"
```



--- CONNECTED ---


### 4. Creating Jobs on Jenkins with Node Configuration


Create a new Jenkins freestyle project named "nodeapp-todo"

GitHub URL :- YOUR GITHUB URL

Under "General Settings" > Select "Restrict where this project can be run" > Select the "Node".

In the Build Steps section > Select Add Build Steps > Select Execute Shell > And type the commands required for your activity. Click on Save.

```
docker build -t app .
docker run -d --name todoapp -p 8000:8000 app:latest
```


Click on “Build Now” and monitor the output.

Verify that the application is running correctly on the agent server.




----------------------------------------


**note**

facing issues then, re-use "Run from agent command line: (Unix) :- On Jenkins-agent instance just paste the commands"
