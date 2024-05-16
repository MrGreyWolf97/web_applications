## What is [Tomcat](https://tomcat.apache.org/)


The Apache Tomcat® software is an open source implementation of the following  [Jakarta EE platform](https://projects.eclipse.org/projects/ee4j.jakartaee-platform) specifications:
- [Jakarta Servlet](https://projects.eclipse.org/projects/ee4j.servlet)
- [Jakarta Server Pages (JSP)](https://projects.eclipse.org/projects/ee4j.jsp)
- [Jakarta Expression Language](https://projects.eclipse.org/projects/ee4j.el)
- [Jakarta WebSocket](https://projects.eclipse.org/projects/ee4j.websocket)
- [Jakarta Annotations](https://projects.eclipse.org/projects/ee4j.ca)
- [Jakarta Authentication](https://projects.eclipse.org/projects/ee4j.authentication) 


---
### Set-up

> [!success]
> ## [Complete guide - Tomcat on Linux](https://www.digitalocean.com/community/tutorials/install-tomcat-on-linux)
> - [Community Server Connectors](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-community-server-connector) \[CSC\] for Visual  Studio Code
> - [Starting a Tomcat vith CSC](https://stackoverflow.com/questions/74388409/how-to-start-a-tomcat-8-5-server-on-vsc-using-community-server-connector-extensi)
> - [CSC Commands](https://github.com/redhat-developer/vscode-rsp-ui#available-commands)

---
### Install Java

```
sudo apt install default-jdk
```

```
java -version
```

---
### Set tomcat User

- [Guide: `useradd`](https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/)
- [Guide: `bin/true - bin/false`](https://www.baeldung.com/linux/bin-true-bin-false-commands)

It is not advisable to run Tomcat under a root account. Hence we need to create a new user where we run the Tomcat server on our system. We will use the following command to create our new user.
> The `'useradd'` command in Linux is used to create a new user. You can use it with the syntax, `sudo useradd [option] newuser`.

```
sudo useradd -r -m -U -d /opt/tomcat -s /bin/false tomcat
```

| Command | Definition                                                                           |
| ------- | ------------------------------------------------------------------------------------ |
| `-r`    | Creates a system account                                                             |
| `-m`    | Tells the ‘useradd’ command to create the user’s home directory if it does not exist |
| `-U`    | Create a group with the same name as the user                                        |
| `-d`    | Specifies the home directory.                                                        |
| `-s`    | login shell of the new account                                                       |

> [!warning] Delete User/Group
> If you fucked up and you have to delete the user, remember to:
> 1. `sudo vim /etc/passwd`
>    It's the list of users in the system. **Remove tomcat**
>2. `sudo rm -r /opt/tomcat`
>3. `sudo groupdel tomcat
> 
> ##### Change Tomcat user password
> Shouldn't be necessary, maybe even breaks something.
> `sudo passwd tomcat`
> Set it to **tomcat**, it's easier.

> [!tip]
> Linux groups are organization units that are used to organize and administer user accounts in Linux. The primary purpose of groups is to define a set of privileges, such as reading, writing, or executing permission for a given resource that can be shared among the users within the group.
> 
> ---
> 
> When creating a new user, the default behavior of the `useradd` command is to create a group with the same name as the username and the same GID as the UID.

---
### Download/Install Tomcat
##### Download
```
wget -c https://downloads.apache.org/tomcat/tomcat-9/v9.0.88/bin/apache-tomcat-9.0.34.tar.gz
```

Onestly did not work and I don't know why. You can download the latest stable release from the [Official Website](https://downloads.apache.org/tomcat/), choose the version and download the .tar

##### Extract
```
sudo tar xf apache-tomcat-9.0.88.tar.gz -C /opt/tomcat
```

##### Create Symbolic Link
To make updating Tomcat easy, we create a symbolic link that will point to the installation directory of Tomcat.
Now, if you wish to install Tomcat on Linux with a newer version in future, simply unpack the new archive and change the symbolic link so that it points to the new version.
```
sudo ln -s /opt/tomcat/apache-tomcat-9.0.34 /opt/tomcat/updated
```

##### Provide Tomcat user access to /opt/tomcat/
we need to provide the user Tomcat with access for the Tomcat installation directory. We would use the [chown command](https://www.digitalocean.com/community/tutorials/linux-chown-command-examples) to change the directory ownership.
```
sudo chown -R tomcat: /opt/tomcat
```

---
### Configure Tomcat Service
Once you install Tomcat on Linux, you need to configure it before you can start using it.
First, we need to create a _systemd_ unit file to be able to run Tomcat as a service.
We need to create a new unit file for this.
We will open a new file named _tomcat.service_ in the directory _/etc/systemd/system_ using nano or your preferred editor.
```
sudo nano /etc/systemd/system/tomcat.service
```

Now enter the following in your file and save it. Note that you need to update the value of _JAVA_HOME_ if your Java installation directory is not the same as given below.
```
[Unit]
Description=Apache Tomcat Web Application Container
After=network.target

[Service]
Type=forking

Environment="JAVA_HOME=/usr/lib/jvm/jre-21-openjdk-21.0.3.0.9-1.fc40.x86_64"
Environment="CATALINA_PID=/opt/tomcat/updated/temp/tomcat.pid"
Environment="CATALINA_HOME=/opt/tomcat/updated/"
Environment="CATALINA_BASE=/opt/tomcat/updated/"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
Environment="JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom"

ExecStart=/opt/tomcat/updated/bin/startup.sh
ExecStop=/opt/tomcat/updated/bin/shutdown.sh

User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
```

> [!tip]
> #### [How to find Java Path](https://www.scaler.com/topics/how-to-find-java-path-in-linux/)
> #### [How to change Read-Only access](https://www.pluralsight.com/blog/it-ops/linux-file-permissions)
> #### [How to add group permissions to a folder](https://serverfault.com/questions/136826/add-group-rwx-permissions-to-a-folder)


Now we reload the daemon to update the system about the new file.
```
sudo systemctl daemon-reload
```

We use the following command to start the Tomcat service on our system.
```
sudo systemctl start tomcat
```

We use the following command to check over the Tomcat status
```
sudo systemctl status tomcat
```


---
##### ***References***
- 