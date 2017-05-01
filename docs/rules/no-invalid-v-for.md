# Disallow invalid v-for directives (no-invalid-v-for)

This rule checks whether every `v-for` directive is valid.

## 📖 Rule Details

This rule reports `v-for` directives if the following cases:

- The directive has that argument. E.g. `<div v-for:aaa></div>`
- The directive has that modifier. E.g. `<div v-for.bbb></div>`
- The directive does not have that attribute value. E.g. `<div v-for></div>`
- If the element which has the directive is a custom component, the component does not have `v-bind:key` directive. E.g. `<your-component v-for="item in list"></your-component>`
- The directive is on the root element. E.g. `<template><div v-for="item in list"></div></template>`

If the element which has the directive is a reserved element, this rule does not report even if the element does not have `v-bind:key` directive because it's not faital error. [require-v-for-key] rule reports it.

This rule does not check syntax errors in directives. [no-syntax-error] rule reports it.
The following cases are syntax errors:

- The directive's value is not the form `alias in expr`. E.g. `<div v-for="foo"></div>`
- The alias is not LHS. E.g. `<div v-for="foo() in list"></div>`


👎 Examples of **incorrect** code for this rule:

```html
<template>
    <div v-for="x in list">
        <div v-for></div>
        <div v-for:aaa="x in list"></div>
        <div v-for.bbb="x in list"></div>
        <your-component v-for="x in list"></your-component>
    </div>
</template>
```

👍 Examples of **correct** code for this rule:

```html
<template>
    <div>
        <div v-for="x in list"></div>
        <your-component v-for="x in list" :key="x.id"></your-component>
    </div>
</template>
```

## 🔧 Options

Nothing.

## 👫 Related rules

- [require-v-for-key]
- [no-syntax-error]


[no-syntax-error]: no-syntax-error.md