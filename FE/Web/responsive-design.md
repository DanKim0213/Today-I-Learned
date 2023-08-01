# Responsive Design

## Types of design

There were lots of designs before responsive designs occurred. 

- Fixed-width design
    - If you specify a fixed width for your layout, then your layout will only look good at that specific width. If a visitor to your site has a wider screen than the width you have chosen, then there'll be wasted space on the screen. 
- Liquid layouts
    - Instead of using fixed widths for your layouts you could make a flexible layout using percentages for your column widths.
    - while a liquid layout will look good across a wide range of widths, it will begin to worsen at the extremes. On a wide screen the layout looks stretched. On a narrow screen the layout looks squashed. Both scenarios aren't ideal.
    - One option is to make a separate subdomain for mobile visitors. But then you have to maintain two separate codebases and designs. And in order to redirect visitors on mobile devices, you'd need to do user-agent sniffing, which can be unreliable and easily spoofed. Chrome will be deprecating its user-agent string for privacy reasons.
- Adaptive layouts
    - One technique involved switching between a handful of fixed-width layouts at specified widths. Adaptive design allowed designers to provide layouts that looked good at a few different sizes, but the design never looked quite right when viewed between those sizes.
- Responsive Web design
    - If adaptive layouts are a mashup of media queries and fixed-width layouts, responsive web design is a mashup of media queries and liquid layouts.


## Responsive Design

The term was coined by Ethan Marcotte in an article in A List Apart in 2010. Ethan defined three criteria for responsive design: 
1. Fluid grids 
2. Fluid media 
3. Media queries

But there was one problem. By default mobile browsers assumed that 980 pixels was the width that people were designing for (and they weren't wrong). So even if you used a liquid layout, the browser would apply a width of 980 pixels and then scale the rendered web page down to the actual width of the screen.

If you're using responsive design you need to tell the browser not to do that scaling. You can do that with a meta element in the head of the web page:

> <meta name="viewport" content="width=device-width, initial-scale=1">

- `width=device-width` tells the browser to assume the width of the website is the same as the width of the device.
- `initial-scale=1` tells the browser how much or how little scaling to do. With a responsive design, you don't want the browser to do any scaling at all.

## Furthermore

- [Learn Responsive Design](https://web.dev/learn/design/)
