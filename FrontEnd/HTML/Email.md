# Email

* [Email Bugs Database](https://github.com/hteumeuleu/email-bugs)
* [Gmail finally support embedded `<style>`, `display: none` and media queries in Sept 2016](https://developers.google.com/gmail/design/css)
* [Email Client Market Share](https://emailclientmarketshare.com/)

```html
<!-- If you want to disable auto-scaling -->
<meta name="x-apple-disable-message-reformatting">
```

Now that Gmail supports the style block in the `<head>`, inlining is no longer necessary when optimizing for Gmail.

* [Here's why Litmus didn't inline CSS for its first newsletter of 2017](https://litmus.com/community/discussions/6116-here-s-why-litmus-didn-t-inline-css-for-its-first-newsletter-of-2017)

## Media Queries

Because most email client do not have media queries support, we can't use mobile-first approach with `min-width`, rather we need to use `max-width` and go desktop-first.

```css
@media screen and (max-width: 600px) {
  .responsive-table {
    display: block;    width: 100% !important;
  }  .responsive-image {
    height: auto;
    max-width 100% !important;
  }
}
```