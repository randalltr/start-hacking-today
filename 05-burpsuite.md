# Burp Suite

## Seeing How Web Applications Really Work

Many machines you encounter will expose a web service. When Nmap shows port 80 or 443 open, a browser is usually the next step. Opening the website shows what the application wants users to see, but it does not show how the application actually works.

Burp Suite reveals the conversation happening between your browser and the server. Every request your browser sends and every response the server returns passes through Burp. Once you can see that conversation, you can also modify it.

This ability turns web applications from black boxes into systems you can observe and test.

## Start Burp Suite

Launch Burp Suite from Kali. When it starts, choose a **temporary project** and accept the default configuration.

Your browser should already be configured to route traffic through Burp using the proxy setup completed earlier in this book. When Burp is running and FoxyProxy is enabled, web requests will begin appearing inside Burp automatically.

Open a website in your browser and look at the **Proxy → HTTP history** tab. You should see requests appearing as you navigate the site.

At this point, you are already intercepting traffic.

## The Proxy Tab

The **Proxy** tab shows the full history of requests sent by your browser. Every page load, image request, script file, and API call appears here.

When you first open a web application, the list can become large quickly. Sorting the history makes it easier to understand what is happening.

Click the **Host** column to group requests by domain. Click the **Method** column to group similar requests together. Sorting helps you quickly identify interesting requests such as login attempts, file uploads, or API calls.

Another useful feature is **scope**.

Right click on the domain of the application you are testing and select **Add to scope**. Once the target is in scope, Burp can filter requests so you only see traffic related to that application.

Working within scope reduces noise and helps you focus on the target.

## Intercepting Requests

Burp allows you to pause and modify requests before they reach the server.

In the **Proxy → Intercept** tab, click **Intercept is on**.

Now when your browser sends a request, Burp will capture it before the server receives it. You can inspect the request and modify any part of it.

For example, you might change a parameter value, modify a cookie, or adjust a form submission.

After reviewing the request, click **Forward** to send it to the server.

When you want normal browsing to resume, turn interception off by clicking **Intercept is off**.

Many testers browse with interception off and only enable it when investigating a specific request.

## Repeater

Repeater allows you to resend a request multiple times while modifying different parts of it. This tool is extremely useful when testing inputs.

When you see an interesting request in the Proxy history, right click it and choose **Send to Repeater**.

Switch to the **Repeater** tab. The full request appears on the left side and the server response appears on the right side.

Now you can modify parts of the request and resend it repeatedly.

Common tests include changing parameter values, modifying usernames, adjusting file paths, or experimenting with input fields. Each time you click **Send**, Burp returns the server response so you can observe the effect of your changes.

Repeater turns testing into a controlled experiment.

## Intruder

Intruder allows you to automate repeated requests using lists of possible inputs.

This is useful for discovering hidden values such as usernames, passwords, file names, or directory paths.

From the Proxy history, right click a request and select **Send to Intruder**.

In the **Positions** tab, Burp marks potential injection points using special markers. You can remove unnecessary markers and leave only the parameter you want to test.

Next, open the **Payloads** tab and load a list of values. These might be common passwords, usernames, or directory names.

When the attack starts, Burp sends requests automatically using each payload and records the responses.

You can then sort the results by response length, status code, or other indicators to identify unusual responses.

Intruder helps uncover things that are difficult to find manually.

## What to Look for in Web Traffic

When analyzing requests in Burp, focus on areas where input interacts with the application.

Examples include:

- Login forms
- File upload features
- Search fields
- Parameters in URLs
- API requests
- Cookies and session tokens

These locations often reveal vulnerabilities or unexpected behavior when modified.

Every parameter represents a possible opportunity to test how the application handles input.

## Building Your Web Hacking Workflow

At this point your workflow should feel familiar.

First you scan a machine with Nmap and identify a web service. Then you open the site in a browser and observe the traffic using Burp Suite.

Burp allows you to inspect requests, modify inputs, repeat experiments, and automate testing.

Combined with Nmap and ExploitDB, Burp completes the core toolkit for exploring many beginner machines.

## Learn by Investigating

As with Nmap and ExploitDB, curiosity drives progress.

When you encounter unfamiliar requests or parameters, research them. Use YouTube and AI to understand what the application is doing and what kinds of attacks are commonly attempted against it.

Over time, patterns begin to appear. Certain types of requests start to look suspicious. Certain inputs begin to suggest possible vulnerabilities.

Burp Suite makes those patterns visible.

## Use Your Research Partners

At this point you have seen the core pieces of Burp Suite that matter most for beginners: Proxy, Repeater, and Intruder. These tools form the foundation of how many web vulnerabilities are discovered.

**As you continue learning, remember your two best friends: YouTube and AI.**

Burp Suite is a large and powerful tool. A short ten minute tutorial on YouTube often demonstrates more practical usage than several pages of written explanation. Watching someone intercept a request, send it to Repeater, and experiment with parameters makes the workflow immediately clear.

AI assistants can also help you understand what you are seeing. When a request looks confusing, paste it into an AI tool and ask questions about it. You can ask what each parameter means, what the request is doing, or how testers typically investigate that type of functionality.

These tools accelerate learning dramatically.

For now, keep your focus on the three Burp tools introduced in this chapter. Proxy shows you the traffic. Repeater allows you to experiment with requests. Intruder automates repeated testing.

Mastering these three tools will carry you through many beginner machines. As your experience grows, additional features inside Burp will begin to make more sense.

For now, keep intercepting traffic, asking questions, and experimenting.

And let's start hacking some real boxes! [Chapter 6 - HackTheBox](06-hackthebox.md)