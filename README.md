# TCV-406

This is the Experiment of cloud computing....

<br>
<h1>Download and Install Oracle VirtualBox
<h5>VirtualBox is a powerful x86 and AMD64/Intel64 virtualization tool that allows you to run multiple operating systems simultaneously.
<br>
<h1>1. Download VirtualBox
<h6>Visit the official Oracle VirtualBox website and download the latest version for your OS.
<br>
Configure Ubuntu in VirtualBox
After installing VirtualBox, you can set up Ubuntu as a virtual machine.

<h1>1. Download Ubuntu ISO
Download Ubuntu 22.04.5 from the official Ubuntu releases page:

<h5>File: ubuntu-22.04.5-desktop-amd64.iso
Release Date: 2024-09-11
Size: 4.4GB
<h1>2. Create a New Virtual Machine in VirtualBox
<h5>Open VirtualBox.
Click New and enter a name (e.g., UbuntuVM).
Select Linux as the type and Ubuntu (64-bit) as the version.
Allocate memory (at least 4GB recommended).
Create a virtual hard disk (minimum 20GB).
<h1>3. Load Ubuntu ISO and Install</h1>
<h5>Select your Ubuntu VM and click Settings > Storage.
<br>Add the downloaded Ubuntu ISO as a boot device.
<br>Start the VM and follow the Ubuntu installation steps.</h5>
<h1></h1>4. Install Essential Packages After Booting Ubuntu
<h5>sudo apt update && sudo apt upgrade -y
<br>
sudo apt install build-essential curl git -y</h5>
<h6>By following these steps, you'll have a fully functional virtual environment, VirtualBox setup, and Ubuntu installation ready for work</h6>
<br>
<h4>Experiments with SSH, Jupyter Notebook, Ollama, FTP, Apache Tomcat, and Hadoop
Welcome to this repository, where we explore various experiments involving SSH, Jupyter Notebook, Ollama, FTP, Apache Tomcat, and Hadoop. Whether you're a beginner or an experienced user, these step-by-step instructions will guide you through setting up, deploying, and managing different technologies effectively.</h4>

<h1>Experiment 1: Setting Up SSH Connection to a Remote Laptop</h1>
<h4>Overview
<br>
SSH (Secure Shell) is a cryptographic network protocol that allows secure remote access to a system. This experiment provides an in-depth guide on setting up SSH to connect to a friend’s laptop securely for remote file transfers, command execution, and system administration.</h4>
<br>
<h3>Step 1: Install OpenSSH Server and Client</h3>
<br>
<h4>To establish an SSH connection, both your laptop and your friend’s laptop must have the OpenSSH package installed.
<br>
On Your Friend's Laptop (Server Side)
<br>Update the package lists and install the OpenSSH server:
<br>sudo apt update
<br>sudo apt install openssh-server -y
<br>Enable and start the SSH service so that it runs automatically:
<br>sudo systemctl enable ssh
<br>sudo systemctl start ssh
<br>Verify that SSH is running:
<br>sudo systemctl status ssh
<br>If successful, the output should display Active: running.
<br>On Your Laptop (Client Side)
<br>Ensure that the OpenSSH client is installed:
<br>sudo apt install openssh-client -y
<br>Check the installed SSH version:
<br>ssh -V</h4>
<br>
<h3>Step 2: Find Your Friend’s IP Address</h3>
<br>
To connect remotely, you need your friend’s laptop IP address. They can obtain it using:
<br>
ip a
OR
<br>
hostname -I
<br>
<h4></h4>If both systems are on the same local network, use the private IP address.
<br>If connecting over the internet, use the public IP address (found on sites like whatismyipaddress.com).
<br>
<h3>Step 3: Connect to Your Friend’s Laptop</h3>
<br>
<h4>If connecting for the first time, type yes when prompted to verify the connection.
<br>Enter the password for authentication.
<br>
<h3>Step 4: Enable Port Forwarding (If Required)</h3>
<br><h4>If your friend’s laptop is behind a router (common for home networks), port forwarding must be enabled:</h4>
<br>
<h4>Log into the router’s admin panel (usually 192.168.1.1 or 192.168.0.1).</h4>
<br><h4>Navigate to Port Forwarding settings.
<br>Add a rule to forward port 22 (or another chosen SSH port) to your friend’s local IP.
<br>Save changes and restart the router if necessary.</h4>
<br>
<h3>Step 5: Secure SSH Access (Recommended)</h3>
<br><h4>To prevent unauthorized access, your friend can enhance SSH security by following these steps:
<br>
Disable Root Login
<br>Open the SSH configuration file:
<br>sudo nano /etc/ssh/sshd_config
<br>Locate and change:
<br>PermitRootLogin no
<br>Restart SSH service:
<br>sudo systemctl restart ssh
<br>Change the Default Port
<br>Modify the SSH port (choose an unused port, e.g., 2222):
<br>sudo nano /etc/ssh/sshd_config
<br>Change:
<br>Port 2222
<br>Restart SSH:
<br>sudo systemctl restart ssh
<br>Connect using the new port:
<br>ssh -p 2222 username@friend-ip-address</h4>
<br>
<h3>Step 6: Key-Based Authentication (Advanced Security)</h3>
<br>Instead of using passwords, SSH key authentication provides enhanced security.
<br>
<h4>Generate an SSH Key Pair (On Your Laptop)
<br>ssh-keygen -t rsa -b 4096
<br>Press Enter to accept the default save location and optionally set a passphrase.

<br>Copy the Public Key to Your Friend’s Laptop
<br>ssh-copy-id username@friend-ip-address
<br>Once added, you can connect securely without entering a password.</h4>
<br>
<h3>Step 7: Troubleshooting Common SSH Issues</h3>
<br>
<h4>Connection Refused
<br>Ensure SSH service is running:
<br>sudo systemctl status ssh
<br>Restart SSH if needed:
<br>sudo systemctl restart ssh
<br>Permission Denied (Public Key)
<br>Ensure the correct SSH key is added to ~/.ssh/authorized_keys on the remote laptop.
<br>Firewall Blocking SSH
<br>Open the necessary SSH port:
<br>sudo ufw allow 22/tcp
<br>sudo ufw enable</h4>
<br>
<h2>Experiment 2: Installing and Running Jupyter Notebook</h2>
<br>
<h4>Overview
<br>Jupyter Notebook is an interactive computing environment primarily used for Python programming. This experiment details how to install, configure, and make Jupyter accessible from another device.
<br>Steps
<br>1. Install Python and Pip
   <br>sudo apt update
   <br>sudo apt install python3 -y
   <br>sudo apt install python3-pip -y
<br>2. Verify Installation
   <br>python3 --version
   <br>pip3 --version
<br>3. Install Jupyter Notebook
   <br>pip3 install notebook
   <br>Launch Jupyter:jupyter notebook 
<br>4. Run Jupyter Notebook Remotely
<br>To make Jupyter accessible from another device, run:
<br>sudo apt install jupyter-core
<br>jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser
<br>Example Output:Jupyter Server Running
<br>5. Find Local IP Address
  <br> Find your system's IP address to access Jupyter remotely:

<br>hostname -I
<br>or
<br>ip a
<br>Example Output:Find Local IP
<br>6. Allow Firewall Access (If Required)
   <br>If you have a firewall enabled, allow Jupyter's port:
<br>sudo ufw allow 8888 7. Access from Another Laptop
<br>On a different device, enter the following in a web browser:
<br>http://<your-ip>:8888 8. Set Up a Password
<br>To prevent unauthorized access, set a password:jupyter notebook password
<br>Follow the prompts to enter and confirm a password.
<br>9. Run Jupyter in Background
  <br> If you want Jupyter to keep running even after closing the terminal, use:nohup jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser &</h4>
<br>
Experiment 3: Setting Up Apache Tomcat and Deploying a Web Page
Overview
Apache Tomcat is an open-source web server and servlet container designed for running Java-based web applications. This experiment walks you through installing Tomcat, setting up a basic web application, and managing files.

Steps

1. Install Java
   Since Tomcat relies on Java, install OpenJDK 11 using the following commands:

sudo apt update
sudo apt install openjdk-11-jdk -y
Verify the installation:

java --version 2. Download and Install Apache Tomcat
Fetch the latest version of Tomcat and extract it:

cd /opt
sudo wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.36/bin/apache-tomcat-10.1.36.tar.gz
sudo tar -xvzf apache-tomcat-10.1.36.tar.gz -C /opt
Rename the folder for simplicity:

sudo mv /opt/apache-tomcat-10.1.36 /opt/tomcat
Ensure script files are executable:

sudo chmod +x /opt/tomcat/bin/\*.sh 3. Start Apache Tomcat
Launch the Tomcat server:

sudo /opt/tomcat/bin/startup.sh
Verify by accessing:

http://localhost:8080 4. Deploy a Web Page
Create a new directory inside the Tomcat webapps folder:

sudo mkdir /opt/tomcat/webapps/anime
Add web files:

sudo nano /opt/tomcat/webapps/anime/index.html
sudo nano /opt/tomcat/webapps/anime/style.css
sudo nano /opt/tomcat/webapps/anime/script.js
Restart Tomcat to apply changes:

sudo /opt/tomcat/bin/shutdown.sh
sudo /opt/tomcat/bin/startup.sh
Access the page:

http://localhost:8080/anime 5. Managing Files
To remove a file:

sudo rm /opt/tomcat/webapps/anime/style.css
Confirm deletion:

ls /opt/tomcat/webapps/anime
Experiment 4: Installing and Using Ollama
Overview
Ollama allows you to run AI models locally for text generation, machine learning, and other AI-based applications. This section covers installing Ollama, running pre-trained models, and creating custom AI models.

Steps

1. Install Git and Curl
   Before installing Ollama, ensure Git and Curl are installed:

sudo apt install git -y
sudo apt install curl -y 2. Install Ollama
Download and install Ollama using the following command:

curl -fsSL https://ollama.com/install.sh | sh 3. Run a Pre-Trained Model
Ollama comes with pre-trained AI models. To run a model, use:

ollama run llama3:2.1b
Example Output:

Ollama Running

4. Create a Custom AI Model
   To create a personalized AI model, define a Modelfile with your desired parameters:

FROM llama3:2.1
PARAMETER temperature 1
SYSTEM """
You are Rias from High School DxD. Answer as Rias, the assistant, only.
""" 5. Build and Use Custom Model
Once your Modelfile is ready, create and run your model:

ollama create rias -f ./Modelfile
ollama run rias 6. List Installed Models
Check which models are installed on your system:

ollama ls 7. Remove an Ollama Model
If you no longer need a model, remove it with:

ollama rm <model_name> 8. Troubleshooting and Logs
If you encounter issues, check Ollama logs:

cat ~/.ollama/logs/latest.log
This helps diagnose errors and ensure smooth operation.

Experiment 5: Setting Up Hadoop Environment
Overview
Hadoop is an open-source framework that enables the distributed processing of large datasets across clusters of computers using simple programming models. This guide walks you through installing, configuring, and running Hadoop in a single-node environment.

Steps

1. Install Java (If Not Already Installed)
   Hadoop requires Java. If you haven’t installed it yet, follow these steps:

sudo apt update
sudo apt install openjdk-11-jdk -y # Or use openjdk-8-jdk if required
Verify Java installation:

java -version
If Java is not installed correctly, ensure that the correct version is set as the default:

sudo update-alternatives --config java 2. Create Hadoop User
Create a dedicated user for running Hadoop to ensure proper file permissions and security:

sudo adduser hadoop
sudo usermod -aG sudo hadoop
Switch to the Hadoop user:

su - hadoop
Grant necessary permissions to Hadoop user:

sudo chown -R hadoop:hadoop /home/hadoop/ 3. Configure SSH (Required for Hadoop Operations)
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
ssh localhost 4. Download Hadoop
Download the Hadoop tar file from the Apache Hadoop website or use wget:

wget https://downloads.apache.org/hadoop/common/hadoop-3.4.0/hadoop-3.4.0.tar.gz
Extract the Hadoop tar file:

sudo tar -xzvf hadoop-3.4.0.tar.gz
Rename the folder to 'hadoop':

sudo mv hadoop-3.4.0 hadoop 5. Set Hadoop Environment Variables
Open the .bashrc file:

nano ~/.bashrc
Add the following environment variables:

export HADOOP_HOME=/home/hdoop/hadoop/
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS="-Djava.libraray.path=$HADOOP_HOME/bin/native"
Apply the changes by running:

source ~/.bashrc
Check Current Directory for Hadoop:

cd $HADOOP_HOME
pwd 6. Configure Hadoop
chacking whrere is JAVA_HOME

readlink -f $(which java)
For example, you might get an output like:

/usr/lib/jvm/java-11-openjdk-amd64/bin/java
From this, you can extract the directory path without the /bin/java part, like:/usr/lib/jvm/java-11-openjdk-amd64

Set Java Home in Hadoop Configuration

cd $HADOOP_HOME/etc/hadoop
ls
cat hadoop-env.sh
sudo nano hadoop-env.sh
Update the following line:

export JAVA_HOME= /usr/lib/jvm/java-11-openjdk-amd64  
update-alternatives --config java
Edit Hadoop configuration files (core-site.xml, hdfs-site.xml, mapred-site.xml, yarn-site.xml) as needed.

Configure core-site.xml

nano $HADOOP_HOME/etc/hadoop/core-site.xml
Add the following configuration:

<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
Configure hdfs-site.xml

nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml
Add the following configuration:

<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
Configure mapred-site.xml

nano $HADOOP_HOME/etc/hadoop/mapred-site.xml
Convert the template to a working file:

cp $HADOOP_HOME/etc/hadoop/mapred-site.xml.template $HADOOP_HOME/etc/hadoop/mapred-site.xml
Add the following configuration:

<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
Configure yarn-site.xml

nano $HADOOP_HOME/etc/hadoop/yarn-site.xml
Add the following configuration:

<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
7. Format the Hadoop Filesystem
Before starting Hadoop, format the NameNode:

hdfs namenode -format 8. Start Hadoop Services
Start HDFS and YARN services:

start-dfs.sh
start-yarn.sh
To check the status of services:

hdfs dfsadmin -report 9. Verify Hadoop Setup
Check the status of Hadoop services:

jps
You should see the following services running:

NameNode
DataNode
ResourceManager
NodeManager
Additionally, to access the Hadoop web UI:

NameNode Web UI: http://localhost:9870
ResourceManager Web UI: http://localhost:8088
To test the Hadoop installation, create a test directory in HDFS:

hdfs dfs -mkdir /test
hdfs dfs -ls /
Hadoop COVID-19 Data Processing & Word File Analysis
Download COVID-19 Dataset
Download the latest COVID-19 dataset from open data sources using wget:

wget https://raw.githubusercontent.com/owid/covid-19-data/master/public/data/latest/owid-covid-latest.csv -P /home/hadoop/
wget https://covid.ourworldindata.org/data/owid-covid-data.csv -P /home/hadoop/
wget https://github.com/CSSEGISandData/COVID-19/raw/master/csse_covid_19_data/csse_covid_19_daily_reports/01-01-2024.csv -P /home/hadoop/
Upload Data to HDFS
hadoop fs -mkdir -p /user/hadoop/covid19
hadoop fs -put /home/hadoop/owid-covid-latest.csv /user/hadoop/covid19/
change the file name by the file you use "owid-covid-latest.csv"

we will use here python code so wait
we will use here python code
we will use here python code

Run MapReduce Job to Analyze Data
Example: Count cases by country using a MapReduce job:

hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.4.0.jar wordcount /user/hadoop/covid19/owid-covid-latest.csv /user/hadoop/covid19/output
Verify Results
hadoop fs -cat /user/hadoop/covid19/output/part-r-00000
Upload and Analyze a Word File to HDFS
Create a Directory in HDFS
hadoop fs -mkdir /user/hadoop/wordfiles
Upload the Word File to HDFS
hadoop fs -put /path/to/document.docx /user/hadoop/wordfiles/
Verify File in HDFS
hadoop fs -ls /user/hadoop/wordfiles/
Convert the Word File to Text
Install Apache Tika for text extraction:

sudo apt-get install tika
Convert the Word file to text:

tika -t document.docx > document.txt
Upload the Text File to HDFS
hadoop fs -put document.txt /user/hadoop/wordfiles/
Run a Word Count MapReduce Job
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.2.4.jar wordcount /user/hadoop/wordfiles/document.txt /user/hadoop/wordcount_output
Check the Output
hadoop fs -cat /user/hadoop/wordcount_output/part-r-00000
Step 3: Troubleshooting
Check Logs
Logs are stored in $HADOOP_HOME/logs/. Example:

tail -f $HADOOP_HOME/logs/hadoop-hadoop-namenode-<hostname>.log
Verify Hadoop Services
jps
If any of the required daemons (NameNode, DataNode, etc.) are not running, restart the services:

stop-dfs.sh
stop-yarn.sh
start-dfs.sh
start-yarn.sh
Check Java Installation
echo $JAVA_HOME
Ensure it points to a valid Java installation directory.

Verify Files in HDFS
hadoop fs -ls /user/hadoop/wordfiles/
Run MapReduce Again
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.2.4.jar wordcount /user/hadoop/wordfiles/document.txt /user/hadoop/wordcount_output
Check Output Again
hadoop fs -cat /user/hadoop/wordcount_output/part-r-00000
