CSS
================================================================================


Nesting
--------------------------------------------------------------------------------

It's recommended for performance to not next CSS rules more than 3 deep. 

    .logo {}                /* good */
    #footer li {}           /* good */
    #header .logo a {}      /* good */
    #header nav ul li {}    /* bad! */

CSS is read backwards so taking the last example there, the browser will look
for all `li` elements, then find parents that equal `ul` then `nav` and lastly
`#header`. It very ineffeicant but that's how it works.

A more intelligent approach could be:

    .header-nav .item {}

So it will look for all `.item` and then thoses with parents of `.header-nav`.
That method also scales better as if we are to add a second nav to the header
then it won't interfer with the existing rules (so long as it's not named
`.header-nav` but something like `.additional-nav`).


IDs or Classes
--------------------------------------------------------------------------------

There is alot of talk if IDs are a good thing to use or not. Taking all the
points into account, I cannot say for sure to if IDs should be used or not in
this case of standarisation. Your best bet is to use your professional judgement
whether or not a case requires an ID or not.

My personal prefences they are good to use for a high-level of design. So I
always use IDs for the main site header and footer - `#header` and `#footer`
respectively. The reason for these is there won't be a case where these are
repeated on the page, ever, so I can safetly refer to these via IDs as apposed
to their element (`header`/`footer`) or a class (`.header`/`.footer`). There
are also cases within the document where you could use IDs; these are typically
parts of the page that you know will never be repeated on the page. These
should only be applied to the direct children of the main section, or just
outside.

This is only a guide though so do use your best judgement keeping in mind
issues with specificity (check out [CSS Specificity][1] by Vitaly Friedman to
understand them better) and also keeping the IDs unique. Also worth mentioning
that IDs are very handy when it comes to JavaScript and link achoring in HTML,
so could be worth concidering these aspects when deciding on what to use.



Format of Code
--------------------------------------------------------------------------------

* Use `-` (not `_` or `camelCase`) for elegancy
* 4 spaces instead of a tab to indent
* Space after `:`
* Space before `{`
* Don't over qualify selectors e.g. `div#header {}` (`#header {}` works)
    * Though cases like `p.header {}` and `h2.header {}` are valid
* Don't add units onto zero values e.g. `padding: 0px` (`padding: 0;` works)
* If measurement is 0.*, then concider removing the initial zero (so `0.8em`
  becomes `.8em`)

Each CSS element rule should be on one line but never two on one line for one
rule group. There should also be a space between the end of the attribute call
and the start of the group (`{}`)

    .content img {}         /* good */
    p,
    h3 {}                   /* good */
    h4, h5 {}               /* bad! */
    h6{}                    /* bad! */
   
Tabbing shouldn't be used but fixed number of spaces for indendation (4 is a
nice number to use). The reason being that tabs have a habit of being
interpreted differently depending on what ever the hell is viewing the file.
Spaces don't have this issue has the size is always fixed and will fit, but
also makes it easier to align items sensibly.


Documenting Code
--------------------------------------------------------------------------------

Documenting CSS is just as important as any other code; it helps developers get
an understanding of choices made and what's going on. With that said, there is 
no real defined way to document the code so rather than take a working method
from another language and repurpose that, here I'll try to define a working
documenting method for CSS.


### Start of Document

All documents should start with a title, author list, description and content.

    /**
     * [title]
     * =========================================================================
     * @author [name] <[email]>
     *
     * [description]
     *
     * Content
     * - [content]
     */

[title] is a descriptive name for the document. So for something like main.css,
you could call it "Main style sheet".

On the third line I have a repeated number of `=` signs; this, along with the
rest of the document should follow the standards set in markdown writing. So
that line for me is no wider than the document (typically 80 characters).

`@author [auth]` is where we state who has worked on that document. If more than
one person has worked on it then we seperate the list of authors via commas as
so: `@author [name] <[email]>, [name] <[email]>`. Also worth noting that 
`<[email]>` isn't required but good for quickly being able to query a particular
author.

`[description]` is a long description of the document, explaining any major
points of interest or just that the document is for a particular page. It just
need to be helpful.

`Content` just lists the main sections of the document as parent-children. A
parent can have any number of children deemed nessary, but keep in mind rules on
nesting.


### Group Selectors & Elements

With group of elements we want to document we can add the following:


    /**
     * [title]
     * -------------------------------------------------------------------------
     * [description]
     */
     
     .parent-one {}
         .parent-one .child {}
     
     .parent-two {}     


`[title]` is required and is the part you can refernce in the `[content]`
section.

Note the use of `-` instead of a `=` this time; this is show that it's a sub-
heading within the doc.

`[description]` is optional but good if you want to describe what's happening.

Also worth noting that when reference a group of selectors that you should have
an empty line between the documentation and the first selector.


### Specific Selector & Element

Using the same format as Group Elements we can document a single selector


    /**
     * [title]
     * -------------------------------------------------------------------------
     * [description]
     */
     .child {}


The only difference this time is there is no gap between the doucmentation and
the selector as it shows we are directly refering to that particular selector
or element. Though if you have nested style, it's still advisable to leave the
blank line as we are refering to that primary parent

The `-` line can be removed in this case, but I keep this personally to break up
the code.

Both Groups and Sepecifics can be nested to provider deeper documentation



Thoughts
--------------------------------------------------------------------------------

> Broad selectors allow us to be efficient, yet can have adverse consequences if
  not tested. Location-specific selectors can save us time, but will quickly 
  lead to a cluttered stylesheet. Exercise your best judgement.


Terms
--------------------------------------------------------------------------------

- **element** is the single definition given; e.g. `article` `#header` and
              `.parent` are all elements.
- **attribute** is a single style case given to an element; e.g. `color: #FFF`
- **selector** is the rule to select an element; appears before `{`. So
               `.parent .child {}` is a selector as well as `article {}`. The
               main difference between an element and selector then is it can 
               contain one or more elements to select part of the DOM.


References
--------------------------------------------------------------------------------

* [CSS Style guide](http://css-tricks.com/css-style-guides/)
* [GitHub CSS Styleguide](https://github.com/styleguide/css)
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [My HTML/CSS coding style](http://csswizardry.com/2012/04/my-html-css-coding-style/)
* [Improving Code Readability with CSS Styleguides](http://coding.smashingmagazine.com/2008/05/02/improving-code-readability-with-css-styleguides/)
* [ThinkUp Code Style Guide: CSS](https://github.com/ginatrapani/ThinkUp/wiki/Code-Style-Guide:-CSS)
* [WordPress CSS Coding Standard](http://make.wordpress.org/core/handbook/coding-standards/css/)



[1]: http://coding.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/