---
title: We built our website without CSS: the highs and the lows
---

> In the olden days, people would have CSS files with selectors and declarations. Then they would have HTML elements with class names. The styles get applied to an element because the class names in the HTML match the selector in the CSS file.
>
> ```jsx
> <div className="home-page">
>  Hello, world
> </div>
> ```
>
> ```css
> .home-page { background: whitesmoke; }
> ```
>
> The way you go about things if you’re not using CSS files, is to do this:
>
> ```jsx
> const homePageStyle = {
>   background: 'whitesmoke'
> }
> return <div style={homePageStyle}>
>   Hello, world
> </div>
> ```
>
> Go find a developer that doesn’t know about CSS and ask them which of these two makes more sense.

I like this argument, I've seen it a few times recently. It's clear to me why the more programattic approach would appeal to the more traditional-computer-science minded. There's a lot to be gained by taking an approach like this too, real logic in the visual layer is huge. Native conditionals that respond to complex business logic sounds like the CSS we've all been waiting for.

At the same time, a DSL like CSS allows us to much more susicintly describe things like media queries and and grid systems. I look at the current solutions for "media queries in React" and all I see is added complexity forcing a feature where it doesn't belong.

I'll be the first to drop CSS once we get something better, that's natively supported by the major browsers. Until then, CSS in JavaScript feels like an ugly hack without much added value.
