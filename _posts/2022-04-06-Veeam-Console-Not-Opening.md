---
layout: post
title:  "Veeam Console Not Opening"
date:   2022-04-06
tags: veeam server-2016 server-2019 software-updates
---

Everyone ~~loves~~ loathes a software update. We all know they're needed to fight the everlasting war agains vulnerabilities and bugs. We all love the new features becoming available, after they were promised years ago. These positive gains, are still often dwarfted by the the process and risk of replacing the bits and the bytes that make up their lovely digital binary objects.

I'm yet to meet anyone, other than middle management, who love Change Control. The easiest way to get an engineer to cry is to softly whisper "I need to you to raise a Change Request" into their ear. If you can get those words out before their first cup of coffee, you may near crush them. Change Request, CR's as I'll now call them, can be something as trivial as a call to a stake holder, letting them know you're doing something, to a complex process requiring many sign offs, roll back plans, proof of testing and scheduling conflicts.

Formal or not, all successful CR's have a roll back option. A get out of free jail card. You only get burnt once without one, then you'll never do it again. But what do you do when your most often relied upon roll back option, the old faithful backup, is the CR. You have a backup of your backups

<centre><div class="tenor-gif-embed" data-postid="16756828" data-share-method="host" data-aspect-ratio="1.77778" data-width="40%"><a href="https://tenor.com/view/inception-deeper-go-deeper-we-need-to-go-deeper-leonardo-di-caprio-gif-16756828">Inception Deeper GIF</a>from <a href="https://tenor.com/search/inception-gifs">Inception GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script></centre>

That is in Veeam, you have a configuration backup. A configuration backup that is:

- Current
- Accessible
- Encrypted with Password (So other password and secrets are restorable)

Do this, as your number one priority before starting **any** works on your backup servers. Don't be a cow(boy/girl). If you're roll back plan is to "remove update" or "restore config backup" then ENSURE YOUR CONFIG BACKUP IS CURRENT AND THAT YOU CAN ACCESS THE .bco FILE BEFORE STARTING.

Okay. Lecturing over.

You've done an update/patch/repair/whatever. Everything was smooth enough. You go to check that data is flowing on your backup jobs, and the console won't open. This is a pseudo known issue, that relates to other consoles being open at the start

Big Sad. 😭

Here's some helpful hints, from a recent issue.

1. Check all the Veeam services are started
2. Stop all veeam.backup.satellite processes
3. Stop all veeam.backup.uiserver processes
4. Try again, no bueno?
5. Reboot (If you've not done this already)
6. Try again
7. Look through the logs in C:\ProgramData\Veeam\
    You want to look at the UIServer logs. If there's nothing logging in there, it could be this issue.
8. Download the ISO for the same version. Check the hash
    ~~~~~powershell
        Get-FileHash C:\Users\ItsYou\Download\NotAbrokenVeeam.iso
    ~~~~~~
9. Re-Install Veeam, you may need to do this: KB4204: Veeam Repair/Reinstall/Upgrade fails with "The following SQL database patches are missed"
10. Restore that glorious BCO file.
11. Chin Chin 🍻
