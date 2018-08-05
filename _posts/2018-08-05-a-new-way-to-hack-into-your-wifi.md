---
layout: post
title: A New Way To Hack Into Your Wi-Fi
---

About 8 hours ago, a branch new way of attacking Wi-Fi networks was discovered and [published on the Hashcat forums](https://hashcat.net/forum/thread-7717.html). It describes a "new technique to crack WPA PSK passwords". But what does this actually mean? Here is my attempt to understand why this is important.

WPA stands for Wi-Fi Protected Access and is widely used security protocol developed to keep Wi-Fi networks secure. WPA2 replaced it, and in January 2018 WPA3 was released. The WPA standard requires a Primary Master Key (PMK) to authenticate supplicants (clients wanting to connect).

The PMKID is calculated using [HMAC](https://en.wikipedia.org/wiki/HMAC) where the key is the PMK and the message to be authenticated is a concatenation of the label PMK name (a fixed-length string), the [MAC](https://en.wikipedia.org/wiki/MAC_address) address of the access point and the MAC address of the supplicant.

{% highlight python %}
PMKID = HMAC-SHA1-128(PMK, "PMK Name" | MAC_AP | MAC_STA)
{% endhighlight %}

As the PMK is essentially a hash of the WPA2 password, and the PMKID is a hash of a hash, we can attack it the same way we can attack any other hash. 

The issue with bruteforcing Wi-Fi passwords is that each Wi-Fi event takes too long. So what we can do is send a deauthentication signal a legitimate client, who already has the WPA2 password. When they try to reconnect (this will happen automatically) you can capture the 4-way handshake and brute force that offline. But we already knew that, so how does this differ from the status quo?

Only now, you don't need to do the de-auth and capture the handshake. The PMKID is right there.

Using a tool called hcxdumptool to capture packets, we can request the PMKID from the AP.
We can retrieve the
- PMKID
- MAC AP
- MAC Station
- ESSID

Attack the hash. Find the PMK.

It's so simple, I'm surprised nobody thought of it earlier!

