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
