---
title: GSoC Evaluations
layout: single
author_profile: true
read_time: true
share: true
related: true
categories: Misc
toc: true
---

My GSoC project was with [Zulip Mobile](http://github.com/zulip/zulip-mobile), which is a cross platform application built with React Native. My project originally centered around developing the features which were missing in the mobile app but present in the web app, as well as certain UX improvements which made the app easier to use. The project then pivoted slightly to include some bug fixes as well as some changes which weren’t outlined in the project proposal.

One thing I should mention, is that I used my community bonding period to code as well, because my university concluded earlier than others and 5th semester started a month before the coding period ended — resulting in less amount of time contributing during that last month of the coding period.

This document is a log of my contributions during that time period!

## PRs / Issues Before GSoC started.

* webViewEventHandlers: Add ability to copy links to Clipboard. [#3404](https://github.com/zulip/zulip-mobile/issues/3404)

  After this implementation, users could long press on a link which appeared in the message list, and that link would be copied straight to the device’s clipboard, essentially saving the user another click to do the same from the Action Sheet presented on a regular long press in the message list.

  During the implementation of this PR another bug was discovered which was related to irregular behavior on Android and iOS, [#3429](https://github.com/zulip/zulip-mobile/issues/3429).

* webview header: Modify topic header to include date. [#3435](https://github.com/zulip/zulip-mobile/issues/3435)

  This implementation makes topic headers in the message list include a date on the right hand side, the names of the topics being on the left. Since a new topic header is created every time the date changes, this seemed like a perfect place to put the date of the messages which came below it. The problem was that PM narrows didn’t contain a header in which to put in the date. This is why, in order to solve the parent issue, [#1336](https://github.com/zulip/zulip-mobile/issues/1336), another PR ([#3496](https://github.com/zulip/zulip-mobile/issues/3496)) was created, which is explained later in the blog. To note: this PR was closed, but few commits inside it — a6b4b5e, b1b873f, ada59a7, and 123fd7a, have been merged.

* webview js: Improve `longPress` detection logic. [#3434](https://github.com/zulip/zulip-mobile/issues/3434)

  The commits in this PR essentially refactors the logic we had in place to detect long presses in the implemented webview (through which we display all our messages!) to make it more intelligible.

## PRs / Issues After GSoC started!

### Merged:

* Mentions: spacing breaks when it appears at the beginning of line. [#3512](https://github.com/zulip/zulip-mobile/issues/3512)

  A small fix which does exactly what it says :)

The next two PRs revolve around introducing slide in time pills in order to display the time each message was sent — which was previously only showing the time on full-messages.

* Add interactive timestamp to brief messages. [#3491](https://github.com/zulip/zulip-mobile/issues/3491)

  Add the slide in labels to brief-messages. There were some webview related issues here as well. There were a lot of design changes in this PR which were difficult to discuss and solve, but with the help of the Zulip community, were ultimately solved!

* time pills: Make slide-in time pills quieter. [#3527](https://github.com/zulip/zulip-mobile/issues/3527)

  As mentioned above, the design on this was particularly tricky, and as guessed, there were a few issues users were experiencing with regards to this. This PR addresses those issues.

* RGB -> HSL [#3519](https://github.com/zulip/zulip-mobile/issues/3519)
  
  This commit fixes [#3516](https://github.com/zulip/zulip-mobile/issues/3516), and refactors the colors present in the app to HSL(A) type colors, for the sake of better clarity and editability.

* Improve the Realtime docs slightly. [#3543](https://github.com/zulip/zulip-mobile/issues/3543)

  This document was a very important one explaining how Zulip deals with the universal problem every chat application has — how to deal with data changes in the server, i.e. data inconsistencies. Improve a little bit by adding some wikipedia links to explain what some hard to understand terms mean.

* Upload custom files of any type. [#3490](https://github.com/zulip/zulip-mobile/issues/3490)

  This PR enables the users to upload files to Zulip from the mobile app — previously, we were only able to upload images. For this, we had to add a third party library to integrate the native UIs for file picking on Android and iOS.

* codehilite: Update values for syntax highlighting from webapp. [#3530](https://github.com/zulip/zulip-mobile/issues/3530)

  A user noticed that the colors used for code syntax highlighting were not uniform between the web app and the mobile app. This resulted in accessibility concerns, which this PR fixes.

* Avatar sizes increase to 48px globally. [#3529](https://github.com/zulip/zulip-mobile/issues/3529)

  Does exactly what the title says! :)

### Open, but close to Merge:

* Make timerow persistent (WhatsApp like implementation). [#3496](https://github.com/zulip/zulip-mobile/issues/3496)

  This implementation removes the showcasing of dates in the headers in the message list of the app, replacing it with a persistent time pill which appears on scrolling the message list and gets hidden again after a short delay. This takes care of the problem of headers not being present in a personal chat, as mentioned at the beginning of this blog!

* settings card: Add header - Label and separator. [#3533](https://github.com/zulip/zulip-mobile/issues/3533)

  The settings screen has been draped with a nice looking header, which explains that the content is supposed to be settings. Found a little bug while implementing this, which was that the custom fonts found in devices from certain OEMs like OnePlus and Oppo caused clipping in certain bold text in the app. As a result, we might shift to providing a font with the app.

* Add `recent_private_conversations` key to `/register`. [#3535](https://github.com/zulip/zulip-mobile/issues/3535)

  Does just as the title says, and consequently enables a list of chats in the PM/group chats screen which is much larger than what the app is currently capable of, without the use of this key.

* Add support for showing Poll Widgets. [#3554](https://github.com/zulip/zulip-mobile/issues/3554)

  This was part of my original project where an essential feature from the web app got ported to the mobile app which allowed users to participate in polls happening in their organization even from the mobile app.

* messages: Add missing conditions for `shouldBeMuted`. [#3542](https://github.com/zulip/zulip-mobile/issues/3542)

  This was made after a user reported that messages in muted topics that mentioned them were not being shown in the app list like they should be, assuming the control to be the web app. [#3592](https://github.com/zulip/zulip-mobile/issues/3592) was filed as a consequence of another bug found while resolving this.

* mentions: Fix highlight extending unproportionately. [#3514](https://github.com/zulip/zulip-mobile/issues/3514)

  (no description)

### Open, but not close to merge:

* messageActionSheet: Add option to copy link of message to clipboard [#3412](https://github.com/zulip/zulip-mobile/issues/3412)

  Intended to enable the user to copy the link to a message from the message list, so that they can then go on to share the link with someone else.

* brief-messages: Add timestamp. [#3488](https://github.com/zulip/zulip-mobile/issues/3488)

  Depending on user reception of the slide in timestamps referred to above, this PR might need to be brought to fruition.

## Issues Created:

* Pinned Streams: Should be easily accessible. [#3419](https://github.com/zulip/zulip-mobile/issues/3419)
* Easier way to switch back from topic narrow to stream narrow. [#3455](https://github.com/zulip/zulip-mobile/issues/3455)
* Highlight when mentioned extends to the bottom disproportionately. [#3513](https://github.com/zulip/zulip-mobile/issues/3513)
* Feature Suggestion: Image customisation during upload flow. [#3523](https://github.com/zulip/zulip-mobile/issues/3523)
* No internet connection banner does not disappear on regaining connection. [#3485](https://github.com/zulip/zulip-mobile/issues/3485)

Overall, my experience with Zulip was amazing, and I would even say that my skills before I started pushing initial PRs to Zulip were nothing when compared to my prowess now. For that, I would like to thank @jainkuniya, @agzuniverse, my mentors, and @gnprice as well as @borisyankov, the maintainers for zulip-mobile. Without their support, I don’t think my technical as well as soft skills would be where they are now.