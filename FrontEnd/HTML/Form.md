# Form

* [Form Design for Complex Applications](https://uxdesign.cc/form-design-for-complex-applications-d8a1d025eba6#.dygbocq3i)
* [Better form design - One thing per page](https://www.smashingmagazine.com/2017/05/better-form-design-one-thing-per-page/)
* [11 form design guidelines](https://uxdesign.cc/11-form-design-guidelines-4b2f1c659414)

---

* Conversational form
* Move away from "data entry" look

## Good Practice

* Turn off HTML5 validation
* Turn off IE/Edge "Show password" helper
* Use onSubmit always
* Use [implicit submission](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#implicit-submission)
* Update `<title>` when there are errors: "(2 errors) Registration"
* Move submit button to be left-align instead of right-align
* Never says "There's an error". Say "There's a problem"

```html
<form novalidate>

</form>
```

```css
input[type=password]::-ms-reveal {
  display: none;
}
```

## Validation

* [How to Report Errors in Forms: 10 Design Guidelines](https://www.nngroup.com/articles/errors-forms-design-guidelines/)
* [PPK - Native form validation — part 1](https://medium.com/samsung-internet-dev/native-form-validation-part-1-bf8e35099f1d)
* [Happier HTML5 Form Validation](https://daverupert.com/2017/11/happier-html5-forms/)
* [HTML5 Pattern](http://html5pattern.com/)
* [Capture form validation back from the browser](https://hyperform.js.org/)

Never use `input:invalid` as it is broken.

```html
<div role="group" tabindex="-1">
  <h2>There's a problem</h2>
</div>

<input aria-invalid="true" />
```