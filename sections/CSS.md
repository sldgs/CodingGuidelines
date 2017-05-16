[Back to Home](../README.md)
# CSS

* If you get the basics right, it’s much easier to add stuff later, than to overwrite some poorly written code you imported to save time!
* Quick & dirty solutions often come back to haunt you later
* There is always a point where just tossing everything out and writing from ground up becomes quicker in the long run. You just have to realise when this point happened.

## Specificity
The more different selectors you use to target an element, the more complicated it is to override this selector later.

Poorly written CSS often has a high level of specificity and is then hard to overwrite. This often happens in Wordpress plugins (where it can be also because they are coded defensively, so they are not overwritten unintentionally). An example of this is Woocommerce’s css, which is easier to just get rid of in the beginning.

### Ways to prevent too high specificity:
* **not using IDs in your CSS**  
do you really need that `#content table { }`? Cannot you just target it with `.my-content-table`?
* **not nesting selectors**  
it’s too easy to just nest selectors with SASS/LESS files. BEM can help you write less specific code while maintaining this hierarchy (also it’s less pain to indent everything)   

```
// instead of
.widget{
   .widget-title {
   }
}
// use this
.widget {
}
.widget__title {
}
```
* **not chaining selectors**  
try to add a direct class to the element if possible so you can target it on the first level (ie. `<div class=“header__link”></div>`)
.

* [CSS Wizardry: Hacks for dealing with specificity](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)

## BEM Syntax
* please try to use BEM syntax in your css. It enables you to lower your specificity and a common naming methodology helps when multiple people are working on a project
* for more information: http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/

## Typography
* try using mixins for setting weights of fonts. This helps a lot if you need to exchange fonts for different notation/weights later

### Headings
While `<h1>,<h2>…<h6>` tags signal the content importance of the heading, it’s visual style often depends on context and placement. Especially in more complex apps, these two goals can differ.

Therefore it is advisable to set just some base <h*> tag hierarchy and then use purely presentational tags for their look (such as `<h1 class="heading heading—small">…</h1>`).

<h*> tags can then be used/changed according to their semantic importance at any time and we do not need too much specificity in setting the look.

For more reasoning see [CSS Wizardry: Managing Typography on Large Apps](http://csswizardry.com/2016/02/managing-typography-on-large-apps/)

## Preprocessors
* because we ran into handoff issues, **try to use SASS in projects you are setting up**. This will help us with moving people between projects

## Bootstrap
* Bootstrap comes with many modules out of the box
* be sure to **load the sass version** and work with variables! This enables you to override stuff more easily and load less code.
* it’s preferable to load Bootstrap through a package manager (bower or npm) and not change its code. This makes updating possible
* also it’s preferable to comment out objects/parts you do not need.
* be aware of the $spacer variable and try to use its fractions to set margin & padding. This lets you keep vertical rhythm more easily

## Great Sources
* [CSS Guidelines](http://cssguidelin.es/)
* [CSS Wizardry](http://csswizardry.com/#section:articles)
