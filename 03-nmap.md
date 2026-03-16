# Nmap

## Seeing the Target

Nmap is the first tool that made hacking start to feel logical to me. Before learning how to scan a target, hacking felt random. After learning how to read scan results, the process started to look like investigation.

Nmap answers the first question every hacker asks: what exists on the target?

Computers communicate through services that listen on network ports. Web servers, file shares, remote login services, databases, and many other systems expose themselves through these ports. Nmap reveals those services so you can start thinking about how they might be attacked.

Over time you can learn dozens of Nmap switches and scanning techniques. Many professionals use complex scanning profiles for specialized situations. In practice, however, most real work begins with the same simple commands.

After solving more than one hundred machines, I found myself using two scans almost every time.

## The ONLY Two Commands That Matter

The first command provides a quick overview.

```
nmap <ip-address>
```

This scan runs quickly and shows common open ports. It gives an immediate sense of what kind of system you are dealing with. You might see a web server, SSH service, or database appear within seconds. That early information helps you begin forming ideas about what the target might contain.

Once you have a quick overview, run the deeper scan.

```
nmap -p- -sCV <ip-address> -T4 -oA nmap_scan_tcp
```

This scan takes longer but reveals the full picture. The `-p-` option scans every TCP port instead of only the most common ones. The `-sC` option runs useful default scripts that gather additional information. The `-sV` option attempts to identify service versions. The `-T4` option increases scan speed. The `-oA` option saves the results so you can review them later.

These two commands form the foundation of reconnaissance. Many machines can be solved using exactly this approach.

## A Quick Word Before You Start Scanning

Before you begin running Nmap scans, take a moment to understand something important. Scanning systems that you do not own or have permission to test can violate laws or acceptable use policies. Even a simple port scan can be interpreted as reconnaissance activity.

Responsible hackers only test systems where permission is clear.

For practice during this chapter, you can safely scan the public testing server provided by the Nmap project:

```
nmap scanme.nmap.org
```

This server exists specifically so people can learn how Nmap works.

Later in this book, we will use intentionally vulnerable machines on platforms such as Hack The Box. Those environments are designed for learning and provide legal targets for practice.

Stay curious, stay responsible, and always hack with permission.

## Build the Habit of Taking Notes

Once the scan completes, slow down and review the output carefully. Each service represents an opportunity. A good habit is to record every open port and service in your notes.

Your notes might look like this:

```
PORT     SERVICE
22       SSH
80       HTTP
3306     MySQL
```

Writing these down prevents you from missing anything. During longer engagements it becomes easy to forget which services you already investigated. Clear notes create a checklist so every potential attack surface receives attention.

Treat each port as a new lead in an investigation.

## Reading an Nmap Scan

A typical Nmap result might look like this:

```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu
80/tcp   open  http    Apache httpd 2.4.29
3306/tcp open  mysql   MySQL 5.7.29
```

Each column tells you something important.

**PORT** shows where the service is listening.
**STATE** tells you whether the port is open.
**SERVICE** describes what type of service is running.
**VERSION** provides additional detail about the software.

These details guide your next decisions.

An open **SSH** service suggests possible credential attacks or key-based access. An **HTTP** service invites exploration through a web browser or Burp Suite. A database service such as **MySQL** hints at stored data or authentication mechanisms.

Every line in the output represents a potential entry point.

## Turn Information Into Questions

The most important skill when reading Nmap output is curiosity. Each discovered service should trigger a question.

Examples might include:

- What does the website on port 80 contain?
- Does the software version have known vulnerabilities?
- Are default credentials available?
- Does this service allow file uploads or remote access?

This investigative mindset transforms scanning into exploration.

Nmap gives you the map of the target. Your job is to follow the leads.

## Learning From Your Scans

Every Nmap scan contains far more information than you will understand at first. That is normal. The goal at this stage is not perfect understanding. The goal is curiosity and momentum.

Each line of output is an opportunity to ask questions. When you see something unfamiliar, treat it like a clue and start investigating. This is where your two best friends come back into the picture: YouTube and AI.

Suppose your scan shows something like this:

```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu
80/tcp   open  http    Apache httpd 2.4.29
```

Instead of moving past this information, begin asking questions.

You might search YouTube for phrases like:

```
OpenSSH hacking basics
Apache 2.4 enumeration
What can you do with an open SSH port
```

Watching a short video often reveals common attack ideas, enumeration techniques, or tools people use to investigate those services.

AI tools provide another powerful way to explore the output. You can paste a section of your Nmap scan and ask questions about it. For example:

```
What attacks are commonly attempted against OpenSSH 7.6?
What should I check first when port 80 is open?
What does Apache httpd 2.4.29 usually indicate?
```

AI can help explain the service, suggest investigation paths, and point you toward useful next steps. Sometimes the answer leads you to a web directory to explore. Other times it suggests searching ExploitDB for known vulnerabilities.

This process of asking questions and following leads is how hackers develop intuition. Each scan teaches something new. Over time, patterns start to appear. Certain services begin to signal specific attack paths. Version numbers start to look familiar. You begin to recognize which findings deserve deeper investigation.

The combination of Nmap, curiosity, and your research tools creates a powerful learning loop. Every machine you scan becomes both a target and a lesson.

## This ONE Trick Will Make You a Great Hacker

Another habit that helps enormously is writing down every open port and service in your notes. Enumeration becomes much easier when you treat each service like a lead in an investigation. When you record the results of your scan, you create a checklist that ensures nothing gets overlooked.

After running a scan, go through the output one line at a time and write down each open port, the service, and any useful details you notice. Your notes might look something like this:

```
22/tcp  - SSH  - OpenSSH 7.6p1 Ubuntu
80/tcp  - HTTP - Apache httpd 2.4.29
```

As you continue enumerating the machine, update your notes with anything you discover. For example, visiting port 80 might reveal a default Apache page or a web application login panel. Adding those observations to your notes helps you track what you have already investigated and what still deserves attention.

Your notes might grow into something like this:

```
22/tcp  - SSH  - OpenSSH 7.6p1 Ubuntu
          Possible credential access point

80/tcp  - HTTP - Apache httpd 2.4.29
          Default Apache webpage visible
```

Keeping notes like this makes the enumeration process much clearer. Each service becomes a potential foothold. When you feel stuck, you can return to your list and ask questions about each entry. One of those services often becomes the entry point into the machine.

Good hackers build the habit of documenting everything they see. Clear notes transform a confusing scan into a structured investigation.

## Expanding Your Knowledge

Nmap includes many additional capabilities such as UDP scanning, operating system detection, stealth scanning, and specialized scripting. These features become useful as your experience grows.

For now, the two commands in this chapter will carry you through the majority of beginner machines. Mastering how to interpret scan results matters more than memorizing dozens of flags.

Clarity grows through repetition. Each new scan improves your ability to recognize patterns and identify promising targets.

The next chapter builds on this discovery process. After identifying services, the next step is learning how to locate real exploits that turn information into access.

Let's Find Some Exploits: [Chapter 4 - ExploitDB](04-exploitdb.md)