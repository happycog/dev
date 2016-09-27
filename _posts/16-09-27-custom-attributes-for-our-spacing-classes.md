---
title: Custom Attributes for our Spacing Classes
---

Recently here at Happy Cog, we’ve been using the lobotomized owl selector to handle vertical spacing between elements. Up until now, we’ve been adding a class of `.spacing` on a container to create equal spacing between all of its direct child elements. While using this method on our projects, we noticed our class attribute was getting extremely cluttered with a variety of spacing classes on a single element. Here's an example:

```
<article class="article article--full spacing spacing-half--s-to-m spacing-half--m spacing-triple--l border-top">
    <h2>{{ title }}</h2>
    <p>{{ date }}| {{ category }} | {{ author }}</p>
    <p>{{ body }}</p>
    <ul class="tag spacing-half spacing--l">...</ul>
</article>
```

As you can see, there’s an overload of spacing-based class names littering the codebase. Scanning over this code with your text editor or devtools can become overwhelming. So how can we simplify this? Mark and I discussed a possible solution for this problem and came up with something like this:

```
<div class="article article--full" spacing="1 small-medium(.5) large(3)">
    <h2>{{ title }}</h2>
    <p>{{ date }}| {{ category }} | {{ author }}</p>
    <p>{{ body }}</p>
    <ul class="tag tag-meta" spacing=".5  large(1)">...</ul>
</div>
```

We decided to use a custom attribute called `spacing` to separate our spacing classes from the stylistic classes. Our spacing classes only handle margin top while our stylistic classes set the background, borders, padding, etc. This ensures all the classes applied to an element are specifically for visual styling whereas any value in the spacing attribute is specifically for our vertical spacing throughout the project.

## SCSS File
Here is a snippet of our `.spacing.scss`. We are using include-media to handle our media queries.

```
// Variables
$spacingDesktop: 20px;
$spacingMobile: 14px;

// Default
[spacing^="1"]  > * + * {
    margin-top: $spacingMobile;

    @include media('>large') {
        margin-top: $spacingDesktop;
    }
}

[spacing^="1.5"]  > * + * {
    margin-top: $spacingMobile * 1.5;

    @include media('>large') {
        margin-top: $spacingDesktop * 1.5;
    }
}

[spacing^="2"]  > * + * {
    margin-top: $spacingMobile * 2;

    @include media('>large') {
        margin-top: $spacingDesktop * 2;
    }
}
```

In this snippet, we are defining our spacing variables as well as setting our default CSS rulesets. we use a complex CSS selector to provide two, collaborative, abilities. First, the 'begins with' selector is used to allow a default spacing to be set. Then using a wildcard match we can override that spacing on specific breakpoints using our custom `large()` syntax". In some cases the spacing can vary from screen size to screen size. Following our default classes, we have a CSS ruleset to target spacing at different screen sizes.

```
// $large only
@include media('>=large', '<mlarge') {
    [spacing*="large(1)"] > * + * {
        margin-top: $spacingDesktop;
    }
}
// $xsmall to $large
@include media('>=xsmall', '<large') {
    [spacing-top*="xsmall-large(1)"] {
        margin-top: $spacingMobile;
    }
}
```

Following the default spacing classes, we’re using CSS selectors to target any value in our attribute. If we don't define `xsmall-xlarge` then it won't be available. This is to keep the generated CSS size small and reduce extraneous code that we may never even use.

## Putting it all together

```
<div class="article article--full" spacing="1 small-medium(.5) large(3)">
    <h2>{{ title }}</h2>
    <p>{{ date }}| {{ category }} | {{ author }}</p>
    <p>{{ body }}</p>
    <ul class="tag tag-meta" spacing=".5  large(1)">...</ul>
</div>
```

The browser reads the example like this:
Give each direct child of the article element a margin-top of 14px on small screens and 20px on large screens.
For small to medium screens, give the direct child elements a margin top of 10px
On large screens give the direct child elements a margin-top of 60px

Some may ask, why aren't you using “data-” to define your custom attribute? This is still up for discussion here on the development team. Sure, we might run into some issues further down the line, but that's as easy as doing a `replace all` to fix our spacing attributes. We’re testing this method with one of our current projects and it’s going pretty smoothly. Does adding “data-” to our custom attribute really matter nowadays? I’d like to hear your opinions.
