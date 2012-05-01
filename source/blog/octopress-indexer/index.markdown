---
layout: page
title: "Indexer for Octopress"
date: 2012-05-01 11:56
comments: true
sharing: true
footer: true
indexer: true
---
{% raw %}
## Description

A tool for Octopress to generate IDs in heading tags and index list aside. It helps you easily build a tutorial page with many chapters.

*   [gist](https://gist.github.com/2565249/6151c81f7af333d5c1d9dd0b2bdcba2c7a966dca)

## Features

*   Support all languages.

## Syntax

    {{ page.indexer_aside }}

    or

    {{ content | indexer }}
    {{ content | indexer_aside }}

## Usage

1.  Download [Indexer for Octopress](https://gist.github.com/gists/2565249/download) into `source/plugins`
2.  This plugin should be used in pages with a variable `indexer` being `true`, for example:

         ---
         layout: page
         title: "Getting start with Indexer for Octopress"
         indexer: true
         ---
         ## Chapter 1

         blablabla...

         ### Chapter 1.1

         blablabla...

         ### Chapter 1.2

         blablabla...

         ## Chapter 2

    Note that your page cannot contain any h1 tag (Because h1 has been used for your title).

3.  You will need an aslide to make it work, for example:

    In `source\_includes\custom\asides\indexer.html`

        {% if page.indexer == true %}
          <section>
          <h1>Catalog</h1>
          {{ page.indexer_aside }}
          </section>
        {% else %}
          {% if site.page_asides.size %}
            {% include_array default_asides %}
          {% endif %}
        {% endif %}

4.  Don't forget to edit `_config.yml`:

        page_asides: [custom/asides/indexer.html]

5.  That's it! Headings in your page will be given an unique ID, and `{{ page.indexer_aside }}` will generate a 2 level nested list with anchors to each heading.

## Troubleshooting

### Alternative Way

Becasue this plugin uses some hacking way (Override Jekyll methods) for porviding easy usage. You can use `{{ content | indexer }}` or `{{ content | indexer_aside }}`

*   `{{ content | indexer }}`

    If the content contains HTML heading tag, this filter will give IDs to each heading. That is, you have to edit `source\_layouts\page.html` like:

        - {{ content }}
        + {% if page.indexer %}
        +   {{ content | indexer }}
        + {% else %}
        +   {{ content }}
        + {% endif %}

*   `{{ content | indexer_aside }}`

    If the content contains HTML heading tag, this filter will convert it into a list usded for aside. Then in `source\_includes\custom\asides\indexer.html`:

        {% if page.indexer == true %}
          <section>
          <h1>Catalog</h1>
          {{ content | indexer_aside }}
          </section>
        {% else %}
          {% if site.page_asides.size %}
            {% include_array default_asides %}
          {% endif %}
        {% endif %}

### Not Work

Try removing `Page` class in `indexer.rb`, and keep using alternative way.

### Still Not Work

tonytonyjan(at)gmail(dot)com
 
## Licence

Distributed under the [MIT License][MIT].
 
[MIT]: http://www.opensource.org/licenses/mit-license.php
{% endraw %}