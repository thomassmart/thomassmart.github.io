---
layout: post
title:  "VS Code remote powershell"
date:   2020-07-26
tags: powershell vs-code server-2016 server-2019
---

Being a Microsoft centric engineer with a Mac OS laptop has raised pleny of eyebrows during meetings. I'm sure there have been pleny of times people have internally questions my credentials, and who can blame them? Walking into a meeting to talk about specific windows issues, only to open up my mac, seems completely hypocritical. 

We all have our reasons for what devices, applications, operating systems we choose, mine typically boil down to the fact that I'm in the Apple ecosystem. I tried throwing myself in to the land of Microsoft, but they failed to impress. Only recently has Windows 10 piqued my interest, but the integration between devices is still plain awful, IMO.

This leads me to what's always been the crux of my BYOD mac whilst working on Windows. Creating powershell scripts in a 

&lt;/rant&gt;

# The solution
It turns out you can have your cake and eat it. Who knew?

Turns out the team working on VS Code knew. 

VS Code is an amazing application that should be in almost all IT professionals toolkit. It's insanely powerful, whilst remaining quite simple.

## Highlevel


The setup consists of the following:

* My MacBook Pro, you guessed it, running MacOS
* [Visual Studio Code](https://code.visualstudio.com)
* A Windows Server 2016 VM
* [OpenSSH 7.7](https://github.com/PowerShell/Win32-OpenSSH/releases/tag/v7.7.2.0p1-Beta)

This setup gives me the flexibility I've always wanted.  
* Native text rendering on my mac, with no keyboard passthrough or lag. 
* Source Code stored on my mac
* Native powershell debugging running on my target environment

# The Setup

## 1. Setup Open SSH
I'm a nice guy, so you can read the text, or just copy paste the below code block
```powershell
Invoke-WebRequest -Uri "https://github.com/PowerShell/Win32-OpenSSH/releases/download/v7.7.2.0p1-Beta/OpenSSH-Win64.zip" -OutFile OpenSSH-Win64.zip
Unblock-File OpenSSH-Win64.zip
Expand-Archive OpenSSH-Win64.zip -destination 'C:\Program Files'
& 'C:\Program Files\OpenSSH-Win64\install-sshd.ps1'
Get-Service ssh* | Start-Service
Get-Service ssh* | Set-Service -StartupType Automatic
```

Whats the above doing? Its really simple. 
1. Download the ZIP file from github
2. Unblock the zip file, so that the executables aren't blocked
3. Extract the archive into the C:\Program Files directory
4. Run the provided install powershell script
5. Start the SSH services
6. Set the SSH services to automatic

Running this will install 2 services. 

## 2. Install VS Code + Extensions
VS Code is really straight forward to install. Download for your OS flavour and run the install following their documentation.

Once installed, open the marketplace and install `Remote-SSH`.

![RemoteSSH](/assets/img/vscode-sshremote/VSCode.RemoteSSH.png)

## 3. Connect to the remote machine
When you have your workspace open, open the command pallet (F1 or ⌘+⇧+P) and type `Remote-SSH: Connect to Host`

![RemoteSSHConnecting](/assets/img/vscode-sshremote/VSCode.ConnectCmd.png)

Follow the prompts, entering your hostname, username and password. Its worth noting that you may have to accept the remote host key. It maybe simpler to do this through a standard SSH session.

When authenticating, the username and password are the standard windows username and passwords on the remote host. You can use domain credentials also!

This process will take a few moments to setup the VS Code server on your remote host

## 4. Enjoy the benefits.

You can now reap the rewards of setting up remote-ssh. Here you can see that I have a simple one liner to query the OS, written and displayed on my Mac, running on the Windows Server instance. Pure joy 😊.

![RemotelyDebugging](/assets/img/vscode-sshremote/VSCode.DebuggingRemotely.png)
