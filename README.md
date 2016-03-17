# Quaintous i18n Custom Element
This is a simple Polymer 1.0 which loads translation files asynchronously and provides other elements with a behavior (in Polymer terms) which can be used for internationalization.

## Example
```html
<link rel="import" href="../../components/polymer/polymer.html">

<dom-module is="localized-tag">
  <template><span>[[__(myProperty)]]</span></template>
  <script>
  Polymer({
    is: 'localized-tag',

    properties: {
      myProperty: String
    },

    behaviors: [I18N]
  });
  </script>
</dom-module>
```

so eventually this:

```html
<template is="dom-bind">
  <i18n-props locales-path="/locales/fa.json" loading="{{i18nLoading}}"></i18n-props>
  <template is="dom-if" if="{{!i18nLoading}}">
    <localized-tag my-property="hello"></localized-tag>
  </template>
</template>
```

renders to:

```html
<span>سلام</span>
```

## Gotcha
The previous example assumes that fetching the translation file (i.e. `fa.json`) is succeeded *before* the `localized-tag` is ready and attached, otherwise `myProperty` cannot be bound (i.e. translated) correctly when the element is rendered. This is the reason for using [**conditional templates**](https://www.polymer-project.org/1.0/docs/devguide/templates.html#dom-if).
