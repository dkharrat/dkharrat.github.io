---
layout: post
title:  "Continuously Rebooting System and BSOD in Windows Logon Process STOP:0xc000021a"
date:   2008-09-16 00:00:00 -0800
---
Today, I accomplished something that I thought was quite challenging. I solved a very cryptic and frustrating STOP message. I wake up one morning, and discover that my WinXP computer was completely hung. I restart it and wait for it to boot up, but a couple of seconds in the boot up process (in the "Windows XP" boot logo) , it rebooted. Thinking it was a one-time glitch, I waited for my computer to start up again. But it rebooted yet again. It kept rebooting each time. I then remembered that this might be because of a STOP error occurring that is triggering the reboot. I pressed `F8` right before boot up and chose the `Disable Automatic Restart on System Failure` option. As I expected, I got the "Blue Screen of Death" (BSOD) error message:

    STOP: c000021a {Fatal System Error}
    
    The windows Logon Process system process terminated unexpectedly with a status of 0xc0000139 (0x00000000 0x00000000). The system has been shut down.

Luckily, I had a laptop around so I was able to search about the problem on the Internet. However, I wasn't able to find anything related. I found an Microsoft support article about troubleshooting this kind of error, but it was unrelated. It talked about the STOP error occurring during normal operations of the system.

I knew the "Windows Logon Process" corresponds to `winlogon.exe`, so I wanted to find out what the status `0xc0000139` meant. I searched in the XP Windows DDK files and found this:

{% highlight c %}
// The procedure entry point %hs could not be located in the dynamic link library %hs.
#define STATUS_ENTRYPOINT_NOT_FOUND      ((NTSTATUS)0xC0000139L)
{% endhighlight %}

Hmm; interesting. So, what I understood from this status code was that `winlogon.exe` isn't able to load because some entry point wasn't found in one of its dependent DLLs. In order to find out the details, I needed a way to get access to my hard disk and run some tools. Eventually, I found out about this really useful tool: BartPE which creates a bootable Windows system on a CD. What's really cool about this tool is that you can boot into Windows from the CD and have a complete functioning Windows environment, where you can perform maintenance tasks, run applications, access the NTFS/FAT hard disk, and more.

With BartPE, I was able to boot into a working Windows system and have complete access to my hard disk. Then, I used the "depends" tool to get the DLL dependencies of `winlogon.exe`. I then compared that to the dependencies of a working XP installation (I used the system32 windows files in BartPE itself as reference, since it's technically a "working XP installation". Eventually, I found out that the difference was in the following two files:

    oleaut32.dll
    olepro32.dll

Those files were using an entry point in `msvcrt.dll` called `strcat_s` that doesn't exist. It looked like `oleaut32.dll` and `olepro32.dll` failing to load caused `winlogon.exe` to fail to load. It looked like they were for Vista since their version number matched the versioning scheme on Vista. I have no clue how those files got replaced. Maybe a bad update?

Anyways, after replacing those files with the ones from my WinXP installation CD and rebooted, my system started successfully! After wasting around 6 hours trying to solve this, at the end it's quite relieving to know that the time spent didn't end up being wasted for nothing.

