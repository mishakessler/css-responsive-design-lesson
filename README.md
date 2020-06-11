# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Responsive CSS Design

## LEARNING OBJECTIVES

During this lesson, we're going to touch on:

- Understanding responsive design concepts, and the difference between mobile-up and desktop-down.
- Understanding that responsive design is dictated by _visual_ break points, not device sizes.
- Identifying the various CSS units of measurement and when alternatives are advantageous.
- Understanding and planning for responsive screen sizes, including identifying breakpoints and implementing media queries.
- Understanding how CSS cascade– and the importance of organization of your code, to utilize the cascade effectively– will affect your app.

---

## Contextual Review

### CSS Selectors & Specificity

Remember the different types of selectors?

1. Simple Selectors (ie: `div`, `.class`, or `#id` names)
1. Pseudo Class Selectors (ie: `link:hover`, `input:required`, `input:not(required)`)
1. Pseudo Element Selectors (ie:
1. Combinator (Descendant, Child, Sibling) Selectors (ie: `div > p`)

Specificity

### Organizing Your Stylesheet

Personal Preferences (Alphabetic? By specificity? What about pseudo classes and media queries? A single global sheet or multiple sheets? Component styling?)

Never, never, never repeat the same selector with the same specificity. (Media queries take a higher specificity, so of course that's allowed.)

---

## Introduction

<details>
<summary><strong>What is Responsive Design?</strong></summary>
<br>

Responsive Design is the strategy of making a site that "responds" to the browser and device on which it's being displayed.

This means a website is _usable_, _readable_, _navigable_, and _looks great_ on any screen size.

From Wikipedia: "Responsive web design (RWD) is a web design approach aimed at crafting sites to provide an optimal viewing experience — easy reading and navigation with a minimum of resizing, panning, and scrolling — across a wide range of devices (from mobile phones to desktop computer monitors)."

</details>

<br>

<details>
<summary><strong>Responsive Design is not device-specific. Why?</strong></summary>
<br>

A responsive site doesn't just look good on the _newest_ phone, watch, tablet, or mega-screen; it should look good on _any_ screen– and, on desktop screens, at any width of the browser window. This might seem impossible, but it's relatively straightforward!

<p align="center">

![Responsive Design](https://media2.giphy.com/media/uOZg6EKGGZG5G/source.gif)

</p>

</details>

<br>

As you begin understanding the sheer scope of effective and comprehensive stylesheets, you may feel a little intimidated, but don't worry.

All that's required is understanding all the tools available to you and some advanced planning for your stylesheets.

Let's dive in!

<br>

---

## CSS Units

Of course, we've worked almost entirely with the `px`, or pixel, until now. The pixel is one option for an _**absolute**_ length, but there are also _**relative**_ and _**calculated**_ lengths.

<br>

### Absolute Values

| name       | value |
| :--------- | :---: |
| pixel      |  px   |
| point      |  pt   |
| pica       |  pc   |
| inch       |  in   |
| centimeter |  cm   |
| millimeter |  mm   |

<br>

<details>
<summary><strong>What even is a pixel?</strong></summary>
<br>

For a long time, a computer screen's best pixel density was **96 ppi**. This means that, in the beginning of wed design, 1 pixel was exactly **1/96th of an inch**.

Absolute lengths based on common measurements will render according to this ratio, not the actual length relative to the viewer. This is called the **1:96 fixed ratio** of CSS.

Tangentially, while absolute lengths become less common in digital design, they are still the standard for _**print**_ design due to paper/ink printers' standards. High definition images and PDFs will print at least 300 or 450dpi, if not 600.

</details>

<br>

<details>
<summary><strong>Why are absolute values helpful?</strong></summary>
<br>

Short answer? It's complicated!

As you become more comfortable with CSS, you'll begin to appreciate the power of absolute values when they're needed, but best practice discourages absolute values– **especially** any values besides the pixel– and even then, try use them selectively.

I mean, have you seen the absolutely epic [SpaceJam.com](https://www.spacejam.com/) website?

</details>

<br>

### Relative Values

| name            | value | example           |
| :-------------- | :---: | :---------------- |
| percent         |   %   | `width: 100%`     |
| viewport-width  |  vw   | `width: 100vw`    |
| viewport-height |  vh   | `height: 100vh`   |
| viewport-min    | vmin  | `width: 100vmin`  |
| viewport-max    | vmax  | `width: 100vmax`  |
| element         |  em   | `font-size: 2em`  |
| root-element    |  rem  | `font-size: 2rem` |
| x-height        |  ex   | `font-size: 2ex`  |
| 0-width (zero)  |  ch   | `font-size: 2ch`  |

<br>

<details>
<summary><strong>Why are relative values helpful?</strong></summary>
<br>

Because of the extreme variability in screen sizes, when we're trying to design responsive apps, relative lengths can help bake in responsiveness. This is advantageous compares to using all absolute lengths, and then having to adjust for precise design at all screen sizes.

</details>

<br>

### Calculated Values

Occasionally, you may see calculated values in use:

| value | example                      |
| :---: | :--------------------------- |
| auto  | `margin: 0 auto`             |
| calc  | `height: calc(100vh - 50px)` |

<br>

<details>
<summary><strong>Why are calculated values helpful?</strong></summary>
<br>

In certain circumstances, the precision of your values is extremely important.

Consider it through the lens of _value compatibility_:

Let's say you make a `header`, and you assign it a height of `100px` to perfectly fit your logo and navigation links. Next, you see that the body div of the page isn't filling the whole screen, so you give the body div a height of `900px`.

This would be great if your viewport was _always_ 1000px in height, but then you look at it on another screen, and you see the body div is still too short.

Eyeballing your app, you decide to reassign the height of the body div, this time opting for a relative value of `92vh`, thinking this will save some effort in the future.

Again, this would be great if your 100px header was _always_ exactly 8% of your viewport height, but that's just not going to be the case.

</details>

<br>

### Extremely Rare Values

#### Resolution & Pixel-Density Values

Even more rarely, you may see values that account for the differences between high-pixel density (such as Retina) and low-pixel density screens.

| name                | value | example                     |
| :------------------ | :---: | :-------------------------- |
| dots per inch       |  dpi  | `min-resolution: 192dpi`    |
| dots per centimeter | dpcm  | `max-resolution: 150dpi`    |
| device pixel ratio  | dppx  | `min-resolution: 2dppx`     |
| dppx alias          |   x   | `min-device-pixel-ratio: 2` |

<br>

#### `var` Values

The `var` value in CSS, just like the deprecated JavaScript `var` is a means of declaring a CSS variable.

```css
:root {
  --main-bg-color: coral;
}

#div1 {
  background-color: var(--main-bg-color);
}
```

This is rarely used because of new advances in CSS pre-processors like SASS, SCSS, LASS, and LESS, which apply much more programmatic thinking to styling.

<br>

#### `rhythm` Values

The `vertical rhythm` value in CSS is **not** itself a keyword or value, but rather, a manipulation of `calc` and `var` values to easily implement consistency.

<br>

### The `!important` Exception

What happens when you're working with a massive stylesheet, you've tried everything you can think of to find whatever is breaking, and this _one_ CSS value that you need is just being ignored?

| name                |   value    | example                    |
| :------------------ | :--------: | :------------------------- |
| Important Exception | !important | `height: 125px !important` |

Please note, this `!important` exception is considered **bad practice**, since it violates the cascading norms. This makes later edits difficult because they may simply be overwritten, leading you to believe you're using an erroneous selector or property/value.

<br>

---

## Media Queries

Media queries are _conditional styling rules_ for the size of the user's viewport which is rendering the site. Let's look at an example.

We already know that if we do something like this:

```css
p {
  color: red;
}

p.blue_text {
  color: blue;
}
```

By default, all `p` tags will have red text – unless they have the class `blue_text`, in which case the text will be blue. We can do a similar thing with media queries, using **cascading**.

```css
p {
  color: blue;
}

@media screen and (min-width: 600px) {
  p {
    color: red;
  }
}
```

Now all `p` tags will be red until the screen size reaches 600px, when they'll turn blue.

In practice, a media query alerts the user's browser to overwrite or render additional styling rules, as long as the user's viewport falls within the width defined by your query.

Media queries should **_always_**:

1. Come at the end of your stylesheets.
1. Use **width** properties and **pixel** values.
1. Be organized by screen size, from largest to smallest.

However, this begs the question, how do we know the width to use in the media query, and how can we possibly account for all the variations in screens?

<br>

### Common Resolutions

Let's think about some common resolutions in use, using Apple devices:

| Model & Size                   | Type    | Width  | Height  | Density (ppi) |
| :----------------------------- | :------ | :----: | :-----: | :-----------: |
| iMac 27" (Retina 5K)           | Desktop | 5120px | 2880px  |    218 PPI    |
| iMac 27"                       |         | 2560px | 1440px  |    109 PPI    |
| iMac 21.5" (Retina 4K)         |         | 4096px | 2304px  |    219 PPI    |
| iMac 21.5"                     |         | 1920px | 1080px  |    102 PPI    |
| MacBook Pro 16" (Retina)       | Laptop  | 3072px | 1,920px |    226 PPI    |
| MacBook Pro 15" (Retina)       |         | 2880px | 1920px  |    220 PPI    |
| MacBook Pro & Air 13" (Retina) |         | 2560px | 1600px  |    227 PPI    |
| MacBook Pro 13"                |         | 1280px |  800px  |    113 PPI    |
| MacBook 12" (Retina)           |         | 2304px | 1440px  |    226 PPI    |
| MacBook Air 11"                |         | 1366px |  768px  |    135 PPI    |

<br>

And don't forget the market share of website visitors worldwide by device type:

<a href="https://gs.statcounter.com/platform-market-share/desktop-mobile-tablet">StatCounter Global Stats - Platform Comparison Market Share</a>

<br>

### Breakpoints

While there are commonly used breakpoints, there's no "boilerplate" for your best approach to identifying the size of a media query is to test your site for breakpoints. A breakpoint is simply a specific browser width where the layout either breaks or no longer follows the intended design.

Another way to think about it: The design looks 'off' or just plain bad!

<br>

### Responsive Developer Tools

You can use Chrome Dev Tools to measure the width of a page open in the browser. Adjust the width of the browser and identify breakpoints.

If you see an unintended or unacceptable change occur in the design or layout, your media query is likely missing the target width; rather than adding new, highly specific media queries, best practice suggests trying to refactor the media queries in use.

[Quick Demo](https://beta.crisisinternational.org)

<br>

---

## Common Breakpoints

Extra small devices (phones, 600px and down):
`@media only screen and (max-width: 600px) {...}`

Small devices (portrait tablets and large phones, 600px and up)
`@media only screen and (min-width: 600px) {...}`

Medium devices (landscape tablets, 768px and up)
`@media only screen and (min-width: 768px) {...}`

Large devices (laptops/desktops, 992px and up)
`@media only screen and (min-width: 992px) {...}`

Extra large devices (large laptops and desktops, 1200px and up)
`@media only screen and (min-width: 1200px) {...}`

<br>

Alternatively, you may see them like this:

```css
@media all and (min-width: 1200px) {
  ...;
}
@media all and (min-width: 960px) and (max-width: 1199px) {
  ...;
}
@media all and (min-width: 768px) and (max-width: 959px) {
  ...;
}
@media all and (min-width: 480px) and (max-width: 767px) {
  ...;
}
@media all and (max-width: 599px) {
  ...;
}
@media all and (max-width: 479px) {
  ...;
}
```

<br>

---

## Troubleshooting Responsiveness with Dev Tools

Here's the thing: CSS is frustrating. Very frustrating.

<br>

<details>
<summary><strong>You have a nice looking project.</strong></summary>
<br>

<p align="center">

![pokemon](/assets/pikachu1.jpg)

</p>

</details>

<br>

<details>
<summary><strong>You want to add flexbox.</strong></summary>
<br>

<p align="center">

![pokemon](/assets/flexbox1.jpg)

</p>

</details>

<br>

<details>
<summary><strong>You correct flexbox.</strong></summary>
<br>

<p align="center">

![pokemon](/assets/flexbox2.jpg)

</p>

</details>

<br>

<details>
<summary><strong>You delete everything you just did and start working on media queries.</strong></summary>
<br>

<p align="center">

![pokemon](/assets/breakpoint.png)

</p>

</details>

<br>

<details>
<summary><strong>You fix that, then add some more UI elements.</strong></summary>
<br>

<p align="center">

![pokemon](/assets/pickachu2.png)

</p>

</details>

<br>

<details>
<summary><strong>You fix that, then deploy to surge and realize your opacity messed up.</strong></summary>
<br>

<p align="center">

![pokemon](/assets/opacity.png)

</p>

</details>

<br>

---

## Self-Directed Learning

### Videos

- [CSS Responsive Design](https://www.youtube.com/watch?v=BsuCBmzLf_U&list=PLdnONIhPScST0Vy4LrIZiYKpFNoxgyH7J&index=21)
- [CSS Responsive Design - Media Queries](https://www.youtube.com/watch?v=GYygtVolViM&list=PLdnONIhPScST0Vy4LrIZiYKpFNoxgyH7J&index=23)
- [CSS Mobile First - min/max-width/height](https://www.youtube.com/watch?v=iQIj7Lu64M4&index=22&list=PLdnONIhPScST0Vy4LrIZiYKpFNoxgyH7J)

### Readings

- [Responsive Web Design - An Original Introduction](http://alistapart.com/article/responsive-web-design)
- [Why You Don't Need Device Specific Breakpoints](https://responsivedesign.is/articles/why-you-dont-need-device-specific-breakpoints)
- [7 Habits of Highly Effective Media Queries](http://bradfrost.com/blog/post/7-habits-of-highly-effective-media-queries/)
- [Media Queries for Standard Devices](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/)
- [Logical Operators in Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#Logical_operators)
- [A Tale of Two Viewports](http://www.quirksmode.org/mobile/viewports.html)
- [Responsive Design Pattern Examples](https://bradfrost.github.io/this-is-responsive/patterns.html)
- [Complex Navigation Patterns for Responsive Design](http://bradfrost.com/blog/web/complex-navigation-patterns-for-responsive-design/)
- [mediaqueri.es - a collection of responsive site examples](http://mediaqueri.es/)
