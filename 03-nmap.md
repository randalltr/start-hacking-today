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

## Expanding Your Knowledge

Nmap includes many additional capabilities such as UDP scanning, operating system detection, stealth scanning, and specialized scripting. These features become useful as your experience grows.

For now, the two commands in this chapter will carry you through the majority of beginner machines. Mastering how to interpret scan results matters more than memorizing dozens of flags.

Clarity grows through repetition. Each new scan improves your ability to recognize patterns and identify promising targets.

The next chapter builds on this discovery process. After identifying services, the next step is learning how to locate real exploits that turn information into access.