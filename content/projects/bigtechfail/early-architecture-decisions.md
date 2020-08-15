---
weight: 3
title: Early Architecture Decisions
date: 2020-06-04
---

Since BigTech.fail was personally such a huge undertaking, many mistakes were amplified, especially those of unnecessary complexity.
By far the most consequential ones were in regards to project structure and the choice of tools.
I want to elaborate on how the project went from its initial structure during alpha development to its current structure today: a simple, static, No-JS website.

## Background and Alpha Setup

As brainstorming and development started, the original structure that took shape looked something like this: content in the form of markdown files, a server to parse and serve the content, and a rich frontend to present the content.
This structure appeared complicated in the beginning when the project was small, but I figured it would provide plenty of room for the project to grow into.

The frontend was built using Vuejs mainly because Patreon.fail (the predecessor to BigTech.fail) was a Vuejs project.
I of course relied on the Vue stack for all of the typical UI stuff, such as opening and closing side drawers, but I also leveraged it in two other ways that are important to note:

1. Connecting components such as dialogs to Vue Router routes so that the sharable URLs would contain whether a dialog was open or not.
2. Most importantly, the timeline functionality.
On the surface, I relied on the reactiveness to filter the events when the user modified the filter options.
Behind the scenes, I used Vuex for storing the raw timeline data after it was initially downloaded in order to avoid requesting the same large amounts of data over and over again.

After a few months, I started to realize that most of my time was spent _engineering_.
This was not desirable seeing as my todo list for content was growing out of control.
**I could never seem to get out of _coding_ and into _writing_.**
This turned out to be a symptom of the underlying architecture problem, which would be fixed with an unsurprising remedy: _simplification_.

## Static: No Backend, No Frontend

Of course there would still be a "frontend."
What I mean, and the reason I use quotes, is that I decided to drop the focus on some rich, interactive user interface.
The site would now mainly be about serving _content_ to the user instead of _an experience_ (so to speak).
Therefore, no reactive frontend would be required -- it was just a matter of designing how this content should look -- and no backend would be required since the content would be in the statically generated pages.

The obvious choice here was to use [Hugo](https://gohugo.io/).
(I had tried it previously and liked it very much, but I wasn't ready at that time to drop the interactive timeline mentioned above.
I had considered using Hugo to build the static site and using a reactive framework on the timeline page alone, but I ultimately decided against it primarily out of concern for development overhead.
However, now that I brought myself to drop the heavy UI/UX altogether, this was clearly the right tool for the job.)

## No JavaScript Whatsoever

Any project that ships with a reactive framework (Vuejs, Angular, React) relies heavily on JavaScript.
Since I was going to drop the need for a reactive framework on the frontend, I opened up the possibility of dropping JavaScript altogether.
I had seen / heard about sites without JavaScript as well as the circumstances under which some people disable JavaScript.
(They are primarily security related as JavaScript opens the door to potentially dangerous exploits.)
Overall, this was a challenge that was right up my alley that would further _simplify_ things quite a bit.

## Conclusion

After only about a month of implementing this plan, the core _engineering_ aspect of the project (getting the main sections, pages and styling done) is nearly complete and has been thoroughly more enjoyable than I ever would have thought.
I can't describe the happiness that comes from not having to look at a single line of JavaScript or TypeScript.

And I haven't even mentioned the joy that comes from dropping the entire JavaScript toolchain: no NodeJS, no npm / yarn, no Vuejs / React.
The entire site (120+ pages and 80+ static resources, at the time of writing) builds in less than half a second; that's down from more than two minutes (those numbers are from repeated builds on the lowest tier DigitalOcean droplet running FreeBSD).
