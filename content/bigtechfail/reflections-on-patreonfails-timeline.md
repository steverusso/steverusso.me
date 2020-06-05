---
weight: 1
title: Reflections On Patreon.fail's Timeline
date: 2019-10-06
---

There were several lessons that I learned after developing and reviewing Patreon.fail's timeline.
I already documented one of these key lessons which was to [not use Twitter's API](../on-not-using-twitters-api/) for displaying tweets relevant to a given event.
However, looking back, Patreon.fail's Timeline page was a bit of a fail on my part.
The page took 5 seconds to load, making over 100 requests of all different types, and that's without scrolling. Sure, a few could have been lazy-loaded, but performance isn't the only concern at that point.

## Overall Design - Display Entirety of Event Content

For Patreon.fail, each timeline event's main content was _all_ the media related to the event, _maybe_ prefixed by a sentence or two.
This has it's advantages and disadvantages:

### Advantages
- **Shorter Time to Production:** Once an event occurs, I just have to retrieve the media (image, tweet, video thumbnail) related to the event, and _maybe_ write a sentence if it's necessary.

### Disadvantages
- **Heavier UI/UX:** Having everything that relates to a given event visible in the timeline event cards is a lot to throw at the user all at once.
- **Lack of Uniformity:** Each event is a different size, has different types of media, a different number of source links, different lenght titles, etc. Some events have a lot of content and others have very little. This results in an inconsistent and non-symmetrical UI.

### Solution
The solution here is a design that displays a truncated / overview of each event and offers an intuitive way to view the entirety of the event separately.
Also, using the timeline to _only_ display a minified version of the event allows for **increased uniformity** across events.
The UI will therefore not only be a bit more "symmetrical" but significantly **more lightweight** as well.

## External Resources - Using BigTech's (and Other) APIs

For Patreon.fail, I used Twitter's API for rendering an event's relevant tweets and iframes for embedding videos from YouTube via YouTube's "embed" sharing option.
Again, this method had its advangtages and far weightier disadvantages.

Generally speaking, all of the concepts around using / not using Twitter's API apply to the idea of using external APIs in general. To recap, the main are ideas are:

### Advantages:
- **Makes development a little easier** as a portion of the UI/UX can be offloaded to another developer / team.

### Disadvantages:
- **Lack of reliablity** as the media could (and in these cases, likely _**would**_) eventually be removed and then the API call fails and my site has a minor, temporary break as a result.
- **Lack of privacy** as these information scavengers are always collecting every bit of data they possibly can. Twitter's API automatically added referrer information, as just _one simple example_, and I don't even want to _begin_ to find out what else they were doing or what YouTube is collecting.
- **Lack of consistency** as these APIs are each (rightfully) doing what they think is best. Some are async JavaScript API calls, some are iframes to embed videos, etc.

### Solution
The solution is to avoid using external APIs where possible.
This means taking on a heavier development load, but it will likely mean a more logically consistent design (as everything will be reduced to a common denominator, such as images).
It will also lead to increased privacy and reliablity for the users.

On the off chance that screenshots or the like are a copyright infringement (or something like that), then that specific type of media will be reducded to a simple text link with documentation as to why that is.
