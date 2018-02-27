Templates
=========

In Craft, you define your site’s HTML output with templates.

Templates are files that live within your craft/templates folder. The structure of your templates is completely up to you – you can put templates at the root of that folder, within subdirectories, or within subdirectories’ subdirectories (and on and on). Whatever works for your site’s needs.

Craft uses [Twig](http://twig.sensiolabs.org/) to parse your templates. Twig is elegant, powerful, and blazing fast. If you’re new to Twig, be sure to read through our [documentation](twig-primer.md) to familiarize yourself with its syntax.

PHP code isn’t allowed in your templates. If you have a need to do something that is not possible out-of-the-box with Craft or Twig, you can create a [plugin](plugin-intro.md) that provides a new [Twig extension](https://twig.symfony.com/doc/2.x/advanced.html#creating-an-extension).

## Template Paths

There are several times when you’ll need to enter a path to one of your templates:

* When choosing which template [entry](sections-and-entries.md) and [category](categories.md) URLs should load
* When assigning a template to a [route](routing.md#dynamic-routes)
* Within [`{% include %}`](http://twig.sensiolabs.org/doc/tags/include.html), [`{% extends %}`](http://twig.sensiolabs.org/doc/tags/extends.html), and [`{% embed %}`](http://twig.sensiolabs.org/doc/tags/embed.html) template tags

Craft has a standard template path format that applies to each of these cases: a Unix-style file system path to the template file, relative from your `craft/templates` directory.

For example, if you have a template located at `craft/templates/recipes/entry.html`, the following template paths would point to it:

* `recipes/entry`
* `recipes/entry.html`

### Index Templates

If you name your template `index.html`, you don’t need to specify it in the template path.

For example, if you have a template located at `craft/templates/recipes/ingredients/index.html`, the following template paths would point to it:

* `recipes/ingredients`
* `recipes/ingredients/index`
* `recipes/ingredients/index.html`

If you have templates located at both `craft/templates/recipes/ingredients.html` *and* `craft/templates/recipes/ingredients/index.html`, the template path `recipes/ingredients` will match `ingredients.html`.


### Hidden Templates

Craft treats templates with names prefixed with an underscore, for example `recipes/_entry.html`, as hidden templates that are not directly accessible.

If we have a recipe entry that is available at the entry URL `http://mysite.com/recipes/gin-tonic`, which uses the template located at `recipes/entry`, someone could access the template directly at `http://mysite.com/recipes/entry`.

In this example there is no reason to access the template directly because it's only ever used as part of an entry URL. We change its file name to `_entry.html` so it is considered hidden by Craft and update the settings in our Section. 

Now when we try to access `http://mysite.com/recipes/entry` Craft returns a 404 error instead of attempting to render the template.

## Template Localization

If you’re running multiple sites with Craft, you can create site-specific subdirectories in your `craft/templates/` directory, which contain templates that will only be available to a specific site. 

For example, if you want to create a special template welcoming your German customers, but there’s no need for it on your English site, then you could save it in `craft/templates/de/welcome.html`. That template would be available from http://example.de/welcome.

Craft will look for localized templates _before_ it looks for templates in the normal location, so you can use them to override non-localized templates. See our [Localization Guide](sites-localization.md) for more details.
