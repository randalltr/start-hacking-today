# Chapter 7: Tmux (BONUS!!!)

## Become the Hacker From the Movies

At some point, every hacker has the same thought.

How are those people flying through terminals, switching screens instantly, running multiple things at once, and never touching their mouse?

That tool is tmux. The name stands for Terminal MUltipleXer.

Tmux lets you:

- run multiple terminals inside one window
- switch between them instantly with keyboard shortcuts
- split your screen into panes
- keep sessions running even if you disconnect

This is the tool that makes you feel like a real hacker.

It is also, realistically, the only thing standing between you and looking like the ultra cool hacker from the movies.

Before you get started, here's a couple of my favorite resources to help you learn tmux.

[Network Chuck Teaches Tmux](https://youtu.be/nTqu6w2wc68)

[Tmux Cheatsheet](https://tmuxcheatsheet.com/)

## The Only Commands You Need

You do not need to learn everything in tmux.

These commands will cover almost everything you need.

Start tmux

```
tmux
```

This creates a new session.

Detach from tmux

```
Ctrl + b, then d
```

This leaves tmux running in the background.

List sessions

```
tmux ls
```

Reattach to a session

```
tmux a
```

Kill a session

```
tmux kill-session
```

Or kill everything:

```
tmux kill-server
```

## Windows (Tabs)

Think of windows like tabs in a browser.

Create a new window

```
Ctrl + b, then c
```

Move to next window

```
Ctrl + b, then n
```

Move to previous window

```
Ctrl + b, then p
```

Rename a window

```
Ctrl + b, then ,
```

Give it a name like:

```
nmap
web
shell
```

This helps you stay organized during a box.

## Panes (Split Screens)

This is where tmux becomes powerful.

You can split your terminal into multiple views.

Split horizontally

```
Ctrl + b, then "
```

Split vertically

```
Ctrl + b, then %
```

Move between panes

```
Ctrl + b, then arrow keys
```

## Closing Things

Close a pane or window

```
Ctrl + b, then x
```

This closes whatever shell you are in.

## A Simple Workflow

Here is how you might use tmux on a Hack The Box machine.

1. Start tmux

```
tmux
```

2. Create a window for scanning

```
Ctrl + b, then c
```

Rename it:

```
Ctrl + b, then ,
```

Call it `nmap`.

3. Run your scan.

4. Create another window for web work.

5. Split panes so you can:

- run commands
- view output
- keep notes

Now you are working in multiple terminals at once without losing anything.

## Why This Matters

When you start working on real machines, things get messy fast.

You will have:

- scans running
- shells open
- web apps to test
- notes to track

Tmux keeps everything organized in one place.

It also keeps your sessions alive if your connection drops.

## Keep It Simple

You do not need to master tmux.

Use it just enough to:

- create sessions
- switch windows
- split panes
- stay organized

That alone will make your workflow faster and smoother.

## Your Next Step

Open tmux right now.

Create two windows.

Split one into two panes.

Move between them.

That is enough to get started.

Now you've mastered enough to become dangerous. Here's some next steps - [Chapter 8 - Next Steps](08-nextsteps.md).