# HTML Intro: IDs vs Classes

### `id`
* used identify unique elements on a page
* an element can only have one ID
* CSS Selector: hashtag prefix `#buy-now-main-btn`

### `class`
* used identify elements of the same type
* imply stylistic or behavioural properties about an element
* an element can have many classes
* CSS Selector: period/dot prefix `.nav-item`
* microformats are just specific class names

> General rule: use class *much* more frequently than IDs

### When to use ID?
* When you have a unique element that is styled and/or behaves very differently than other elements on a page or website

* Use when need to reference items from URL anchor **hash value** (AKA *page fragment*)
    * Eg: `http://yourdomain.com#comments` will jump to element with ID `comments`

> Important reason why ID is unique: so broswer knows where to scroll!

### Using ID is more *performant*
* Since browser is just searching for that one element, it'll be faster to find the element

* But, often times, that also conflict with writing clean, modular, and maintainable code, so keep that in mind.

### Use neither unless necessary
* If you don't need them, don't use them!

### Switching the Two Around
* CSS doesn't care
* JavaScript cares: `getElementById` function