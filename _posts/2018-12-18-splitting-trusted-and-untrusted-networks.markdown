---
layout: post
title: Splitting trusted and untrusted networks
date: '2018-12-18 10:50:12'
image: /images/posts/thomas-jensen-740972-unsplash-min.jpg
tags:
- security
- tutorial
- network
---

There have been a number of articles in the press in the last year about Internet of Things (IOT) devices being hacked and forming parts of botnets, or just exposing data from the networks they sit on. Most users just pick up a device and type in their wireless password or plug in a network cable; being the IT Professional (ha !) that I am I decided it was time to look into network segmentation.

For those reading who do not understand what this is: the two basic categories are Trusted and Untrusted devices; I trust my personal laptop and my server (I manage their security after all), the IOT thermostat and the bargain price CCTV system I bought years back, however, are a different story. So they need to be in seperate secured areas of my home network.

Following some guides from [Troy Hunt](https://troyhunt.com) and other [Ubiquiti fans](https://community.ubnt.com/t5/custom/page/page-id/Forums), I have succeeded in splitting these two sets of network clients using my [Ubiquiti](https://www.ubnt.com/) [Unified Security Gateway (USG)](https://www.ubnt.com/unifi-routing/usg/). The following is a rough guide to separating your networks using Ubiquiti equipment with an optional step of creating a captive guest wifi portal for visitors. I am sure that other network equipment manufacturers provide the ability to layout a network in this way, but I do not have their hardware to test!

## 1. Create a VLAN for the untrusted network
A VLAN separates the network into virtual segments which can be controlled by the firewall in the USG. Access the network settings via settings > networks, and create a new network. Choose a network name such as "Untrust VLAN" setup as a corporate network with a VLAN ID and IP Range of your choosing.
![ubnt-untrust](/images/content/ubnt-untrust.png)
## 2. Create a new wireless network for the new Untrusted VLAN.
The Ubiquiti Access Points (AP) have the ability to run multiple independent wireless networks which can be tied to a VLAN. We are going to use this ability to create a new wireless network which will allocate all clients directly to the untrusted VLAN. Access the wireless settings via settings > wireless networks, and create a new wireless network. Choose a network name and password (for the name I just added UT for Untrusted to my standard network name) and set the network to use the VLAN ID you picked in the previous section.
![ubnt-iot-2](/images/content/ubnt-iot-2.png)
## 3. Ensure the networks are segmented by the firewall
Some simple firewall rules will ensure that clients on the Untrusted VLAN cannot connect to your previous trusted network. Access the firewall settings by navigating to settings > routing & firewall and locate the "LAN IN" section. This section of the firewall controls all access into network segments; although we are technically already inside our network the VLANs act as separate virtual networks. Create a new rule using the settings shown in the following screenshot.
![ubnt-iot-3](/images/content/ubnt-iot-3.png)
You have now successfully separated your potentialy dangerous IOT devices from your trusted personal equipment; well you will have when you move them all over to the new wireless network! I suggest you do this a few devices at a time so as to cope with any glitches in their systems!