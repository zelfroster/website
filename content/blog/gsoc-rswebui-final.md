---
title: "GSoC’23: Implementation of Web Interface of Retroshare – Final Report"
date: 2023-09-11T09:13:43+05:30
description: "This blog contains the details of the work I have done during Google Summer of Code 2023"
---

> This is a mirror of the [final report](https://blog.freifunk.net/2023/08/27/gsoc23-implementation-of-web-interface-of-retroshare-final-report/) which I wrote recently on Freifunk.

Hello again folks 👋,
<br />
My journey in Google Summer of Code has come to an end, and I am excited to
share all the things I have accomplished during this program and the progress
done in the Implementation of Web Interface of Retroshare.

![Retroshare Homepage](https://blog.freifunk.net/wp-content/uploads/2023/08/image-4-1536x762.png)

## Project Description

### About Retroshare

Retroshare provides a decentralized, encrypted connection with maximum security
between nodes where they can chat, share files, mail, etc. It uses GXS (Generic
eXchange System) that provides asynchronous distribution, authentication,
privacy, security of generic data. It is designed to provide maximum security
and anonymity to its users beyond direct friends. Likewise, it is entirely free
and open-source software.

It is a C++ software program that comprises a headless lib called libretroshare.
And, this lib helps in making a headless server (retroshare-service), a
standalone app with a user interface built using Qt, an android client and more.

### Project Goal

The main goal of my project was Implementation of Web Interface of Retroshare in
which I had to improve the Web UI and add missing features from the Qt
counterpart of Retroshare. The milestones which I had to achieve during GSoC are
described below.

## Milestones Achieved

> You can view all of my contributions at once – [GitHub Link](https://github.com/RetroShare/RSNewWebUI/pulls?q=+is%3Apr+author%3Azelfroster+).

### File Section

- Implemented [File Search](https://github.com/RetroShare/RSNewWebUI/pull/74) feature using JavaScript Proxy which was pending from a long time.

  ![Retroshare File Search](https://blog.freifunk.net/wp-content/uploads/2023/08/image-10-1536x762.png)

- Implemented [feature](https://github.com/RetroShare/RSNewWebUI/pull/82) to view which chunks are getting downloaded in the
  progress bar and the state of the chunks getting downloaded. Also, fixed the
  Download action buttons and implemented the feature to manage the chunk
  strategy for a file getting downloaded.

  ![Retroshare File Download](https://blog.freifunk.net/wp-content/uploads/2023/08/image-12-1536x762.png)

- Implemented the [Share Manager](https://github.com/RetroShare/RSNewWebUI/pull/84) feature, which lets you add and manage the
  shared directories and manage different level of access and permissions for
  each directory. It is in progress and will be complete soon.

  ![RetroShare Share Manager](https://blog.freifunk.net/wp-content/uploads/2023/08/image-13-1536x762.png)

### Config Section

- Implemented the [mail config](https://github.com/RetroShare/RSNewWebUI/pull/75) panel to create and manage all the mail tags.

  ![RetroShare Mail Config](https://blog.freifunk.net/wp-content/uploads/2023/08/image-16-1536x762.png)

- Implemented [features](https://github.com/RetroShare/RSNewWebUI/pull/76) to set Dynamic DNS and configure Tor/I2P Socks Proxy from
  Web UI and fixed NAT and some other existing options in the network config
  section.

  ![RetroShare Network Config](https://blog.freifunk.net/wp-content/uploads/2023/08/image-15-1536x762.png)

- [Added](https://github.com/RetroShare/RSNewWebUI/pull/78) more missing options in files config section from Qt app.

### Mail Section

- [Improved](https://github.com/RetroShare/RSNewWebUI/pull/80) and made the mail composer reusable to help user to search and select
  the nodes (contacts) and improved the UI of composer.

  ![RetroShare Mail Composer](https://blog.freifunk.net/wp-content/uploads/2023/08/image-18-1536x762.png)

- Implemented [feature](https://github.com/RetroShare/RSNewWebUI/pull/80#issuecomment-1639544317) to reply to any mail from Web UI by reusing the mail
  composer.

- Implemented [feature](https://github.com/RetroShare/RSNewWebUI/pull/72) to view all the Attachments in one place and also to view
  the attachments sent in a mail.

  ![RetroShare Mail Attachments](https://blog.freifunk.net/wp-content/uploads/2023/08/image-19-1536x762.png)

- [Fixed](https://github.com/RetroShare/RSNewWebUI/pull/80#issuecomment-1639544317) mail view and the order of mail in all mail sections.

### Forums Section

- [Implemented](https://github.com/RetroShare/RSNewWebUI/pull/83) Caching in Forums section to reduce repeated numerous API calls
  and reuse the already fetched data and invalidate the cache and refetch the
  data again. It is also a WIP.
- Fixed the bug which was causing infinite calls to the same endpoint and
  freezing or crashing the Web UI.

I also improved the whole User Interface of the Web UI and made it more
user-friendly. Furthermore, I [refactored](https://github.com/RetroShare/RSNewWebUI/pull/85) the directory structure, tidied up the
repository and optimized the build.

## Other Contributions

Apart from the contributions in the Web UI, I also contributed to the
libretroshare where I

- [Added code](https://github.com/RetroShare/libretroshare/pull/100) to generate the jsonapi endpoints for the file section and [other
  sections](https://github.com/RetroShare/libretroshare/pull/98) in Web UI.
- [Implemented](https://github.com/RetroShare/libretroshare/pull/103) `getChunkStrategy()` endpoint in the libretroshare in `C++` and also
  added more code to generate other API endpoints.
- [Fixed](https://github.com/RetroShare/libretroshare/pull/113) MIME type for content-type in HTTP header and added routes for new
  directory structure.

## What’s Next?

The Web Interface of Retroshare has improved so much since I have undertaken
this project, and It’s almost ready for release in the next release cycle of
Retroshare. Still, there is a lot of room for improvement on the Web UI and I
will keep adding more features in it.
I will complete all the features which are currently in progress and even after
GSoC I would love to keep contributing and improving this truly wonderful open
sourced project created solely for the welfare of society.

## Wrapping Up

My journey in GSoC with Retroshare has been an incredible learning experience
for me. I got to learn so much all thanks to my mentor [Cyril Soler](https://github.com/csoler), [M. Saud](https://github.com/rottencandy) and
fellow community members. GSoC has bridged the gap between aspiring open source
contributors and industry level experts and has enabled folks like me to gain
experience by working on enterprise level projects under the guidance of
wonderful people.

This summer has turned out to be a pivotal point in my career and has boosted my
confidence and helped me to strengthen my arsenal by learning new skills,
gaining hands-on experience and improving my programming skills.

As I keep moving forward in my coding journey after this project, I’m excited to
utilize the knowledge and experience I’ve gained here in future projects. I plan
to stay engaged in this community after GSoC and My aim is to continue
contributing actively to the project’s growth and achievements.

And, I will see you now in the next blog. Until then, Good Bye : )
