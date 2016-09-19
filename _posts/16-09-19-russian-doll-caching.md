---
title: Russian Doll Caching
---

Recently, I've been working on a submission for the [10k Apart](https://a-k-apart.com) challenge and in doing so have been thinking of how I can submit this thing without needing an entire server farm running throughout the evaluation process. So I'm looking to host it on Heroku and therefore wanted to cache `:allthethings:`. But, I really didn't want to set TTLs and wait for stale data to reset. Enter [russian doll caching](https://signalvnoise.com/posts/3112-how-basecamp-next-got-to-be-so-damn-fast-without-using-much-client-side-ui), popularized by 37 signals but around for a while, it's a method of caching based on the modified date of your models.

I set it up for my little kanban app and was plesantly surprised at how little effort it took in Laravel. One thing that I couldn't wrap my head around though was visualizing the cache resets. Espically when you have nested caches that don't reset their children because the parent isn't updating. To work around this I whipped together a Twig tag that caches a section of the page while inserting a visual border around each cache. It ended up looking like this,

![Russian Doll Caching Visualization](https://happycog.github.io/dev/public/assets/Screen%20Shot%202016-09-19%20at%204.53.53%20PM.png)

And with that any confusion about the cache is gone. It all makes sense and I can see the exact key name for each cache. This way if something's not updating it's immediately obvious what key is at fault.

Source, [https://github.com...](https://github.com/markhuot/cards)
