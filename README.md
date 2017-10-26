# Dynamit's Front-end Playbook

---

# Table of Contents

1. [Development Process](#development-process)
  * [Version Control](#version-control)
  * [Code Quality](#code-quality)
  * [Ops](#ops)
  * [Preventative Maintenance](#preventative-maintenance)
2. [Markup](#markup)
3. [Style Sheets](#style-sheets)
4. [JavaScript](#javascript)
5. [Performance](#performance)
6. [SEO & Meta](#seo--meta)
7. [Accessibility](#accessibility)
  * [Visually Hidden Text (for Screen Readers)](#visually-hide-text-but-allow-screen-readers-to-read)
  * [Links](#links)
  * [Skip Links/Bypass Blocks](#skip-links--bypass-blocks)
  * [Visible Focus](#visible-focus)
  * [Images](#images)
  * [Headings](#headings)
  * [Color Contrast](#color-contrast)
  * [Tab/Focus Order](#tab-order)
  * [Form Elements](#form-elements)
  * [Miscellaneous](#random-tidbits)

---

# Development Process

## Version Control

- use version control
- use semver
- keep branching to a minimum, prune dead branches
- associate a ticket number with a commit when applicable

## Code Quality

- Adhere to the [Code Style Guide](http://dynamit.github.io/code-standards/standards/front-end/)
- DRY
- Leverage Technical Debt
- Use IE VMS to test code (or [BrowserStack](https://www.browserstack.com))
- Thoroughly document code use [JSDoc](http://usejsdoc.org/) conventions

## Ops

- use codepen to rapidly protoype ideas
- use the front-end starter kit when starting a project. Continually improve it by contributing learning during each project.
- use gulp to manage the asset compilation pipeline
- use webpack for asset bundling

## Preventative Maintenance

- keep tooling up to date
- keep disk perms clean

# Markup

- use semantic markup?
- structure pages (headings, sections) in logical, linear order
- `button type=button` outside the context of a form

# Style Sheets

- Adhere to the [Code Style Guide](http://dynamit.github.io/code-standards/standards/front-end/stylesheets.html)
- use Sass
- use low-specificty selectors. avoid ids, tags, combining selectors, prefer classes and attr selectors
- compose styles mobile-first. example: @media (min-width: 768px) as opposed to @media (max-width: 767px)
- use bullet-proof font-face declaration

# JavaScript

- vanilla if possible
- use [axios](https://github.com/axios/axios) for ajax
- use js-cookie
- write in modules
- prefer libraries to full-blown frameworks
- write [modern javascript](https://babeljs.io/) when you can
- keep bundles small (< 50k), consider [lazy-loading](https://webpack.js.org/guides/lazy-loading) pages / components

# Performance

- use [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
- turn on server-side caching
- develop for mobile users on 3G (slower) networks
- test on real devices
- use progressive jpgs
- use [resource hints](https://www.keycdn.com/blog/resource-hints/)
- prevent render-blocking javascript using [async or defer](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)
- gzip
- minify scripts and stylesheets
- turn off sourcemaps in production
- reduce http requests
- lazy-load [css](https://github.com/filamentgroup/loadCSS) and [js](https://webpack.js.org/guides/lazy-loading)
- lazy load [images](https://github.com/aFarkas/lazysizes)

# SEO & Meta

Include a canonical url tag on each page. Use [trailing slashes](http://googlewebmastercentral.blogspot.com/2010/04/to-slash-or-not-to-slash.html) appropriately. Prefer `https` when available.

```html
<link rel="canonical" href="https://example.com/some-page" />
```

- use a well-formatted title tag on every page
- include social meta data https://adactio.com/journal/9881
- include a retina favicon https://daringfireball.net/2013/01/retina_favicons
- add schema.org tags

# Accessibility
## Visually Hide Text, But Allow Screen Readers to Read

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip-path: rect(0,0,0,0);
  border: 0;
}
```

## Links
- Avoid using ALL CAPS (even `text-transform: uppercase` can make it sound like a screen reader is yelling at you)
- Use visually hidden spans to add additonal context

```html
<!-- not much context -->
<a href="tel:18885555555">1-888-555-5555</a>

<!-- text is hidden visually, but screen reader can read it -->
<a href="tel:18885555555"><span class="visually-hidden">For more information on XYZ Corp. call</span> 1-888-555-5555</a>
```

- Don't use URLs as only text
- When a link will do something unexpected, announce that to the user
- Don't use `target="_blank"` (confusing to the user, removes back button functionality)
- If `target="_blank"` must be used, inform the user they will be taken away from the site
- Font icon / SVG links need to have, at the very least, complimentary text that explains the link
- For internal actions, use `<button>`
- For taking users away from the current page, use `<a>`
- `<a>` must always have an `href` to pass testing
- Don't bother using [`title`](https://www.paciellogroup.com/blog/2012/01/html5-accessibility-chops-title-attribute-use-and-abuse/)

## Skip Links / Bypass Blocks

Coming Soon

## Visible Focus
- [WCAG 2.4.7](http://www.w3.org/TR/2012/NOTE-UNDERSTANDING-WCAG20-20120103/navigation-mechanisms-focus-visible.html) - Any keyboard operable user interface has a mode of operation where the keyboard focus indicator is visible. (Level AA)
- Never use `outline: none`
- Can update the outline so it looks different than default, but a visible border must be displayed
- Common failure is using `blur()` to take off focus, instead focus on another item
- Give your elements `:focus` wherever you have `:hover` in your CSS
- Focus needs to be taken into account when using `.hover()`
- Typical failures occur for dropdown navigation not shown when the user focuses on a the top level menu item

## Images
- Always have alt text of some sort
```html
<!-- indicates the image is decorative and does not have text in the image -->
<img alt="" src="../..">

<!-- indicates the image is decorative and does not have text in the image -->
<img alt="This text should be descriptive/informative, but not repeat information that is already present" src="../..">
```
- `alt` text Should be kept under 125 characters
- Items like charts or maps that represent a lot of information, `<caption>` or `longdesc` should be used (example needed)
- GIFs should not have more than 3 flashes per second
- If possible, don't play GIF until hovered over
- Never use the filename as alt text

## Headings
- [Use semantic markup and structure your page with one](http://adrianroselli.com/2013/12/the-truth-about-truth-about-multiple-h1.html) `<h1>`
- Think of your page as the table of contents
- Turn off styling to test if the visual heirarchy makes sense
- Screen readers use headings as hot key points

## Color Contrast
- #000 on #fff background is not the best for readability and can [cause eye strain](http://ux.stackexchange.com/questions/53264/dark-or-white-color-theme-is-better-for-the-eyes)
- Ratio of 4.5:1 must be met for regular text
- 19px and bold is 3:1, 24px and basic color is 3:1
- Dyslexics do better with unique fonts (Comic Sans all characters are unique)
- Automated testing tools can't judge color contrast of text over an image
- Images with text in them need to have this contrast level and alt text equal to the text on the image
- [Testing color contrast] (http://jxnblk.com/colorable/demos/text/)

## Tab Order
- `tabindex="0"` and `tabindex="-1"` are all that should ever be used
- Never use `tabindex="1+"`
- Seriously. Don't.
- `tabindex="-1"` removes the element from the default tab order but allows you to focus on it programatically
- `tabindex="0"` places the element in the default tab order
- Proposal is in to deprecate any tab index that is greater than 0

## Form Elements
- All `<input>` must have `<label>` associated with them
- Note the `name` attribute does not have to match
```html
<label for="theinput">Input here:</label>
<input type="text" name="whatever" id="theinput">
```

## Random Tidbits
- Include a `lang=` attribute on the `<html>` tag
- Don't use `<meta name="viewport" content="user-scalable=no" />`. Users must be able to zoom
- Take into account that users should be able to go to zoom in to 200% and have the site still work

## Further Reading
An excellent resource on accessibility for the web: [eBay MIND Patterns](http://ianmcburnie.github.io/mindpatterns/)
