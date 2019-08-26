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

My GSoC project was with [Zulip Mobile](http://github.com/zulip/zulip-mobile), which is a cross platform application built with React Native. My project originally centered around developing the features which were missing in the mobile app but present in the web app, as well as certain UX improvements which made the app easier to use. It then pivoted slightly to include some bug fixes as well as some changes which weren’t outlined in the project proposal.

One thing I should mention, is that I used my community bonding period to code as well, because my university concluded earlier than others and 5th semester started a month before the coding period ended.

This document is a log of my contributions during that time period, and I have tried to make it useful and understandable for people who are not familiar with Zulip terminology as well!

## Merged PRs!

* Mentions: spacing breaks when it appears at the beginning of line. [#3512](https://github.com/zulip/zulip-mobile/issues/3512)

  A small fix which does exactly what it says :)
	For clarity, in Zulip, a message which mentions you gets highlighted, and the mentioning part itself (eg. '@Isham Mahajan') gets 'quoted' (eg. `@Isham Mahajan`).

The next two PRs revolve around introducing sent-time indicators which slide in from the bottom right of each message; previously only messages with an avatar contained a timestamp (henceforth 'message-full').

For context, the architecture of Zulip's message list is such that if there are several consecutive messages from one user, they're group together to form one structure  -- so the data `[msgFrmUsr1, msgFrmUsr1, msgFrmUsr1, msgFrmUsr2]` would convert to `[message-full, message-brief, message-brief, message-full]` for displaying purposes. The difference in message-full and message-brief being that a message-full displays the message's content along with the details of the user who sent the message, and the time when that message was sent.

* Add interactive timestamp to brief messages. [#3491](https://github.com/zulip/zulip-mobile/issues/3491)

  Add the slide in labels to `message-brief`. Because we use a webview to display our message list, a set of problems concerning that were present as well. There were a lot of design changes in this PR which were difficult to discuss and solve, but with the help of the Zulip community (on chat.zulip.org -- czo for short), were ultimately solved!

* time pills: Make slide-in time pills quieter. [#3527](https://github.com/zulip/zulip-mobile/issues/3527)

  As mentioned above, the design on this was particularly tricky, and as guessed, there were a few issues users were experiencing with regards to this. This PR addresses those issues.

* RGB -> HSL [#3519](https://github.com/zulip/zulip-mobile/issues/3519)
  
  This commit fixes [#3516](https://github.com/zulip/zulip-mobile/issues/3516), and refactors the colors present in the app to HSL(A) type colors, for the sake of better clarity and editability, which the HSL color model is famous for.

* Improve the Realtime docs slightly. [#3543](https://github.com/zulip/zulip-mobile/issues/3543)

  This document was a very important one explaining how Zulip deals with the universal problem every chat application has — how to deal with data changes in the server, i.e. data inconsistencies. Improve a little bit by adding some wikipedia links to explain what some hard to understand terms mean.

* Upload custom files of any type. [#3490](https://github.com/zulip/zulip-mobile/issues/3490)

  This PR enables the users to upload files to Zulip from the mobile app — previously, we were only able to upload images. For this, we had to add a third party library to integrate the native UIs for file picking on Android and iOS.

* codehilite: Update values for syntax highlighting from webapp. [#3530](https://github.com/zulip/zulip-mobile/issues/3530)

  A user noticed that the colors used for code syntax highlighting were not uniform between the web app and the mobile app. This resulted in accessibility concerns, which this PR fixes.

* Avatar sizes increase to 48px globally. [#3529](https://github.com/zulip/zulip-mobile/issues/3529)

  Does exactly what the title says! :)

## Close to Merge

* Make timerow persistent (WhatsApp like implementation). [#3496](https://github.com/zulip/zulip-mobile/issues/3496)

  This implementation removes the showcasing of dates in the headers in the message list of the app, replacing it with a persistent time pill which appears on scrolling the message list and gets hidden again after a short delay. This takes care of the problem of headers not being present in a personal chat, as mentioned at the beginning of this blog!
	
	Again, for context, Zulip's messaging paradigm consists of `stream`s and `topic`s, streams being the higher level categorization of messages (which usually segregates different contexts of an org), and topic being the lower level (functionality is indicative by the word `topic` itself). While in a stream, different topics are separated by headers. I highly recommend checking out the structure yourself -- it's quite facinating how this simple design boosts productivity.

* settings card: Add header - Label and separator. [#3533](https://github.com/zulip/zulip-mobile/issues/3533)

  The settings screen has been draped with a nice looking header, which explains that the content is supposed to be settings. Found a little bug while implementing this, which was that the custom fonts found in devices from certain OEMs like OnePlus and Oppo caused clipping in certain bold text in the app. As a result, we might shift to providing a font with the app.

* Add `recent_private_conversations` key to `/register`. [#3535](https://github.com/zulip/zulip-mobile/issues/3535)

  Does just as the title says, and consequently enables a list of chats in the PM/group chats screen which is much larger than what the app is currently capable of, without the use of this key.
	
	Context: zulip-mobile uses the redux library to manage it's state. We use the very powerful [zulip events API](https://zulipchat.com/api/register-queue) in order to avoid data inconsistency issues which come with any mobile messaging app. (This API was quite facinating and informative for me, please do check it out for yourself!) That document should very clearly explain the context for this PR.

* Add support for showing Poll Widgets. [#3554](https://github.com/zulip/zulip-mobile/issues/3554)

  This was part of my original project where an essential feature from the web app got ported to the mobile app which allowed users to participate in polls happening in their organization even from the mobile app.

* messages: Add missing conditions for `shouldBeMuted`. [#3542](https://github.com/zulip/zulip-mobile/issues/3542)

  This was made after a user reported that messages in muted topics that mentioned them were not being shown in the app list like they should be, assuming the control to be the web app. [#3592](https://github.com/zulip/zulip-mobile/issues/3592) was filed as a consequence of another bug found while resolving this.

* mentions: Fix highlight extending disproportionately. [#3514](https://github.com/zulip/zulip-mobile/issues/3514)

  A slight overlook in the structure of the CSS resulted in a non-uniform looking highlight -- the screenshots of which are visible in the PR itself.  Have a look!

## Open

* messageActionSheet: Add option to copy link of message to clipboard [#3412](https://github.com/zulip/zulip-mobile/issues/3412)

  Intended to enable the user to copy the link **to** a message from the message list, so that they can then go on to share the link with someone else.

* brief-messages: Add timestamp. [#3488](https://github.com/zulip/zulip-mobile/issues/3488)

  Depending on user reception of the slide in timestamps referred to above, this PR might need to be brought to fruition.

## Issues Created

* Pinned Streams: Should be easily accessible. [#3419](https://github.com/zulip/zulip-mobile/issues/3419)
* Easier way to switch back from topic narrow to stream narrow. [#3455](https://github.com/zulip/zulip-mobile/issues/3455)
* Highlight when mentioned extends to the bottom disproportionately. [#3513](https://github.com/zulip/zulip-mobile/issues/3513)
* Feature Suggestion: Image customisation during upload flow. [#3523](https://github.com/zulip/zulip-mobile/issues/3523)
* No internet connection banner does not disappear on regaining connection. [#3485](https://github.com/zulip/zulip-mobile/issues/3485)

Overall, my experience with Zulip was amazing, and I would even say that my skills before I started pushing initial PRs to Zulip were nothing when compared to my prowess now. For that, I would like to thank @jainkuniya, @agzuniverse, my mentors, and @gnprice as well as @borisyankov, the maintainers for zulip-mobile. Without their support, I don’t think my technical as well as soft skills would be where they are now.