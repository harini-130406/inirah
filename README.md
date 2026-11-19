Jenkins

Execution shell command common:
echo "Compiling Java Program..."
mkdir -p build
         javac -d build src/main/java/org/example/Main.java
         echo "Executing Java Program..."
          echo -e "INPUT" | java -cp build org.example.Main


1           Develop a Java application to calculate and display the gross salary of an employee based on the basic salary, House Rent Allowance (HRA), and Dearness Allowance (DA) provided as input, using the formula Gross Salary = Basic Salary + HRA + DA. Install and configure Jenkins on a cloud virtual machine, configure Java, and create a Jenkins job to compile and execute the application.
Experiment 1 – Gross Salary Calculation using Java & Jenkins
Step 1: Start Jenkins on Linux
Open the Linux terminal:
sudo systemctl start jenkins
Check whether Jenkins is running:
sudo systemctl status jenkins
If it shows active (running), Jenkins is ready.
Open Jenkins in your browser:
http://localhost:8080
If Jenkins requires the initial password:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Step 2: Create Java Project in IntelliJ IDEA
Open IntelliJ IDEA.
Click New Project.
Select Java.
Project name: GrossSalary
Select JDK 17.
Click Create.
Project structure:
GrossSalary
└── src
    └── Main.java
Step 3: Write Java Program
Create Main.java inside the src folder.
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter Basic Salary: ");
        double basic = sc.nextDouble();

        System.out.print("Enter HRA: ");
        double hra = sc.nextDouble();

        System.out.print("Enter DA: ");
        double da = sc.nextDouble();

        double grossSalary = basic + hra + da;

        System.out.println("Gross Salary: " + grossSalary);

        sc.close();
    }
}
Step 4: Run in IntelliJ IDEA
Open Main.java.
Click the green ▶ Run button beside main().
Enter the values in the Run console.
Example:
Enter Basic Salary: 25000
Enter HRA: 5000
Enter DA: 3000
Gross Salary: 33000.0
Step 5: Upload the Project to GitHub
Create a GitHub repository called GrossSalary.
Open the IntelliJ terminal:
git init
git add .
git commit -m "Gross salary Java application"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/GrossSalary.git
git push -u origin main
Replace YOUR_USERNAME with your GitHub username.
Step 6: Create Jenkins Job
Open Jenkins at http://localhost:8080.
Click New Item.
Enter the job name GrossSalaryJob.
Select Freestyle project.
Click OK.
Step 7: Configure GitHub Source Code
Under Source Code Management:
Select Git.
Repository URL:
https://github.com/YOUR_USERNAME/GrossSalary.git
3. Branch:
*/main
Step 8: Configure Build Step
Under Build Steps:
Click Add build step.
Select Execute shell.
Enter:
mkdir -p build
javac -d build src/main/java/org/example/Main.java
echo "25000
5000
3000" | java -cp build org.example.Main

4. Click Save.
Step 9: Build the Jenkins Job
Open GrossSalaryJob.
Click Build Now.
Wait for the build to complete.
Click the build number.
Open Console Output.

CI
1           Develop a Java application to calculate the factorial of a non-negative integer using a loop. Create a Jenkins CI pipeline with stages for checking out the source code from GitHub, compiling the program, and executing it.
Experiment 13: Factorial Calculation Using Java and Jenkins CI Pipeline
Step 1: Create a Java Project in IntelliJ IDEA
Open IntelliJ IDEA.
Click New Project.
Select Java.
Enter project name: factorial.
Select JDK 17.
Select Build System: IntelliJ.
Click Create.
Your project structure will be:
factorial/
├── .idea/
├── src/
│   └── Main.java
├── .gitignore
└── factorial.iml
Important: We will use this exact structure. Do not create a package or additional main/java directories.
Step 2: Write the Java Program
Open src/Main.java and replace its contents with:
Main.java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter a non-negative integer: ");
        int num = sc.nextInt();

        if (num < 0) {
            System.out.println("Factorial is not defined for negative numbers.");
        } else {
            long factorial = 1;

            for (int i = 1; i <= num; i++) {
                factorial = factorial * i;
            }

            System.out.println("Factorial of " + num + " is " + factorial);
        }

        sc.close();
    }
}
Step 3: Execute the Java Program in IntelliJ
Open Main.java.
Click the green Run button beside main().
Enter the input:
5
Expected output:
Enter a non-negative integer: 5
Factorial of 5 is 120
Test additional inputs:
Input
Expected output
0
Factorial of 0 is 1
4
Factorial of 4 is 24
5
Factorial of 5 is 120
-3
Factorial is not defined for negative numbers.

Note: The long data type can store factorials up to 20! without overflow.
Step 4: Create a GitHub Repository
Open GitHub.
Log in to your account.
Click the + icon in the top-right corner.
Select New repository.
Enter repository name:
Factorial

Select Public.
Click Create repository.
Step 5: Push the Java Project to GitHub
Open the IntelliJ terminal.
Make sure you are in the project root directory:
C:\Users\SRIJAA\IdeaProjects\factorial
Execute the following commands one by one.
1. Initialize Git
git init
2. Add the Java source file
git add src/Main.java
3. Commit the source code
git commit -m "Factorial Java application"
4. Set the branch name
git branch -M main
5. Connect the GitHub repository
git remote add origin https://github.com/YOUR_USERNAME/Factorial.git
Replace YOUR_USERNAME with your GitHub username.
6. Push the source code
git push -u origin main
Open your GitHub repository and verify that src/Main.java is uploaded.
Step 6: Create the Jenkinsfile
Return to IntelliJ IDEA.
Right-click the project root folder factorial.
Select New → File.
Enter the filename:
Jenkinsfile
5. Paste the following pipeline code.
Jenkinsfile
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling Java Program'

                sh '''
                    mkdir -p build
                    javac -d build src/Main.java
                '''
            }
        }

        stage('Execute') {
            steps {
                echo 'Executing Factorial Program'

                sh '''
                    echo "5" | java -cp build Main
                '''
            }
        }
    }
}
Explanation of Jenkins stages
Stage
Description
Checkout
Fetches the source code from GitHub
Build
Compiles Main.java using the Java compiler
Execute
Executes the compiled Java program with input 5

Step 7: Push Jenkinsfile to GitHub
Open the IntelliJ terminal and execute:
git add Jenkinsfile

git commit -m "Add Jenkins CI pipeline"

git push origin main
Your final project structure will be:
factorial/
├── .idea/
├── src/
│   └── Main.java
├── Jenkinsfile
├── .gitignore
└── factorial.iml
Your GitHub repository should contain both Main.java and Jenkinsfile.
Step 8: Start Jenkins
Since Jenkins is installed in your Ubuntu environment, open the Ubuntu terminal.
Start Jenkins:
sudo systemctl start jenkins
Check Jenkins status:
sudo systemctl status jenkins
Open the browser:
http://localhost:8080
Log in to Jenkins.
Step 9: Create a Jenkins Pipeline Job
Open the Jenkins dashboard.
Click New Item.
Enter the job name:
FactorialPipeline

Select Pipeline.
Click OK.
Step 10: Configure GitHub Source Code Checkout
Scroll down to the Pipeline section.
Select and enter the following details:
Field
Configuration
Definition
Pipeline script from SCM
SCM
Git
Repository URL
https://github.com/YOUR_USERNAME/Factorial.git
Credentials
None (for public repository)
Branch Specifier
*/main
Script Path
Jenkinsfile

Click Save.
Automating CI/CD and GitOps with Jenkins | Red Hat Developer
Step 11: Execute the Jenkins Pipeline
Open the FactorialPipeline job.
Click Build Now.
Wait for the pipeline to complete.
Click the latest build number.
Select Console Output.
Expected output:
Checking out source code from GitHub

Compiling Java Program

Executing Factorial Program

Enter a non-negative integer: 5
Factorial of 5 is 120

Finished: SUCCESS
Step 12: Configure Automatic Build Trigger
To trigger a new build whenever the GitHub source code is updated:
Open the FactorialPipeline job.
Click Configure.
Find the Build Triggers section.
Select Poll SCM.
Enter the following schedule:
H/2 * * * *
6. Click Save.
Jenkins will check the GitHub repository approximately every two minutes and trigger a new build when it detects a change.
Step 13: Test Automatic Build Triggering
Open Main.java in IntelliJ.
Modify the output message slightly.
Save the file.
Open the IntelliJ terminal.
Push the updated source code:
git add .
git commit -m "Update factorial program"
git push origin main

Wait for Jenkins to detect the update.
Open the Jenkins dashboard.
Verify that a new build has started automatically.
Step 14: Verify Jenkins Pipeline Stages
The Jenkins Stage View should show three successful stages:
FactorialPipeline
Checkout
Success
Build
Success
Execute
Success
Important: Jenkins Environment
Your Java project is created on Windows, but Jenkins is running on Ubuntu/WSL.
Therefore:
Push your project from Windows IntelliJ to GitHub.
Jenkins checks out the project from GitHub into its own workspace.
Jenkins executes the sh commands on Ubuntu.
Ensure Java JDK is installed and java and javac are available to the Jenkins service.
If Jenkins reports javac: not found, configure the JDK in the Jenkins environment before running the pipeline.




1           Develop a Java application to determine whether a given integer reads the same forwards and backwards. Configure a Jenkins Continuous Integration (CI) pipeline to retrieve the source code from GitHub, compile the program, and execute it.

package org.example;
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter an integer: ");
        int num = sc.nextInt();
        int original = num;
        int reversed = 0;
        while (num > 0) {
            int digit = num % 10;
            reversed = reversed * 10 + digit;
            num = num / 10;
        }
        if (original == reversed) {
            System.out.println(original + " is a Palindrome");
        } else {
            System.out.println(original + " is not a Palindrome");
        }
        sc.close();
    }
}
 
1           Develop a Java application to determine whether a given integer is a prime number. Configure a Jenkins CI pipeline with source code checkout and build stages, and trigger a new build whenever the source code is updated in GitHub.

package org.example;

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        System.out.print("Enter an integer: ");
        int num = sc.nextInt();

        boolean isPrime = true;

        if (num <= 1) {
            isPrime = false;
        } else {
            for (int i = 2; i <= Math.sqrt(num); i++) {
                if (num % i == 0) {
                    isPrime = false;
                    break;
                }
            }
        }

        if (isPrime) {
            System.out.println(num + " is a Prime Number");
        } else {
            System.out.println(num + " is not a Prime Number");
        }

        sc.close();
    }
}


 
1           Develop a Java application to read five integers into an array and calculate their sum. Configure a Jenkins CD pipeline to build the application, generate the JAR file, deploy it to a separate deployment directory on the local machine, and execute the deployed application.
package org.example;
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
 Scanner sc = new Scanner(System.in);
        int[] arr = new int[5];
        int sum = 0;
        System.out.println("Enter five integers:");
        for (int i = 0; i < 5; i++) {
            arr[i] = sc.nextInt();
            sum += arr[i];
        }
        System.out.println("Sum of five integers = " + sum);
   	   sc.close();
    }
}







1           Develop a Java application to calculate simple interest using the principal amount, rate of interest, and time period provided as input. Create a Gradle Java project, configure the build.gradle file, and build the application to generate the required build artifacts.
Experiment: Simple Interest Calculation Using Java and Gradle
Aim
To develop a Java application to calculate Simple Interest using the principal amount, rate of interest, and time period provided as input. Create a Gradle Java project, configure the build.gradle file, compile the source code, and package the application into an executable JAR file.
Step 1: Install Gradle
Open the Ubuntu terminal (WSL) and execute:
sudo snap install gradle --classic
Verify Gradle installation:
gradle --version
Expected: Gradle version 8.14.6 or another installed version.
Step 2: Check Java Installation
Execute:
java -version

javac -version
Ensure Java JDK is installed. The instructions below use Java 21.
Step 3: Create a Project Directory
mkdir java_application
Navigate into the directory:
cd java_application
Step 4: Initialize the Gradle Project
Execute:
gradle init
Select the following options when prompted:
Gradle prompt
Selection
Project type
1 – Application
Implementation language
1 – Java
Target Java version
17
Project name
java_application
Application structure
1 – Single application project
Build script DSL
2 – Groovy
Test framework
1 – JUnit 4
Generate build using new APIs
No

Note: Select Groovy so that the project generates build.gradle instead of build.gradle.kts.
Step 5: Install Tree Utility
Install the tree command to view the project structure:
sudo apt install tree -y
Display the project structure:
tree -L 4
Your generated project will have this structure:
java_application/
├── app/
│   ├── build.gradle
│   └── src/
│       ├── main/
│       │   └── java/
│       │       └── org/
│       │           └── example/
│       │               └── App.java
│       └── test/
├── gradle/
├── gradlew
├── gradlew.bat
├── gradle.properties
└── settings.gradle
Important: Since you selected Single application project, the Java source and build configuration are inside the app directory. The root directory does not need a build.gradle file.
Step 6: Run the Default Gradle Application
Make sure you are in the project root:
cd ~/java_application
Execute:
./gradlew run
The default application should display:
Hello World!
Step 7: Navigate to the Java Source Directory
Navigate to:
cd ~/java_application/app/src/main/java/org/example
List the files:
ls
You should see:
App.java
Open the file:
nano App.java
Step 8: Write the Simple Interest Java Program
Replace the existing code with:
App.java
package org.example;

import java.util.Scanner;

public class App {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter Principal Amount: ");
        double principal = sc.nextDouble();

        System.out.print("Enter Rate of Interest: ");
        double rate = sc.nextDouble();

        System.out.print("Enter Time (in years): ");
        double time = sc.nextDouble();

        double simpleInterest = (principal * rate * time) / 100;

        System.out.println("Simple Interest = " + simpleInterest);

        sc.close();
    }
}
Save the file:
Press Ctrl + O.
Press Enter.
Press Ctrl + X.
Step 9: Configure the app/build.gradle File
Navigate to the application directory:
cd ~/java_application/app
Open the Gradle configuration:
nano build.gradle
Replace its contents with:
app/build.gradle
plugins {
    id 'application'
}

repositories {
    mavenCentral()
}

application {
    mainClass = 'org.example.App'
}

tasks.named('run') {
    standardInput = System.in
}

tasks.jar {
    manifest {
        attributes(
            'Main-Class': 'org.example.App'
        )
    }
}
Save the file.
Important configurations:
application specifies the main Java class.
standardInput = System.in enables Scanner input when running through Gradle.
Main-Class specifies the entry point in the JAR manifest, allowing the JAR to execute using java -jar.
Step 10: Return to the Project Root
cd ~/java_application
Always execute the following Gradle Wrapper commands from this root directory.
Step 11: Run the Simple Interest Application
Execute:
./gradlew run
Enter the following values:
Sample Input
Enter Principal Amount: 10000
Enter Rate of Interest: 5
Enter Time (in years): 2
Expected Output
Simple Interest = 1000.0
If the program accepts input and displays the correct result, the application is working.
Step 12: Build the Gradle Project
Execute:
./gradlew clean build
This command:
Removes previous build files.
Compiles the Java source code.
Compiles and executes the tests.
Generates the build artifacts.
Expected output:
BUILD SUCCESSFUL
Step 13: Generate the Executable JAR File
Execute:
./gradlew :app:jar
Expected output:
BUILD SUCCESSFUL
Step 14: Verify the Generated JAR
Navigate to the generated JAR directory:
ls app/build/libs/
Expected output:
app.jar
The complete JAR path is:
app/build/libs/app.jar
Step 15: Verify the JAR Manifest
This step ensures that the JAR contains the main class configuration.
Execute:
unzip -p app/build/libs/app.jar META-INF/MANIFEST.MF
Expected output:
Manifest-Version: 1.0
Main-Class: org.example.App
If Main-Class is missing, check the tasks.jar configuration in app/build.gradle and rebuild.
Step 16: Execute the Generated JAR
Execute:
java -jar app/build/libs/app.jar
Enter:
10000
5
2
Expected output:
Enter Principal Amount: 10000
Enter Rate of Interest: 5
Enter Time (in years): 2
Simple Interest = 1000.0
JAR execution successful
Step 17: Verify the Complete Project Structure
Return to the project root:
cd ~/java_application
Execute:
tree -L 6
Expected important structure:
java_application/
├── app/
│   ├── build/
│   │   ├── classes/
│   │   ├── generated/
│   │   ├── libs/
│   │   │   └── app.jar
│   │   └── tmp/
│   ├── build.gradle
│   └── src/
│       ├── main/
│       │   └── java/
│       │       └── org/
│       │           └── example/
│       │               └── App.java
│       └── test/
├── gradle/
├── gradlew
├── gradlew.bat
├── gradle.properties
└── settings.gradle
Important Commands for the Practical
Operation
Command
Check Gradle version
gradle --version
Initialize project
gradle init
Run application
./gradlew run
Build project
./gradlew clean build
Generate JAR
./gradlew :app:jar
View build files
tree app/build
List JAR files
ls app/build/libs/
Check manifest
unzip -p app/build/libs/app.jar META-INF/MANIFEST.MF
Execute JAR
java -jar app/build/libs/app.jar

 
1           Develop a Java application to read an English alphabet character and determine whether it is a vowel or a consonant. Create a Gradle Java project, configure the build script, and compile and package the application into a JAR file.

package org.example;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter an English alphabet character: ");
        char ch = sc.next().charAt(0);

     
            ch = Character.toLowerCase(ch);

            if (ch == 'a' || ch == 'e' || ch == 'i' ||
                ch == 'o' || ch == 'u') {
                System.out.println(ch + " is a Vowel");
            } else {
                System.out.println(ch + " is a Consonant");
            }
        

        sc.close();
    }
}






Installation of ansible

Experiment: Installation and Configuration of Ansible on Ubuntu Linux
Step 1: Open Ubuntu Terminal
Open your Ubuntu terminal (WSL).
Update the package repository:
sudo apt update
Step 2: Install Software Properties Common
Execute:
sudo apt install software-properties-common -y
Step 3: Add Ansible PPA
Add the official Ansible repository:
sudo add-apt-repository --yes --update ppa:ansible/ansible
Step 4: Install Ansible
Execute:
sudo apt install ansible -y
Wait until the installation is completed.
Step 5: Verify Ansible Installation
Check the installed Ansible version:
ansible --version
Expected output (version may differ):
ansible [core 2.x.x]
  config file = None
  python version = 3.x.x
Step 6: Check Ansible Galaxy
Verify that Ansible Galaxy is installed:
ansible-galaxy --version
Step 7: Check Ansible Configuration
Display the default Ansible configuration:
ansible-config list
Step 8: Test Ansible Connectivity with Localhost
Execute:
ansible localhost -m ping -c local
Expected output:
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
Step 9: Check Python Installation
Ansible requires Python.
Verify Python:
python3 --version
Step 10: Verify Locale Configuration
Check the locale:
locale
Ansible requires UTF-8 encoding.
If the locale is not UTF-8, execute:
sudo apt install locales -y
sudo locale-gen en_US.UTF-8
sudo update-locale LANG=en_US.UTF-8
Close and reopen the terminal, then verify:
locale
Important Commands
Operation
Command
Update packages
sudo apt update
Install Ansible repository support
sudo apt install software-properties-common -y
Add Ansible PPA
sudo add-apt-repository --yes --update ppa:ansible/ansible
Install Ansible
sudo apt install ansible -y
Check Ansible version
ansible --version
Check Galaxy version
ansible-galaxy --version
Test localhost
ansible localhost -m ping -c local
Check Python
python3 --version

Note: Ansible does not require starting a service. Once installed, it can be used directly from the terminal.







