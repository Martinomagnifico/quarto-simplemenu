# Simplemenu

## For Quarto

A quarto extension for [Reveal.js](https://revealjs.com) that creates menubars and menus.

[![Screenshot](https://martinomagnifico.github.io/reveal.js-simplemenu/screenshot.png)](https://martinomagnifico.github.io/quarto-simplemenu/docs/demo.html)

In Powerpoint you can make slides with a nice bottom- or top bar in which ***the active menu item is highlighted***. This menu works in the same way, but automatically. Simplemenu now also supports the Markdown syntax. Combined with the `barhtml` option, you don't have to edit the template in HTML at all.

* [Demo with bar on top](https://martinomagnifico.github.io/quarto-simplemenu/docs/demo.html)
* [Demo, custom styling, including a logo](https://martinomagnifico.github.io/quarto-simplemenu/docs/demo-custom.html)
* [Demo, flat chapter navigation](https://martinomagnifico.github.io/quarto-simplemenu/docs/demo-flat.html)


### What it does
- Make menu items of your vertical stacks (top-level sections).
- Moving to another vertical stack (by whatever navigation) will automatically update the current menu item.
- Clicking an item in the menu will open the first section in the corresponding vertical stack.
- Note: Menu items can only be top-level sections: regular horizontal slides or vertical stacks.

#### Auto mode
Simplemenu can generate the menu, using sections with an attribute of `data-name`. If you add a menubar (manually or through the `barhtml` option) and an empty menu, Simplemenu will automatically populate it for you. You can also add such a menu anywhere else in the presentation, to serve as a Table Of Contents or an Agenda.


#### Manual mode 
However, if you add a menu (in either a menubar or a standalone TOC menu), and manually add links to your sections to it, Simplemenu goes into 'manual' mode, and you have to take some things into account:

- There has to be an element that will hold the links. By default this selector is the class `menu`. The selector can be changed in the Simplemenu options.
- Inside this main menu, there have to be anchors with an href. These need to point to an ID of a top-level section. Reveal uses links with hashes to navigate, so the link has to be written like that: `href="#/firstchapter"`.


## Installation

### Installation with Quarto

```console
quarto add martinomagnifico/quarto-simplemenu
```

### Other installations

The original plugin is also published to npm. To use Simplemenu in a normal Reveal.js installation, or for more information about the original plugin, go to [Martinomagnifico/reveal.js-simplemenu](https://github.com/Martinomagnifico/reveal.js-simplemenu)

### Styling

The styling of Simplemenu is automatically inserted from the included CSS styles.

If you want to change the Simplemenu style, you can simply make your own style and use that stylesheet instead through the Quarto options.


### Markup

Reveal.js works with Markdown, but you need to consider how you add `data-name`s to your sections. Because of the way how Reveal generates vertical stacks, you can't directly add a `data-name` to those. The workaround is to add a `data-stack-name` to the first vertical slide in those stacks:

```md
## Table of Contents
<ul class="menu"><ul>

# Slide 1 {data-name="Regular slide"}
A paragraph with some text and a [link](http://hakim.se).

# Vertical slide 1 {data-stack-name="Vertical"}

## Vertical slide 2

```

### Moving the slide number to a menubar

If you add a menubar manually or through the options, you can also move the slide number into it. If a div with the class `slide-number` is found within a menubar, it is removed from the root Reveal element, and used in that menubar. This functionality is similar to the [RelativeNumber](https://martinomagnifico.github.io/reveal.js-relativenumber/demo.html) plugin. You will need to adjust the CSS yourself, like making the elements relative instead of absolute.

```javascript
Reveal.initialize({
    // ...
    simplemenu: {
        // ...
        barhtml: {
            header: "<div class='menubar'><ul class='menu'></ul><div class='slide-number'></div><div>",
            footer: ""
        }
    },
    plugins: [ Simplemenu ]
});
```

### Using the flat option

Sometimes you'll want to limit your presentation to horizontal slides only. To still use 'chapters' with several slides, you can use the `flat` option. By default, it is set to `false`, but you can set it to `true`. Then, when a data-name is set for a slide, any following slides will keep that menu name. Whenever a slide is encountered with `data-sm="false"`, the inheritance will stop.

``` markdown
## Chapter one {data-name="Chapter 1"}
<!-- The 'Chapter 1' menu-item will be active for this slide -->
Lorem ipsum sit dolor amet

## Another slide 
<!-- The 'Chapter 1' menu-item will be active for this slide -->
Lorem ipsum sit dolor amet

## Chapter two {data-name="Chapter 2"}
<!-- The 'Chapter 2' menu-item will be active for this slide -->
Lorem ipsum sit dolor amet
```


## Configuration

There are a few options that you can change in the YAML options. The values below are default and do not need to be set if not changed.

```yaml
format:
    revealjs:
        simplemenu:
            menubarclass: "menubar"
            menuclass: "menu"
            activeclass: "active"
            activeelement: "li"
            barhtml:
                header: ""
                footer: ""
            flat: false
            scale: 0.67
revealjs-plugins:
    - simplemenu
```

* **`menubarclass`**: This option sets the classname of any menubar.
* **`menuclass`**: This option sets the classname of the menu.
* **`activeclass`**: This option is the class an active menuitem gets.
* **`activeelement`**: This option sets the element that gets the active class. Change it if you directly want to style the `a`, for example. 
* **`barhtml`**: 
	* **`header`**: Here you can add the HTML for the header. If you include an empty menu in it, that will be populated with actual links. You might also add a logo here, or anything else you like.
	* **`footer`**: Here you can add the HTML for the footer. If you include an empty menu in it, that will be populated with actual links. You might also add a logo here, or anything else you like.
* **`flat`**: This turns the `flat` option on or off. See the description above.
* **`scale`**: When you have a lot of subjects/chapters in your menubar, they might not all fit in a row. To avoid the need to adjust the CSS for each presentation, you can tweak the scale in the options. By default it is 1 (based on 2/3 of the main font size).


## Like it?
If you like it, please star this repo! 

And if you want to show off what you made with it, please do :-)


## License
MIT licensed

Copyright (C) 2023 Martijn De Jongh (Martino)
