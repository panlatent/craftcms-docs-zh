# Filters

On top of the template filters that [Twig comes with](http://twig.sensiolabs.org/doc/filters/index.html), Craft provides a few of its own.


## `camel`

Returns a string formatted in “camelCase”.

```twig
{{ "foo bar"|camel }}
{# Outputs: fooBar #}
```

## `currency( currency, stripZeroCents )`

Formats a number with a given currency according to the user’s preferred language.

If you pass `true` into the second argument, the “.00” will be stripped if there’s zero cents.

```twig
{{ 1000000|currency('USD') }} => $1,000,000.00
{{ 1000000|currency('USD', true) }} => $1,000,000
```

## `datetime`

Formats a date according to the user’s preferred language.

## `filesize`

Formats a number of bytes into something nicer.

## `filter`

Removes any empty elements from an array and returns the modified array.

## `group`

Groups the items of an array together based on common properties.

```twig
{% set allEntries = craft.entries.section('blog').all() %}
{% set allEntriesByYear = allEntries|group('postDate.year') %}

{% for year, entriesInYear in allEntriesByYear %}
    <h2>{{ year }}</h2>

    <ul>
        {% for entry in entriesInYear %}
            <li><a href="{{ entry.url }}">{{ entry.title }}</a></li>
        {% endfor %}
    </ul>
{% endfor %}
```

## `hash`

Prefixes the given string with a keyed-hash message authentication code (HMAC), for securely passing data in forms that should not be tampered with.

```twig
<input type="hidden" name="foo" value="{{ 'bar'|hash }}">
```

PHP scripts can validate the value via [CSecurityManager::validateData](http://www.yiiframework.com/doc/api/1.1/CSecurityManager#validateData-detail):

```php
$foo = craft()->request->getPost('foo');
$foo = craft()->security->validateData($foo);

if ($foo !== false) {
    // data is valid
}
```

## `indexOf`

Returns the index of a passed-in value within an array, or the position of a passed-in string within another string. (Note that the returned position is 0-indexed.) If no position can be found, `-1` is returned instead.

```twig
{% set colors = ['red', 'green', 'blue'] %}
<p>Green is located at position {{ colors|indexOf('green') + 1 }}.</p>

{% set position = "team"|indexOf('i') %}
{% if position != -1 %}
    <p>There <em>is</em> an “i” in “team”! It’s at position {{ position + 1 }}.</p>
{% endif %}
```

## `intersect`

Returns an array containing only the values that are also in a passed-in array.

```twig
{% set ownedIngredients = [
    'vodka',
    'gin',
    'triple sec',
    'tonic',
    'grapefruit juice'
] %}

{% set longIslandIcedTeaIngredients = [
    'vodka',
    'tequila',
    'rum',
    'gin',
    'triple sec',
    'sweet and sour mix',
    'Coke'
] %}

{% set ownedLongIslandIcedTeaIngredients =
    ownedIngredients|intersect(longIslandIcedTeaIngredients)
%}
```

## `kebab`

Returns a string formatted in “kebab-case”. 

Tip: That’s a reference to [shish kebabs](http://en.wikipedia.org/wiki/Kebab#Shish) for those of you that don’t get the analogy.

```twig
{{ "foo bar?"|kebab }}
{# Outputs: foo-bar #}
```

## `lcfirst`

Lowercases the first character of a string.

## `markdown` or `md`

Processes a string with [Markdown](http://daringfireball.net/projects/markdown/).

```twig
{% set content %}
# Everything You Need to Know About Computer Keyboards

The only *real* computer keyboard ever made was famously
the [Apple Extended Keyboard II] [1].
    
    [1]: http://www.flickr.com/photos/gruber/sets/72157604797968156/
{% endset %}

{{ content|markdown }}
```

## `number`

Formats a number according to the user’s preferred language.

You can optionally pass `false` to it if you want group symbols to be omitted (e.g. commas in English).

```twig
{{ 1000000|number }} => 1,000,000
{{ 1000000|number(false) }} => 1000000
```

## `parseRefs`

Parses a string for [reference tags](reference-tags.md).

```twig
{% set content %}
    {entry:blog/hello-world:link} was my first blog post. Pretty geeky, huh?
{% endset %}
    
{{ content|parseRefs|raw }}
```

## `pascal`

Returns a string formatted in “PascalCase” (AKA “UpperCamelCase”).

```twig
{{ "foo bar"|pascal }}
{# Outputs: FooBar #}
```

## `percentage`

Formats a percentage according to the user’s preferred language.

## `replace`

Replaces parts of a string with other things.

You can replace multiple things at once by passing in an object of search/replace pairs:

```twig
{% set str = "Hello, FIRST LAST" %}

{{ str|replace({
    FIRST: currentUser.firstName,
    LAST:  currentUser.lastName
}) }}
```

Or you can replace one thing at a time:

```twig
{% set str = "Hello, NAME" %}

{{ str|replace('NAME', currentUser.name) }}
```

You can also use a regular expression to search for matches by starting and ending the replacement string’s value with forward slashes:

```twig
{{ tag.name|lower|replace('/[^\\w]+/', '-') }}
```