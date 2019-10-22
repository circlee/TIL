[](#comparison-by-example)Comparison by example
-----------------------------------------------

The following table shows the AsciiDoc syntax as it compares to Markdown. Since AsciiDoc supports a broader range of syntax than Markdown, this side-by-side comparison focuses mainly on areas where the syntax overlaps.

Table 1. A selection of AsciiDoc language features compared to Markdown  

Language Feature

| Feature | <div style="width:300px;">Markdown</div> | <div style="width:300px;">AsciiDoc</div> |
| --- | ---| --- |
| Bold (constrained) | ``**bold**`` | ``*bold*``|
| Bold (unconstrained) | ``**b**old`` | ``**b**old`` |
| Italic (constrained) | ``*italic*`` | ``_italic_`` |
|Italic (unconstrained) | _n/a_ | ``__i__talic``|
|Monospace (constrained) | `` `monospace` `` | `` `monospace` ``|
|Monospace (unconstrained) | `` `m`onospace `` | ``` ``m``onospace ```|
|Link with label | ``[AsciiDoc](http://asciidoc.org)`` | ``http://asciidoc.org[AsciiDoc]``|
| Relative link | ``[user guide](user-guide.html)`` | ``link:user-guide.html[user guide]``<br>``xref:user-guide.adoc[user guide]``|
|File link | ``[get the PDF]({% raw %}{{ site.url }}{% endraw %}/assets/mydoc.pdf)``|``link:{site-url}/assets/mydoc.pdf[get the PDF]``|
|Cross reference |``See link:#_usage[Usage].``<br>``<h2 id="_usage">Usage</h2>``|``See <<_usage>>.``<br>``== Usage``|
|Block ID / anchor | ``<h2 id="usage">Usage</h2>`` | ``[#usage] ``<br>``== Usage``|
|Inline anchor | _n/a_ | ``. [[step-1]]Download the software`` |
|Inline image w/ alt text|``![Logo](/images/logo.png)``|``image:logo.png[Logo]``|
|Block image w/ alt text|_n/a_|``image::logo.png[Logo]``|
|Section heading\*|``## Heading 2``|``== Heading 2``|
|Blockquote\*|> Quoted text.<br>><br>> Another paragraph in quote. | ____ <br>Quoted text.<br><br>Another paragraph in quote.<br>____|
|Literal block | ``$ gem install asciidoctor`` | <strong>Indented (by 1 or more spaces)</strong><br>``$ gem install asciidoctor`` <br><br><strong>Delimited</strong><br>....<br>$ gem install asciidoctor<br>....|
|Code block\*|
    ```java
    public class Person {
      private String name;
      public Person(String name) {
        this.name = name;
      }
    }
    ```|

    [source,java]
    ----
    public class Person {
      private String name;
      public Person(String name) {
        this.name = name;
      }
    }
    ----

Unordered list

    * apples
    * orange
      * temple
      * navel
    * bananas

    * apples
    * oranges
    ** temple
    ** navel
    * bananas

Ordered list

    1. first
    2. second
    3. third

    . first
    . second
    . third

Thematic break (aka horizontal rule)\*

    ***
    
    * * *
    
    ---
    
    - - -
    
    ___
    
    _ _ _

    '''

Typographic quotes (aka “smart quotes”)

Enabled through an extension switch, but offer little control in how they are applied.

    The `'90s popularized a new form of music known as "`grunge`" rock.
    Its influence extended well beyond music.

Document header

Slapped on as “front matter”

    ---
    layout: docs
    title: Writing posts
    prev_section: defining-frontmatter
    next_section: creating-pages
    permalink: /docs/writing-posts/
    ---

Native support!

    = Writing posts
    :awestruct-layout: base
    :showtitle:
    :prev_section: defining-frontmatter
    :next_section: creating-pages

Admonitions

_n/a_

    TIP: You can add line numbers to source listings by adding the word `numbered` in the attribute list after the language name.

Sidebars

_n/a_

    .Lightweight Markup
    ****
    Writing languages that let you type less and express more.
    ****

Block titles

_n/a_

    .Grocery list
    * Milk
    * Eggs
    * Bread

Includes

_n/a_

    include::intro.adoc[]

URI reference

    Go [Home][home].
    
    [home]: https://example.org

    :home: https://example.org
    
    Go {home}[Home].

Custom CSS classes

_n/a_

    [.path]_Gemfile_

\* Asciidoctor also supports the Markdown syntax for this language feature.

You can see that AsciiDoc has the following advantages over Markdown:

*   AsciiDoc uses the same number of markup characters or less when compared to Markdown in nearly all cases.
    
*   AsciiDoc uses a consistent formatting scheme (i.e., it has consistent patterns).
    
*   AsciiDoc can handle all permutations of nested inline (and block) formatting, whereas Markdown often falls down.
    
*   AsciiDoc handles cases that Markdown doesn’t, such as a proper approach to inner-word markup, source code blocks and block-level images.
    

Certain Markdown flavors, such as Markdown Extra, support additional features such as tables and description lists. However, since these features don’t appear in “plain” Markdown, they’re not included in the comparison table. But they’re supported natively by AsciiDoc.

Asciidoctor, which is used for converting AsciiDoc on GitHub and GitLab, emulates “the good parts” of the Markdown syntax, like headings, blockquotes and fenced code blocks, making migration from Markdown to AsciiDoc fairly simple. For details about migration, see [Markdown Compatibility](https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/#markdown-compatibility).

To read more about the shortcomings of Markdown, see these opinion pieces:

*   [Why You Shouldn’t Use “Markdown” for Documentation](http://ericholscher.com/blog/2016/mar/15/dont-use-markdown-for-technical-docs/)
    
*   [Markdown Considered Harmful](https://medium.com/@bbirdiman/markdown-considered-harmful-495ccfe24a52)
    
*   [Sundown on Markdown?](https://www.simple-talk.com/blogs/2014/02/28/sundown-on-markdown/)