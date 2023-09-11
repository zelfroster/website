---
title: "GSoC’23 : Implementation of Web Interface of Retroshare - Part 2"
date: 2023-08-10T13:58:18+05:30
description: "No Description"
---

Hello again folks 👋 ,
If this is your first time here, then consider reading [Part 1](https://blog.freifunk.net/2023/05/22/gsoc23-implementation-of-webui-of-retroshare/) of this blog.

> This is a mirror of the [post](https://blog.freifunk.net/2023/07/08/gsoc23-implementation-of-web-interface-of-retroshare-part-2/) which I wrote recently on Freifunk.

Now, let’s continue.
The first phase of GSoC has been amazing, up until now. I was able to implement
a lot of features, fixed bugs and issues, faced difficulties, got stuck and
learned a lot. I am going to discuss my journey so far, so buckle up your seat
belts.

## Progress on the WebUI

I have been able to improve the Web Interface of Retroshare very much in terms
of usability and a better UI. All thanks to my mentors and the community
members.

![Retroshare HomePage](https://blog.freifunk.net/wp-content/uploads/2023/07/Retroshare2-1536x841.png)
Here is what the homepage looks right now.

### File Search feature

During the start of the Coding Period, I was already working on implementing the
File Search feature, so naturally It was completed in the first week of GSoC
itself. This was a very difficult feature to implement as there were only a few
options on how to do it correctly.

Previously, the file search results data was sent as a response to the request
made to the endpoint `/rsFiles/turtleSearchRequest`. So, I thought of using
[Event Source](https://developer.mozilla.org/en-US/docs/Web/API/EventSource), as It would create a persistent connection to get the data in
stream. But it needed its own auth headers to be used properly. Also, there was
some issue in the format of response coming from the backend, which was causing
webui to crash. I had a discussion upon this with the mentors in the [issue](https://github.com/RetroShare/RSNewWebUI/issues/73) I
created on GitHub.

Later the mentors discussed and decided that It would be better to make the
results of file search as a stream of events which would be then captured at the
frontend side and displayed. As there was already a way to handle events, It was
not much of a problem. But the real issue was to update them in the UI after
capturing them, as I was not sure how to do that in Mithril.js, and this was a
perfect opportunity to learn something new.

And after some research, I found out that [Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) in JavaScript can be used to
check for any change in the objects made using the handler defined in
`eventQueue`. And, then I could manually trigger a re-render using `m.redraw()` in
mithril.js to update the results in the UI.

```js
// Custom Proxy code
const createArrayProxy = (arr, onChange) => {
  return new Proxy(arr, {
    set: (target, property, value, reciever) => {
      const success = Reflect.set(target, property, value, reciever);
      if (success && onChange) {
        onChange();
      }
      return success;
    },
  });
};

const createProxy = (obj, onChange) => {
  return new Proxy(obj, {
    get: (target, property, reciever) => {
      const value = Reflect.get(target, property, reciever);
      return typeof value === "object" && value !== null
        ? Array.isArray(value)
          ? createArrayProxy(value, onChange)
          : createProxy(value, onChange)
        : value;
    },
    set: (target, property, value, reciever) => {
      const success = Reflect.set(target, property, value, reciever);
      if (success && onChange) {
        onChange();
      }
      return success;
    },
  });
};

const proxyObj = createProxy({}, () => {
  m.redraw();
});
```

So, after some head banging and googling, I was able to implement this feature.
Furthermore, I improved the small issues in next iterations. You can see the
merged PR [here](https://github.com/RetroShare/RSNewWebUI/pull/74).

![RetroShare File Search](https://blog.freifunk.net/wp-content/uploads/2023/07/image-8-1536x841.png)
This is how the File Search looks currently.

### Config Mail

After that, I started working on the config section, in which I implemented the
feature to create and manage custom tags for mails in the mail config. The PR I
raised is [here](https://github.com/RetroShare/RSNewWebUI/pull/75).

![RetroShare Config Mail](https://blog.freifunk.net/wp-content/uploads/2023/07/image-9-1536x841.png)

### Config Network

Then, I implemented some missing features in existing section of Config section.
In the Network config, some options weren’t working. So, after discussing with
my mentor, I implemented the Hidden Network Configuration for TOR/I2P Socks
Proxy [here](https://github.com/RetroShare/RSNewWebUI/pull/76).

![RetroShare Config Network](https://blog.freifunk.net/wp-content/uploads/2023/07/image-10-1536x841.png)

### Config Files

I implemented the missing options as well as fixed the options which were not
working in the config files section also for this, I implemented the
`getQueueSize()` function in libretroshare.

![RetroShare Config Files](https://blog.freifunk.net/wp-content/uploads/2023/07/image-12-1024x560.png)

By this time, I was also getting a hang of How things were working internally in
the [libretroshare](https://github.com/RetroShare/libretroshare). And, my mentor [Cyril Soler](https://github.com/csoler) motivated me and supported me to
start writing code in libretroshare for Doxygen to generate the JSON API for the
required endpoint. I raised three PRs in total, where I also implemented an
endpoint in the actual `C++` code.

Honestly, this was more satisfying to be able to do this rather than writing
code for the webui. You can view all of my libretroshare PRs [here](https://github.com/RetroShare/libretroshare/pulls?q=is%3Apr+author%3Azelfroster+is%3Aclosed).

### Fix UI of whole Interface

This was a very big task but didn’t take that long, I did it gradually in small
bits. Improved the whole UI of the web interface, and it looks much better now.
See all the changes made in this PR [here](https://github.com/RetroShare/RSNewWebUI/pull/77).
I would not include any screenshots here as It would be too much.

### Fix working and UI of mail Composer

Of all the features I have implemented so far, none of this were this confusing
where I was fighting with the code. I was stuck trying this on my own for two
days, since the code I wrote was fine on its own. But, there was something which
was causing an issue, and I was not able to understand what it was. So finally,
I asked for help from a community member, [M. Saud](https://github.com/rottencandy). He is also the code reviewer
of all of my PRs, since as far as I know he is the only JS dev in RSWebUI team.

He found the issue and told me some ways It could be done. Those seemed too
complex to me, I read some mithril.js docs and tried to figure out ways to do
it. And In the end, I found a very easy way to do it. You can read the
discussion [here](https://github.com/RetroShare/RSNewWebUI/pull/77#issuecomment-1614640284) on GitHub.

![Retroshare Mail Composer](https://blog.freifunk.net/wp-content/uploads/2023/07/image-11-1024x560.png)
This is how the mail composer looks.

This PR is related to the mail reply as well, so this is still in the Draft
version, And I am currently working on it to implement the features. You can see
it [here](https://github.com/RetroShare/RSNewWebUI/pull/80). Other than this, I have been doing some minor fixes and refactoring in
the whole webui along with completing the major goals in the timeline.

So, this is the progress made in the WebUI until now. And, I have learned and still learning many new things while working on it.

## What's Next?

First, I will finish the [PR#80](https://github.com/RetroShare/RSNewWebUI/pull/80) where I have to implement the Reply feature in
the Mail Section, and then will work on the next set of goals as mentioned in
the timeline which are :

- Forums Section
  - Implement the remaining features from the Qt app in the forum section.
  - Implement a better layout of the forum and posts view, comment and reply feature etc.
- Boards and Channel Section
  - Implement the remaining features and make them more user-friendly and easy to use.
- Implement a feature for Configuring and Visualizing own shared files with features such as managing shared directories, user permissions etc.

Apart from these goals, I have also discussed with my mentor to work on more
important issues and necessary features for the upcoming release of the webui.

Now, I will see you in the next and final blog of this GSoC series.

Thanks for reading and have a great day : )
