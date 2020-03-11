# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Responsive CSS Design

## LEARNING OBJECTIVES

During this lesson, we're going to touch on:

- Understanding responsive design concepts, and the difference between mobile-up and desktop-down.
- Understanding that responsive design is dictated by _visual_ break points, not device sizes.
- Identifying the various CSS units of measurement and when alternatives are advantageous.
- Understanding and plan for responsive screen sizes, including identifying breakpoints and implementing media queries.
- Understanding how the CSS cascade– and organization of your code– will affect your app.

***

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

<summary><strong>Responsive Design is <b>not</b> device-specific. Why?</strong></summary>
<br>

A responsive site doesn't just look good on the newest phone, watch, tablet, or mega-screen; it looks good on *any* screen– and, on desktop screens, at any width of the browser window.

This might seem impossible, but it's relatively straightforward. All that's required is writing a series of rules, known as media queries, that check the size of the browser/device on which the site is being viewed, and adjust the CSS as needed.

</details>

<br>

Before we dive further, let's consider some other factors.

***

![](https://media2.giphy.com/media/uOZg6EKGGZG5G/source.gif)

<br>

***

## CSS Units

Of course, we've worked almost entirely with the `px`, or pixel, until now. The pixel is one option for an _**absolute**_ length, but there are also _**relative**_ and _**calculated**_ lengths.

<br>

### Absolute Values

| name       | value | description         |
| :--------- | :---: | :------------------ |
| pixel      |  px   |                     |
| point      |  pt   | 1pt = 1/72 of 1in   |
| pica       |  pc   | 1pc = 12 pt         |
| inch       |  in   | 1in = 96px = 2.54cm |
| centimeter |  cm   |                     |
| millimeter |  mm   |                     |

<br>

<details>
<summary><strong>What even is a pixel?</strong></summary>
<br>

For a long time, screen density was 96ppi. This means 1 pixel was 1/96th of an inch. Absolute lengths based on common measurements will render according to this ratio, not the actual length relative to the viewer. This is called the **1:96 fixed ratio** of CSS.

Absolute lengths are much more important for _**print**_ design. Commonly, high definition images and PDFs will print at 300 or 450dpi.

For CSS, we highly discourage any absolute lengths, besides the pixel; and even then, use them selectively.

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
<summary><strong>Why are relative lengths helpful?</strong></summary>
<br>

When we're trying to design responsive apps, relative lengths can help bake in responsiveness, rather than using all absolute lengths and then having to adjust for different sizes.

</details>

<br>

### Calculated Values

Occasionally, calculated lengths will help you prepare for edge cases:

| value | example            |
| :---: | :----------------- |
| auto  | `width: auto`      |
| calc  | `calc(80% - 50px)` |

<br>

### Resolution & Pixel-Density Values

Rarely, you may see values that account for the differences between high-density (such as Retina) and low-density screens:

| name                | value | example                     |
| :------------------ | :---: | :-------------------------- |
| dots per inch       |  dpi  | `min-resolution: 192dpi`    |
| dots per centimeter | dpcm  | `max-resolution: 150dpi`    |
| device pixel ratio  | dppx  | `min-resolution: 2dppx`     |
| dppx alias          |   x   | `min-device-pixel-ratio: 2` |

<br>

***

## Finally, Media Queries

Media queries are _conditional style rules_ for the size of the user's viewport which is rendering the site. Let's look at an example.

We already know that if we do something like this:

```css
p {
  color: red;
}

p.blue_text {
  color: blue;
}
```

By default, all `p` tags will have red text – unless they have the class `blue_text`, in which case the text will be blue. We can do a similar thing with media queries.

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

Now all `p` tags will be red until the screen size reaches 600px, when they'll turn blue. In practice, a media query alerts the user's browser to render additional styling rules, if the user's viewport falls within the width defined by your query.

However, this begs the question, how do we determine the widths to use in the media query, and how can we possibly account for all the variations in screens?

<br>

### Common Desktop Resolutions

| Model & Size                   | Width  | Height  | Density (ppi) |
| :----------------------------- | :----: | :-----: | :-----------: |
| iMac 27" (Retina 5K)           | 5120px | 2880px  |    219 PPI    |
| iMac 27"                       | 2560px | 1440px  |    109 PPI    |
| iMac 21.5" (Retina 4K)         | 4096px | 2304px  |    218 PPI    |
| iMac 21.5"                     | 1920px | 1080px  |    102 PPI    |
| MacBook Pro 16" (Retina)       | 3072px | 1,920px |    226 PPI    |
| MacBook Pro 15" (Retina)       | 2880px | 1920px  |    226 PPI    |
| MacBook Pro & Air 13" (Retina) | 2560px | 1600px  |    227 PPI    |
| MacBook Pro 13"                | 1280px |  800px  |    113 PPI    |
| MacBook 12" (Retina)           | 2304px | 1440px  |    226 PPI    |
| MacBook Air 11"                | 1366px |  768px  |    135 PPI    |

<br>

### Breakpoints

The best approach to identifying the size of a media query is to test your site for breakpoints. A breakpoint is simply a specific browser width where the layout either breaks or no longer follows the intended design.

Another way to think about it: The design looks 'off' or just plain bad!

<br>

### Responsive Developer Tools

You can use Chrome Dev Tools to measure the width of a page open in the browser. Adjust the width of the browser and identify breakpoints. If you see an unintended or unacceptable change occur in the design or layout, your media query should be set to the width of the browser when the change occurs.

[Quick Demo](https://beta.crisisinternational.org)

<br>

***

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
@media all and (min-width:1200px){ ... }
@media all and (min-width: 960px) and (max-width: 1199px) { ... }
@media all and (min-width: 768px) and (max-width: 959px) { ... }
@media all and (min-width: 480px) and (max-width: 767px){ ... }
@media all and (max-width: 599px) { ... }
@media all and (max-width: 479px) { ... }
```

<br>

***

## CSS Detective Work

So what happens when everything is breaking? Let's consider some examples of how different measurements can work well together.



<br>

***

#### Hungry for More?
##### Exercises
- [Make the Dream Team Responsive!](independent-practice/starter-code)
  - [Check Your Work](independent-practice/solution-code)

##### Videos
- [CSS Responsive Design](https://www.youtube.com/watch?v=BsuCBmzLf_U&list=PLdnONIhPScST0Vy4LrIZiYKpFNoxgyH7J&index=21)
- [CSS Responsive Design - Media Queries](https://www.youtube.com/watch?v=GYygtVolViM&list=PLdnONIhPScST0Vy4LrIZiYKpFNoxgyH7J&index=23)
- [CSS Mobile First - min/max-width/height](https://www.youtube.com/watch?v=iQIj7Lu64M4&index=22&list=PLdnONIhPScST0Vy4LrIZiYKpFNoxgyH7J)

##### Readings
- [Responsive Web Design - An Original Introduction](http://alistapart.com/article/responsive-web-design)
- [Why You Don't Need Device Specific Breakpoints](https://responsivedesign.is/articles/why-you-dont-need-device-specific-breakpoints)
- [7 Habits of Highly Effective Media Queries](http://bradfrost.com/blog/post/7-habits-of-highly-effective-media-queries/)
- [Media Queries for Standard Devices](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/)
- [Logical Operators in Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#Logical_operators)
- [A Tale of Two Viewports](http://www.quirksmode.org/mobile/viewports.html)
- [Responsive Design Pattern Examples](https://bradfrost.github.io/this-is-responsive/patterns.html)
- [Complex Navigation Patterns for Responsive Design](http://bradfrost.com/blog/web/complex-navigation-patterns-for-responsive-design/)
- [mediaqueri.es - a collection of responsive site examples](http://mediaqueri.es/)
