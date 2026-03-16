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
htb <box_name> walkthrough
```

There is no shame in reading walkthroughs during the learning process. The goal is understanding the workflow.

Machine 1: Nibbles (Linux)

Nibbles is an excellent beginner machine. It demonstrates how a vulnerable web application can lead to initial access and eventually root privileges.

Skills Practiced

Nmap enumeration

Web application investigation

Using Searchsploit

Privilege escalation

Step 1: Scan the Machine

Run your standard scans.

nmap <target-ip>

Then run the deeper scan.

nmap -p- -sCV <target-ip> -T4 -oA nmap_scan_tcp

The scan will reveal a web service.

Example:

80/tcp open http Apache
Step 2: Visit the Website

Open the site in your browser.

Spend time exploring the application. Click links. Look for login forms or interesting pages.

Enable Burp Suite and observe the traffic in Proxy → HTTP history while browsing.

Watching requests appear in Burp often reveals how the application works.

Step 3: Identify the Application

While exploring the site you will discover that the server runs Nibbleblog.

Now search ExploitDB.

searchsploit nibbleblog

One of the results will match the version of the application.

Step 4: Use the Exploit

Copy the exploit locally.

searchsploit -m <exploit-id>

Read the exploit and follow the instructions.

This should give you access to the system.

Step 5: Privilege Escalation

Once you gain a shell, continue investigating the machine.

Look for:

configuration files

writable directories

sudo permissions

Eventually you will find a path to escalate privileges to root.

Lesson

Web applications frequently contain vulnerabilities that lead to system access. Careful investigation combined with vulnerability research often reveals the path forward.

Machine 2: Jerry (Windows)

Jerry is a simple Windows machine that demonstrates how weak configuration can lead to compromise.

Skills Practiced

Nmap enumeration

Investigating web services

Identifying default credentials

Step 1: Run Nmap

Run your standard scan workflow.

nmap <target-ip>

Then run the full scan.

nmap -p- -sCV <target-ip> -T4 -oA nmap_scan_tcp

One of the services will appear similar to:

8080/tcp open http Apache Tomcat
Step 2: Investigate the Web Service

Open the site in your browser.

http://<target-ip>:8080

Look for administrative panels or login pages.

Burp Suite can help you observe how the application communicates with the server.

Step 3: Research the Service

Search for Tomcat vulnerabilities or common configuration issues.

You might search YouTube for:

tomcat manager exploitation

Or ask AI tools questions about Tomcat.

Through research you will discover that Tomcat installations sometimes use default credentials.

Step 4: Gain Access

After accessing the Tomcat manager interface, you can upload a web application that executes commands on the server.

This results in a shell on the Windows machine.

Lesson

Many compromises occur because of configuration weaknesses rather than software bugs.

Default credentials and exposed administrative panels are common attack paths.

Machine 3: Bashed (Linux)

Bashed demonstrates how discovering a web shell can lead to full system compromise.

Skills Practiced

Nmap enumeration

Web directory investigation

Privilege escalation

Step 1: Run Nmap

Start with your usual scans.

nmap <target-ip>

Then run the deeper scan.

nmap -p- -sCV <target-ip> -T4 -oA nmap_scan_tcp

You will see a web service running on port 80.

Step 2: Explore the Website

Open the site in your browser and explore the directories.

Pay attention to files or scripts that may allow command execution.

Burp Suite can help observe how requests are sent to the server.

Eventually you will discover a web shell already present on the system.

Step 3: Gain a Shell

Use the web shell to execute commands on the system.

Once you have command execution, upgrade your access to a more stable shell.

Step 4: Escalate Privileges

After gaining a shell, begin investigating the system.

Look for:

writable scripts

sudo permissions

misconfigured services

These clues will lead you to root access.

The Pattern

Each machine in this chapter reinforces the same pattern.

Scan the system with Nmap

Identify exposed services

Research vulnerabilities using ExploitDB

Interact with applications using Burp Suite

Gain access and escalate privileges

With repetition, this process becomes natural.

Services begin to suggest possible attack paths. Vulnerabilities start to look familiar. Enumeration becomes easier.

Eventually hacking stops feeling random and begins to feel systematic.

That transformation happens through practice.