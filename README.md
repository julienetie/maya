# MaYa
An efficient an maintainable CSS Framework Architecture 

A minimalistic Sass framework that avoids common architectures such as OOCSS, SMACSS or BEM. 
Because there is not "One size fits all" methodology for optimising CSS.

- A frame refers to an SPA representation of a page.
- Base style inheritence 



## Reset sheet

A customized version of normailize.scss

## Grid system

A 24 column customized Pure CSS grid using Foundation media queries.

## Sub-class

There are two types of sub-class:

1. Common sub-class
2. Variant sub-class

**A common sub-class is used to avoid duplicating by providing common elements with common styles.**
Common sub-classes reside in: `./common/*`

A common sub-classe should be shorthand ( Max 4 characters ) and start with a hyphen.
`.-bttn {//...`

**A variant sub-class is used to extend or override with a new variant** of the class it proceeds.
Variant sub-classes reside below the class it extends or overrides. 

```css
.button {//...

.button .download {//...

```

## JavaScript 
An element that needs to be accessed by JavaScript should have an ID attribute or the specific class prefix.
It shoudl be prefixed with `js-`.

- `#js-user-interface`
- `.js-user-interfaces  // Must be plural`

Style selectors and JavaScript selectors should be completely decoupled.
JavaScript class selectors must be pluralised.

## State
State is a class that starts with an understore, uppercase and spaced by underscores.
- `._LIGHTS_ON`
- `._LIGHTS_OFF`
- .`_SHOW_VOUCHER`

## Members
A member is a specific type of component that is either or all of:
- Repeated thoughout the site
- A small component
- Text based
- A button or typical point of interaction
- An inidcation, Icon or small notification
- A list of component sections

A member is not typically:
- A main section of the page or frame
- A majority portion of a component.

There is no specific definiton of what a member can and can not be, it is purely based on descretion.
It' usually a small part of an interface such as an input field link button or list icon.

Members should differentated because they are sometimes:
- Sometimes Heavily varianted
- Used repetatively in a viewport
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

- Rapid style development withough breaking other parts of the site
- Clean, readable and predictable CSS classes
- Better maintainability

## Workflow

Maya has tackled the concept of not duplicating code (Similar to OOCSS) but also decouples code for members, which are the parts of the website that are usually prone to tight coupling.

Maya does not solve decoupling for components and layout design, as the scenarios are too broad to decipher. For instance In some cases it is convenient to sub-class child componetns and even grandchild components, in other cases it's a terrible idea.
But here are some mandatory principals to enforce an agile codebaase for dedicated teams or your future self.

#### 1. Directories: 
- `./common/*` Common sub-classes
- `./members/*` Member components
- `./components/*` Components
- `./mixins/*` Mixins
- `./framework/*` The Maya Framework
- `./libs/*` Your third party libraries
- `./options.scss` Variables & Global defaults 
- `./index.scss` Directory imports and main CSS file
- `./README.md` Directory imports and main CSS file

#### 1. All directories must contain an index.scss file 
  The index is the main import file of a directory and the 
  main file to import modules within the directory. Therefore 
  When a file is added/ removed within a folder you should only 
  need to update the index.scss of that folder it resides in.
 
#### 2. Selectors are hyphonated with the exception of state.
  Hyphen separated names are arguably easier to read especially in markup
 
#### 3. JavaScript Id's and classes must start with js- `js-something`
  How many times have you been curious if a class is being used by JavaScript?
  Now you are fully aware.

#### 4. JavaScirpt Id's and classes can not be used within the CSS codebase
  We want JavaScript to be decoupled from CSS to prevent breakage.

#### 5. Common sub-classes reside in `./common/*` or `./common.scss`
  This is where repeat code snippets lives. It is safe to @extend within common.

#### 6. Common sub-classes start with a hyphen `base-class -dimensions`
  We know -dimensions contains repeat code essential to base-class. 
  This means there should be no use of base-class without -dimensions.
  
#### 7. Variant sub-classe code resides below the base class

#### 8. Variant sub-classes do not use hyphens `base-class turquoise`
  We know turquoise is a variant and not an essential part of base-class.

#### 9. State classes are captialized like this: `._SHOW_PANEL`
  This differentiates satate from any other type of class.

#### 10. Every directory must contain a README.md
  This doesn't replace comments but it is essential to provide a central
  reference to explain how the codebase works because there maybe parts
  of the styling you may not need to touch for weeks, months if not years.
 
#### 11. Everything design part is not a component, it is either a component or member.
  If you do not differntiate comoponents from members you may not have a clear sense
  of what to extend and what not to extend. This separation is crucial for 
  rapid featuers and maintainability.

