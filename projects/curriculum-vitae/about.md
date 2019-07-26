---
description: What? A CV on GitHub?
---

# About

Yup. I host my LaTeX CV on a dedicated repository on GitHub and release every version of it using dedicated _Releases_. I really enjoyed the idea to review it as a coding project, making it buildable as a common project using `make` and release its binary version - the PDF.

It's pretty easy: `tex` files get built using `pdflatex` into a `pdf` and released everytime I have something new to put inside the CV. But it's not all about this. I actually organized the _code_ to handle two problems explained below.

## Document templating

The first issue I faced was about few companies being very strict on the CV format, hence asking for the [EuroPass](https://europass.cedefop.europa.eu/it/documents/curriculum-vitae/templates-instructions/templates/doc) one, for example. On the other hand, I really enjoyed _my_ custom format and didn't want to just drop it. And what if another company would have come asking for a CV formatted following another one format?

All of this lead me considering templating my documents: many `tex` files as many formats I wanted to support and a single _database_ file keeping the informations used to fill the templates.

In order to do that I opted for using a simple `json` structured file collecting key/values in this very simple way:

{% code-tabs %}
{% code-tabs-item title="keys.json" %}
```text
{
    "key_1": "value_1",
    "key_2": "value_2",
    ...
    "key_n": "value_n"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Once I got my database populated with all my CV informations, I revised the `tex` templates to replace all the informations occurrences with `{{key_X}}` corresponding database keyword.

Using `jq` command I iterated over the `keys.json` file entries to export any key as a shell environment key, then using a nice tool called [`mush`](https://github.com/jwerle/mush) I replaced any `{{key_X}}` corresponding to an environment key with the same name with its value. A simple `pdflatex` command was needed at that moment and _tada!_, my custom / _EuroPass_ was ready for an application.

## Multiple internationalized documents

The latter issue I wanted to fix was the internationalization. The idea behind the solution above needed to be pushed further on.

`keys.json` evolved to support multiple languages or a single default value \(used for any language\):

{% code-tabs %}
{% code-tabs-item title="keys.json" %}
```text
{
	"key_1": {
		"it": "valore_1",
		"en": "value_1"
	},
	...
	"key_n": {
		"default": "value_n"
	}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This time, the `jq` script needed a little bit more modifications to iterate over supported languages and select a coherent value. Something just like this:

```bash
jq -r --arg lang "${lang}" -r 'to_entries[]
    | "\(.key)=\(.value[$lang] // .value.default)"' < keys.json
```

Where `$lang` is a Bash variable corresponding to `it` or `en`, in this case.



