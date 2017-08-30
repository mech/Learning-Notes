# Colors

* [CSS Custom Properties and Theming](https://css-tricks.com/css-custom-properties-theming/)
* [How we made our product more personalized with CSS Variables and React](https://medium.com/geckoboard-under-the-hood/how-we-made-our-product-more-personalized-with-css-variables-and-react-b29298fde608)
* [Ambiance](http://ambiance.somethingjustlikethis.com/)

```css
.subheader {
  background: 
    /* Make a bit darker */
    linear-gradient(
      to top,
      rgba(0, 0, 0, 0.25),
      rgba(0, 0, 0, 0.25)
    )
    var(--mainColor);
}
```

## Color Functions

```css
.box {
  background-color: color-mod(
                      #278da4
                      hue(+ 5deg)
                      lightness(+ 15%)
                      alpha(75%)
                    );
}
```

```css
:root {
  --base: crimson;
  --base-dark: color-mod(var(--base) lightness(- 30%));
  --base-light: color-mod(var(--base) lightness(+ 25%));
  
  --complement: color-mod(var(--base) hue(+ 180deg));
  --complement-light: color-mod(var(--complement) lightness(+ 10%));
}
```