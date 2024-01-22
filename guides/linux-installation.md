---
description: Installing a QBCore Server on Linux step by step
---

# 🐧 Linux Installation

## MariaDB

While Windows has XAMPP, we'll be using a standalone version of SQL called MariaDB. We will be installing this via shell.

The first thing that is recommended to do before installing a package is updating your system, we do that with the following command

```
sudo apt-get update
```

{% hint style="danger" %}
Make sure to always use a user that has sudo privileges. On Linux, root accounts have access to everything on the system. It is advised that a specific user has sudo privileges and remote root access is turned off to prevent any incidents related to possible breaches. You can read more about initial Linux security [here](https://blog.avast.com/secure-your-linux-server-avast).
{% endhint %}

After you've updated your system, it's time to install the MariaDB server. You do so by entering the command below

```
sudo apt-get install mariadb-server
```

Follow the setup that guides you through. There should be a few options that you select with the space key. Eventually, when you've completed the installation, you'll need to run through a secure installation with the command below.

```
sudo mysql_secure_installation
```

The script will prompt you to set up the root user password, remove the anonymous user, restrict root user access to the local machine and remove the test database. At the end the script will reload the privilege tables ensuring that all changes take effect immediately.

All steps are explained in detail and it is recommended to answer “Y” (yes) to all questions.

After you've done the secure installation above, you can then connect to your mysql service via the command below. You log in as the local mysql root user with the password that you've set in the secure installation.

```
mysql -u root -p
```

{% hint style="warning" %}
If you've done the secure installation but forgot the root user password, a sudo privileged user can bypass logging into the mysql service by running the command

**sudo mysql -u root**
{% endhint %}

### **Creating an Admin user**

After you've done the steps above, you should now have a fully functional MariaDB service on your server. Congratulations! We now have to set up a user with proper credentials, as well as a database that we'll use for setting up QBCore.

Let's start by creating an administrative user that can handle creation of other users and databases. It is very much advised that the user you're running is not the standard root user, because it has access to everything that goes on with MariaDB.

Open up your mysql instance with the command below

```
mysql -u root -p
```

Once you're in the console, it should look a bit like this

![MariaDB Command Line](../.gitbook/assets/Terminus\_LjifucOy4i.png)

We will now proceed with creating an administrator user account. Enter the commands as they are seen below in numerical order. You will only need to edit a few things (Such as username, password and host)

```
CREATE USER 'user1'@localhost IDENTIFIED BY 'password1';
(Check the user created by running this line) SELECT User FROM mysql.user;
GRANT ALL PRIVILEGES ON *.* TO 'user1'@localhost IDENTIFIED BY 'password1';
FLUSH PRIVILEGES;
```

{% hint style="info" %}
'user1', localhost and 'password1' variables are all expected to be changed. You can change anything in the 'user1' and 'password1' fields to your desired values as that's what you'll use while logging in.

\
Localhost is a bit tricky. Since Linux does not natively feature a Desktop Environment, you will most likely access the database with the user remotely. To do so, instead of localhost, enter a % (A % means any host) so it looks as **'user1'@'%'**
We will be covering how to connect and what ports to open below.
{% endhint %}

### Allowing remote access (DB)

As a default setting, MariaDB and MySQL both only allow connections from the local network. In order to connect to the database with external software (Such as HeidiSQL) and from our PC, we will need to change those settings.

The file that has these settings can be found in **/etc/mysql/mariadb.conf.d/50-server.cnf**

We open this file using the command **`sudo nano 50-server.cnf`**, which opens a command line text file editor.

The screenshot below shows you what line needs changing. The default setting will have the bind address set to 127.0.0.1, which only allows local host connections. We will change this to 0.0.0.0 to allow any and all connections to the database.

![50-server.cnf](../.gitbook/assets/Terminus\_SOG5oqcssc.png)

Editing in nano is fairly simple, it's the same as using a notepad but without a mouse. Use arrow keys to move through the code and normally edit the file as you would in a normal environment.

After you've edited the bind address to 0.0.0.0, you can exit the file using CTRL+X, pressing Y when prompted to save changes and Enter when prompted what to save the file as (It will always be the same file name as when it was open).

![After pressing CTRL+X we press Y to save changes](<../.gitbook/assets/Terminus\_Sf4x4s5sbx (1).png>)

![Leave the file name the same and press enter.](<../.gitbook/assets/Terminus\_Ot5jFzizkD (1).png>)

After that, we restart the mariadb service to confirm changes to the files using the commands below

```
sudo systemctl restart mariadb
```

You can check the status of the service by using the below command

```
sudo systemctl status mariadb
```

![systemctl status of MariaDB](../.gitbook/assets/Terminus\_f7VVyPHkLC.png)

We have allowed remote access from all other hosts. Are we able to connect now? Not quite yet. There is one more thing left to do.

### Opening ports

Ports can be a pain to understand, especially for a beginner. Let's break it down.

Ports are like doors that have specific things behind them. A door needs to be unlocked in order to pass through it. Without an open door, no traffic can pass through our services.

MySQL services have a default port of 3306, you can change these in the settings, but you do not need to do so. We will be using a firewall software called iptables that allows us to open these ports. These usually do come as standard and already installed with certain distributions of Linux. You can check if iptables is already installed with the command below.

```
sudo iptables --version
```

If you get a response similiar to what is below in the screenshot, then you've got iptables installed and ready for use.

![iptables returning its version](../.gitbook/assets/Terminus\_8ovVMYD2CK.png)

Once you've verified that you have iptables installed, just run the following command to open the 3306 port for MySQL Connections.

```
sudo iptables -A INPUT -p tcp --dport 3306 -j ACCEPT
```

You can check if the port is open and able to be seen by using this website [here](https://portchecker.co/).

## Running Artifacts

Using artifacts is the most important bit, because it is essentially the brain of the server. We use wget, a tool present on the Linux system to directly download the archive from Cfx's Webpage. [Here](https://runtime.fivem.net/artifacts/fivem/build\_proot\_linux/master/) is a list of all Linux artifacts, but it's best if you just get the latest one. Once you've made your decision on which version of the artifacts to get, simply right click and use "Copy Link". This will copy a direct link to the artifacts that we'll use in the wget command.

Move to whichever folder you are going to download the file to. (I usually make a seperate folder for Artifacts and Files, just so they're seperated.) Use the following command (Remember to replace the link with whatever you get from the Artifacts website)

```
wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/5742-ded89bc6acf29a720a7686a1de70d28b62c75af8/fx.tar.xz
```

![Using wget](https://user-images.githubusercontent.com/89489089/179919507-a17cbce0-5307-4a34-9bf1-64acdd68e29c.png)

After this is done, you will have the files in the directory you currently are. You then simply "untar" the archive with the tar command found below

```
tar -xf fx.tar.xz
```

The console will hang for a bit. After it is done, you should see the files in the directory after you run the dir command.

![Using tar and dir command](https://user-images.githubusercontent.com/89489089/179920224-e8c933b9-91a2-4dc9-9ba5-71dc7e59484d.png)

The only thing left to do now is running the actual artifacts. While Windows uses .exe and .bat files, Linux uses so called .sh files to run Cfx Artifacts. Make sure that you're in a screen like we've discussed earlier and run the following command in the directory with the run.sh file to start your FiveM server.

```
./run.sh
```

The rest of the setup is relatively easy, since you are now setting up txAdmin, it is identical to the Windows installation. Continue the tutorial in the Windows section, just skipping the part about the artifacts and continuing after the .exe is ran [here](https://docs.qbcore.org/qbcore-documentation/guides/windows-installation#artifact-and-txadmin).
