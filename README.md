# Front End Coding Guidelines

## Contents

* [Overview](#overview) 
* [Supported Browsers](#supported-browsers)
* [Markup](#markup)
    * [HTML5](#html5)
    * [General Markup Guidelines]
* [Styles](#styles)
    * [Organization](#organization)
    * [Pattern Library](#pattern-library)
    * [Themes](#themes)
    * [Style Guide](#style-guide)
        * [Indentation](#indentation)
        * [Selectors](#selectors)
        * [Properties](#properties)
        * [Variables](#variables)
        * [Mixins](#mixins)
    * [CSS3]
        * progressive enhancement
    * [Animations]
    * [Stay Rad](#stay-rad)
* [JavaScript](#javascript)
    * [Unit testing](#unit-tests)
    * [Code Quality](#code-quality)
    * [Formatting](#javascript-formatting)
        * [Indentation](#indentation)
        * [Statement Termination](#statement-termination)
        * [Line Length](#line-length)
        * [Blank Lines](#blank-lines)
        * [Naming](#naming)
        * [Equality Operators](#equality-operators)
        * [Ternary Operator](#ternary-operator)
        * [Compound Statements](#compound-statements)
        * [White Space](#white-space)
    * [JsHint](#jshint)
    * [Write Modular Code](#write-modular-code)
        * [Private module](#private-module)
        * [Module with Public API](#module-with-public-api)
    * [Best Practices](#best-practices)
        * Animate and Style with CSS, not JavaScript
        * [Declaring Variables](#declaring-variables)
        * Manage State, Not Style
        * Use delegated events
    * Third-party libraries and plugins
* [Responsive Design](#responsive-design)
* [Accessibility]
    * Standards Compliance
    * Simple Markup
    * WAI-ARIA
* [Performance]
    * Create Markup on the Server
    * Limit Number of Requests
        * Combine CSS
        * Combine JS
        * Combine Images
    * Optimize include order
    * Embed CSS and JS when appropriate
    * Tools to test performance
* [Principles]
    * Separation of Content, Style, and Behavior
    * Consistency
    * Prefer progressive enhancement to polyfills
* [Working With Design]
* [References]

## Overview

This document contains guidelines for web applications built by WHS. It is to be readily available to anyone who wishes to check the iterative progress of our best practices.

This document's primary motivation is to promote code consistency. By maintaining consistency in coding styles and conventions, we can ease the burden of legacy code maintenance, and mitigate risk of breakage in the future. By adhering to best practices, we ensure a consistent user experience, optimized page loading, and maintainable code.

This document outlines the conventions we use at WHS. This is an open document and everything is up for discussion/consideration. We have a tremendous amount of legacy code that does not adhere to these rules, and if you find yourself in one of those files it is in everyone's best interest to refactor it.

These guidelines are not specific to WHS. Our product is not unique enough to warrant deviations from industry standards. Much of this document has been adapted from other front end development guidelines. We're not developing on a seperate internet or for a unique browser, so we shouldn't need to invent new standards.


## Supported Browsers

[Supported Browser List](http://foswiki.dev.webmd.com/bin/view.pl/Main/SupportedBrowsers)

We do not guarantee that all functionality will work the same between browsers. In fact, with responsive design, we intentionally change layout and style for different browsers. Users need to be able to accomplish the same tasks with all of our supported browsers, but the mechanisms are free to change based on browser features. 

## Markup

Markup defines the structure and outline of a document. Markup is not intended to define the look and feel of the content on the page beyond rudimentary concepts such as headers, paragraphs, and lists. The presentation attributes of HTML have all been deprecated and style should be contained in style sheets.

* Defines content
* Establishes Information Hierarchy
* Adds semantic context to content

### HTML5

HTML5 is a new version of HTML and XHTML. The HTML5 draft specification defines a single language that can be written in HTML and XML. It attempts to solve issues found in previous iterations of HTML and addresses the needs of web applications, an area previously not adequately covered by HTML4. [source](http://www.w3.org/TR/html5-diff/#history).

We use the HTML5 Doctype and will use HTML5 features when appropriate.

?? We will test our markup against the W3C validator, to ensure that the markup is well formed. 100% valid code is not a goal, but validation certainly helps to write more maintainable sites as well as debugging code. We do not guarantee code is 100% valid, but instead assures the cross-browser experience is fairly consistent. ??

#### Use Attribute Selectors

[Attribute Selectors](http://www.w3.org/TR/css3-selectors/#selectors) are magic.

### General Markup Guidelines

The following are general guidelines for structuring your HTML markup. Authors are reminded to always use markup which represents the semantics of the content in the document being created.

* Use actual `p` elements for paragraph delimiters as opposed to multiple `br` tags.
* Items in list form should always be housed in a `ul`, `ol`, or `dl`, never a set of `div`s or `p`s.
* Use label fields to label each form field. Either wrap the input field with a label tag or use the label's `for` attribute to associate itself with the input field, so users can click the labels.
* NEVER use tables for layout.
* Use [Microformats](http://microformats.org/) and/or [Microdata](http://en.wikipedia.org/wiki/Microdata_(HTML)) where appropriate, specifically hCard and adr.
* Make use of `dl` (definition lists) and `blockquote`, when appropriate.
* Make use of `thead`, `tbody`, and `th` tags (and Scope attribute) when appropriate.
* Table markup with proper syntax (`thead`, `tbody`, `th [scope]`)

```html
<table>
    <thead>
        <tr>
            <th>Table header 0</th>
            <th>Table header 1</th>
            <th>Table header 2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Row header</th>
            <td>Table data 1</td>
            <td>Table data 2</td>
        </tr>
    </tbody>
</table>
```

* ?Always use title-case for headers and titles.? Do not use all caps or all lowercase titles in markup, instead apply the CSS property `text-transform:uppercase/lowercase`.

#### Quoting Attributes

The HTML5 specification defines quotes around attributes values as optional. For consistency with attributes that accept whitespace, all attributes values should be quoted.

```html
<p class="line note" data-attribute="106">This is my paragraph of special text.</p>
```


## Styles

The second component of a web page is the presentation information contained in the Cascading Style Sheet (CSS.) Web browsers successful implementation of CSS has given web authors site-wide control over the look and feel of their web sites.

Just as the information on a web page is semantically described in the HTML Markup, CSS describes all presentation aspects of the page via a description of its visual properties. CSS is powerful in that these properties are mixed and matched via identifiers to control the page's layout and visual characteristics through the layering of style rules (the "cascade").

We use the [.LESS CSS preprocessor](www.dotlesscss.org) to aid our CSS generation.


    .LESS makes it easy to nest selectors that compile into long selectors
        files size bloat
        performance
        maintainability (selector wars!)

        Rule of thumb 
            avoid creating selectors with more than 2 spaces in them
    Get to know CSS Selectors
        * > 
        * + 
        * ~ 
        * []
    Avoid !important
        It is a sign that we have a selector war and other selectors have too high of specificity

    SMACSS, OOCSS
    Embrace CSS3 to progressively enhance styles for newer browsers
    In 2012 we got rid of rounded corners for <IE9 throughout the site.
        We didn't hear any client complaints.
    We aren't all CSS experts, reach out to one of our many knowledgable CSS devs before hacking together a solution in JavaScript.




### Organization

You should include exactly __one__ stylesheet on your page and no more. This base file should then import all dependancies and components. Components and styles for different sections should be contained in their own stylesheet and should not cross-pollinate. The home page styles directory, for example, contains the files 

`homepage.less` `layout.less` `featuredNews.less` `featuredVideo.less` `promoWeblets.less`

`homepage.less` is included on the page and imports the different files for each section like this:

```css
@import '/themes/common/css/minimal';
@import 'layout';
@import 'featuredNews';
@import 'featuredVideo';
@import 'promoWeblets';
```

And that's it. `minimal.less` and the legacy-filled `theme_builder.less` import site chrome like the header, footer, nav, and other junk you don't have to worry about unless you're Obelisk. *One of these files must be included.* The master `themes_common.less` and a sponsor's `theme.less` are magically included in every stylesheet by default and import our [Pattern Library](#pattern-library) components, so you can utilize our global variables and mixins in any LESS file on the site.

### Pattern Library

Our [Pattern Library](http://localhost/wminternal/ui/patternlibrary) is broken up into three pieces, `core`, `components`, and `modules`.

__*Core*__ contains base styles for our site's body, header, footer, and navigation. It also handles a lot of the global responsive bits. Anything between the nav and the footer should not use anything from core.

__*Components*__ describe define things like forms, buttons, tables, sprites, grids, etc, that are used frequently across the site. All of these components are organized into mixins and included for you so you can call them at any time, but some have special instructions. Check the documentation.

__*Modules*__ are more specialized components like modals, tab panels, and progress bars. Since these components are used infrequently and tend to be more customizable they live here.

There is one more piece of the Pattern Library that contains legacy/deprecated components, and you should stay away from it unless you're Obelisk.

### Theme Variables

Use common variables for things like colors and gutters. This way clients can override variables with their branding colors and fonts if need be. All global variables can all be located in `themes_common.less`, but the ones we recommend using are in the Pattern Library.

Here's a good example of how to use theme variables wisely.

```css
.class {
    color: @themePrimary;
    background: @matteShading;
    border: 1px solid @borderShade;
}
```

### Style Guide

We want to make sure our LESS looks familiar to everyone editing it. That's why these guidelines are not simply suggestions, but the *de facto* style you should be coding. The Front-End Community of Practice decides on the style based on our standards. Don't get busted by the COPs.

#### Indentation

Indent four spaces, no tabs

#### Selectors

Class and ID names should be `camelCase`

```css
.className {...}
#theIdName {...}
```

State rules added via Javascript should us hyphens between words

```css
.is-visible {...}
```

HTML elements should be lowercase, of course. That said, avoid styling naked tags.

```css
div, span {...}
```

Put a space between selector and opening bracket and put the closing bracket on a separate, non-indented line

```css
.class {
    color: #000;
}
```

Return after each closing bracket

```css
.class1 {
    color: #000;
}

.class1 {
    color: #000;
}
```

Put multiple selectors on separate lines, separated by commas

```css
.class1,
.class2,
.class3,
.class4 {
    color: #000;
}
```

#### Properties

Make sure there is a space between property and value, each property is indented one level, and end each line with a semi-colon `;`

```css
div {
    color: #000;
    padding: 16px;
    height: 100px;
}
```

Specify units (`px, em, %`) unless it is `0` (then omit the units).

```css
padding: 10px 0 15px;
```

Specify HEX values for colors

```
#000
#FF0138
```

Use LESS functions to adjust hue, saturation, lightness, or transparency

```css
color: fade(#000, 50%);
background: darken(#FFF, 50%);
```

Strings must use single-quotes

```css
a:after {
    content: 'pizza';
}
```

CSS3 properties that support layering should be on separate lines, with the semi-colon on the last line

```css
.class {
    box-shadow:
        0 2px 4px #000,
        0 4px 8px #333;
    color: #000;
}
```

#### Variables

In LESS, variables are declared with `@` preceding the name.

```css
@themeColor: #F00;
```

Any color or layout value used more than once should be a variable

```css
@alertColor: #0F0;
@columnWidth: 80px;
```

__Any variable that is available for client customization *must be declared globally* in themes_common__

#### Mixins

Always add parenthesis to declare mixins. Mixins should be styled like selectors. Do not put a space after the mixin name.

```css
.mixin() {
    color: #F00;
}
```

Include mixins first when declaring mixins inside selectors

```css
div {
    .mixin();
    padding: 16px;
}
```

Define mixins at the bottom of the document or in their own separate file via `@import`

```css
div {
    .mixin();
}
...
.mixin() {
    color: #F00;
}
```

Do not put spaces around parameters

```css
.mixin(@color) {
    background: @color;
}
```

Specify default parameters whenever possible.

```css
.mixin(@color: #F00) {
    background: @color;
}
```

When calling mixins, you do not need to specify the parameter name, just the value

```css
.class {
    .mixin(#F00, 100px);
}
```

Multiple parameters with values should be separated on their own lines.

```css
.mixin(
    @color: #F00,
    @width: 100px
    ) {
    background: @color;
    width: @width;
}
```

Guarded mixins with boolean values that are true do not need `= true`

```css
.mixin(@boolean) when (@boolean) {...}
```

Use the `when not` keyword when specifying falsey booleans

```css
.mixin(@boolean) when not (@boolean) {...}
```

Use bundles to contain similar mixins

```css
#gradient {
    .linear() {...}
    .radial() {...}
}
```

Call the bundles with the greater than `>` character

```css
div {
    #gradient > .linear(...);
}
```

__Make sure you're not redefining mixins that exist globally! Check components > common.less__



### Stay Rad

* Don't use inline styles
* Use semantically descriptive class names (`.orangeButton` is terrible)
* Never nest deeper than three levels (The Inception Rule)
* Never nest an ID within and ID
* Avoid name spacing with element + class names unless it's a state rule (i.e., `div.class`)
* Don't repeat yourself (DRY), abstract patterns into reusable mixins and variables
* Use shorthand whenever possible (`margin` instead of `margin-top` + `margin-right`, etc.)
* group properties together (layout, fonts, background, prefixes, hacks)
* Use the star-hack `*property: value;` to easily target IE7
* When importing LESS files, do not put .less extension (`@import 'component'`)
* If your LESS file is over 100 lines it's time to start breaking things apart
* If you're doing something dumb, document why with a `//` comment





## Javascript

JavaScript can be added to augment existing functionality on a page. JavaScript is a last resort. Do not use JavaScript to style the page. 

Do not rely on JavaScript to render the initial page contents. [Read about Twitter's dropping hash urls](https://blog.twitter.com/2012/improving-performance-twittercom)

### Formatting (#javascript-formatting)

#### Indentation

Indent with a tab, do not mix spaces and tabs.

#### Statement Termination

Always include semi-colons, don't rely on Javscript's [automatic semi-colon insertion](http://bclary.com/2004/11/07/#a-7.9.1) rules.

#### Line Length

Limit line length to 80 characters, for lines greater than 80 characters break after an operator and double indent the next line unless doing an assignment.

```javascript
// double indent wrapped lines
if (isLongPoorlyNamedFunctionReturningBoolean() && !isGiraffe() && !isFishy() ||
        isBriney() && isFishy()) {
    fooWithFeeling();
}

// exception: when doing assignment
var UI_MESSAGE = stringBegin + option[1] + option[3] + stringMiddle +
                 stringEnder;
```

#### Naming

Use camel case for variables and regular functions, pascal case for constructors and all caps to indicate a constant. Variables and constructors should begin with a noun and regular functions should begin with a verb.

```javascript
function MoneyMaker(amount) {
    var UI_UNIT = 'dollars';

    this.money = amount || 1;
    this.addMoney = function (amount) {
        return this.money += amount;
    };
}

var piggyBank = new MoneyMaker(1000);
piggyBank.addMoney(1);
```

#### Equality Operators

Use `===` and `!==` instead of `==` and `!=` to avoid type coercion.

```javascript
var same = (a === b);
```

#### Ternary Operator

Use ternary operator to conditionally assign a value, not as a shortcut for an if statement.

```javascript
var val = (a > b) ? b : a;
```

#### Compound Statements

Opening braces should be at the end of the line that begins the compound statement. Braces should be used around all statements even one-liners. Variables should not be declared in the initialization section of a for statement.

```javascript
// put opening brace on same line as statement
if (true) {
    // ...
}

while (condition) {
    // ..
}

do {
    // ...
} while (value);

switch (true) {
    case 1:
        /* fall through */
    case 2:
        fn();
        break;
    default:
        return undefined;
}

try {
    // ...
} catch (e) {
    // ...
} finally {
    // ...
}


// define loop variables at the beginning of scope
var i,
    len;

for (i = 0, len = 10; i < 10; i++) {
    // ...
}

var prop;

for (prop in someObject) {
    // ...
}
```

#### White Space

Blank lines improve readability by setting off sections of code that are logically related.

It's a good idea to add blank lines:

* between methods
* between local variables and the next statement
* before comments
* before control statements e.g. `if`, `for`, `while` etc.
* between logical sections inside a method to improve readability

```javascript
(function() {
    'use strict';
    var a,
        b = 10;

    function theFunction() {

        if (true) {

            if (!!0) {

                while (--b) {
                    a = b;

                    // HACK: nonsense
                    b = a;
                }
            }
        }
    }

    function aFunction() {
        // ...
    }
})();
```

### JsHint

We use jsHint to enforce a consistent coding style and to help prevent JavaScript errors.
[Using JsHint inside Visual Studio - the basics](http://blog.stevensanderson.com/2012/08/17/using-jshint-inside-visual-studio-the-basics/)

make sure your code passes [JsHint](http://jshint.com/). If you must include code that doesn't pass add a [directive](http://jshint.com/docs/#directives) to make it pass.

```javascript
/*global jQuery*/ // jshint option: to declare jQuery a valid global
(function ($) {
    'use strict';
    var module = {
        prop: false
    };

    function toggleProp() {
        /*jshint validthis: true*/ // jshint option: ignore 'possible strict mode violation'
        this.prop = !this.prop;
    }

    toggleProp.apply(module);
})(jQuery);
```

### Strict Mode

Always use [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode).

```javascript
(function () {
    'use strict'; // turn on strict mode

    // do something

})();
```


### Declaring variables

Declare variables at the beginning of their scope in a single statement. Declaring variables in a single statement performs faster than spreading them around, minifies better, makes them easier to find, and reduces [hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting) errors.

```javascript
(function (){
    'use strict';
    // declare module wide variables at the beginning of module scope in a single statement
    var moduleA = 4,
        moduleB = 5;

    function aFunc (msg) {
        // declare local variables at the beginning of function scope
        var standardGreeting = 'Hello';

        if (!!msg) {
            return standardGreeting + ' A: ' + moduleA;
        } else {
            return msg + 'B: ' + moduleB;
        }
    }

    alert(aFunc()); // Hello A: 4
    alert(aFunc('ohai!')); // ohai! B: 5
})();
```


### Unit Tests

Automated testing is not optional. You will have to change the way you write JavaScript to make it testable.

        QUnit
            Some semantics:
            Unit Tests
                self contained
                targetted
                any markup to test against is embedded in test js file
                not dependent on CSS files
                Will be included in CI build
            Integration Tests
                may depend on production markup created by executing controls
        build appTarget qunit
            generates qunit.html file to run tests

JavaScript should be created using Test Driven Development. We use QUnit as our testing framework. We have had a few iterations of unit test patterns. You will see these in the codebase. Model your new tests off of the Health Concierge project.

Test files should be located at `\unittests\web\[ApplicationName]\`. The paths to individual files within `\unittests\web\[ApplicationName]\` should match the locations of the production files under `\production\web\[ApplicaitonName]\`.

#### Command-line QUnit test runner coming soon
    You will soon be able to execute `> build myapp qunit` to create a qunit html file and execute your application's javascript tests from the command line and a CI build.

### JavaScript Architecture


### jQuery usage

Do not default to using jQuery for everything. It is a large library that includes much more functionality than is typically needed. 

jQuery promotes some no-so-great practices. These should be avoided:
* `$(document).ready(function(){...})` instead just put your scripts at the bottom of the markup and don't depend on CSS.
* setting style with jQuery
    These are just as bad as setting inline styles in HTML:
    * `$('.item').hide('slow')` - this effectively sets an inline style of `display:none`
    * `$('.item').show('fast')`
    * `$('.item').toggle()`
    * `$('.item').css({color: 'red'})` - this effectively sets an inline style of `color:red`

    prefer
    * `$('.item').removeClass('is-visible')`
    * `$('.item').addClass('is-visible')`
    * `$('.item').toggleClass('is-visible')`
    * `$('.item').addClass('is-error')`
    And ___move styling and animation decisions to CSS, where they belong___.

    [Updating styles via class name rather than setting styles from script is also faster](http://jsperf.com/change-class-vs-inline-styling/5)

### Delegated Event Handlers



### Write Modular Code

Prefer small, decoupled, independent, and cohesive modules of functionality over big architectures.

Why modules?
    
> Now that we're delivering page content faster, the next step is to ensure that our JavaScript is loaded and the application is interactive as soon as possible. To do that, we need to minimize the amount of JavaScript we use: smaller payload over the wire, fewer lines of code to parse, faster to execute. To make sure we only download the JavaScript necessary for the page to work, we needed to get a firm grip on our dependencies.
>
> To do this, we opted to arrange all our code as CommonJS modules, delivered via AMD. This means that each piece of our code explicitly declares what it needs to execute which, firstly, is a win for developer productivity. When working on any one module, we can easily understand what dependencies it relies on, rather than the typical browser JavaScript situation in which code depends on an implicit load order and globally accessible properties.
    
Define all dependencies, do not access them from global scope within a module. This includes objects like `window` and `document` as well as other custom or third-party scripts. This improves performance as there is one less level to walk in the scope-chain in order to find an object definition. More importantly, it improves maintainability by documenting dependencies.

#### Private Module

Use this pattern when:
	* you don't need to export a JavaScript API to another JavaScript module/file
	* your unit tests aren't dependent on re-running the IFFE

If you don't need to export or import any functionality wrap it in an [Immediately-Invoked Function Expression](http://benalman.com/news/2010/11/immediately-invoked-function-expression/) to prevent variable name collisions and keep the global namespace clean. 

```javascript
(function (document) {
    'use strict';
	
    var privateVar = true,
        danceparty = document.getElementById('danceparty');

    if (privateVar) {
        danceparty.className = 'dance-time';
    }
})(document);
```

#### Module with Public API

Use this pattern if you must create an API that other JavaScript code will call into. 

We use the AMD pattern for modularization. 

We use a custom-built implementation of the AMD loader that reinitializes all module constructors for each QUnit test - this enables us to isolate test runs and prevent state leakage between multiple QUnit tests.

```javascript
// explicitly assign your module to window property
define("InterstitialModal", ["minQ", "InterstitialModal"], function($, dependency2) {
    'use strict';

    // setup
    var privateCount = 0

    return {
        count: function () {
            return privateCount;
        },

        increment: function () {
            return ++privateCount;
        },

        decrement: function () {
            return --privateCount;
        }
    }
});

```

NOTE: we used to use the revealing module pattern for this. It was not as testable as AMD modules due to the non-reinitialized state that can be captured in the IFFE and cause conflicts between unit test runs. The AMD pattern also simplifies namespace creation, provides better documentation, and reduces file-include-order dependencies.


## Responsive Design

There is no mobile web, there is no `http://m.webmdhealth.com` site, all functionality should be available to all of our supported browsers/devices provided by the same 

HTML/CSS/JavaScript.

For browsers that support CSS media queries, our pages should render and look/work well at any resolution from 320px to 997px+.

We do not have site-wide breakpoints for "mobile" or "tablet" or "desktop" - let the content and layout on individual pages drive the layout decisions.

### A Lot of Media Queries?

If you find yourself needing a lot of media queries in your layout's CSS, it might be a sign that your layout is too brittle. 


## Accessibility

[Wiki Documentation](http://foswiki.dev.webmd.com/bin/view.pl/Main/AccessibilityGuidelines)

Keyboard - some people are unable to use, or prefer not to use the mouse or trackpad. Our site needs to be fully functional with just a screen and keyboard.

Screenreader

* Offscreen text is a last resort for accessibility. Ask yourself, are you giving the screenreader context that everyone should get?

### VPATs

[VPATs for our products](http://sharepoint.webmd.net/privateportals/HealthServices/ProjectMgmt/ets/Shared%20Documents/Forms/AllItems.aspx?RootFolder=http%3a%2f%2fsharepoint%2ewebmd%2enet%2fprivateportals%2fHealthServices%2fProjectMgmt%2fets%2fShared%20Documents%2fVPATs&FolderCTID=0x0120007D8B64EDF19CCE48B01E97AD2B0B3CAE)

This is the list of tests we need to verify to report that we are technically compliant with 508C. ___New applications MUST conform to these rules.___

* (a) A text equivalent for every non-text element shall be provided (e.g., via "alt", "longdesc", or in element content).
___this is not needed if the non-text element is just used for styling and has no semantic value___
* (b) Equivalent alternatives for any multimedia presentation shall be synchronized with the presentation.
* (c) Web pages shall be designed so that all information conveyed with color is also available without color, for example from context or markup.
* (d) Documents shall be organized so they are readable without requiring an associated style sheet.    
___We interpret this to just apply to documents that are not web pages___
* (e) Redundant text links shall be provided for each active region of a server-side image map.
___Just avoid server-side image maps altogether___
* (f) Client-side image maps shall be provided instead of server-side image maps except where the regions cannot be defined with an available geometric shape.
* (g) Row and column headers shall be identified for data tables.
* (h) Markup shall be used to associate data cells and header cells for data tables that have two or more logical levels of row or column headers.
* (i) Frames shall be titled with text that facilitates frame identification and navigation.
* (j) Pages shall be designed to avoid causing the screen to flicker with a frequency greater than 2 Hz and lower than 55 Hz.
___We've never seen this to be an issue on our site___
* (k) A text-only page, with equivalent information or functionality, shall be provided to make a web site comply with the provisions of this part, when compliance 

cannot be accomplished in any other way. The content of the text-only page shall be updated whenever the primary page changes.
* (l) When pages utilize scripting languages to display content, or to create interface elements, the information provided by the script shall be identified with 

functional text that can be read by Assistive Technology.
* (m) When a web page requires that an applet, plug-in or other application be present on the client system to interpret page content, the page must provide a link to 

a plug-in or applet that complies with §1194.21(a) through (l).
___Just avoid applets and plugins (no more Flash)___
* (n) When electronic forms are designed to be completed on-line, the form shall allow people using Assistive Technology to access the information, field elements, and 

functionality required for completion and submission of the form, including all directions and cues.
* (o) A method shall be provided that permits users to skip repetitive navigation links.
* (p) When a timed response is required, the user shall be alerted and given sufficient time to indicate more time is required.




## Performance

### Optimize Images

Use [tinypng](tinypng.com) or similar tool to compress `png` files and speed up downloads.

### Limit # of http requests

* Combine multiple icons/graphics into one download with [CSS sprites](http://css-tricks.com/css-sprites/).
* Combine CSS requests using .LESS includes
* Combine JavaScript files using *.manifest.js
* Embed small images into css files using data uri's (beware of IE7 mixed-security errors)
* For pages that are typically only requested once per session (verify with actual data):
    * Consider embedding page-specific JavaScript files in HTML response
    * Consider embedding page-specific CSS files in HTML response

### Maximize cachability

Referenced CSS, JavaScript and image files will automatically contain caching headers.

Can your AJAX request be cached client-side (with HTTP caching)? If so, add the proper HTTP headers server-side.

### Include Order

CSS in the `head`, scripts at the bottom of the `body`.

### Do not depend on JavaScript for initial Render

The following is from Twitter(https://blog.twitter.com/2012/improving-performance-twittercom)

> Looking at the components that make up this measurement, we discovered that the raw parsing and execution of JavaScript caused massive outliers in perceived rendering speed. In our fully client-side architecture, you don't see anything until our JavaScript is downloaded and executed. The problem is further exacerbated if you do not have a high-specification machine or if you’re running an older browser. The bottom line is that a client-side architecture leads to slower performance because most of the code is being executed on our users’ machines rather than our own.
>
> There are a variety of options for improving the performance of our JavaScript, but we wanted to do even better. We took the execution of JavaScript completely out of our render path. By rendering our page content on the server and deferring all JavaScript execution until well after that content has been rendered, we’ve dropped the time to first Tweet to one-fifth of what it was.


## Working with the Design Team

do not expect (or wait for) pixel-perfect design
do not expect the site to look the same on different browsers
    it should look consistent within any single browser though.
    user's should be able to accomplish everything they need to with whatever supported browser they are using.
question fidelity of designs
don't code exactly to mockups. look for opportunities to leverage standard styles
collaborate

## Tools

* Web Essentials Visual Studio Plugin - provides enhanced .LESS and JavaScript code editor support
* [DOM Monster](http://mir.aculo.us/dom-monster/) - analyze markup quality
* [WebPageTest](http://www.webpagetest.org)
* [Fiddler2](http://fiddler2.com/) - web debugging proxy. Shape local HTTP traffic to more closely match site usage in production environment.
* f12 (browser dev tools)

## References

This guide borrows heavily from around the net and [Nicholas Zakas](https://www.twitter.com/slicknet)' book [Maintainable Javascript]

(http://www.amazon.com/Maintainable-JavaScript-ebook/dp/B0082CXEB0).

http://taitems.github.io/Front-End-Development-Guidelines/
http://isobar-idev.github.io/code-standards/
http://www.mediawiki.org/wiki/Front-End_Coding_Standards

https://github.com/bitmap/less-style
https://github.com/objectfoo/js-style/blob/master/guide.md

<!--

## TODO

CSS Specificity Wars (http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html)

Developer settings
    JsHint
    .LESS tools
    VS2012 text editor settings


IE8 represents ~40% of our traffic today.

General
    Pattern Library
    Consistency
    Hacks will break, prefer progressive enhancement
    Browsers are different, adopt a development stratagy to embrace this and not try to patch over it

Use the right technology for the job
    Animations belong in CSS
        Transitions and animations
HTML
    Avoid adding tags just to style
    custom attributes
        data-
        can be styled "[data-expanded=true]" works in all of our supported browsers
        all lowercase

JavaScript
    Javascript should be a last resort.
    Style Guide

    For new pages, include script references at the bottom of the markup
        improves performance - *performance link*
        simplifies code - no longer need $(document).ready event in most cases
    Understand scoping and closures
    Understand browser dom api
    Use JS to manage state, not style
        
    jsHint
        Shared WHS settings
    Modular
        AMD
        
    Do not pollute the global namespace
        Global objects are bad, avoid them.
    Prefer scripts that do not expose any global api
        When that isn't possible, create as small of an API as possible
        Changing an existing JavaScript API is expensive
        *JS maintainance is hard, we don't have a compiler to enforce correctness like C#
    Prefer small decoupled modules to large monolithic applications
    Do not reach for a third-party library as a first solution
    Do not use jQuery for everything
        Our proliferation of dependencies on jQuery have prevented us from updating versions since

    
Progressive Enhancement

	Nice-to-have features can be considered progressive enhancements and excluded from less capable browsers. 
-->

