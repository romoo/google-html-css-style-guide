#Google HTML/CSS 风格指南#

版本：0.2

英文版：[http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)

翻译：Romoo Chen ([Twitter](https://twitter.com/romoo))

译文状态：草稿

##前言##

本文定义了 HTML 和 CSS 的格式和样式规则，旨在改善代码协作编码、代码质量和规范基本结构。它适用于使用 HTML 和 CSS 的源文件，也包括 GSS 文件。该文档可免费用于混淆、压缩和编译代码的工具，同时保持通用代码质量。

##通用样式规则##

###协议###

**省略嵌入资源的协议**

在引用样式表文件、脚本文件、图片以及其他媒体文件时忽略协议部分（`http:`，`https:`），除非使用这两种协议都无法获取到该资源。

省略协议可以避免相对 URL 产生的问题，也可以减少文件的体积。

    <!-- 不推荐 -->
    <script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>

    <!-- 推荐 -->
    <script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
    
    /* 不推荐 */
    .example {
      background: url(http://www.google.com/images/example);
    }
    
##通用格式化规则##

###缩进###

**使用两个空格**
      
不要使用 tab 或者混用 tab 和空格的方式作为缩进。

    <ul>
      <li>Fantastic
      <li>Great
    </ul>
    .example {
      color: blue;
    }

###大小写###

**只使用小写**

所有代码只使用小写：包括标签、选择器、属性及属性值（text/`CDATA` 例外，作为内容时例外）。

    <!-- 不推荐 -->
    <A HREF="/">Home</A>

    <!-- 推荐 -->
    <img src="google.png" alt="Google">

###尾部空格###

**删除多余的尾部空格**

尾部空格是多余的，可能会引起代码混乱。

    <!-- 不推荐 -->
    <p>What?_

    <!-- 推荐 -->
    <p>Yes please.

##通用 Meta 规则##

###编码###

**使用 UTF-8 (no BOM) 编码。**

确保你的编辑器文档编码为 UTF-8，没有字节顺序标记。

在 HTML 中使用 `<meta charset="utf-8">` 置顶文档编码，在 CSS 中默认就是 UTF-8 编码，不需要特别指定。

（更多编码和指定方式的资料可以参见[Character Sets & Encodings in XHTML, HTML and CSS](http://www.w3.org/International/tutorials/tutorial-char-enc/en/all.html)）

###注释###

**根据需要，给代码做注释。**

用注释解释代码：它实现了什么功能，它的目的是什么，为什么这种方案更好？

（注释代码不是强制要求，视乎项目性质和复杂程度）

###待办事项###

**使用 `TODO` 关键词标识待办事项**

只使用 `TODO` 关键词标识待办事项，而不用 `@@` 等其他格式。

使用  `TODO(contact)` 的形式附上联系方式（用户名和邮件列表）方便联系。

在冒号后加入待办事项内容，如  `TODO: action item` 。
        
    {# TODO(john.doe): revisit centering #}
    <center>Test</center>
    <!-- TODO: remove optional tags -->
    <ul>
      <li>Apples</li>
      <li>Oranges</li>
    </ul>

##HTML 风格规则##

###文档类型###

**使用 HTML5。**
      
HTML5 (HTML syntax) is preferred for all HTML documents: `<!DOCTYPE html>`.

(It’s recommended to use HTML, as `text/html`. Do not use XHTML. XHTML, as [`application/xhtml+xml`](http://hixie.ch/advocacy/xhtml), lacks both browser and infrastructure support and offers less room for optimization than HTML.)

Although fine with HTML, do not close void elements, i.e. write `<br>`, not `<br />`.

###HTML validity###
      
**Use valid HTML where possible.**
      
Use valid HTML code unless that is not possible due to otherwise unattainable performance goals regarding file size.

Use tools such as the [W3C HTML validator](http://validator.w3.org/nu/) to test.

Using valid HTML is a measurable baseline quality attribute that contributes to learning about technical requirements and constraints, and that ensures proper HTML usage.

    <!-- 不推荐 -->
    <title>Test</title>
    <article>This is only a test.

    <!-- 推荐 -->
    <!DOCTYPE html>
    <meta charset="utf-8">
    <title>Test</title>
    <article>This is only a test.</article>

###语义化###
      
**Use HTML according to its purpose.**
      
Use elements (sometimes incorrectly called “tags”) for what they have been created for. For example, use heading elements for headings, `p` elements for paragraphs, `a` elements for anchors, etc.

Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.
        
    <!-- 不推荐 -->
    <div onclick="goToRecommendations();">All recommendations</div>
    <!-- 推荐 -->
    <a href="recommendations/">All recommendations</a>

###Multimedia fallback###
      
**Provide alternative contents for multimedia.**
      
For multimedia, such as images, videos, animated objects via `canvas`, make sure to offer alternative access. For images that means use of meaningful alternative text (`alt`) and for video and audio transcripts and captions, if available.

Providing alternative contents is important for accessibility reasons: A blind user has few cues to tell what an image is about without `@alt`, and other users may have no way of understanding what video or audio contents are about either.

(For images whose `alt` attributes would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in `alt=""`.)
        
    <!-- 不推荐 -->
    <img src="spreadsheet.png">
    <!-- 推荐 -->
    <img src="spreadsheet.png" alt="Spreadsheet screenshot.">

###Separation of concerns###
      
**Separate structure from presentation from behavior.**
      
Strictly keep structure (markup), presentation (styling), and behavior (scripting) apart, and try to keep the interaction between the three to an absolute minimum.

That is, make sure documents and templates contain only HTML and HTML that is solely serving structural purposes. Move everything presentational into style sheets, and everything behavioral into scripts. 

In addition, keep the contact area as small as possible by linking as few style sheets and scripts as possible from documents and templates.

Separating structure from presentation from behavior is important for maintenance reasons. It is always more expensive to change HTML documents and templates than it is to update style sheets and scripts.
        
    <!-- 不推荐 -->
    <!DOCTYPE html>
    <title>HTML sucks</title>
    <link rel="stylesheet" href="base.css" media="screen">
    <link rel="stylesheet" href="grid.css" media="screen">
    <link rel="stylesheet" href="print.css" media="print">
    <h1 style="font-size: 1em;">HTML sucks</h1>
    <p>I’ve read about this on a few sites but now I’m sure:
      <u>HTML is stupid!!1</u>
    <center>I can’t believe there’s no way to control the styling of
      my website without doing everything all over again!</center>
    <!-- 推荐 -->
    <!DOCTYPE html>
    <title>My first CSS-only redesign</title>
    <link rel="stylesheet" href="default.css">
    <h1>My first CSS-only redesign</h1>
    <p>I’ve read about this on a few sites but today I’m actually
      doing it: separating concerns and avoiding anything in the HTML of
      my website that is presentational.
    <p>It’s awesome!

###Entity references###
      
**Do not use entity references.**
      
There is no need to use entity references like `&amp;mdash;`, `&amp;rdquo;`, or `&amp;#x263a;`, assuming the same encoding (UTF-8) is used for files and editors as well as among teams.

The only exceptions apply to characters with special meaning in HTML (like `<` and `&amp;`) as well as control or “invisible” characters (like no-break spaces).

    <!-- 不推荐 -->
    The currency symbol for the Euro is &amp;ldquo;&amp;eur;&amp;rdquo;.
    <!-- 推荐 -->
    The currency symbol for the Euro is “€”.

###Optional tags###
      
**Omit optional tags (optional).**
      
For file size optimization and scannability purposes, consider omitting optional tags. The [HTML5 specification](http://www.whatwg.org/specs/web-apps/current-work/multipage/syntax.html#syntax-tag-omission) defines what tags can be omitted.

(This approach may require a grace period to be established as a wider guideline as it’s significantly different from what web developers are typically taught. For consistency and simplicity reasons it’s best served omitting all optional tags, not just a selection.)

    <!-- 不推荐 -->
    <!DOCTYPE html>
    <html>
      <head>
        <title>Spending money, spending bytes</title>
      </head>
      <body>
        <p>Sic.</p>
      </body>
    </html>
    <!-- 推荐 -->
    <!DOCTYPE html>
    <title>Saving money, saving bytes</title>
    <p>Qed.
    
###type attributes###
      
**Omit `type` attributes for style sheets and scripts.**
      
Do not use `type` attributes for style sheets (unless not using CSS) and scripts (unless not using JavaScript).

Specifying `type` attributes in these contexts is not necessary as HTML5 implies [`text/css`](http://www.whatwg.org/specs/web-apps/current-work/multipage/semantics.html#attr-style-type) and [`text/javascript`](http://www.whatwg.org/specs/web-apps/current-work/multipage/scripting-1.html#attr-script-type) as defaults. This can be safely done even for older browsers.

    <!-- 不推荐 -->
    <link rel="stylesheet" href="//www.google.com/css/maia.css"
      type="text/css">
    <!-- 推荐 -->
    <link rel="stylesheet" href="//www.google.com/css/maia.css">
    <!-- 不推荐 -->
    <script src="//www.google.com/js/gweb/analytics/autotrack.js"
      type="text/javascript"></script>
    <!-- 推荐 -->
    <script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

##HTML Formatting Rules##

###General formatting###
      
**Use a new line for every block, list, or table element, and indent every such child element.**
      
Independent of the styling of an element (as CSS allows elements to assume a different role per `display` property), put every block, list, or table element on a new line.

Also, indent them if they are child elements of a block, list, or table element.

(If you run into issues around whitespace between list items it’s acceptable to put all `li` elements in one line. A linter is encouraged to throw a warning instead of an error.)

    <blockquote>
      <p><em>Space</em>, the final frontier.</p>
    </blockquote>
    <ul>
      <li>Moe
      <li>Larry
      <li>Curly
    </ul>
    <table>
      <thead>
        <tr>
          <th scope="col">Income
          <th scope="col">Taxes
      <tbody>
        <tr>
          <td>$ 5.00
          <td>$ 4.50
    </table>
    
###HTML quotation marks###
      
**Use double quotation marks for attribute values where necessary.**
      
When quoting attribute values, use double (`""`) rather than single quotation marks (`''`).

    <!-- 不推荐 -->
    <a class='maia-button maia-button-secondary'>Sign in</a>
    <!-- 推荐 -->
    <a class="maia-button maia-button-secondary">Sign in</a>

##CSS Style Rules##

###CSS validity###
      
**Use valid CSS where possible.**
      
Unless dealing with CSS validator bugs or requiring proprietary syntax, use valid CSS code.

Use tools such as the [W3C CSS validator](http://jigsaw.w3.org/css-validator/) to test. Using valid CSS is a measurable baseline quality attribute that allows to spot CSS code that may not have any effect and can be removed, and that ensures proper CSS usage.

###ID and class naming###
      
**Use meaningful or generic ID and class names.**
      
Instead of presentational or cryptic names, always use ID and class names that reflect the purpose of the element in question, or that are otherwise generic.

Names that are specific and reflect the purpose of the element should be preferred as these are most understandable and the least likely to change.

Generic names are simply a fallback for elements that have no particular or no meaning different from their siblings. They are typically needed as “helpers.”

Using functional or generic names reduces the probability of unnecessary document or template changes.

    /* 不推荐: meaningless */
    #yee-1901 {}

    /* 不推荐: presentational */
    .button-green {}
    .clear {}
    /* Recommended: specific */
    #gallery {}
    #login {}
    .video {}

    /* Recommended: generic */
    .aux {}
    .alt {}
    
###ID and class name style###
      
**Use ID and class names that are as short as possible but as long as necessary.**
      
Try to convey what an ID or class is about while being as brief as possible.

Using ID and class names this way contributes to acceptable levels of understandability and code efficiency.

    /* 不推荐 */
    #navigation {}
    .atr {}
    /* Recommended */
    #nav {}
    .author {}

###Type selectors###
      
**Avoid qualifying ID and class names with type selectors.**
      
Unless necessary (for example with helper classes), do not use element names in conjunction with IDs or classes.

Avoiding unnecessary ancestor selectors is useful for [performance reasons](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/).

    /* 不推荐 */
    ul#example {}
    div.error {}
    /* Recommended */
    #example {}
    .error {}
    
###Shorthand properties###
      
**Use shorthand properties where possible.**
      
SS offers a variety of [shorthand](http://www.w3.org/TR/CSS21/about.html#shorthand) properties (like `font`) that should be used whenever possible, even in cases where only one value is explicitly set.

Using shorthand properties is useful for code efficiency and understandability.

    /* 不推荐 */
    border-top-style: none;
    font-family: palatino, georgia, serif;
    font-size: 100%;
    line-height: 1.6;
    padding-bottom: 2em;
    padding-left: 1em;
    padding-right: 1em;
    padding-top: 0;
    /* Recommended */
    border-top: 0;
    font: 100%/1.6 palatino, georgia, serif;
    padding: 0 1em 2em;
    
###0 and units###
      
**Omit unit specification after “0” values.**
      
Do not use units after `0` values unless they are required.
          
    margin: 0;
    padding: 0;
    
###Leading 0s###
      
**Omit leading “0”s in values.**
      
Do not use put `0`s in front of values or lengths between -1 and 1.

    font-size: .8em;
    
###Hexadecimal notation###
      
**Use 3 character hexadecimal notation where possible.**
      
For color values that permit it, 3 character hexadecimal notation is shorter and more succinct.

    /* 不推荐 */
    color: #eebbcc;
    /* Recommended */
    color: #ebc;
    
###Prefixes###
      
**Prefix selectors with an application-specific prefix (optional).**
      
In large projects as well as for code that gets embedded in other projects or on external sites use prefixes (as namespaces) for ID and class names. Use short, unique identifiers followed by a dash.

Using namespaces helps preventing naming conflicts and can make maintenance easier, for example in search and replace operations.

    .adw-help {} /* AdWords */
    #maia-note {} /* Maia */
    
###ID and class name delimiters###
      
**Separate words in ID and class names by a hyphen.**
      
Do not concatenate words and abbreviations in selectors by any characters (including none at all) other than hyphens, in order to improve understanding and scannability.

    /* 不推荐: does not separate the words “demo” and “image” */
    .demoimage {}

    /* 不推荐: uses underscore instead of hyphen */
    .error_status {}

    /* Recommended */
    #video-id {}
    .ads-sample {}
    
###Hacks###
      
**Avoid user agent detection as well as CSS “hacks”—try a different approach first.**
      
It’s tempting to address styling differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be considered last resort in order to achieve and maintain an efficient and manageable code base. Put another way, giving detection and hacks a free pass will hurt projects in the long run as projects tend to take the way of least resistance. That is, allowing and making it easy to use detection and hacks means using detection and hacks more frequently—and more frequently is too frequently.

##CSS Formatting Rules###

###Declaration order###
      
**Alphabetize declarations.**
      
Put declarations in alphabetical order in order to achieve consistent code in a way that is easy to remember and maintain.

Ignore vendor-specific prefixes for sorting purposes. However, multiple vendor-specific prefixes for a certain CSS property should be kept sorted (e.g. -moz prefix comes before -webkit).

    background: fuchsia;
    border: 1px solid;
    -moz-border-radius: 4px;
    -webkit-border-radius: 4px;
    border-radius: 4px;
    color: black;
    text-align: center;
    text-indent: 2em;
    
###Block content indentation###
      
**Indent all block content.**
      
Indent all [block content](http://www.w3.org/TR/CSS21/syndata.html#block), that is rules within rules as well as declarations, so to reflect hierarchy and improve understanding.

    @media screen, projection {

      html {
        background: #fff;
        color: #444;
      }

    }
    
###Declaration stops###
      
**Use a semicolon after every declaration.**
      
End every declaration with a semicolon for consistency and extensibility reasons.

    /* 不推荐 */
    .test {
      display: block;
      height: 100px
    }
    /* Recommended */
    .test {
      display: block;
      height: 100px;
    }
    
###Property name stops###
      
**Use a space after a property name’s colon.**
      
Always use a single space between property and value (but no space between property and colon) for consistency reasons.

    /* 不推荐 */
    h3 {
      font-weight:bold;
    }
    /* Recommended */
    h3 {
      font-weight: bold;
    }
    
###Selector and declaration separation###
      
**Separate selectors and declarations by new lines.**
      
Always start a new line for each selector and declaration.

    /* 不推荐 */
    a:focus, a:active {
      position: relative; top: 1px;
    }
    /* Recommended */
    h1,
    h2,
    h3 {
      font-weight: normal;
      line-height: 1.2;
    }
    
###Rule separation###
      
**Separate rules by new lines.**
      
Always put a line between rules.

    html {
      background: #fff;
    }

    body {
      margin: auto;
      width: 50%;
    }
    
###CSS quotation marks###
      
**Use single quotation marks for attribute selectors and property values where necessary.**
      
When quoting attribute selectors and property values, use single (`''`) rather than double (`""`) quotation marks. Do not use quotation marks in URI values (`url()`).

    /* 不推荐 */
    @import url("//www.google.com/css/maia.css");

    html {
      font-family: "open sans", arial, sans-serif;
    }
    /* Recommended */
    @import url(//www.google.com/css/maia.css);

    html {
      font-family: 'open sans', arial, sans-serif;
    }

##CSS Meta Rules##

###Section comments###
      
**Group sections by a section comment (optional).**
      
If possible, group style sheet sections together by using comments. Separate sections with new lines.

    /* Header */

    #adw-header {}

    /* Footer */

    #adw-footer {}

    /* Gallery */

    .adw-gallery {}


##PARTING_WORDS##

**Be consistent.**

If you’re editing code, take a few minutes to look at the code around you and determine its style. If they use spaces around all their arithmetic operators, you should too. If their comments have little boxes of hash marks around them, make your comments have little boxes of hash marks around them too.

The point of having style guidelines is to have a common vocabulary of coding so people can concentrate on what you’re saying rather than on how you’re saying it. We present global style rules here so people know the vocabulary, but local style is also important. If code you add to a file looks drastically different from the existing code around it, it throws readers out of their rhythm when they go to read it. Avoid this.

Revision 2.2

