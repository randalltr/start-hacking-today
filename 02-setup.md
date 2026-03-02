# Ultra Fast Setup

## Meet Your New Best Friends

Let me introduce you to your new best friends:

- YouTube
- AI

Before setting anything up, it helps to understand how hackers actually learn. Hacking is not about memorizing everything or solving problems alone. Hacking is about learning how to find answers quickly and keep moving forward.

Your two best friends from this point forward are **YouTube** and **AI**.

YouTube gives you visual walkthroughs when something feels confusing. Watching someone perform a setup or demonstrate a workflow often makes things click immediately. If something does not work the first time, there is almost always someone who has already recorded the solution.

AI tools such as ChatGPT, Claude, Gemini, and similar assistants act like interactive troubleshooting partners. When you encounter an error message, copy it and ask for help. When a command behaves unexpectedly, describe what happened and ask what to try next. Professional hackers constantly research, test, and iterate. Using modern tools to accelerate learning is part of the process.

Learning hacking means learning how to learn efficiently. These tools help you maintain momentum.

---

## Install a Virtual Machine and Kali Linux

The easiest way to begin hacking is inside a virtual machine. A virtual machine allows Kali Linux to run safely inside your existing computer while keeping your main operating system separate.

Choose a virtualization platform:

- VMware Workstation Player or Fusion
- VirtualBox
- Any equivalent VM software you prefer

Next, download Kali Linux from the official source:

[https://kali.org/get-kali](https://kali.org/get-kali)

Download the prebuilt virtual machine image when available. This option saves time and removes unnecessary setup decisions.

**Follow a YouTube walkthrough if anything feels unclear during installation.** 

Watching someone complete the setup step by step often resolves confusion quickly. AI assistants are excellent for troubleshooting installation errors or configuration issues. Copy error messages directly and work through them one step at a time.

Once Kali boots successfully, you are ready to continue.

---

## Run Pimp My Kali to Optimize Setup

After logging into Kali, open a terminal and run:

```
cd /opt

git clone https://github.com/Dewalt-arch/pimpmykali

cd pimpmykali

./pimpmykali.sh
```

Pimp My Kali updates packages, installs useful defaults, and prepares the environment for practical work. This step saves hours of manual configuration and helps ensure tools behave consistently.

**Follow a YouTube walkthrough or ask AI if any error encountered.** 

Allow the script to complete fully. Restart the machine if prompted.

---

## Verify Core Tools Installed

This book focuses on three tools. Confirm they are available before moving forward.

Open a terminal and check each one.

### Check Nmap

```
nmap --version
```

You should see version information displayed.

### Check ExploitDB / Searchsploit

Searchsploit is the same as ExploitDB and allows quick vulnerability searching from the terminal.

```
searchsploit
```

Alternatively, you can browse ExploitDB on the internet at [https://www.exploit-db.com/](https://www.exploit-db.com/)

### Check Burp Suite

Launch Burp Suite from the Kali menu or terminal:

```
burpsuite
```

Burp should open but checkout the next section for Burp Suite setup.

**Remember your friends YouTube and AI are here to help with any problems.** 

Once these three tools run successfully, your environment matches the workflow used throughout this book.

---

## Configure Burp Suite

Burp Suite works by placing itself between your browser and the internet. This allows you to observe and modify web traffic in real time. Once this is configured, web applications stop feeling mysterious because you can see exactly what is being sent and received.

The fastest way to set this up is to watch a YouTube video showing how to configure Burp Suite with FoxyProxy and how to install the Burp CA certificate in your browser. A short walkthrough makes this process clear and usually takes only a few minutes.

Search YouTube for:

```
Burp Suite FoxyProxy Setup Kali Linux

How to Install Burp CA Certificate
```

Follow along and complete these steps:

- Install the FoxyProxy browser extension
- Configure FoxyProxy to route traffic through 127.0.0.1:8080
- Start Burp Suite and ensure the proxy listener is running on port 8080
- Visit the Burp proxy page in your browser
- Download and install the Burp CA certificate
- Import the certificate into your browser so HTTPS traffic works correctly

After configuration, enable FoxyProxy and browse to any website. Requests should begin appearing inside Burp Suite under the Proxy tab. Seeing live traffic confirms that Burp is successfully intercepting communication.

**Remember that YouTube and AI are you best friends and will make your hacking journey infinitely easier!**

Once traffic flows through Burp, your environment is fully prepared for the workflow used throughout this book.

Let's Learn The Only 2 Nmap Commands You Need: [03 - Nmap](03-nmap.md)