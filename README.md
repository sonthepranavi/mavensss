maven java
---
1️⃣ Check Maven Version
Steps

Press Windows + R

Type: cmd
.
Click OK

Type:

mvn -version


Press Enter

If you get 'mvn' not recognized → Maven not installed or PATH not added.

2️⃣ Create Maven Java Project (Using Eclipse)
Steps

Open Eclipse IDE

On top menu → click File

Click New

Click Project…

Expand Maven

Click Maven Project

Click Next

Check Create a simple project (skip archetype selection)

Click Next

Fill details:

Field	Value
Group Id	maven_java
Artifact Id	java_maven
Version	0.0.1-SNAPSHOT
Packaging	jar

Click Finish

3️⃣ Maven Java Project Structure (as shown in PDF)

In Project Explorer, you will see:

src/main/java  
src/test/java  
pom.xml  


No action needed — Eclipse creates it automatically.

4️⃣ Run the Java Program (Output in PDF)
Steps

Right-click src/main/java

Click New → Class

Enter:

Name: Demo     click:finish

Paste sample code:

public class Demo {
    public static void main(String[] args) {
        System.out.println("Maven Java Project");
    }
}        save with ctrl+s


Right-click on the file → Run As → Java Application     ---->>>MAVEN_JAVA

Click New Repository (green button or “+” → “New repository”)   

 Click Create Repository   Open your project folder in Terminal / PowerShell      
 git init                                                                                                      
 git add .
 git commit -m "Initial Maven project commit"                                                                                  
 git remote add origin https://github.com/Navya-0408/my-maven-java-project.git     
 git branch -M main
git push -u origin main
 DONE

 ----------------
 maven webb
 MAVEN WEB PROJECT — RUN LOCALLY WITHOUT JENKINS

Below steps work for any Maven Web Application (.war project).

⭐ Step 1: Check Maven Installation

Open CMD:

mvn -version


If Maven is installed, it shows version.
If not → install Maven + set MAVEN_HOME.

⭐ Step 2: Go to Your Maven Web Project Folder

Example:

cd C:\Projects\MavenWeb


Make sure this folder contains:

✔ pom.xml
✔ src/main/java
✔ src/main/webapp (JSP, HTML, etc.)

⭐ Step 3: Clean & Build the Project

Run:

mvn clean install


This will:

✔ Clean target folder
✔ Compile
✔ Test
✔ Package .war file

After success, you will get:

target/yourprojectname.war

⭐ Step 4: Download & Install Apache Tomcat

Go to Tomcat website

Download Apache Tomcat 9 (Windows ZIP)

Extract to:

C:\tomcat9

⭐ Step 5: Deploy the WAR to Tomcat
Method 1 — Copy WAR file

Copy your .war to:

C:\tomcat9\webapps\


Example:

copy target\mavenweb.war C:\tomcat9\webapps\


Tomcat will auto-extract it into a folder.

⭐ Step 6: Start Tomcat Server

Go to Tomcat bin folder:

cd C:\tomcat9\bin
startup.bat


If server starts correctly → it shows Tomcat started.

⭐ Step 7: Open App in Browser

Browser → enter:

http://localhost:8080/mavenweb


(Use your project name after 8080.)

Your JSP/HTML homepage will open.

⭐ Step 8: Stop Tomcat
shutdown.bat

🎯 OPTIONAL: If you want to run without


 ---------------------------------------
 jenkin pipelines steps
 ======Jenkins Pipeline Steps======
+New Item -> enter item name "pipeline-Navya"
under that-> click pipeline  -> ok
paste this code
pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning java-hello-world-with-maven repo'
                git branch: 'master', url: 'https://github.com/jabedhasan21/java-hello-world-with-maven.git'
            }
        }

        stage('Clean') {
            steps {
                echo 'Running mvn clean'
                bat "mvn clean"
            }
        }

        stage('Compile') {
            steps {
                echo 'Running mvn compile'
                bat "mvn compile"
            }
        }

        stage('Test') {
            steps {
                echo 'Running mvn test'
                bat "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo 'Running mvn package'
                bat "mvn package"
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving JAR output'
                archiveArtifacts artifacts: "target/*.jar", fingerprint: true
            }
        }
    }

    post {
        success {
            echo '🎉 BUILD SUCCESS — JAR created and archived ✔'
        }
        failure {
            echo '❌ BUILD FAILED'
        }
    }
}    
click  Apply then save
click Build Now
click on green right symbol then click on pipeline overview  
DONE
AWS
# ✅ **Exercise 1: Deploy index.html on EC2 using Docker (Clean, Correct Steps)**

### **Step 1: Login to AWS Academy**

* Open course email → click **Start**
* Choose **Student Login** → enter credentials
* Go to **Modules** → select **Launch AWS Academy Lab**
* Click **Start Lab** → wait until icon turns **green**
* Click **AWS** to open the console

---

### **Step 2: Create EC2 Instance**

#### **Stage 1 — Name**

* Name: **ubuntu**

#### **Stage 2 — Select AMI**

* Select: **Ubuntu Server (Free-tier eligible)**

#### **Stage 3 — Architecture**

* Choose: **64-bit (x86)**

#### **Stage 4 — Instance Type**

* Select: **t2.micro**

#### **Stage 5 — Create Key Pair**

* Click **Create new key pair**
* Name it: e.g., **awskey**
* Download `.pem` file
* Save in a folder (e.g., **AWS/**)

#### **Stage 6 — Network Settings**

Enable:

* **SSH (22)**
* **HTTP (80)**
* **HTTPS (443)**
  Security group will be created.

#### **Stage 7 — Storage**

* Default: **8 GB**

#### **Stage 8 — Launch Instance**

* Click **Launch Instance**
* Wait until:

  * **Instance state = Running**
  * **Status checks = 2/2 passed**

---

## **Step 3: Connect Using SSH**

* Select instance → click **Connect**
* Go to **SSH client** tab
* Copy SSH command:

Example:

```
ssh -i "awskey.pem" ubuntu@ec2-xx-xx-xx-xx.compute-1.amazonaws.com
```

On your system:

```
cd <path-to-pem-file>
```

Example:

```
cd D:\AWS
```

Run the SSH command to access EC2.

---

## **Step 4: Install Required Software on EC2**

Run:

```
sudo apt update
sudo apt-get install docker.io -y
sudo apt install git -y
sudo apt install nano -y
```

---
/**
## **Step 5: Create & Upload index.html (Local System)**

1. Create a folder **Example**
2. Add `index.html`
3. Open Git Bash inside folder:

```
git init
git add .
git commit -m "first commit"
```
4. Create GitHub repo → copy HTTPS URL
5. Push the code:

```
git branch -M main
git remote add origin <github-url>
git push -u origin main
```

---
**/
## **Step 6: Clone Repo on EC2**

```url:https://github.com/sonthepranavi/website-project.git
git clone <github-repo-url>
cd <folder>
ls
```

---

## **Step 7: Create Dockerfile**

```
nano Dockerfile
```

Paste:

```
FROM nginx
COPY . /usr/share/nginx/html
```

Save:
**Ctrl + O → Enter → Ctrl + X**

---

## **Step 8: Build Docker Image**

```
sudo docker build -t mywebapp .
```

---

## **Step 9: Run Docker Container**

```
sudo docker run -d -p 80:80 mywebapp
```

---

## **Step 10: Test Deployment**

* Go to EC2 → select instance
* Copy **Public IPv4 address**
* Paste in browser:

```
http://<public-ip>
```
//
Your **index.html** should open.

---

## **Step 11: Stop & Cleanup**

Stop container:

```
sudo docker ps
sudo docker stop <container-id>
```

Terminate instance:

* EC2 → Instances
* Select instance
* **Instance state → Terminate**

Finally → **End Lab**

# awscomm

