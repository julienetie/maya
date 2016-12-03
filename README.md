# MaYa
An efficient an maintainable CSS Framework Architecture 

A minimalistic Sass framework that avoids common architectures such as OOCSS, SMACSS or BEM. 
Because there is not "One size fits all" methodology for optimising CSS.

- A frame refers to an SPA representation of a page.
- Base style inheritence 

## Do not extend components, subclass them into ./common

Let's say you have a weather widget and a news update widget:

`.weather-widget {}` 

`.news-widget {}`

They both share: 

```css
width: 50%;
height: auto;
border: 1px solid #cc0000;
position: relative;
```

Code should be put into:
`./common/index.scss`

As a 3-4 letter shorthand/ abbreviation.

```css
  .wid {
    width: 50%;
    height: auto;
    border: 1px solid #cc0000;
    position: relative;
  }
```

And used as:

```html
<div class="wid weather-widget">...
<div class="wid news-widget">...
```

## Document common components.

Each common subclass should be documented in `REFERENCE.md`
With a discription of:

1. The subclass:
2. The type of comonent it is to be used with.

` Subclass: .wid, component type: Widgets`

It is more preferable to have a central document for subclass references
than relying on code comments for speed, but should not eliminate the need
for comments.

## Avoid sub-classing changes to child components when possible

Sometimes this can not be avoided.



## Global Components 

Global components refers to any "component" that will be reused across mulitple pages/ frames.
Members are global but are not considered as "components".

#### No extensions

Components used acoross mulitple pages/ frames should not be extended as changes to the base component could become:

- Difficult to maintain as various other instances of the style depend on it.
- Encourage more code to be written for future variants. 
- Tight coupling.

This may seem like duplicate code but it is agle for changes.


#### Variants should live in the same space

If every page has a notice widget, each notice widget should e

## Local Components

Local components refers to "components" that are expected to only be used within a single page/ frame.

## Sub Components

A sub-component is any child component.

## Members

Members are typical small UI parts such as buttons, input fields, titles etc.
It is important to dirrentiate members from components to avoid cumbersom maintainability.

/


## Memeber and sub-component inherit from a base class

It is generally best to avoid re-using components that contain a variety of variating 
sub-components and/ or members. For somewhat complex components avoid reusing classes, 
unless
