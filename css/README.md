# STS_Angular_coding_conventions-

#Formatting

1. Use soft tabs (2 spaces) for indentation.

Bad
```scss
.header {
       padding: 0;
}
```

Good
```scss
.header {
  padding: 0;
}
```

2. Prefer dashes over camelCasing in class names.

Bad
```scss
.toggleButton {
  color: red;
}
```

Good
```scss
.toggle-button {
  color: red;
}
```

3. Avoid Using id Selectors
>Because you can only have one element per id per document, rule sets that use id selectors are hard to repurpose.

4. When using multiple selectors in a rule declaration, give each selector its own line.

Bad
```scss
.red, .blue, .green {
  background-color: white;
}
```

Good
```scss
.red,
.blue,
.green {
  background-color: white;
}
```

5. Put a space before the opening brace **{** in rule declarations.

Bad
```scss
.header{
  /* ... */
}
```

Good
```scss
.header {
  /* ... */
}
```

6. In properties, put a space after, but not before, the **:** character.

Bad
```scss
.header {
  color:red;
}
```

Good
```scss
.header {
  color: red;
}
```

7. Put closing braces **}** of rule declarations on a new line.

Bad
```scss
.avatar {
  border-radius: 50%
}
```

Good
```scss
.avatar {
  border-radius: 50%;
}
```

8. Put blank lines between rule declarations.

Bad
```scss
.class-one {
  border-radius: 50%;
}
.class-two {
  border-radius: 50%;
}
```

Good
```scss
.class-one {
  border-radius: 50%;
}

.class-two {
  border-radius: 50%;
}
```

#Comments

1. avoid comments

> “Don’t comment bad code. Rewrite it.” — Brian W. Kernighan

2. Prefer comments on their own line. Avoid end-of-line comments.

Bad
```scss
.class-one { // comment here
  border-radius: 50%; // comment here
}
```

Good
```scss
// comment here
.class-one {
  // comment here
  border-radius: 50%;
}
```

#Clean code

1. Use 0 instead of none to specify that a style has no border because it's shorter and save an amount of bandwidth.

Bad
```scss
.box {
  border: none;
}
```

Good
```scss
.box {
  border: 0;
}
```

2. DRY
> DRY stands for "Don't Repeat Yourself". As we can understand from its name, DRY aims to avoid repetition as much as possible.

Bad
```scss
.submit-btn {
  padding: 10px 30px;
  text-align: center;

  background: pink;
}

.cancel-btn {
  padding: 10px 30px;
  text-align: center;

  background: gray;
}
```

Good
```scss
.btn {
  padding: 10px 30px;
  text-align: center;
}

.submit-btn {
  background: pink;
}

.cancel-btn {
  background: gray;
}
```

3. Use Shorthands

Bad
```scss
.box {
  padding-left: 20px;
  padding-right: 20px;
  padding-top: 10px;
  padding-bottom: 10px;
}
```

Good
```scss
.box {
  padding: 10px 20px;
}
```

4. Don't Use Inline-Styles
> According to the separation of concerns principle, CSS, and HTML should be separated for reasons like better readability and maintenance.
Another problem using inline-styles is that you need to use !important tag to override!!

5. Use specific classes when necessary.

Bad
```html
<div class="section">
    <aside>
        <h1>
            <span></span>
        </h1>
    </aside>
</div>
```
```scss
.section aside h1 span {
  margin-left: 25%;
}
```

Good
```html
<div class="section">
    <aside>
        <h1>
            <span class="left-offset"></span>
        </h1>
    </aside>
</div>
```
```scss
.left-offset {
  margin-left: 25%;
}
```

6. Drop units from zero values.

Bad
```scss
div {
  margin: 20px 0px;
  letter-spacing: 0%;
  padding: 0px 5px;
}
```

Good
```scss
div {
  margin: 20px 0;
  letter-spacing: 0;
  padding: 0 5px;
}
```

#Sass

> Ordering of property declarations

1. Property declarations

List all standard property declarations, anything that isn't an @include or a nested selector.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  // ...
}
```

2. @include declarations

Grouping @includes at the end makes it easier to read the entire selector.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);
  // ...
}
```

3. Nested selectors

Nested selectors, if necessary, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

```scss
.btn {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);

  .icon {
    margin-right: 10px;
  }
}
```

#Variables

Prefer dash-cased variable names (e.g. $my-variable) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. $_my-variable).

#Nested selectors

Do not nest selectors more than three levels deep!

Bad
```scss
.container {
  height: 100%;
  
  .page {
    display: flex;

    .header {
      color: white;

      .left-header {
        background-color: red;
      }
    }
  }
}
```

Good
```scss
.container {
  height: 100%;
  
  .page {
    display: flex;

    .header {
      color: white;
    }

    .left-header {
      background-color: red;
    }
  }
}
```

#Be mindful of the structure
```html
- abstracts
    _variables.scss
    _functions.scss
    _mixins.scss
    _placeholders.scss
- base
    _reset.scss
    _typography.scss
    ...
```

#BEM
BEM – meaning block, element, modifier – is a front-end naming methodology.
    
The naming convention follows this pattern:
```css
.card {}
.card--rounded {}
.card__header {}
.card__header--dark {}
```
```html
<div class="card card--rounded">
    <div class="card__header card__header--dark"></div>
    <div class="card__body"></div>
    <div class="card__footer"></div>
</div>
```

- card represents the higher level of an abstraction or component.
- card__element represents a descendent of .block that helps form .block as a whole.
- card--modifier represents a different state or version of .block.

