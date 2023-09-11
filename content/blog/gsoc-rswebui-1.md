---
title: "GSoC’23 : Implementation of Web Interface of Retroshare"
date: 2023-08-09T13:58:16+05:30
description: "No Description"
---

Hello folks 👋
<br/>
My proposal has been selected in GSoC by Freifunk for the implementation of Web
Interface of Retroshare, and I am going to write a bit about it.

> This is a mirror of the [post](https://blog.freifunk.net/2023/05/22/gsoc23-implementation-of-webui-of-retroshare/) which I wrote recently on Freifunk.

## Project Context

[RetroShare](https://github.com/Retroshare/Retroshare) provides a decentralized, encrypted connection with maximum security
between nodes where they can chat, share files, mail, etc. It uses GXS (Generic
eXchange System) that provides asynchronous distribution, authentication,
privacy, security of generic data. RetroShare is a C++ software program that
comprises a headless lib called libretroshare. And, this lib helps in making a
headless server (retroshare-service), a standalone app with a user interface
built using Qt, an android client and more.

Moreover, a web interface has started being developed that allows users to
control the headless server from their web browsers. The web interface uses an
automatically generated JSON API. And, It includes all necessary functions to
send and receive data from the software, communicating with libretroshare.

## Goals and Deliverables

![retroshare-webui](https://blog.freifunk.net/wp-content/uploads/2023/05/Retroshare-1-1536x841.png)
This is the homepage of Retroshare’s web interface.

The previous GSoC contributors have accomplished [astonishing work](https://blog.freifunk.net/2022/09/06/completing-the-retroshare-web-interface-gsoc22-final-report/) on the WebUI,
yet there remain many functionalities to implement and bugs to fix. This summer,
I intend to implement some of the most important features and make the design
more appealing and user-friendly as well.

The main deliverables during the GSoC period will be :

- Config Section
  - Implement the panels which have not yet been implemented from the Qt
    application.
  - Enhance the already existing panels and fix the existing inconsistencies.
- Mail Section
  - Implement the Reply, Reply All and Forward feature in the mail view.
  - Fix the Compose Mail popup and make it usable.
- Forums Section
  - Implement the remaining features from the Qt app in the forum section.
  - Implement a better layout of the forum and posts view, comment and reply
    feature etc.
- Boards and Channel Section
  - Implement the remaining features and make them more user-friendly and easy
    to use.
- Implement a feature for Configuring and Visualizing own shared files with
  features such as managing shared directories, user permissions etc.

## Previous Contributions

During and before the community bonding period, I contributed and added features
for the implementation of webui of retroshare. And, The most recent contribution
I did was the implementation of file search in Files section, which wouldn’t
have been possible without the help of my mentor [Cyril Soler](https://github.com/csoler).

I have also implemented various other features such as Attachment view for Mail
section to view all the mail attachments in one place, improving the sidebar
etc. Likewise, I have also tried to reduce the overall size of the WebUI by
minifying the files. The PRs I raised until now can be seen [here](https://github.com/RetroShare/RSNewWebUI/pulls?q=is%3Apr+author%3Azelfroster+).

## What’s Next?

Currently, The community bonding period is going on, and I have made myself a
bit familiar with my mentors and some fellow members. The mentors are really
supportive, and I couldn’t have made it to GSoC without my mentor [Cyril Soler](https://github.com/csoler)
and one more amazing person, [Defnax](https://github.com/defnax). In addition, I actively participate in
weekly meetings where I report my progress, discuss different approaches.

So, for the first phase which is until the midterm evaluation I have planned to
work towards the implementation of the first two features listed in the Goals
and Deliverables section of this blog. It has been an amazing learning
experience, and I am looking forward to achieving more amazing things this
summer with Freifunk and Retroshare!

Thanks for reading and Have a great day 😃
