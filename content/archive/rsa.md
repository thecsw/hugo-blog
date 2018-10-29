---
title: "RSA: Encrypting, Decrypting, Hacking"
date: 2018-08-23T20:41:53-05:00
---

### Click here to open the full paper [rsa.pdf](rsa.pdf)

Introduction
============

First time when I heard about RSA technique, was during the ITGS class
in IB course. In ITGS Course Companion[@itgs] there is a chapter about
Security and Secret Key Encryptions. As an example, the author included
two cases of encryption: Symmetric Key Encryption or Single Key
Encryption and Asymmetric key encryption, more known as Public Key
Encryption.

During the lesson, the fact that a message can be encrypted by one key
and only a second key can decrypt the message intrigued me. After that,
I did some research on asymmetric encryptions, particularly about RSA
and other cryptographic technique based on it. I found that RSA is not
only used for messages encryption, but also for signing online
certificates to prove one's identity. I chose this topic for my Extended
Essay because I believe the Mathematics in the algorithm is simple and
elegant; also, it is safe to say that RSA is used everywhere and the
Internet trust relies on this algorithm.

RSA encryption algorithm is essential if not the most critical security
algorithm today, as nearly every system in the world uses this
asymmetric encryption technique to encrypt and decrypt data. In this EE,
I will be researching the methods of RSA: the way the algorithm works,
why it is considered secure, where and how it is used, mathematical
proof with examples and ways to break or brute-force the algorithm.

Historical background
=====================

Ever since people began to write down events or private information,
there has been a need for cryptography. Cryptography is a study of
techniques of encrypting a text in such a manner that outsiders to the
code cannot understand the contents, but the desired reader can decrypt
and read the message in its original form. Just like for an early man
and modern man, there always has been a need for secrecy.

Caesar Cypher
-------------

First records of known cryptographic techniques go back to the times
that were Before the Common Era, in the times Julius Caesar. Caesar
cypher or Caesar's code is one the first methods of encrypting texts. It
works in a way that there are a text and a key, where the key is an
integer value.

The key shows a shift of letters in the document according to the Latin
alphabet. For example, if the key is two, then the first letter of the
alphabet will become third, the second will become forth and so on.
During his lifetime, Julius Caesar mostly used three as a shift to
protect messages of military significance.[@singh]

Enigma Machine
--------------

We can say for sure that the moment, when encryption was the tool of
secretly transmitting data so important and valuable that lives of
thousands of people depended on how well that information is transferred
from one end to another, is World War II.

Enigma machine was the German perfection of cryptography and
engineering, the device so small and so complex, that it produced code,
which was considered as impossible to crack. However, during the war, a
brilliant mathematician and cryptographer Alan Turing found a flaw in
Enigma Machine and was able to build the first computer to exploit the
system's vulnerability[@enigma].

Flaw in Symmetric Cryptography
------------------------------

All existing algorithms had one most significant vulnerability in all of
them- both ends should have known the key or secret passphrase, which is
used to encrypt and decrypt messages. In the example with Enigma
machine, German radio operators had a book with Enigma codes for the
next month, and it was a massive risk if hostile troops possess the
codes.

Whitfield Diffie and Martin Hellman
-----------------------------------

The first attempt at solving the problem of symmetric algorithms goes
back to a pair of cryptologists: Whitfield Diffie and Martin Hellman. In
the book by Simon Singh [@singh], there is a story about how these
cryptographers came up with the idea of a public-key encryption: "I
walked downstairs to get a Coke, and almost forgot about the idea. I
remembered that I'd been thinking about something interesting, but
couldn't quite recall what it was. Then it came back in a real
adrenaline rush of excitement. I was aware for the first time in my work
on cryptography of having discovered something really valuable."

They have discovered a revolutionary type of cyphering -- asymmetric
cryptography. This means that it solved the problem of single key
encryption, where encoder and decoder needed to know the passphrase.
Unfortunately, they did not find a one-way function for solving the
problem, they have published the concept in 1976 and left it open.

Rivest, Shamir, and Adleman
---------------------------

The paper released by Whitfield Diffie and Martin Hellman showed that
there was a solution for the problem of symmetric encryption in the form
of a one-way function. Another trio of researchers made the actual
discovery and proof: Ron Rivest, Adi Shamir, and Leonard Adleman.
Rivest, Shamir, and Adleman were a perfect team, as Rivest was a
computer scientist, who was tracking all the latest scientific papers
and with an ability to implement something new in new places. Shamir is
also a computer scientist with a lightning intellect and ability to
directly focus on the core of the problem. Adleman was a mathematician
with broad knowledge and patience, so during the research, he was
finding flaws in the works of Rivest and Shamir, and ensured that
cryptographers did not follow a false lead.[@singh]

A year later Ron Rivest with the help of Adi Shamir and Leonard Adleman
has made a breakthrough by finding the desired one-way function, thus
solving the problem of symmetric encryptions. In 1977, the trio
published a full paper about the new asymmetric encryption technique,
which was named after its creators- R.S.A.[@rsapaper]


The Usage of RSA 
================

As an algorithm and cryptographic technique, RSA is brilliant without a
doubt. It is safe to say that RSA and its versions are used everywhere
in our digital world. It is crucial for modern cryptography techniques
to be sophisticated for computers to brute-force but not too complicated
and inefficient for computers to encrypt and decrypt data. RSA is
located right in the middle, as the operations performed in part
[4](#sec:math){reference-type="ref" reference="sec:math"} do not need a
lot of computational power but to attack it requires a lot of it. For
more information please refer to part
[6](#sec:security){reference-type="ref" reference="sec:security"}

To demonstrate the work and the functionalities of the algorithm, three
types of cryptography techniques will be displayed: single key
encryption, assymetric encryption and certificate signatures.

Symmetric Encryption
--------------------

This type of encrypting and decrypting algorithms is the oldest way to
cypher data. It works with one key, one text and two ends. On the first
end, there is an encoder, who cyphers the text with a known key and then
sends the encrypted data to the other end, decoder, who later decrypts
text with the same key. The example with Blowfish[@blowfish] algorithm
with key "jeopardize" can be seen below in Figure
[\[fig:symmetric\]](#fig:symmetric){reference-type="ref"
reference="fig:symmetric"}.

![Example of Symmetric
Encryption[]{label="fig:symmetric"}](symmetric.png "fig:"){#fig:symmetric
width="\textwidth"}1

The downside is that both ends of the transmission should know the
shared key. In the scenario where people have met and shared the
encryption key in real life, there is no danger that someone can steal
the shared key and decrypt transmissions. The problem arises when we
have a scenario where parties on both ends never talked with each other
and are located on distinct physical locations. Both ends want to
transmit data securely, so the eavesdropper in the middle will not
understand the contents of the transmitted information.

In this scenario, it is impossible to transmit data securely, because to
decrypt text messages, both ends should know the same key. Before the
conversation, one end should send the key to the other end; however, the
eavesdropper will be able to \"sniff\" the key and will be able to
understand all further encrypted transmissions, thus compromising all
further interactions.

Asymmetric Encryption 
---------------------

Asymmetric encryption relies on two distinct keys, where one is used for
encrypting data and the second one is for decrypting data that was
decoded by its unique pair. Keys for encrypting and decrypting are
called public and private, respectively. There are two ways of using
RSA: to send an encrypted message to the decoder and signing
certificates for proving one's identity.

### Encrypting Messages 

Every user has a pair of connected keys: a public key and private key.
The public key is available to everyone while the private key should be
kept private to the owner of the unique pair of keys. It is a preferred
way of encryption; because both ends do not need to exchange the secret
key, they would already know the required part of the pair to transmit
messages securely. Continuing from part
[3.2](#bsec:asymmetric){reference-type="ref"
reference="bsec:asymmetric"}, this is widely used for secure data
transmissions.


### Click here to open the full paper [rsa.pdf](rsa.pdf)