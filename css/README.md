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
  border-radius: 50% }
```

Good
```scss
.avatar {
  border-radius: 50%
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

2. Prefer line comments (// in Sass-land) to block comments.

Bad
```scss
/*
.class-one {
  border-radius: 50%;
}
*/
```

Good
```scss
// .class-one {
//  border-radius: 50%;
// }
```

3. Prefer comments on their own line. Avoid end-of-line comments.

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

1. Use 0 instead of none to specify that a style has no border.

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
  padding-left:20px;
  padding-right:20px;
  padding-top:10px;
  padding-bottom:10px;
}
```

Good
```scss
.box {
  padding:10px 20px;
}
```

4. Don't Use Inline-Styles
> According to the separation of concerns principle, CSS, and HTML should be separated for reasons like better readability and maintenance.
Another problem using inline-styles is that you need to use !important tag to override!!

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

#Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.

#Extend directive

@extend should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using @extend, and you can DRY up your stylesheets nicely with mixins.

#Nested selectors

Do not nest selectors more than three levels deep!

Bad
```scss
.page {
  display: flex;
  
  .header {
    color: white;
    
    .left-header {
      background-color: red;
    }
  }
}
```

Good
```scss
.page {
  display: flex;
  
  .header {
    color: white;
  }

  .left-header {
    background-color: red;
  }
}
```

