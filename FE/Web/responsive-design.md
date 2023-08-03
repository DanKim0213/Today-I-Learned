# Responsive Design

Table of Content

1. Types of design
1. Responsive Design
1. Media queries
1. Macro layouts
1. Micro layouts
1. Typography
1. Responsive images
1. User interface patterns
1. Furthermore

## 1. Types of design

Before we dive in, I'd like to inform about lots of designs before responsive designs developed. 

- Fixed-width design
    - If you specify a fixed width for your layout, then your layout will only look good at that specific width. If a visitor to your site has a wider screen than the width you have chosen, then there'll be wasted space on the screen. 
- Liquid layouts (a.k.a fluid layouts or flexible layouts)
    - Instead of using fixed widths for your layouts you could make a flexible layout using percentages for your column widths.
    - while a liquid layout will look good across a wide range of widths, it will begin to worsen at the extremes. On a wide screen the layout looks stretched. On a narrow screen the layout looks squashed. Both scenarios aren't ideal.
    - One option is to make a separate subdomain for mobile visitors. But then you have to maintain two separate codebases and designs. And in order to redirect visitors on mobile devices, you'd need to do user-agent sniffing, which can be unreliable and easily spoofed. Chrome will be deprecating its user-agent string for privacy reasons.
- Adaptive layouts
    - One technique involved switching between a handful of fixed-width layouts at specified widths. Adaptive design allowed designers to provide layouts that looked good at a few different sizes, but the design never looked quite right when viewed between those sizes.
- Responsive Web design
    - If adaptive layouts are a mashup of media queries and fixed-width layouts, responsive web design is a mashup of media queries and liquid layouts.


## 2. Responsive Design

> Let the browser do the math!

The term was coined by Ethan Marcotte in an article in A List Apart in 2010. Ethan defined three criteria for responsive design: 
1. Fluid grids 
2. Fluid media 
3. Media queries

But there was one problem. By default mobile browsers assumed that 980 pixels was the width that people were designing for (and they weren't wrong). So even if you used a liquid layout, the browser would apply a width of 980 pixels and then scale the rendered web page down to the actual width of the screen.

If you're using responsive design you need to tell the browser not to do that scaling. You can do that with a meta element in the head of the web page:

> <meta name="viewport" content="width=device-width, initial-scale=1">

- `width=device-width` tells the browser to assume the width of the website is the same as the width of the device.
- `initial-scale=1` tells the browser how much or how little scaling to do. With a responsive design, you don't want the browser to do any scaling at all.

## 3. Media queries

> Designers can adjust their designs to accommodate users. The clearest example of this is the form factor of a user's device; its width, the device aspect ratio, and so on.

If your content is mostly image-based, pixels might make the most sense. If your content is mostly text-based, it probably makes more sense to use a relative unit that's based on text size, like `em` or `ch`

```css
@media (min-width: 25em) {
  // Styles for viewports wider than 25em.
}
```


## 4. Macro layouts

> Macro layouts describe the larger, page-wide organization of your interface.

### 4.1. Grid vs Flexbox

The basic difference between CSS grid layout and CSS flexbox layout is that flexbox was designed for layout in one dimension - either a row or a column. Grid was designed for two-dimensional layout - rows, and columns at the same time. 

Grid:
```css
@media (min-width: 45em) {
  main {
    display: grid;
    grid-template-columns: 2fr 1fr;
  }
}
```

Flexbox:
```css
@media (min-width: 45em) {
  main {
    display: flex;
    flex-direction: row;
  }

  main article {
    flex: 2;
  }

  main aside {
    flex: 1;
  }
}
```

### 4.2. Do you need a media query?

Media queries work fine when you're applying changes to a few elements, but if the layout needs to be updated a lot, your media queries could get out of hand with lots of breakpoints. 

By applying some smart rules in flexbox or grid, it's possible to design dynamic macro layouts with minimal CSS and without any media queries.

For example, say you've got a page full of card components. The cards are never wider than 15em, and you want to put as many cards on one line as will fit. 

Grid:
```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(15em, 1fr));
  grid-gap: 1em;
}
```

Flexbox:
```css
.cards {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 1em;
}
.cards .card {
  flex-basis: 15em;
  flex-grow: 1;
}
```

## 5. Micro layouts

> Build flexible components that can be placed anywhere. Smaller components within the page can have their own self-contained layouts.

Without knowing for sure where a component will end up, you need to make sure that the component can adjust itself to its container.

Let's brifely look through Grid & Flexbox. And then, let's dive in Container queries, which feature has been landing from Feb 2023. 

### 5.1. Grid & Flexbox

Grid:
```css
h1 {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  gap: 1em;
}
h1::before,
h1::after {
  content: "";
  border-top: 0.1em double black;
  align-self: center;
}
```

Flexbox:
```css
.media {
  display: flex;
  align-items: center;
  gap: 1em;
}
.media-illustration {
  flex: 1;
  max-inline-size: 200px;
}
.media-content {
  flex: 3;
}
```

### 5.2. Container queries

Components itself have no awareness of its context. To be able to apply contextually relevant styles, your components need to know more than the size of the viewport they are inside.

To start, define which elements will act as containers:
```css
main,
aside {
  container-type: inline-size; // horizontal axis 
}
```


If a component is inside one of those containers (`main` or `aside`), you can apply styles in a way that's quite similar to media queries:
```css
.media-illustration {
  max-width: 200px;
  margin: auto;
}

@container (min-width: 25em) {
  .media {
    display: flex;
    align-items: center;
    gap: 1em;
  }

  .media-illustration {
    flex: 1;
  }

  .media-content {
    flex: 3;
  }
}
```

Container queries allow you to style components in an independent way. The width of the viewport is no longer what matters. You can write rules based on the width of the containing element.

## 6. Typography

> Good typography is all about presenting your text in an appropriate way.

### 6.1. Scaling Text

Switching between fixed text sizes at specific breakpoints is quite jumpy. A more responsive approach is to let the user's device width influence the text size.

```css
html {
  font-size: clamp(1rem, 0.75rem + 1.5vw, 2rem);
}
```

### 6.2. Line

Don't set your line-lengths with a fixed unit like `px`. Users can scale their font size up and down and your line lengths should adjust accordingly. Use a relative unit like `rem` or `ch`.

Use unitless values for your `line-height` declarations. This ensures that the line height is relative to the `font-size`.

```css
article {
  max-inline-size: 66ch;
  line-height: 1.65;
}
```

### 6.3. Web fonts

Use @font-face to tell browsers where to find your web font files. Use woff2 as your web font format. It's well supported and has the best performance gains.

It's common to use both url() and local() together, so that the user's installed copy of the font is used if available, falling back to downloading a copy of the font if it's not found on the user's device.

```css
@font-face {
  font-family: 'Roboto';
  src: 
    local('Roboto')
    url('/fonts/roboto-regular.woff2') format('woff2');
}
body {
  font-family: Roboto, sans-serif;
}
```

## 7. Responsive images

> Images have an intrinsic size. Give your visitors the most appropriate images for their devices and screens.

### 7.1. General usage of img

#### 7.1.1. img in css
- `max-inline-size: 100%` and `block-size: auto`: Images should never be rendered at a size wider than their containing element. 
-  `aspect-ratio`: If your design calls for a images to have an aspect ratio that's different to the image's real dimensions, squash or stretch the image to make it fit your preferred aspect ratio. 
- `object-fit: cover` and `object-position`: adjust the focus of the crop if the cropping at the top and bottom evenly is an issue.

```css
img {
  max-inline-size: 100%;
  block-size: auto;
  aspect-ratio: 2/1;
  object-fit: cover;
  object-position: top center;
}

```


#### 7.1.2. `<img>` tag
- src: 
- `alt`: Images in HTML are content. That's why you **always** provide an alt attribute with a description of the image for screen readers and search engines.
- `width` and `height`: This will stop your other content jumping around when the image loads.
- `loading`: Use the loading attribute to tell the browser whether to delay loading the image until it is in or near the viewport. `eager` is the default behavior.


```html
<img
  src="image.png"
  alt="A description of the image."
  width="300" 
  height="200"  
  loading="lazy" 
>
```

### 7.2. Fetch Priority

#### 7.2.1. `<img>`
- `loading="eager"` and `fetchpriority="high"`: This will tell the browser to fetch the image right away, and at high priority. But the browser will have to **de-prioritize another resource** such as a script or a font file. Only set fetchpriority="high" on an image if it is truly vital. 

```html
<img
 src="hero.jpg"
 alt="A description of the image."
 width="1200"
 height="800"
 loading="eager"
 fetchpriority="high"
>
```

### 7.3. Multiple versions of  image

Like the `srcset` attribute, the `picture` element will update the value of the `src` attribute in that `img` element. The difference is that where the `srcset` attribute gives suggestions to the browser, the `picture` element gives commands. 

- srcset
```html
<img
 src="small-image.png"
 alt="A description of the image."
 width="300"
 height="200"
 loading="lazy"
 srcset="small-image.png 300w,
  medium-image.png 600w,
  large-image.png 1200w"
 sizes="(min-width: 66em) 33vw,
  (min-width: 44em) 50vw,
  100vw"
>
```
- `<picture>`
```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="A description of the image." 
    width="300" height="200" loading="lazy" decoding="async">
</picture>
```

### 7.4. `<img>` vs `background-image` in css

`<img>` represents content while `background-image` represents presentational images. 

Likewise `srcset` of `<img>` specifies multiple image candidates, you can specify multiple image candidates using the `image-set` function for `background-image`.

### 7.5. Strategy

A good image strategy makes your site feel snappy and sharp, regardless of the user's device or network connection. There are many factors to consider when you're adding images to your site:

- Reserving the right space for each image. 
- Figuring out how many sizes you need. 
- Deciding whether the image is content or decorative.

## 8. User interface patterns

> A successful responsive design makes the most of every form factor.

### 8.1. Guide

Design for smaller screens first. It's easier to adapt small-screen designs to larger screens than the other way around. If you design for a large screen first, there's a danger that your small-screen design will feel like an afterthought.

### 8.2. Try not to hide anything anyway 

However, if not, consider these patterns: 
- Overflow pattern: Users can swipe horizontally to reveal the links that aren't immediately visible.
- Progressive disclosure: Your navigation is hidden by default and provided a toggle mechanism for users to show and hide the contents.



## 9. Furthermore

- [Learn Responsive Design](https://web.dev/learn/design/)
- [Patterns](https://web.dev/patterns/)
- [CSS: Cascading Style Sheets](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [@font-face](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face)
- [Relationship of grid layout to other layout methods](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Relationship_of_grid_layout_with_other_layout_methods)
