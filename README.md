# MaYa

## An Efficient And Highly Maintainable CSS Framework Architecture. 

MaYa uses a minimalistic but rightfully opinionated CSS methodology based on real world results and expectations. MaYa doesn't claim a "One size fits all" solution, because there is none.

## Who is MaYa for?
**MaYa doesn't come with fancy pre-built components, that's your job**. MaYa is for advanced web design and development that considers:

- A light weight footprint.
- Performance.
- Maintainability.
- Rapid development.
- Documentation.
- Ease of use.

## What exactly is MaYA?

MaYa is simply:
- A 24 column grid with [Foundation](http://foundation.zurb.com/sites/docs/v/5.5.3/media-queries.html).
- A [normalize.css reset sheet](https://necolas.github.io/normalize.css/) like media queries.
- A directory structure.
- A documentation structure.
- 2 separation of concerns for components.
- 2 separation of concerns for sub-classes.
- A way better naming convention than that other thing.
- A handful of best practice ̶r̶a̶n̶t̶s̶ helpers.
- Libraries and guides for performance: TBA.
- A conformity node module: TBA.
- Font assets guide and loaders: TBA.


## Normalize

The creator and maintainers of normalize.css have done a fantastic job. MaYa uses a customised version of normalize.css but of course use what you like.

## 24

A 24 column grid allows for detailed column structures that may become more complicated to maintain by nesting.
If you really dislike the concept of 24 units, why not jump to pure.css and customise another. MaYa recommends pure.css
because of it's size and reliability but feel free to use what you like.

#### Grid naming convention
There are 5 media query aliases:

| Alias| Query| 
|-----|-------|
|.sm- | screen and (max-width: 40em)|
|.md- | screen and (min-width: 40.063em) and (max-width: 64em)|
|.lg- | screen and (min-width: 64.063em) and (max-width: 90em)|
|.xl- | screen and (min-width: 90.063em) and (max-width: 120em)|
|.xx- | screen and (min-width: 120.063em)|

Append a division to an alias:

|Divisions|
|-----|
|1-24|
|1-12|
|2-24|
|3-24|
|1-8|
|4-24|
|1-6|
|5-24|
|1-4|
|6-24|
|7-24|
|1-3|
|8-24|
|3-8|
|9-24|
|5-12|
|10-24|
|11-24|
|1-2|
|12-24|
|13-24|
|7-12|
|14-24|
|5-8|
|15-24|
|2-3|
|16-24|
|17-24|
|3-4|
|18-24|
|19-24|
|5-6|
|20-24|
|7-8|
|21-24|
|11-12|
|22-24
|23-24
|1|
|1-1|
|24-24|

e.g. `<section class="third-annoying-advert lg-14-24">`

Named column sizes are a bit silly. e.g. `eleven-twelfths` vs `11-12` I mean c'mon seriously.


## Sub-class

There are two types of sub-classes:

1. **Common sub-class**.
2. **Variant sub-class**.

A common sub-class is used to avoid duplication by providing common elements with common styles.
Common sub-classes reside in: `./common/*`

A common sub-class should start with a hyphen.
`pause -button`

`play -button`

A variant sub-class is used to extend or override with a new variant of the class it proceeds.
Variant sub-classes reside below the class it extends or overrides. 

```css
.button {//...

.button .download {//...

```

## JavaScript hooks
An element that needs to be accessed by JavaScript should contain either an ID or class attribute prefixed with `js-`.

- `#js-user-interface`
- `.js-user-interfaces  // Must be plural`

*Style selectors and JavaScript selectors must be completely decoupled*
JavaScript class selectors must be pluralised and only used for mulitiple references.

## State
State is a class that starts with an underscore, is fully upper-cased and spaced by underscores.
- `._LIGHTS_ON`
- `._LIGHTS_OFF`
- .`_SHOW_VOUCHER`

## Members
A member is a specific type of component that is either or all of:
- Repeated throughout the site.
- A small sized component or minimal in detail.
- Text based.
- A button or typical point of interaction.
- An indication, Icon or small notification.
- A list of component sections.

A member is not typically:
- A main section of the page or frame.
- A majority portion of a component.

There is no specific definition of what a member can and can not be, it is purely based on discretion.
It' usually a small part of an interface such as an input field, link, button or maybe a list icon.

Members must be separated from regular components because they are sometimes:
- Wide in varieties.
- Used repetitively in a view-port.
- Difficult to extend across large scale website.

Members have some different rules:

#### Duplicate code is acceptable for members

Because these are some of the most commonly used CSS resources, on a website with rapid or unpredictable
changes it is acceptable to duplicate CSS in return for ease of extending styles and maintainability.

##### OMG This is outrageous!!!
Not really, `class="can you sub-class the hell out of any thing"` ? yes of course but:
- For large scale projects this commonly becomes a mess to maintain.
- If you are happy to add 4, 5 or more variant sub-classes to a single element, you are probably creating a monster.
- You may save a few bytes but the likely-hood of eventually duplicate even more code due to the complexity is raised.
- Each sub-class introduces precedence, the more precedence the hard it becomes to debug.
- Expecting people to just name lots of shared sub-classes better is more of a frustration of humans than the realisation of a flawed work-flow.
- Considering all aspects of front-end design and development, generally the more subcasses on one element, the higher the cost.

##### Duplication in members
In computing, duplicating code is considered a sin, but let's break down the science of modern day CSS.
Despite duplicating code or not, your medium -> large code base is guaranteed to contain a substantial 
number of duplicate series of bytes before being compressed and served.

For files below 32KB gzip will look for duplicate series of bytes and back-reference them. 
Therefore in CSS world providing we:

1. Keep our CSS files below 32KB each.
2. Ensure we only duplicate properties in consecutive order as the original.

Duplication will not affect css download times. But it will slightly add to the browser parse time so 
this is not a "pass" to duplicate the same CSS a million times.

#### @extend or duplicate members
Members can @extend or be manually duplicated depending on how agile the development of the member is expected to be.
Duplication is applicable because members are expected to contain small amounts of CSS.

#### Do not use "common sub-classes" with members

This is not good `submit -button red` main class | common sub-class | variant sub-class.

This is better good `submit-button red`  main class | variant sub-class.

Although we have to create a news class `submit-button` it is de-coupled from other global members.

A member can have a **Main class** a **Variant sub-class** followed by any **STATE class** or **JS ID/ class** 
To re-iterate, when necessary duplicate the smallest CSS code on the app for:

- Rapid style development without breaking other parts of the site
- Clean, readable and predictable CSS classes
- Better maintainability

## Workflow

Maya has tackled the concept of not duplicating code (Similar to OOCSS) but also decoupling code for members, which are the parts of the website that are usually prone to tight coupling.

Maya does not solve decoupling for components and layout design, as the scenarios are too broad to decipher. For instance in some cases it is convenient to sub-class child components and even grandchild components, in other cases it's a terrible idea.
But here are some mandatory principals to enforce an agile code-base for dedicated teams or your future self.

### 1. Directories: 
- `./common/*` Common sub-classes
- `./members/*` Member components
- `./components/*` Components
- `./mixins/*` Mixins
- `./framework/*` The Maya Framework
- `./libs/*` Your third party libraries
- `./options.scss` Variables & Global defaults 
- `./index.scss` Directory imports and main CSS file
- `./README.md` Directory imports and main CSS file

### 2. All directories must contain an index.scss with the exception of ./components 
  The index is the main import file of a directory and the 
  main file to import modules within the directory. Therefore 
  When a file is added/ removed within a folder you should only 
  need to update the index.scss of that folder it resides in.
  
  Components are global and therefore they should be included in the root index.scss
  file of the project. This is purely for ease of use so you can see at a glance what 
  pages you have and what components are available. The same is not true for members 
  because members are smaller types of components that are expected to be available 
  everywhere and rarely need to be compared on a page to page basis.
 
### 3. Selectors are hyphenated with the exception of state.
  Hyphen separated names are arguably easier to read especially in markup
 
### 4. JavaScript hooks start with "js-" `js-something`
  How many times have you been curious if a class is being used by JavaScript?
  Now it is obvious at a glance.

### 5. JavaScirpt Id's and classes can not be used within the CSS codebase
  We want JavaScript to be decoupled from CSS to prevent funny things happening.

### 6. Common sub-classes reside in `./common/*` or `./common.scss`
  This is where repeat code snippets lives. It is safe to @extend within common.

### 7. Common sub-classes start with a hyphen `base-class -dimensions`
  We know -dimensions contains repeat code essential to base-class. 
  This means there should be no use of base-class without -dimensions.
  
### 8. Variant sub-class code resides below the base class

### 9. Variant sub-classes do not use hyphens `base-class -dimensions turquoise`
  We know turquoise is a variant and not an essential part of base-class.

### 10. State classes are capitalised like this: `._SHOW_PANEL`
  This differentiates state from any other type of class.

### 11. Every directory must contain a README.md
  This doesn't replace comments but it is essential to provide a central
  reference to explain how the code base works because there maybe parts
  of the styling you may not need to touch for weeks, months if not years.
 
### 12. Everything is not a component, it is either a component or member.
  If you do not differentiate components from members you may not have a clear sense
  of what to extend and what not to extend. This separation is crucial for 
  rapid features and maintainability.

### 13. Critical CSS
  The first 14kb of above fold CSS should be injected/ included within a HTML page.
  This is useful for accessibility as well as a graceful fallback for assets that may
  fail in loading.

### 14. Preferably one CSS file
  A web page only requires a single CSS file, this may be less feasible with HTTP2 but the 
  aim of this preference is to avoid unnecessary request from too many external resources. This is a
  vague rule because it should be ideally assessed with knowledge of content delivery systems 
  and compared using benchmarks.

### 15. Asynchronous CSS
  Load the CSS file without blocking other assets. Google likes this.

### 16. Prefix styles
  Automatically add vendor prefixes for required browsers. It is far better to do this using 
  NPM modules than bloated CSS mixins.
  
### 17. Do not touch the root font-size
  Leave it alone, it's commonly 16px but not for all devices and scenarios.
  
### 18. Use REM and EM units for fonts (Do not convert them)
  When you set font-size to let's say `Xpx` it is not exactly `Xpx` in height, especially across
  various devices.
  
  Because: 
    - Of user agent differences.
    - Font sizing variates between font styles.
  **It is not possible to correlate font-size in pixels to the actual pixel value on the screen**
  Ems and rem units are to be tried via trial and error **just like pixels**. 
  Serious CSS development should generally use REM and or EM units for font size.
  
### 19. Keep CSS files to 32KB Max
  As mentioned gzip will compress duplicate series of bytes if the uncompressed file is 32KB or below.
  Despite the methodology you develop your CSS in, you will have duplicate series of bytes to take advantage of.
  
### 20. Keep duplicate properties in order
  When duplicating any amount of properties ensure they are in consecutive order to the original or
  use the @extend method in Sass. This will ensure your duplicate code is back-referenced when gzipped.
  
  
MIT (c) 2016 Julien Etienne
