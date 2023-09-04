# Typst DND5E template

This is a [Typst](https://typst.app) template for DND 5E content, suitable for DMs Guild and the like.

See the included example which should mostly be self explanatory - it includes examples of tables, stat blocks and breakout boxes, and should serve as a good starting point for your own content. 

## Basic usage

The `dndmodule` template sets up your document for you. The arguments you may want to specify up front are as follows:

- `title`: The document's title, this will be rendered as text. Omit if you already have cover art with the title.
- `subtitle`: A slug line for down the bottom of the front cover.
- `author`: Your name.
- `cover`: The location of an image to use on the front cover 
- `fancy_author`: This will put the author's name in that red flame that D&D books tend to have.
- `guild`: Set to `true` to include the DMSGuild logo.
- `font_size`: Defaults to `12pt`.
- `paper`: Defaults (sensibly) to `A4` (Americans, you might want `us-letter`).

From there, just about everything you need can be done with basic Typst markup. Some convenience functions are provided in the template:

`#dnd`: Prints "Dungeons & Dragons" in small caps, as required per the official style guide.
`dndtab(name, columns: (1fr, 4fr), ..contents)`: A table with the conventional formatting. Defaults to 2 columns with ratio 1:4 as shown.
`breakoutbox(title, contents)`: Inserts a box with coloured background, and the optional title in small caps.
`statbox(stats)`: Accepts a dictionary with the following format. The keys are not optional, though feats and actions can be empty lists:

```
#statbox((
  name: "",
  description: [],
  ac: [],
  hp: [],
  speed: [],
  skills: [],
  senses: [],
  Languages: [],
  Challenge: [],
  feats: (
    ("Feat name", [Description...]), 
    // ...
    ("Feat name", [Description...])
  ),
  actions: (
        ("Action name", [Description]), 
        ("Action name", [Description]),
        // ...
    )
 )
)
```

`spell`: Accepts a dictionary as follows; the properties are all optional:

```
#spell((
  name: "",
  spell_type: [2nd level ...],
  properties: (
    ("Casting time", []), 
    ("Range", []), 
    ("Duration", []), 
    ("Components", []), 
  ),
  description: [Spell effects description]
  )
)
```

## Page-wide images and tables

Typst currently has one significant limitation: it is not possible in 2-column mode to include a figure that spans both columns and floats (see [this issue](https://github.com/typst/typst/issues/553)). 
I am hopeful for a fix in the near future. The workaround for the time being is to insert a page break, start a new page with 1 column, insert a floating image, then continue with the text in a 2-column block. A helper function included, to be used like so:

```
// A page break will happen here.
#pagewithfig(top, "images/my_image.png")[
The text that appears on the page goes here; you can include more text that will keep flowing, up to the end of the document, but will need to close the content block if you need another image page.
]
```

However, you may have best results fiddling around with it yourself manually. 

The downside with this method is that you must explicitly divide the content into pages in the right amounts, so that there is not a huge amount of whitespace on the page preceding the one with the image. This is only workable once the content is more or less finalized. 

When this issue is fixed, it should just work without any need for this temmplate to be updated.

## Acknowledgements

Inspiration from the [DND LaTeX module](https://github.com/rpgtex/DND-5e-LaTeX-Template).
