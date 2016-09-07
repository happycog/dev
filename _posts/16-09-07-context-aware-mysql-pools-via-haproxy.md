---
title: Context aware MySQL pools via HAProxy
---

>We set out to create a self-managing topology that will exclude lagging replicas automatically, handle disasters gracefully, and yet allow for complete human control and visibility.

Sounds like a tall order…

>HAProxy’s behavior is to use the main pool for as long as at least three replicas are happy to serve data. If only two replicas or less are in good shape, HAProxy switches to the backup pool, where we re-introduce the lagging replicas; serving more stale data, but still serving.

Smart. There's no magic here. It's vanilla MySQL with vanilla HAProxy. The architects here let each tool do what it does well and then wired them together with a small web server. There's no new technologies, no amazing revelations, just rock solid technologies working together.

Source, [http://githubengineering.com...](http://githubengineering.com/context-aware-mysql-pools-via-haproxy/)
