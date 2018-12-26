How to Write a CVRoller Theme
=============================

This document will describe how the CVRoller theme file works so that you can write or edit your own.

For LaTeX output, CVRoller themes are simply [moderncv](https://www.ctan.org/pkg/moderncv) themes. If you'd like to create your own theme for a PDF CV, you'll need to write a moderncv theme (or write an HTML theme and use Print to get a PDF!).

This document will mostly explain how to write an HTML theme.

Comments can be added to theme files using the percent sign `%`. Any line beginning with `%` will be ignored.

Structure
---------

Each CVRoller theme file is split into attributes marked by two hash tags, `##` followed by the name of the attribute. For example:

```
##footer

</body></html>
```

sets the `footer` attribute of the theme to the value `</body></html>`. No spaces are allowed on the `##` line. `## footer` will not work.

Attributes
----------

There are three required attributes in a CVRoller HTML theme: `header`, `style`, and `footer`. 

`header` is the HTML code that will lead off the file. It will generally end with the `<body>` tag (although if you want some additional text in the body before beginning the CV proper, that's fine too), and it must contain a `{style}` marker, where the `style` theme attribute will be inserted. It is also generally a good idea to include a `<meta>` tag including the character encoding. For example,

```
##header

<html><head><title>{name} CV</title>{style}<meta http-equiv="Content-Type" content="text/html; charset=utf-8"><body>
```

Note that you can also include a `{name}` marker, which will be substituted with the `name` attribute from the `head` section. At the moment `{name}` and `{style}` are the only two recognized markers in the `##header` section.

`style` is a block of CSS formatting instructions, which should begin with `<style>` and end with `</style>`. For example,

```
##style
<style>
*{font-family: Georgia, serif;
	font-size: medium}
</style>
```

The proper CSS class names for formatting are addressed below.

`footer` is the HTML code that will end the file. For example:

```
##footer

</body></html>
```

There are also several optional attributes which have defaults if not assigned. These are the same attributes that the user can specify in the `versions` part of the layout file, or for specific sections. If the theme and the layout file both specify one of these attributes, the layout file takes precedence:

`sectionglue`, which is by default set to a line breaks (`\n`), tells CVRoller how to 'glue' sections together, i.e. what goes between them.

`sectionframe` shows how to paste together the section title and the section `{meat}`. This is by default

```
##sectionframe

<table class = "section"><tr><td class="sectitle">**{title}**</td><td class="secmeat">{subtitle}{meat}</td></tr></table><br/><hr class="secdiv"/><br/>
```

`itemwrapper` allows you to put each item in a tag. By default this is set to `{item}` which just displays the item by itself. `<em>{item}</em>`, for example, would put the `<em>` tag around each item.


These optional attributes: `sectionglue`, `sectionframe`, and `itemwrapper`, as well as **any section attribute that can be specified in the layout file** can be modified in the theme for specific section types, overriding the CV-wide settings (but not overriding any settings detailed in the layout file itself). This can be done using a colon to specify which section to apply it to. For example,

```
##sectionframe:head

<table class = "section"><tr><td class="secmeat">{meat}</td></tr></table>
```

will apply this particular section frame just to sections with the `head` type. 

You may want to seriously consider including a `format:head` part in your theme, as `head` really needs a format, and if it's not in the theme the user will be forced to figure out the syntax for `format` in order to use your theme.

CSS Classes
------------

When writing CSS, you can assign theming to particular parts of the CV by referring to the appropriate classes. Classes of interest:

Under the default `sectionframe`, section titles have the class `sectitle` and section meat has the class `secmeat`. This can be changed using the `sectionframe` attribute of the theme. For example, this part of the `style` attribute formats the meat of the CV:

```
.secmeat {
	text-align: left;
	width: 80%;
	padding: 20px;}
```

Aside from these, each piece of text in the CV is given two classes: its section class and its attribute class.

Each attribute is given the class with that attribute name. When writing documentation for your class, be sure to specify the particular attribute names you want things to have so you can style them appropriately. For example, 

```
.abstract {font-size:small}
```

gives a small font size any time an `abstract` attribute pops up.

Alternately, you can use section as a class. For example, if you want everything in the `teaching` section to be red, you could do:

```
.teaching {color: #FF0000}
```

Don't forget that CSS allows you to style overlapping classes. So if you want the `name` attribute to be big and green, but *only* if it's in the `head` section, and not anywhere else, you can do:

```
.head.name {
	font-size: xx-large;
	color: #33cc33}
```