---
layout: post
title:  "Fixing wifi woes"
date:   2017-11-02 11:10:02 -0400
categories: self-caused NetworkManager dhcpcd runit
---

## Forface
So after updating I restarted my laptop  get all my running software up date (it had been awhile since I used my laptop), after login I noticed that nm (NetworkManger for those unware) was telling me my laptop was no longer conned to my wifi. 

## Troubleshooting
I first started troubleshooting by stoping the nm service and enabling and starting the wpa_supplicant service (I've used wpa_supplicant by itself in the past, but stopped due to diffilcuties adding networks over something like nm or connman) I noticed that even wpa_supplicant wouldn't stay connected, at this point I suspected something weird was going on, so modified the runit config for wpa_supplicant to enable the debug option so I could get some kind of error to search for and got "no agents were available for this request" which pretty much lead me no where in solving my problem following google searches.

## Finally solving the problem
After hoping on the #voidlinux IRC chat in freenode.net following a bit of detective work by the users there we found that I had the dhcpcd service running at the same time. Appernetly that causes all kinds of issues as the network services fight over connecting until no one wins (least in my head), strangly enough I didn't have a problem with this before I updated and one of the earlier posts I found on the matter go back into 2016 on it, suggesting that it wasn't something new.

## Afterwords
Though I have no clue as to why it worked before the last update I did, it certainly killed my wifi in the process, in the future it seems I should avoid having multiple services running at once, good to know.
