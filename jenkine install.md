
## Install Jenkins on Ubuntu 22.04

### Install Java
Jenkins is a Java-based application, so you need to install Java Development Kit (JDK). OpenJDK is a widely used option. Open terminal and run below commands to install OpenJDK 17.

	sudo apt update
	sudo apt install fontconfig openjdk-17-jre -y

![Install-OpenJDK-Jenkins-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Install-OpenJDK-Jenkins-Ubuntu-22-04.png)

Verify the Java version by running:

	java -version

![Check-Java-Version-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Check-Java-Version-Ubuntu-22-04.png)

### Add Jenkins Repository
Jenkins is not available in the default package repositories of Ubuntu 22.04. So we will be adding its official apt repository. Execute the following commands.

	sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
	  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

	echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
	  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
	  /etc/apt/sources.list.d/jenkins.list > /dev/null

![Add-Jenkins-Apt-Repository-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Add-Jenkins-Apt-Repository-Ubuntu-22-04.png)

### Install Jenkins on Ubuntu 22.04
Now, install Jenkins using the following apt commands.
	
	sudo apt update
	sudo apt install jenkins -y

![Install-Jenkins-on-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Install-Jenkins-on-Ubuntu-22-04.png)

### Start and Enable Jenkins Service
Whenever we install Jenkins using apt command then its service started automatically, to verify Jenkins service status, run following command.

	sudo systemctl enable jenkins

### Change Security group

Go to security group attach on your instance and set inbound rule to **type: All traffic** and **CIDR: 0.0.0.0/0**.

### Access Jenkins Setup Wizard
Jenkins runs on port 8080 by default. Open your web browser and navigate to the following URL: http://instance-public-IP-Address:8080

![Jenkins-Web-Interface-First-Page-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Jenkins-Web-Interface-First-Page-Ubuntu-22-04.png)

Retrieve the Jenkins unlock key by executing the following command.

	sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Copy this password and paste it on “Administrator password” field as show below:

![Jenkins-Initial-Admin-Password-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Jenkins-Initial-Admin-Password-Ubuntu-22-04.png)

Click on  Continue

Once unlocked, select “Install suggested plugins” to ensure a smooth Jenkins experience.

![Install-Suggested-Jenkins-Plugins-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Install-Suggested-Jenkins-Plugins-Ubuntu-22-04.png)

![Installing-Suggested-Pulgins-Installation-Progress-Jenkins](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Installing-Suggested-Pulgins-Installation-Progress-Jenkins.png)

Next, create your admin user and its credentials for Jenkins.

![Creating-Admin-User-Jenkins-Web-Interface-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Creating-Admin-User-Jenkins-Web-Interface-Ubuntu-22-04.png)

Click on “Save and Continue”

In the next window, specify the Jenkins URL; usually, it’s the same as your initial access URL.

![Jenkins-URL-Instance-Configuration-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Jenkins-URL-Instance-Configuration-Ubuntu-22-04.png)

Click on “Save and Finish”.

![Jenkins-Ready-for-Use-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Jenkins-Ready-for-Use-Ubuntu-22-04.png)

Click on “Start using Jenkins” and this will take us to Jenkins dashboard.

![Jenkins-Dashboard-Post-Installation-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Jenkins-Dashboard-Post-Installation-Ubuntu-22-04.png)

Great, above dashboard confirms that you have successfully installed Jenkins on Ubuntu 22.04.

### Test Jenkins Installation with FreeStyle project
In order to test our Jenkins installation, let’s create demo job. Follow the instructions as shown in below image.

	#!/bin/bash

	echo "This is Jenkins Demo"

![Jenkins-Demo-Job-Ubuntu-22-04](https://www.linuxbuzz.com/wp-content/uploads/2023/11/Jenkins-Demo-Job-Ubuntu-22-04.gif)

Refrence: [linuxbuzz.com](https://www.linuxbuzz.com/how-to-install-jenkins-on-ubuntu/)
