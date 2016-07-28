Visual Format Language

What has piqued my interest about iOS's Auto Layout, more than anything else, is the quasi-DSL Apple has created to express layout. It takes a complex relationship like "make these two buttons 50px and 8px apart" and turns it into `[button(50)]-[button(50)]`. I was curious enough to see if the same sort of this would be possible in CSS/Sass. Well, I wouldn't be writing this post if it wasn't, so here's the outcome,

```scss
.layout-split-2 {
  @include autolayout('|[column]-[column]|');
}
```

Which says: within `.layout-split-2` create a selector for `.column` (which could have just as easily been `.col`) and make it 50% of the width with the "standard" gutter. This can be extended to something more complex, such as,

```scss
.layout-split-2 {
  @include autolayout('|-[column]-100px-[column]-|');
}
```

That adds a gutter to the left and right of the layout and overrides the default gutter to `100px`.

The boilerplate this replaces is all the repetive junk of defining `.column`, setting the width, floats, clears, etc… Because I couldn't stop there the Auto Layout syntax even supports non-equal column widths, such as,

```scss
.layout-split-2 {
  @include autolayout('|[column(75%)]-[column(25%)]|');
}
```

I spent no time looking into the responsive nature of this because it's easily nested within something like `@include media` with,

```scss
.layout-split-2 {
  @include media('<large') {
    @include autolayout('|-[column]-|');
  }
  @include media('>=large') {
    @include autolayout('|[column(75%)]-[column(25%)]|');
  }
}
```

You can see a demo of this, in action, here, [http://codepen.io/markhuot/pen/kXJjWR](http://codepen.io/markhuot/pen/kXJjWR)

Source, [https://developer.apple.com...](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/VisualFormatLanguage.html)
