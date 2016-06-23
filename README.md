
# Penny Mixins
A set of awesome Sass Mixins


## The Mixins
- [Align](#align)
- [Background](#background)
- [Breakpoints](#breakpoints)
- [Clearfix](#clearfix)
- [Font Size](#font-size)
- [Font Smooth](#font-smooth)
- [Flex Columns](#flex-columns)
- [Float Columns](#float-columns)
- [Google Font Importer](#google-font-importer)
- [Placeholder (Custom Color)](#placeholder)
- [Retina Images](#retina-images)
- [Size](#size)

### Align
Use it to vertically or horizontally align an element to its parent without using Flexbox
The parent item must be with `position: relative` to work.

Example:
```sass
.aligned-both{
  @include align();
}

.aligned-vertical{
  @include align(vertical);
}

.aligned-horizontal{
  @include align(horizontal);
}
```

Output:
```css
.aligned-both {
  position: absolute;
  transform-style: preserve-3d;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); }

.aligned-vertical {
  position: absolute;
  transform-style: preserve-3d;
  top: 50%;
  transform: translateY(-50%); }

.aligned-horizontal {
  position: absolute;
  transform-style: preserve-3d;
  left: 50%;
  transform: translateX(-50%); }
```

### Background
Create a full width contained background with an optional overlay on top of it.

This one uses the `$image-path` variable to get to the img assets.

Example:
```sass
.background{
  @include background('a-background.jpg');
}

.background-with-overlay{
  @include background( 'a-background.jpg', rgba(0,0,0,0.5) );
}


.background-with-2-overlays{
  @include background( 'a-background.jpg', rgba(0,0,0,0.5), rgba(0,0,0, 0.8) );
}

```

Output:
```css
.background {
  background: url("../img/a-background.jpg") no-repeat center/cover; }

.background-with-overlay {
  background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("../img/a-background.jpg") no-repeat center/cover; }

.background-with-2-overlays {
  background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.8)), url("../img/a-background.jpg") no-repeat center/cover; }

```

### Breakpoints
Never do `@media(min-width: xxx)` again, do it in a sensible way.

**This requires the breakpoints map on the settings** you can add remove and rename your breakpoints at will. BYOB (Bring your own Breakpoints)

Example:
```sass
.mobile-first{
  font-size: 1em;
  }
  @include breakpoint(laptop){
    font-size: 2em;
  }
  @include breakpoint(desktop){
    font-size: 3em;
  }
```

Output:
```css
.mobile-first {
  font-size: 1em; }
  @media (min-width: 992px) {
    .mobile-first {
      font-size: 2em; } }
  @media (min-width: 1200px) {
    .mobile-first {
      font-size: 3em; } }
```
### Clearfix
Quickly give cleafix to an element

Example:
```sass
.clearfix{
  @include cf;
}
```

Output:
```css
.clearfix {
  *zoom: 1; }
  .clearfix:before, .clearfix:after {
    content: '';
    display: table; }
  .clearfix:after {
    clear: both; }
```
### Font Size
Px and rem together

Don't forget to set `html { font-size: 62.5%; }`

Example:
```sass
p{
  @include font-size(1.6)
}
```

Output:
```css
p {
    font-size: 16px;
    font-size: 1.6rem;
    line-height: 24px;
    line-height: 2.4rem;
}
```
### Font Smooth
Some fonts need to smooooooth

Example;
```sass
h1{
  @include font-smooth;
}
```

Output:
```css
h1{
  -webkit-font-smoothing: antialiased;
  font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
}
```
### Flex Columns
Give some flex children some col-based widths

**This uses the `$columns--total` variable**

First arg is the number of cols, second optional arg is the total number of columns

Example:
```sass
.four-flex-cols{
  @include flex-cols(4);
}

.seven-flex-cols-of-15{
  @include flex-cols(7, 15);
}
```

Output:
```css
.four-flex-cols {
  max-width: 33.33333%;
  flex-basis: 33.33333%; }

.seven-flex-cols-of-15 {
  max-width: 46.66667%;
  flex-basis: 46.66667%; }
```
### Float Columns
Same idea as the flex-columns but with floats parent should be clearfixed.

Example:
```sass
.eight-cols{
  @include float-cols(8);
}

.nine-cols-of-20{
  @include float-cols(9, 20);
}
```

Output:
```css
.eight-cols {
  float: left;
  width: 66.66667%; }

.nine-cols-of-20 {
  float: left;
  width: 45%; }
```
### Google Font Importer
This just magically works, it looks for the `$font-url--google` and if it exists will import it. Simple!

Example:
```sass
$font-url--google       : "https://fonts.googleapis.com/css?family=Biryani:300,800"
```

Output:
```css
@import url("https://fonts.googleapis.com/css?family=Biryani:300,800");
```

### Placeholder (Custom Color)
Give an input a custom color for the placeholder to get something better than the boring gray

Example:
```sass
.custom-placeholder{
  @include placeholder(red);
}
```

Output:
```css
.custom-placeholder::-webkit-input-placeholder {
  color: red; }

.custom-placeholder::-moz-placeholder {
  color: red;
  opacity: 1; }

.custom-placeholder:-ms-input-placeholder {
  color: red; }

.custom-placeholder::-ms-input-placeholder {
  color: red; }

.custom-placeholder:placeholder-shown {
  color: red; }
```

### Retina Images
Add high resolution images to your site, with a fallback for devices that aren’t displaying high resolution images.

Example:
```sass
div.logo {
  background: url("logo.png") no-repeat;
  @include image-2x("logo2x.png", 100px, 25px);
}
```

Output:
```css
@media not all, (-webkit-min-device-pixel-ratio: 1.3), not all, (min-resolution: 1.3dppx)
div.logo {
  background-image: url('img/logo2x.png');
  background-size: 100px 25px;
}
div.logo {
  background: url('img/logo.png') no-repeat;
}
```

### Size
A really simple mixin for setting width and height of an element

If only one is provided it will be a square.

Great for using with SVGs

Example:
```sass
.square{
  @include size(15px);
}

.rectangle{
  @include size(2em, 2.5em);
}
```

Output:
```css
.square {
  width: 15px;
  height: 15px; }

.rectangle {
  width: 2em;
  height: 2.5em; }
```
