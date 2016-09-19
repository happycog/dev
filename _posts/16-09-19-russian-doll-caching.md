---
title: Russian Doll Caching
---

I've been working on a submission for [10k Apart](https://a-k-apart.com) and in doing so have been thinking of how I can submit this thing without having to spin up a Digital Ocean box and pay for it through the submission process to support the crazy complex queries I'm writing. To get around this I wanted to cache `:allthethings:` but I really didn't want to set TTLs. Enter [russian doll caching](https://signalvnoise.com/posts/3112-how-basecamp-next-got-to-be-so-damn-fast-without-using-much-client-side-ui), popularized by 37 signals but around for a while, it's a method of caching based on the modified date of your models.

I set it up for my little kanban app and was plesantly surprised at how little effort it took in Laravel. One thing that I couldn't wrap my head around though was visualizing the cache updates. Espically when you have nested caches that don't reset their children. To work around this I whipped together a Twig tag that automatically caches a section of the page while also inserting a visual border around each cache. It ended up looking like this,

![Russian Doll Caching Visualization](https://happycog.github.io/dev/public/assets/Screen%20Shot%202016-09-19%20at%204.53.53%20PM.png)

And with that any confusion about the cache is gone. It all makes sense and I can see exactly the key name for each cache so if something's not updating it's obvious what key is at fault and why it's not updating.

Source, [https://github.com...](https://github.com/markhuot/cards)
