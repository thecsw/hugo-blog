---
title: "Cansec2018"
date: 2018-10-28T22:24:57-05:00
---

This competition was the first actual pentest competition in my
experience. And oh boy, was in fun. This document will shortly describe
the things I did during the competition, mostly to just look at it back
sometime later. \newpage

Initial scenario
================

We are working for the company called Asnea. More precisely, it is some
kind of a military group and we serve around 10 users, who have
different positions in the company and have different access levels on
all physical machines. We had 6 machines:

-   Mail Server (Used for mail, SMTP, POP3, FTP), Arch Linux, SSH.
-   Info Server (Used to host a website, HTTP, HTTPS), Windows XP, RDP.
-   Router (Used as an entry point to the system, messed up), Raspbian,
    SSH/RDP.
-   DB (Used to provide database services, port 443), Ubuntu?, SSH.
-   DNS Server (Never used this one)
-   RFID server (This is just a backdoor for the white team), Raspbian,
    SSH.

We had to keep up the uptime, make the system usable and make all users
be able to actually log in with credentials. With your 10 users, if you
change a password on one of the systems, you should change the passowrd
on all of the systems and then report the new credentials to the white
team so their scripts can login into the system and check its
availability. This is the beginning of the end.

Start of the competition
========================

Ethernet problems
-----------------

This is all going to be my own personal experience and all problems I
had. Okay, my laptop does not have an Ethernet jack, so I had to use the
Ethernet-USB adapter and then actually connect it via wired network.
That was hell. As I use Arch Linux, no GUI, we are text boys. I
connected the ethernet to my laptop after another problem of finding the
ethernet cable (Had to ask the faculty to give me a spare one). I saw
the `enpl20u1` weird network interface and when I tried to
`ifconfig up`, `systemctl start dhcpd.service` and other various
commands, I found out this is not gonna work. At least not now. That is
how I wasted first 20 minutes.

Connecting to wifi
------------------

Connecting to the `Cansec2018` wifi wasn\'t bad.

Connecting to proxy
-------------------

Connecting to the proxy was really bad. I wasn\'t sure why all my
commands with `export http_proxy=address:port` and so on weren\'t
working. I did all the combinations possible: `http`, `https`, `HTTPS`,
`HTTP`, `ftp`, `noproxy` and nothing was working. I was on the network
without internet access. Then, it clicked. It was the crappy proxy
server and script they had. Approximately, 30 minutes wasted.

Login systems
=============

The actual connection to the machines was horrifying. Apparently, when
you `RDP` into the router, only **ONE** concurrent user is allowed.
Everytime somebody logged into our router, it would kick out all other
people. That was fun. And no one could connect to the machines that we
needed to secure. That because of the weird obfuscated thing they had.
If you want to `ssh` into the machines, you should first `ssh` into the
router machine and then `ssh` to all other machines from there.
Obviously, not only the router\'s ssh server and daemon were dead, the
router\'s ssh config files were all messed up. So it was a chain of
actions we needed to take to actually log in. We wasted an extra hour
figuring out why our changes to the ssh config weren\'t working. That
happened because we were modifying the raspberry pi\'s `ssh` instead of
the routers. We should have used `exit` to get to the router. This
sounds super easy, but figuring out the network layout took us more than
an hour. Maybe two.

Actual blueteaming
==================

When we had the network all figured out, we all hopped into our
machines. We were missing 2 team members, so some of us had to take new
things. Jonathan, the anomaly guy, bless his soul. He solved all of
them. I did Mail server (More on that later). Chase was doing info?
server. Dmitri was making the database and DNS magic. Ross was on RFID?
and all of it. Noah was the jack of all trades, but mostly working with
our router and iptable rules.

Mail server
===========

Note
----

I was the last one to actually work on my box as the mail server was
really difficult to get into and I needed to use RDP for that. And our
RDP has a connection limit. Took me a while and more. One more hour
passed.

The structure
-------------

This was the worst system I have ever logged into, ever. It was my
favorite Arch Linux but it was so slow and stripped down. Firstly, all
the users\' passwords were updated on all boxes except mine. But I
couldn\'t change the passwords because the root access was invalid and
someone messed with our `/etc/sudoers` file, as the system yelled at me
due to unprivileged `uid` changes that the file has suffered. Took me
quite a while to regain root access to the system. Before getting the
root access back, I found out that the `/etc/sudoers` file was
read-writable to the world. This was the opps moment. I knew, that if
Red Team knows that, that would be it. But instead, I just added one of
the users I had access to to the `sudoers` file, quickly updated all of
the password on the system and double-checked their integrity with the
white team. After finally getting root back, I fixed the `sudoers` file
to the standard permissions, `/etc/sudoers.d` too. Started working on
the services and on their redeployment.

Also!!! The keys on the bok were remapped. Everytime you press backspace
to delete last character, **IT WAS MAKING A SPACE**. Everytime I tried
using arrowkeys to navigate, **IT WAS GOING SEVERAL COMMANDS UP AND
RUNNING THEM**. That was pure hell. Noah and I tried looking at
`.bashrc`, `/etc/systemd/*`, `/etc/*`, and etc. Nothing was giving us a
hint that Red Team messed with our keymaps ar remapped the keys. I never
solved it. I just lived with it. Executing commands on first try and
pressing `CTRL-C` to abort the current command if I made a syntax error.

The hack
--------

I saw on the dashboard that somebody has stolen our Mail server flag
that was located in the `/root` directory. I was wow. At the end of the
competition they told us that the Mail Server had exposed `ftp` server
that was broadcasting the `/root` directory. So that even by being a
stranger, you can take anything from the system. Then, I noticed that
all the home directories are read-write-executable. Somebody did that.
Wow. I started fixing it with chmod and manual investigation
(`chmod 0644 -R /home`). I found that some users had really suspicious
shell executable that pip all password changes to somewhere and that
they have weird python scripts. I started checking the `.bash_history`
of all the users, but nothing suspicious. I was deleting all the files
and damage controlling the situation for an hour. I filed an incident
report with my explanation of what happened.

Continuation
------------

This kind of game continued to go on for a while as I was rebooting the
machine, tailing logs and just defending the box in general.

The lunch
=========

The organizers called a \"fire drill\". That was caused by the Red Team
hacking the alarm system. We all went out and had a lunch with several
speakers. The Read Team was inside of the our room and the were at our
table, manually checking all our notes, pieces of paper, unlocked
laptops and etc. That was wow. Gladly, our team\'s laptops were all
locked and all our docs were with us.

\"The Great Fall\"
==================

Everything went down. Everything. All teams\' services were down. I
guess white team just flushed all iptables rules with `iptables -F`. No
one could log in and we were in the dark. Noah was trying to debug that
with lots of `iptables` commands. We never recovered. Some teams found a
way, we couldn\'t. Our systems were down until the end of the
competition.

The Return
==========

If our systems are down, the last thing we could do was the incidents
reports. We moved all of our team\'s resources to writing the reports.
That is how we won. We won by exactly 5 points. Out of 1500. **0.33%**.

One of the white team members was yelling that we submitted wrong
reports but because they were legitimate reports, we got some points.

Also, one of our trusted white team contacts was a red shirt. Haha
