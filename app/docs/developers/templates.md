---
layout: doc
weight: 1
title: Templates
categories: developers
permalink: /developers/templates/
---

Jekyll uses the [Liquid](https://shopify.github.io/liquid/) templating language to
process templates. All of the standard Liquid [tags](https://shopify.github.io/liquid/tags/) and
[filters](https://shopify.github.io/liquid/filters/) are
supported. Jekyll even adds a few handy filters and tags of its own to make
common tasks easier.

#### Filters

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Description</th>
      <th><span class="filter">Filter</span> and <span class="output">Output</span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p class="name"><strong>Relative URL</strong></p>
        <p>Prepend the <code>baseurl</code> value to the input. Useful if your site is hosted at a subpath rather than the root of the domain.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ "/assets/style.css" | relative_url }}{% endraw %}</code>
        </p>
        <p>
         <code class="output">/my-baseurl/assets/style.css</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Absolute URL</strong></p>
        <p>Prepend the <code>url</code> and <code>baseurl</code> value to the input.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ "/assets/style.css" | absolute_url }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">http://example.com/my-baseurl/assets/style.css</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Date to XML Schema</strong></p>
        <p>Convert a Date into XML Schema (ISO 8601) format.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.time | date_to_xmlschema }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">2008-11-07T13:07:54-08:00</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Date to RFC-822 Format</strong></p>
        <p>Convert a Date into the RFC-822 format used for RSS feeds.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.time | date_to_rfc822 }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">Mon, 07 Nov 2008 13:07:54 -0800</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Date to String</strong></p>
        <p>Convert a date to short format.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.time | date_to_string }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">07 Nov 2008</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Date to Long String</strong></p>
        <p>Format a date to long format.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.time | date_to_long_string }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">07 November 2008</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Where</strong></p>
        <p>Select all the objects in an array where the key has the given value.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.members | where:"graduation_year","2014" }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Where Expression</strong></p>
        <p>Select all the objects in an array where the expression is true. Jekyll v3.2.0 & later.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.members | where_exp:"item",
"item.graduation_year == 2014" }}{% endraw %}</code>
         <code class="filter">{% raw %}{{ site.members | where_exp:"item",
"item.graduation_year < 2014" }}{% endraw %}</code>
         <code class="filter">{% raw %}{{ site.members | where_exp:"item",
"item.projects contains 'foo'" }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Group By</strong></p>
        <p>Group an array's items by a given property.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.members | group_by:"graduation_year" }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">[{"name"=>"2013", "items"=>[...]},
{"name"=>"2014", "items"=>[...]}]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>XML Escape</strong></p>
        <p>Escape some text for use in XML.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ page.content | xml_escape }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>CGI Escape</strong></p>
        <p>
          CGI escape a string for use in a URL. Replaces any special characters
          with appropriate %XX replacements.
        </p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ "foo,bar;baz?" | cgi_escape }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">foo%2Cbar%3Bbaz%3F</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>URI Escape</strong></p>
        <p>
          URI escape a string.
        </p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ "foo, bar \baz?" | uri_escape }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">foo,%20bar%20%5Cbaz?</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Number of Words</strong></p>
        <p>Count the number of words in some text.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ page.content | number_of_words }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">1337</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Array to Sentence</strong></p>
        <p>Convert an array into a sentence. Useful for listing tags.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ page.tags | array_to_sentence_string }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">foo, bar, and baz</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Markdownify</strong></p>
        <p>Convert a Markdown-formatted string into HTML.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ page.excerpt | markdownify }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Smartify</strong></p>
        <p>Convert "quotes" into &ldquo;smart quotes.&rdquo;</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ page.title | smartify }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Converting Sass/SCSS</strong></p>
        <p>Convert a Sass- or SCSS-formatted string into CSS.</p>
      </td>
      <td class="align-center">
        <p>
          <code class="filter">{% raw %}{{ some_scss | scssify }}{% endraw %}</code>
          <code class="filter">{% raw %}{{ some_sass | sassify }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Slugify</strong></p>
        <p>Convert a string into a lowercase URL "slug". See below for options.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ "The _config.yml file" | slugify }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">the-config-yml-file</code>
        </p>
        <p>
         <code class="filter">{% raw %}{{ "The _config.yml file" | slugify: 'pretty' }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">the-_config.yml-file</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Data To JSON</strong></p>
        <p>Convert Hash or Array to JSON.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.data.projects | jsonify }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Normalize Whitespace</strong></p>
        <p>Replace any occurrence of whitespace with a single space.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ "a \n b" | normalize_whitespace }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Sort</strong></p>
        <p>Sort an array. Optional arguments for hashes: 1.&nbsp;property name 2.&nbsp;nils order (<em>first</em> or <em>last</em>).</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ page.tags | sort }}{% endraw %}</code>
        </p>
        <p>
         <code class="filter">{% raw %}{{ site.posts | sort: 'author' }}{% endraw %}</code>
        </p>
        <p>
         <code class="filter">{% raw %}{{ site.pages | sort: 'title', 'last' }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Sample</strong></p>
        <p>Pick a random value from an array. Optional: pick multiple values.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ site.pages | sample }}{% endraw %}</code>
        </p>
        <p>
         <code class="filter">{% raw %}{{ site.pages | sample:2 }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>To Integer</strong></p>
        <p>Convert a string or boolean to integer.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ some_var | to_integer }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Array Filters</strong></p>
        <p>Push, pop, shift, and unshift elements from an Array.</p>
        <p>These are <strong>NON-DESTRUCTIVE</strong>, i.e. they do not mutate the array, but rather make a copy and mutate that.</p>
      </td>
      <td class="align-center">
        <p>
          <code class="filter">{% raw %}{{ page.tags | push: 'Spokane' }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">['Seattle', 'Tacoma', 'Spokane']</code>
        </p>
        <p>
          <code class="filter">{% raw %}{{ page.tags | pop }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">['Seattle']</code>
        </p>
        <p>
          <code class="filter">{% raw %}{{ page.tags | shift }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">['Tacoma']</code>
        </p>
        <p>
          <code class="filter">{% raw %}{{ page.tags | unshift: "Olympia" }}{% endraw %}</code>
        </p>
        <p>
          <code class="output">['Olympia', 'Seattle', 'Tacoma']</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class="name"><strong>Inspect</strong></p>
        <p>Convert an object into its String representation for debugging.</p>
      </td>
      <td class="align-center">
        <p>
         <code class="filter">{% raw %}{{ some_var | inspect }}{% endraw %}</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

#### Tags

##### Includes

If you have small page fragments that you wish to include in multiple places on
your site, you can use the `include` tag.

```liquid
{% raw %}{% include footer.html %}{% endraw %}
```

Jekyll expects all include files to be placed in an `_includes` directory at the
root of your source directory. This will embed the contents of
`<source>/_includes/footer.html` into the calling file.

You can also pass parameters to an include. Omit the quotation marks to send a variable's value. Liquid curly brackets should not be used here:

```liquid
{% raw %}{% include footer.html param="value" variable-param=page.variable %}{% endraw %}
```

These parameters are available via Liquid in the include:

```liquid
{% raw %}{{ include.param }}{% endraw %}
```

##### Including files relative to another file

You can also choose to include file fragments relative to the current file:

```liquid
{% raw %}{% include_relative somedir/footer.html %}{% endraw %}
```

You won't need to place your included content within the `_includes` directory. Instead,
the inclusion is specifically relative to the file where the tag is being used. For example,
if `_posts/2014-09-03-my-file.markdown` uses the `include_relative` tag, the included file
must be within the `_posts` directory, or one of its subdirectories. You cannot include
files in other locations.

All the other capabilities of the `include` tag are available to the `include_relative` tag,
such as using variables.

### Code snippet highlighting

Doc42 has a builtin syntaxt highlighting using Highlight.js.

<p>Code styling is kept basic – just wrap anything in a <code>&lt;code&gt;</code> and it will appear like <code>this</code>. For blocks of code, wrap a <code>&lt;code&gt;</code> with a <code>&lt;pre&gt;</code>.</p>

<div class="docs-example">
<pre>
<code>.some-class {
  background-color: red;
}
</code>
</pre>
</div>


<pre class="code-example">
<code class="language-html">&lt;pre&gt;&lt;code&gt;.some-class {
  background-color: red;
}&lt;/code&gt;&lt;/pre&gt;

&lt;!-- Remember every whitespace and break will be preserved in a &lt;pre&gt;, including indentation in your code --&gt;
</code>
</pre>


### Link

If you want to include a link to a collection's document, a post, a page
or a file the `link` tag will generate the correct permalink URL for the path
you specify.

You must include the file extension when using the `link` tag.

```liquid
{% raw %}
{% link _collection/name-of-document.md %}
{% link _posts/2016-07-26-name-of-post.md %}
{% link news/index.html %}
{% link /assets/files/doc.pdf %}
{% endraw %}
```

You can also use this tag to create a link in Markdown as follows:

```liquid
{% raw %}
[Link to a document]({% link _collection/name-of-document.md %})
[Link to a post]({% link _posts/2016-07-26-name-of-post.md %})
[Link to a page]({% link news/index.html %})
[Link to a file]({% link /assets/files/doc.pdf %})
{% endraw %}
```

### Gist

Use the `gist` tag to easily embed a GitHub Gist onto your site. This works
with public or secret gists:

```liquid
{% raw %}
{% gist parkr/931c1c8d465a04042403 %}
{% endraw %}
```

You may also optionally specify the filename in the gist to display:

```liquid
{% raw %}
{% gist parkr/931c1c8d465a04042403 jekyll-private-gist.markdown %}
{% endraw %}
```

To use the `gist` tag, you'll need to add the
[jekyll-gist](https://github.com/jekyll/jekyll-gist) gem to your project.
