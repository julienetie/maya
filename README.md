# MaYa

An efficient an maintainable CSS Framework and Architecture. 

MaYa uses a minimalistic and opinionated CSS methodology based on real world uses and expectations.
MaYa doesn't look for a "One size fits all" solutions, because there is none.

MaYa dosen't come with fancy pre-built components, because that's your job, MaYa is for advanced
web design and development that considers:

- A light weight footprint
- Performance
- Maintainability
- Rapid development
- Documentation
- Ease of use

### Reset sheet

A customised version of normailize.scss

### Grid system

A 24 column customised Pure.CSS grid based on Foundation media queries.

## Sub-class

There are two types of sub-class:

1. **Common sub-class**
2. **Variant sub-class**

A common sub-class is used to avoid duplicating by providing common elements with common styles.
Common sub-classes reside in: `./common/*`

A common sub-class should be shorthand ( Max 4 characters ) and start with a hyphen.
`.-bttn {//...`

A variant sub-class is used to extend or override with a new variant of the class it proceeds.
Variant sub-classes reside below the class it extends or overrides. 

```css
.button {//...

.button .download {//...

```

## JavaScript 
An element that needs to be accessed by JavaScript should have an ID attribute or the specific class prefix.
It should be prefixed with `js-`.

- `#js-user-interface`
- `.js-user-interfaces  // Must be plural`

Style selectors and JavaScript selectors should be completely decoupled.
JavaScript class selectors must be pluralised.

## State
State is a class that starts with an underscore, uppercase and spaced by underscores.
- `._LIGHTS_ON`
- `._LIGHTS_OFF`
- .`_SHOW_VOUCHER`

## Members
A member is a specific type of component that is either or all of:
- Repeated throughout the site
- A small component
- Text based
- A button or typical point of interaction
- An indication, Icon or small notification
- A list of component sections

A member is not typically:
- A main section of the page or frame
- A majority portion of a component.

There is no specific definition of what a member can and can not be, it is purely based on discretion.
It' usually a small part of an interface such as an input field link button or list icon.

Members should differentiated because they are sometimes:
- Sometimes Heavily variant-ed
- Used repetitively in a view-port
- Difficult to extend on a large scale website

Members have some different rules:

#### Duplicate code is acceptable for members

Because these are some of the most commonly used CSS resources, on a website with rapid changes 
it is acceptable to duplicate CSS in return for ease of extending and maintainability.
Members can @extend or be manually duplicated depending on how agile the development of the member is expected to be.
Duplication is applicable because members only contain small amounts of CSS.

#### Do not use "common sub-classes" with members

This is not good `submit -cont red` main class | common sub-class | variant sub-class.

This is good `submit-cont red`

A member can have a **Main class** a **Variant sub-class** followed by any **STATE class** or **JS ID/ class** 

Once again, when necessary we duplicate the smallest CSS code on the app for:

- Rapid style development without breaking other parts of the site
- Clean, readable and predictable CSS classes
- Better maintainability

## Workflow

Maya has tackled the concept of not duplicating code (Similar to OOCSS) but also decouples code for members, which are the parts of the website that are usually prone to tight coupling.

Maya does not solve decoupling for components and layout design, as the scenarios are too broad to decipher. For instance In some cases it is convenient to sub-class child components and even grandchild components, in other cases it's a terrible idea.
But here are some mandatory principals to enforce an agile codebaase for dedicated teams or your future self.

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

### 2. All directories must contain an index.scss file 
  The index is the main import file of a directory and the 
  main file to import modules within the directory. Therefore 
  When a file is added/ removed within a folder you should only 
  need to update the index.scss of that folder it resides in.
 
### 3. Selectors are hyphenated with the exception of state.
  Hyphen separated names are arguably easier to read especially in markup
 
### 4. JavaScript hooks start with "js-" `js-something`
  How many times have you been curious if a class is being used by JavaScript?
  Now you are fully aware.

### 5. JavaScirpt Id's and classes can not be used within the CSS codebase
  We want JavaScript to be decoupled from CSS to prevent breakage.

### 6. Common sub-classes reside in `./common/*` or `./common.scss`
  This is where repeat code snippets lives. It is safe to @extend within common.

### 7. Common sub-classes start with a hyphen `base-class -dimensions`
  We know -dimensions contains repeat code essential to base-class. 
  This means there should be no use of base-class without -dimensions.
  
### 8. Variant sub-class code resides below the base class

### 9. Variant sub-classes do not use hyphens `base-class turquoise`
  We know turquoise is a variant and not an essential part of base-class.

### 10. State classes are capitalised like this: `._SHOW_PANEL`
  This differentiates state from any other type of class.

### 11. Every directory must contain a README.md
  This doesn't replace comments but it is essential to provide a central
  reference to explain how the code base works because there maybe parts
  of the styling you may not need to touch for weeks, months if not years.
 
### 12. Everything design part is not a component, it is either a component or member.
  If you do not differentiate components from members you may not have a clear sense
  of what to extend and what not to extend. This separation is crucial for 
  rapid features and maintainability.

### 13. Critical CSS
  The first 14kb of above fold CSS should be injected/ included within a HTML page.
  This is useful for accessibility as well as a graceful fallback for assets that may
  fail in loading.

### 14. Preferably one CSS file
  A web page only requires a single CSS file, this may be less feasible with HTTP2 but the 
  aim of this rule is to avoid unnecessary request from too many external resources. This is a
  vague rule because it should be ideally assessed with knowledge of content delivery systems 
  and compared using benchmarks.

### 15. Asynchronous CSS
  Load the CSS file without blocking other assets. 

### 16. Prefix styles
  Automatically add vendor prefixes for required browsers. It is far better to do this using 
  NPM modules than CSS mixins.
  
### 17. Do not touch the root font-size
  Leave it alone, it's commonly 16px but not for all devices so leave it alone.
  
### 18. Use REM and EM units for fonts (Do not convert them)
  When you set font-size to let's say `24px` it is not exactly `24px` in height in all browsers.
  Because: 
    - User agent differences
    - Font sizing variates between font styles.
  **It is not possible to correlate font-size in pixels to the actual pixel value on the screen**
  Ems and rem units are to be tried via trial and error **just like pixels**. 
  Serious CSS development should generally use REM and or EM units for font size, padding and margins.

    

