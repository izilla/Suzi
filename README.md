# Suzi

## A responsive, Sass UI Framework by [Izilla](http://izilla.com.au)

### v1.2.0 (2013-12-12)

Suzi is the starting point for all of our web projects and a culmination of 6+ years' experience in maintaining a front-end framework.

While some of its markup patterns and styles are directly related to our CMS, [Cognition](http://www.cognitionecm.com), we hope Suzi is flexible enough for others to use, learn and cherry pick from.

### Features

* Built in a mobile-first, responsive philosophy *(but can easily be used for fixed sites as well)*
* Mixins for lots of CSS3 features including gradients with SVG & CSS3PIE support, rems with fallbacks and CSS triangles
* Starter content styles, including clean typography, lists, tables, etc
* Starter form element styles: stacked on small-screen to 2-column at the breakpoint of your choice
* Simple form validation
* Responsive, lazy-load, touch-friendly carousels with optional navigation & pagination, analytics tracking & cookie-based remembering of last visible slide
* Simple, accessible JavaScript tabs with cookie-based remembering of the open pane
* Simple, accessible JavaScript accordions which transition to and from `height: auto`, and support multiple open panes
* Tabs instead of spaces :)

---

### Installation

1. Install [Ruby](http://www.ruby-lang.org) *(and add it to your Path Environment Variable on Windows)*
2. Install [Sass](http://sass-lang.com)
3. Install [node.js](http://nodejs.org)
3. Download or clone Suzi
4. If using Grunt, in a shell:
	1. `npm install` *(first-run only)*
	2. `grunt`
5. If using Sass only, run sassqwatch.bat *(on Windows)* or bash sassqwatch.sh *(on Mac)*

---

### Usage

* Set up variables for colors, fonts, sizes, breakpoints, etc in /css/site/partials/_config.scss
* Add @font-face declarations to /css/site/partials/_fonts.scss
* Make simple customisations to links, headings, lists & tables in /css/site/partials/_simple.scss
* Make simple customisations to form elements in /css/site/partials/_forms.scss
* Modify the carousels in /css/site/partials/_slider.scss
* Create and add site specific partials to /css/site/partials/_site.scss
* Add any LT IE9 overrides to /css/site/partials/_ltie9.scss
* Add any print overrides to /css/site/partials/_print.scss

---

### Mixins and Functions

#### Helper functions

* `strip-units($number)`

	Strips units from the number specified

* `em($pixels, $context: 16, $unitless: false)`

	Converts a pixel value to ems, with an optional parameter to make it unitless (which is useful for line-heights)
	
	* `$pixels`: target size in pixels
	* `$context`: context size in pixels (default: 16)
	* `$unitless`: whether to omit the em unit (default: false)

* `percent($pixels, $context: $site-width)`

	Converts a pixel value to a percentage
	
	* `$pixels`: target size in pixels
	* `$context`: context size in pixels (default: $site-width)

#### Functional mixins

* `rem($property, $values, $use-px-fallback: $rem-with-px-fallback)`

	Converts a pixel value to rems, while also outputting the pixel fallback (optional)
	
	* `$property`: valid CSS property
	* `$values`: valid CSS value in pixels
	* `$use-px-fallback`: whether to output a pixel fallback as well (default: $rem-with-px-fallback [true])

* `gradient($nodes: (#f6f8f9, 0%, #e5ebee, 50%, #d7dee3, 50%, #f2f5f7, 100%), $direction: 'to bottom', repeating: false)`

	Outputs the complete CSS3 gradient syntax for Chrome, Safari, Firefox, Opera, IE10, other capable browsers and SVG for IE9

	* `$nodes` takes a list of comma-separated #color, position% pairs. If only a single color is passed in, a plain `background` or `background-color` will be created depending on `$use-background-property`
	* `$direction` takes either the legacy syntax or the unprefixed W3C syntax, including angles. The following angles are supported for SVGs: 0, 10, 45, 90, 135, 170, 180, 190, 225, 270, 315, 350
	* `$repeating`: whether to create repeating linear gradients (default: false)
	* Uses the background property (and background-image for IE9) unless the global `$use-background-property` is `false`
	* Outputs a fallback background of the last color in the list unless the global `$use-background-fallback` is `false`
	* Outputs base 64 SVG syntax for IE9 unless `$repeating` is true
	* Outputs CSS3PIE syntax for LT IE9 unless the global `$use-pie-background` is `false` or `$repeating` is true

* `grid($breakpoints: (480, 600, 768, 960), $percentages: (10, 20, 25, 30, 33.3333, 40, 50, 60, 66.6666, 70, 75, 80, 90, 100))`

	Outputs relevant media queries and classes for Suzi's flexible and responsive grid system
	
	* `$breakpoints`: A list of the breakpoints (in pixels) that media queries and classes should be generated for (default: 480, 600, 768, 960))
	* `$percentages`: A list of the class name percentages to be output for each breakpoint (default: 10, 20, 25, 30, 33.3333, 40, 50, 60, 66.6666, 70, 75, 80, 90, 100)

* `hover($pseudo: false)`

	Outputs `:hover` & `:focus` rules for the current element
	
	* `$pseudo`: the name of a single pseudo-element (after, before) or a list of multiple to create `:hover` & `:focus` rules for
	
* `nth-child($an: 2n, $sibling: '*', $count: 15)`

	Allows nth-child functionality for .ltie9 (if you can't/don't want to use Selectivzr) by outputting crazy sibling selectors
	
	* `$an`: the counting method, eg: 2n, 3n, odd (default: 2n)
	* `$an` can also be a list, with the 2nd parameter being the modifier, eg: 2 for ($an+2) or -3 for ($an-3)
	* `$sibling`: the sibling element selector, eg: 'li', 'div' (default: '*')
	* `$count` how many sibling selectors to support, eg: 10, 20 (default: 15)

* `triangle($direction: right, $width: 5px, $height: 10px, $color: $std-link-color, $layout: true, $border-style: true, $webkit-rotate: true, $important: false)`

	Outputs a CSS triangle for use in :before/:after pseudo-elements. It duplicates the rule, using rgba for transparency to prevent 'black fringes'

	* `direction`: up, down, left, right (default: right)
	* `$width`: width in pixels (default: 5px)
	* `$height`: height in pixels (default: 10px)
	* `$color`: triangle's hex color (default: $std-link-color)
	* `$layout`: whether to output CSS `content`, `display`, `height` & `width` properties (default: true)
	* `$border-style`: whether to output the CSS `border-style` property (default: true)
	* `$webkit-rotate`: whether to rotate the triangle by 360deg in WebKit for smoother appearance (default: true)
	* `$important`: whether to also output `!important` on `border-color` and `border-width` properties (default: false)

#### Class mixins

* `classquery($class-name, $output-ltie9-rule)`

	Generates `.classquery-$class-name & (optional) .ltie9 [data-classquery*=".classquery-$class-name"]` selectors to be used with class.query.js to manage responsive content
	
	* `$class-name`: the class name to use (default: default)
	* `$output-ltie9-rule`: whether to output the `.ltie9` rule. Set to false if the class is used for a max-width media query (default: true)

* `clearfix`

	Float clearing without hacks for IE7+ and every other browser

* `hidden($hide: true)`

	Accessibly hide (and un-hide) an element off-screen
	
	* `$hide`: whether to hide or unhide the (default: true)

* `hide-text($display: false, $width: false, $height: false)`

	Hide an element's text content

	* `$display`: sets the `display` property to a value of your choice (default: false)
	* `$width`: sets the width of the element (default: false)
	* `$height`: sets the heightof the element (default: false)

* `horizontal($vertical-align: top)`

	Sets the `UL` specified (or first `UL` of a parent element) and its immediate `LI`s to use `display: table` to create an evenly spaced, horizontal list for modern browsers and uses floats for `.ltie8`. Used in the `.horizontal` and `.horizontal_always` classes
	
	* `$vertical-align`: the `vertical-align` property to give to the child `LI`s (default: top)
	
#### CSS Property mixins

* `animation($property: default 1s ease)`

	Outputs -moz, -o-, -webkit and unprefixed `animation` with the value passed in (default: default 1s ease)
	
* `animation-delay($value: 1s)`

	Outputs -moz, -o-, -webkit and unprefixed `animation-delay` with the value passed in (default: 1s)
	
* `animation-duration($value: 1s)`

	Outputs -moz, -o-, -webkit and unprefixed `animation-duration` with the value passed in (default: 1s)

* `background($color, $duplicate-as-pie: false)`

	Outputs a background rule with the $color specified. If $duplicate-as-pie is true, it will also output a -pie-background property (useful for overriding a gradient on hover, for example)

* `border-radius($radius: 5px, $background-clip: padding-box)`

	Outputs -webkit and unprefixed `border-radius`
	
	* `$radius`: radius to use (default: 5px)
	* `$background-clip`: which `background-clip` property to use (if any) (default: padding-box)

* `box-shadow($shadow: 0 1px 3px rgba(0,0,0,.25))`

	Outputs, -webkit and unprefixed `box-shadow` with the value passed in (default: 0 1px 3px rgba(0,0,0,.25))

* `box-sizing($boxsize: border-box)`

	Outputs -moz, -webkit and unprefixed `box-sizing` with the value passed in (default: border-box)

* `font-size-line-height($font-size, $line-height: false, $important: false)`

	Outputs a rem (and pixel fallback) font-size and an optional unitless line-height from the values provided
	
	* `$font-size`: target `font-size` to achieve in pixels
	* `$line-height`: target `line-height` size to achieve in pixels if not `false` (default: false)
	* `$important`: whether to also output an `!important` declaration on both properties (default: false)
	
* `keyframes($name)`

	Outputs -moz, -o-, -webkit and unprefixed animation `@keyframes` named with the value passed in

* `line-height($target, $context: 16, $important: false)`

	Outputs a unitless line-height from the target and context sizes provided
	
	* `$target`: target `line-height` size to achieve in pixels
	* `$context`: the `font-size` in pixels of the current element (default: 16)
	* `$important`: whether to also output an `!important` declaration (default: false)

* `pie($position: relative, $path: false)`

	Outputs a `position` property and CSS3PIE `behavior` property with path to PIE.htc
	
	* `$position:` `position` property to use or `false` for none (default: relative)
	* `$path`: path to PIE.htc if specified, otherwise uses `$default-pie-path` variable when `false` (default: false [$default-pie-path: '/css/PIE.htc'])

* `rgba-background($color, $opacity: 0.5, $use-fallback: true, $use-background-color: false)`

	Converts a background color and opacity to `rgba`, with the option to output a default fallback color or a composite fallback color of your choice
	
	* `$color`: color to be converted - either a single value or a list
	* if `$color` is a list, the second parameter is used as the fallback colour - useful for composite fallbacks
	* `$opacity`: alpha opacity of the color (default: 0.5)
	* `$use-fallback`: whether to output the fallback color (default: true)
	* `$use-background-color`: whether to use `background-color` property instead of `background` (default: false)

* `transform($transform-function: none)`

	Outputs, -ms, -moz, -o, -webkit and unprefixed `transform` with the value passed in (default: none)
* `transform-origin($transform-origin: 50% 50% 0)`


	Outputs, -ms, -moz, -o, -webkit and unprefixed `transform-origin` with the value passed in (default: 50% 50% 0)

* `transition($property: all ease 0.2s)`

	Outputs, -moz, -o, -webkit and unprefixed `transition` with the value passed in (default: all ease 0.2s)
	Instances of `transform` or `transform-origin` will be prefixed as required.

* `transition-delay($delay: 0.2s`

	Outputs, -moz, -o, -webkit and unprefixed `transition-delay` with the value passed in (default: 0.2s)

* `transition-duration($duration: 0.2s)`

	Outputs, -moz, -o, -webkit and unprefixed `transition-duration` with the value passed in (default: 0.2s)

* `transition-property($property: all)`

	Outputs, -moz, -o, -webkit and unprefixed `transition-property` with the value passed in (default: all)
	Instances of `transform` or `transform-origin` will be prefixed as required.

* `transition-timing-function($timing: ease)`

	Outputs, -moz, -o, -webkit and unprefixed `transition-timing-function` with the value passed in (default: ease)

31 transition-timing-function variables are defined in src/partials/_easing-functions.scss

* `viewport($width: device-width)`

	Outputs, -moz, -ms, -o, -webkit and unprefixed `@viewport` with the value passed in (default: device-width)

#### Media Query mixins

Four variables are provided for media query operators: `$min`, `$max`, `$min-h` & `$max-h` for `min-width`, `max-width`, `min-height` and `max-height`, respectively

* `media-query($value, $ltie9: $use-ltie9-mq-fallbacks, $operator: $min, $px: false)`

	Outputs a standard media query using ems and an optional .ltie9 fallback
	
	* `$value`: pixel value for the breakpoint
	* `$ltie9`: whether to output .ltie9 fallback (default: $use-ltie9-mq-fallbacks [true])
	* `$operator`: operator for the breakpoint, e.g. min-width, max-width, min-height, max-height (default: $min [min-width])
	* `$px`: use px instead of ems

* `media-query-and($first-value, $second-value, $first-operator: $min, $second-operator: $max, $px: false)`

	Outputs a media query with an 'and' condition and an optional .ltie9 fallback (unless max-width is less than $site-width)
	
	* `$first-value`: pixel value for the first breakpoint
	* `$second-value`: pixel value for the second breakpoint
	* `$ltie9`: whether to output .ltie9 fallback (default: $use-ltie9-mq-fallbacks [true])
	* `$first-operator`: operator for the first breakpoint, e.g. min-width, max-width, min-height, max-height (default: $min [min-width])
	* `$second-operator`: operator for the second breakpoint
	* `$px`: use px instead of ems

* `media-query-retina`

	Outputs a media query for Hi-DPI devices

---

A Dreamweaver extension is available which adds code hint support for all of the above mixins and functions. Download it here: https://github.com/stowball/Suzi-Code-Hints

---

Copyright (c) 2013 [Izilla Partners Pty Ltd](http://www.izilla.com.au)  
Licensed under the MIT license *(see [LICENSE](https://github.com/izilla/Suzi/blob/master/LICENSE) for details)*