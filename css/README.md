# CSS
## 1. Formatting
### 1.1 Use soft tabs (2 spaces) for indentation
```scss
✅ Good
.header {
  padding: 0;
}

❌ Bad
.header   {
    padding: 0;
}
```

### 1.2 Prefer dashes over camelCasing in class names.

```scss
✅ Good
.toggle-button {
  color: red;
}

❌ Bad
.toggleButton {
  color: red;
}
```

### 1.3 Avoid Using id Selectors
>Because you can only have one element per id per document, rule sets that use id selectors are hard to repurpose.

### 1.4 When using multiple selectors in a rule declaration, give each selector its own line.

```scss
✅ Good
.red,
.blue,
.green {
  background-color: white;
}

❌ Bad
.red, .blue, .green {
  background-color: white;
}
```

### 1.5 Put a space before the opening brace **{** in rule declarations.

```scss
✅ Good
.header {
  /* ... */
}

❌ Bad
.header{
  /* ... */
}
```

### 1.6 In properties, put a space after, but not before, the **:** character.

```scss
✅ Good
.header {
  color: red;
}

❌ Bad
.header {
  color:red;
}
```

### 1.7 Put closing braces **}** of rule declarations on a new line.

```scss
✅ Good
.avatar {
  border-radius: 50%;
}

❌ Bad
.avatar {
  border-radius: 50%
}
```

### 1.8 Put blank lines between rule declarations.

```scss
✅ Good
.class-one {
  border-radius: 50%;
}

.class-two {
  border-radius: 50%;
}

❌ Bad
.class-one {
  border-radius: 50%;
}
.class-two {
  border-radius: 50%;
}
```

## 2. Comments

### 2.1 avoid comments

> “Don’t comment bad code. Rewrite it.” — Brian W. Kernighan

### 2.2 Prefer comments on their own line. Avoid end-of-line comments.

```scss
✅ Good
  // comment here
.class-one {
  // comment here
  border-radius: 50%;
}

❌ Bad
.class-one { // comment here
  border-radius: 50%; // comment here
}
```

## 3. Clean code

###3.1 Use 0 instead of none to specify that a style has no border because it's shorter and save an amount of bandwidth.

```scss
✅ Good
.box {
  border: 0;
}

❌ Bad
.box {
  border: none;
}
```

### 3.2 DRY
> DRY stands for "Don't Repeat Yourself". As we can understand from its name, DRY aims to avoid repetition as much as possible.

```scss
✅ Good
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

❌ Bad
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

### 3.3 Use Shorthands

```scss
✅ Good
.box {
  padding: 10px 20px;
}

❌ Bad
.box {
  padding-left: 20px;
  padding-right: 20px;
  padding-top: 10px;
  padding-bottom: 10px;
}
```

### 3.4 Don't Use Inline-Styles
> According to the separation of concerns principle, CSS, and HTML should be separated for reasons like better readability and maintenance.
Another problem using inline-styles is that you need to use !important tag to override!!

### 3.5 Use specific classes when necessary.
✅ Good
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

❌ Bad
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

### 3.6 Drop units from zero values.

```scss
✅ Good
div {
  margin: 20px 0;
  letter-spacing: 0;
  padding: 0 5px;
}

❌ Bad
div {
  margin: 20px 0px;
  letter-spacing: 0%;
  padding: 0px 5px;
}
```

## 4. Sass

> Ordering of property declarations

#### - Property declarations

List all standard property declarations, anything that isn't an @include or a nested selector.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  // ...
}
```

#### - @include declarations

Grouping @includes at the end makes it easier to read the entire selector.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);
  // ...
}
```

#### - Nested selectors

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

## 5. Variables

> Prefer dash-cased variable names (e.g. $my-variable) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. $_my-variable).

## 6. Nested selectors

> Do not nest selectors more than three levels deep!

```scss
✅ Good
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

❌ Bad
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

## 7. Be mindful of the structure
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
## 8. BEM
> BEM – meaning block, element, modifier – is a front-end naming methodology.
    
#### The naming convention follows this pattern:
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

