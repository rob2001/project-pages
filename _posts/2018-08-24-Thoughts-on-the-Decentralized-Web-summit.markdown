---
layout:     post
title:      Thoughts on the Decentralized Web Conference
author:     Robert Smith
tags:       decentralized web dat gnunet
category:   decentralized
---

The [Decentralized Web Summit](https://decentralizedweb.net/) was earlier this month, courtesy of the
wonderful people at the Internet Archive. Although this was a two-day
event, I unfortunately was only able to attend day one. Still, I got a lot
out of the workshops and talks I was able to attend.

Two projects that stood out front and center at the Summit were
the [Interplanetary File System](https://ipfs.io/) project (IPFS for short) and
the [Beaker Browser](https://beakerbrowser.com/), which is built on top of the
[Dat Protocol](https://datproject.org/). Both projects have similar goals, to
decentralize the web by turning web hosting into a peer-to-peer technology.

## Technical Details

I spent the most time talking to the Beaker team, specifically [Paul Frazee](https://pfrazee.hashbase.io/),
who was kind enough to answer my questions about the protocol. Dat was originally
made to facilite the sharing of large datasets. Each file is broken into chunks
which are sent to peers who can then send the file chunks to others and so on.
Updates are recorded in an append-only log, which allows the owner of a Dat archive
to push changes to connected peers. The log records the changed files and contains
the hashes of the new files for verifiation. While the hashes of old files are stored
permanently in the log, by default clients do not store old versions of files.
While anyone can act as a peer, only the owner can update the Dat by signing
changes with their private key. Dats are addressed via dat://*PUBlICKEY*/file-in-archive.example

IPFS has similar goals, however chooses to represent all files in a universal merkle tree.
Similarly to git, updates can be written as diffs, meaning that a file does not have to be
completely reuploaded just to change a single line. However, unlike Dat, there
is no built-in address that can track the changes made to a (group of) file(s). Git solves
this by having *branches* and *tags* that point to specific commits and can be
changed by users over time. IPFS has their own solution, IPNS, which has been
been somewhat controversial and might be covered in a future post.

## Thoughts

Both projects look polished, and they represent slightly different approaches
to the same problem. The most noticible change from the current web is the
complete removal of servers. This has consequences for any mobile app that
needs to "phone home" to store data, however it isn't a problem for the small
personal sites that dominate the decentralized web today.

One result of this is that you can't send someone a "friend request"
through a Dat site - there's no server to receive your message! Instead,
you need to hope that someone has posted their contact information on their
site, so that you can communicate with them. However, once you have exchanged
Dat or IPNS addresses, you will be able to follow each other's pages and check
for updates.

I think that this is worth thinking about a bit more.
All code must be executed on client devices that cannot comnumicae with each
other. Let's consider a social application. One common use case is to inform
users when one of their friends has made a post, or status update, or something
similar. Currently, centralized servers collect all activity, and can send end
users notifications when new activity occurs. However in the Dat/IPFS ecosystem,
each end user must continually poll for changes in a friend's archive. To make
matters worse, since each person has their own file archive, a user with fifty friends
needs to poll fifty different Archives for updates. This results in a huge
increase of social traffic, and possible a non-negligible effect on the battery
of a cell phone.

## Alternatives

One alternative that I didn't see mentioned that often at the conference was
[Gnunet](https://gnunet.org/). While currently unfinished, I think that the
gnunet team has conpelling answers to the communication problem that I've
mentioned above. Similar to IPFS, Gnunet can host content-addressed files and
directories which can be distributed over a large network for higher
availability. Furthermore, Gnunet is designed to be usuable over the existing
internet, but also over ad-hoc mesh networks without global internet access.
What makes it different is that it allows for messages to be delivered to users
(who are identified via aliases) even if they aren't online. Peers with extra
storage capacity hold messages until peers rejoin the network. In addition, the
claim to have an efficient multicasting strategy to reduce the number of
duplicate massages sent. Hopefully this tech continues to mature over the next
few years so that it can be a reasonable alternative to the existing
centralized internet.
