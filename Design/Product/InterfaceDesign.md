# Interface Design

* [What is Atomic Design?](https://blog.prototypr.io/what-is-atomic-design-b8f0368e580d#.bpbyph6i4)

---

* Clarity
* Remove all extra elements - every item should have a purpose
* Simplify color scheme - limit the number of used colors
* Chronological order - feeds, events, etc.

> UI design is just a series of "endless tweaking".

## Content Structure

> You can create good experiences without knowing the content. What you can't do is create good experiences without knowing your content structure. What is your content made from, not what your content is. - Mark Boulton

---

> Content needs to be structured and structuring alters your content, designing alters content. It's not 'content then design', or 'content or design'. It's 'content and design' - Mark Boulton

---

> The best approach to take is to let the content you have on your site dictate the actual widths you put into your media queries.

## Variations

You need to articulate variations in templates, which is crucial for establishing robust and reliant design systems. For examples:

* A user has 1 item in their shopping cart and another has 10 items
* A dashboard typically show recent activity, but that section is suppressed for first-time users.
* An article headline might be 250 characters long.

To create more resilient design systems, you need to account for variations.

* Atoms - UI that can't be broken down any further and serve as the elemental building blocks
* Molecules - Collections of atoms that form relatively simple UI with Single Responsibility
* Organisms - Relatively complex components that form discrete sections of an interface
* Templates - Lo-fi grey boxes of **content structure**
* Pages - Apply real content to templates and articulate variations to demonstrate the final UI and test the resilience of the design system.

## Navigation

* [Great Alternatives to Hamburger Menus](https://uxplanet.org/great-alternatives-to-hamburger-menus-d4c76d9414dd#.9vq36a5ry)