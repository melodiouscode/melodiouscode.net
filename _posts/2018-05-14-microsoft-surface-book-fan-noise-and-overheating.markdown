---
layout: post
title: Microsoft Surface Book fan noise and overheating
date: '2018-05-14 08:00:00'
image: /images/posts/hush-naidoo-595895-unsplash-min.jpg
tags:
- microsoft
- tutorial
---

My work laptop is a first-generation Microsoft Surface Book (the 8GB model); it is by far the best laptop that I have worked with (both personal and professional). Granted there are better devices out there (a few Lenovo models come to mind) but I can't afford them and my employer is unlikely to authorise them (getting the surface book required a guilt trip!).

Other than the first SB that I had suffering death within a few months (horrid grating fan noises, followed by a replacement) I have not had a single problem that wasn't related to configuration or an old application not supporting HDPI screens. My employer's system team can be a little slow at pushing out Windows Updates via WSUS (machines are blocked from accessing the internet variant of Windows Update); since the last "big lump of updates" my device received (I am guessing it included the last Win10 version update) the SBs fan noise has gone through the roof! Within minutes of turning the machine on (without even opening a program) the fans would be screaming along like they were cooling a data centre, and the back of the screen (where all the bits are) would get hot to the touch. After some google based research (and tying a few sets of instructions together) I have found what appears to be a solution!

#Shutting up the fans, and keeping a surface book cool!
In their infinite wisdom Microsoft decided to teach Windows 10 that a device in the "Surface Family" is, in fact, a tablet computer (yes they can undock but they are largely used as laptops); to me this is silly. This includes a feature called "Connected Standby" which allows the machine to run in a low power state responding to the "on button" in much the same way as a smartphone or tablet. There are both plus and negative points to "Connected Standby"; one of the negatives being you lose access to all the normal Windows Power Management features (such as hibernate or sleeping). 

## Step 1: Disable Connected Standby
Disabling "Connected Standby" (CS for short) is as simple as flipping one flag in the registry.

***This is a semi-technical article so I will not go into the perils of messing with the Windows Registry; if you are not comfortable in the registry please ask someone who is for assistance. You have been warned.***
1. Start the registry editor (regedit.exe)
2. Locate the node "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power"
3. Set the key "CsEnabled" to 0 (zero).
4. Reboot

## Step 2: Less is more
The SB is rather powerful for a low profile "2in1" machine; the problem here being that CPUs generate a lot of heat and that heat has nowhere to go inside the case. This means that the small fans inside the "screen case" have to run at insane speeds to force the hot air out of the sides.
When the SB gets too hot (and the fans can't cool it down fast enough) the processor is put into "thermal throttling"; in simple terms it has it's maximum speed lowered to prevent damage from excess heat. This means that things take longer to process causing the heat buildup to last longer (the processor takes longer to return to an idle state).

Preventing the processor from getting into the "thermal throttling range" in the first place prevents the artificial slowdown. Many people will know what "overclocking" is, to deal with this problem we are going to use "underclocking". Now wipe the shocked look off your face, lowering the maximum speed of the processor to prevent thermal throttling will actually give you a net gain in overall average speed! The game we will play here is finding that sweet spot which is low enough to prevent overheating but not so low that we notice the difference. I have found that 90% CPU is about the sweet spot.
### How to under-clock the processor

You could use some complicated CPU Voltage management software (Intel provide a program for the SBs CPU), or you could play a less dangerous game and just use the Windows Power Configuration Manager that we unlocked by disabling "Connected Standby" earlier.
1. Right click on the battery icon in your task tray
2. Select Power Options
3. Depending on which power plan you have set, select "Change plan settings" alongside the active plan
4. Click "Change advanced power settings"
5. Navigate to "Processor power management > Maximum processor state" and set both options to no higher than 90%

Done, you have prevented the processor from reaching critical thermal levels. Before someone comments about it, I am aware this is not true underclocking but it has had the same effect.

Keep an eye on your CPU Temperature using a tool such as SpeedFan and adjust the percentage as necessary over the next few days until you find your devices sweet spot (all physical machines are slightly different, depending on what you do and how well it was put together!).

<small>The header image for this post was provided for free by [Hush Naidoo (@hush52)](https://unsplash.com/@hush52) via [unsplash.com](https://unsplash.com). Thanks Hush!</small>