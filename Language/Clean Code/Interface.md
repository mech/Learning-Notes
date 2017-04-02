# Interface

> The goal is making it simple and intuitive. Not exposing the functionality as it is implemented, but rather as "how it should be used"

```js
// Compare 2 different kinds of jQuery API

// API that is too focus on implmentation
var selection = new jQuery.DomSelection('div', null, 'someClass', null, true);

// API that show "how things should be used"
$('button.continue').html('Next step...');
```

