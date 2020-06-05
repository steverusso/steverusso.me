---
weight: 2
title: Decision to Not Use Twitter's API
date: 2019-10-06
---

Originally, for Patreon.fail's timeline, any relevant tweets were rendered using [Twitter's JavaScript API](https://developer.twitter.com/en/docs/twitter-for-websites/embedded-tweets/guides/embedded-tweet-javascript-factory-function).
This document describes the decision to stop using Twitter's API to display those tweets.

## The Problems

Let's begin with why using the API was starting to cause concern in the first place.

1. **Reliability**
   * The `widgets.js` script would sometimes (a) not load or (b) load and throw and an error. There was no pattern or consistency. Some speculative thoughts are that it might not have played well with Vue.js or async loading (or maybe both).
   * If the tweets were removed from Twitter, there was no way to know ahead of time. So there would be a broken link / tweet while something was retrieved from the web archive.
   * While this is a public API, it's not hard to imagine Twitter restricting their APIs in the future and causing some real development issues for a project like this.
2. **Privacy**
   * Having any user data collected via API use is not ideal. As a minor example, the links to the tweets on Twitter that were displayed using API had the 'ref' parameter set, and therefore told Twitter that those links were being followed from `patreon.fail`.
3. **Performance**
   * Loading an external script like that and making whatever amount of API calls has costs. Eliminating those performance costs would be great.

## The Solution

There are two solutions being considered:
1. Capture **images** of the tweets. The most important thing is that the essential information is captured: _who_ tweeted _what_, _when_.
2. Display the tweet using **text** and link to Twitter or an archive site.

## The Trade-Offs

### For Images

This solution obviously comes with some trade-offs.

1. **Heavier Repo**
   * The source code repository now has to carry all those images.
2. **Increased Overhead For Updates**
   * Any change that applies to all the tweets will have an amount of overhead that wasn't present when using the API. However, it's very likely that any changes will be to the images and any elements above instead of the tweets themselves.
3. **No Theming**
   * When using the API, there was a configuration for a 'theme' (dark or not). With the plain images, the theme of the tweets is 'hard-coded' so to speak. Therefore, this rules out the possibility of doing site-wide theming as it would not be effective since the content of the tweets could not be included.

### For Text

The only real downside here is appearance: images of tweets look better than text.
Other than that, theming is irrelevant, there is no little maintenance burden, and this is the best option for performance.

## The Benefits

1. **Increased Reliability**
   * If the tweets are removed from Twitter, nothing changes on our end now.
   * There is a major third party dependency that no longer gets in the way.
2. **Increased Privacy**
   * The links to any tweets are now just regular links, and they could even link to an archive site instead of Twitter. Therefore, Twitter's data collection and privacy policies don't need to be considered anymore.
