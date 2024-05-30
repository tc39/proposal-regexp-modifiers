<!--#region:intro-->
# Regular Expression Pattern Modifiers for ECMAScript

<!--#endregion:intro-->

<!--#region:status-->
## Status

**Stage:** 3  
**Champion:** Ron Buckton ([@rbuckton](https://github.com/rbuckton))  

_For detailed status of this proposal see [TODO](#todo), below._  
<!--#endregion:status-->

<!--#region:authors-->
## Authors

* Ron Buckton ([@rbuckton](https://github.com/rbuckton))  
<!--#endregion:authors-->

<!--#region:motivations-->
# Motivations

One common capability amongst the majority of regular expression engines that
is commonly used by parsers, syntax highlighters, and other tools is the capability to
control a subset of regular expression flags such as:

- `i` &mdash; Ignore Case
- `m` &mdash; Multiline
- `s` &mdash; Single-line (a.k.a. "dot all")
- `x` &mdash; Extended mode (see https://github.com/rbuckton/proposal-regexp-x-mode)

Modifiers are especially helpful when regular expressions are defined in a context
where executable code cannot be evaluated, such as a JSON configuration file or 
TextMate tmLanguage grammar file.

As part of this proposal, we will investigate each existing (and future-proposed) RegExp flag
to determine whether they are feasible to used as modifiers.

<!--#endregion:motivations-->

<!--#region:prior-art-->
# Prior Art 

* [Perl](https://rbuckton.github.io/regexp-features/engines/perl.html#feature-modifiers)  
* [PCRE](https://rbuckton.github.io/regexp-features/engines/pcre.html#feature-modifiers)  
* [Boost.Regex](https://rbuckton.github.io/regexp-features/engines/boost.regex.html#feature-modifiers)  
* [.NET](https://rbuckton.github.io/regexp-features/engines/dotnet.html#feature-modifiers)  
* [Oniguruma](https://rbuckton.github.io/regexp-features/engines/oniguruma.html#feature-modifiers)  
* [Hyperscan](https://rbuckton.github.io/regexp-features/engines/hyperscan.html#feature-modifiers)  
* [ICU](https://rbuckton.github.io/regexp-features/engines/icu.html#feature-modifiers)  
* [Glib/GRegex](https://rbuckton.github.io/regexp-features/engines/glib-gregex.html#feature-modifiers)  

See https://rbuckton.github.io/regexp-features/features/modifiers.html for additional information.
<!--#endregion:prior-art-->

<!--#region:syntax-->
# Syntax

Modifiers allow you to change the currently active RegExp flags within a subexpression.

- `(?imsx-imsx:subexpression)` &mdash; Sets or unsets (using `-`) the specified RegExp flags for the subexpression.
- ~~`(?imsx-imsx)` &mdash; Sets or unsets (using `-`) the specified RegExp flags starting at the current position until the next closing `)` or the end of the pattern.~~

> NOTE: Certain flags cannot be modified mid-expression. These currently include `g` (global), `y` (sticky), `u` (unicode), and `d` (hasIndices).

> NOTE: The actual supported flags will be determined on a case-by-case basis. See [#1](https://github.com/tc39/proposal-regexp-modifiers/issues/1).

> NOTE: This has no conflicts with existing syntax, as ECMAScript currently produces an error for this syntax in both `u` and non-`u` modes.

> NOTE: The "self-bounded" form (`(?imsx-imsx:subexpression)`) advanced to Stage 2 on December 15th, 2021.

> NOTE: The "unbounded" form (`(?imsx-imsx)`) is no longer being considered as part of this proposal as of December 15th, 2021.

<!--#endregion:syntax-->

<!--#region:semantics-->
<!-- # Semantics -->


<!--#endregion:semantics-->

<!--#region:examples-->
# Examples

```js
const re1 = /^[a-z](?-i:[a-z])$/i;
re1.test("ab"); // true
re1.test("Ab"); // true
re1.test("aB"); // false

const re2 = /^(?i:[a-z])[a-z]$/;
re2.test("ab"); // true
re2.test("Ab"); // true
re2.test("aB"); // false
```

<!--#endregion:examples-->

<!--#region:api-->
<!--
# API

> TODO: Provide description of High-level API.
-->
<!--#endregion:api-->

<!--#region:grammar-->
<!-- # Grammar

```grammarkdown
``` -->
<!--#endregion:grammar-->

<!--#region:references-->
<!-- # References

> TODO: Provide links to other specifications, etc.

* [Title](url)   -->
<!--#endregion:references-->

# History

- October 27th, 2021 &mdash; Proposed for Stage 1 ([slides](https://1drv.ms/p/s!AjgWTO11Fk-Tkfl7c6yR-2P8T4gn0w?e=cvaUL2))
  - Outcome: Advanced to Stage 1
- December 15th, 2021 &mdash; Proposed for Stage 2 ([slides](https://1drv.ms/p/s!AjgWTO11Fk-Tkfs3yIyrh3hZ2k6PCQ?e=Yodx4H))
  - Outcome: Advanced to Stage 2 with "self-bounded" form only ("unbounded" form did not advance).
  - Stage 2 Reviewers: Richard Gibson, Waldemar Horwat
- June 7th, 2022 &mdash; Proposed for Stage 3 ([slides](https://1drv.ms/p/s!AjgWTO11Fk-Tkf5daRnRsxu8BY5Nsg?e=UKVf8W))
  - Outcome: [Advanced to Stage 3](https://github.com/tc39/notes/blob/31edb829db604fdb0255b21238b20898b66cee41/meetings/2022-06/jun-07.md)

<!--#region:todo-->
# TODO

The following is a high-level list of tasks to progress through each stage of the [TC39 proposal process](https://tc39.github.io/process-document/):

### Stage 1 Entrance Criteria

* [x] Identified a "[champion][Champion]" who will advance the addition.  
* [x] [Prose][Prose] outlining the problem or need and the general shape of a solution.  
* [x] Illustrative [examples][Examples] of usage.  
* [ ] ~~High-level [API][API].~~  

### Stage 2 Entrance Criteria

* [x] [Initial specification text][Specification].  
* [ ] ~~[Transpiler support][Transpiler] (_Optional_)~~.  

### Stage 3 Entrance Criteria

* [x] [Complete specification text][Specification].  
* [x] Designated reviewers have [signed off][Stage3ReviewerSignOff] on the current spec text (1 of 2).  
* [x] The ECMAScript editor has [signed off][Stage3EditorSignOff] on the current spec text.  

### Stage 4 Entrance Criteria

* [ ] [Test262](https://github.com/tc39/test262) acceptance tests have been written for mainline usage scenarios and [merged][Test262PullRequest].  
  * [x] written  
  * [ ] merged  
* [ ] Two compatible implementations which pass the acceptance tests:  
  * [X] [V8][Implementation1] - Shipping in [Chrome 125](https://developer.chrome.com/release-notes/125)/Edge 125
  * [ ] [SpiderMonkey][Implementation2] - In Progress
  * [ ] JSC  
  * [ ] [Engine262](https://github.com/engine262/engine262/pull/229)  
* [x] A [pull request][Ecma262PullRequest] has been sent to tc39/ecma262 with the integrated spec text.  
* [ ] The ECMAScript editor has signed off on the [pull request][Ecma262PullRequest].  
  * [x] [Kevin Gibbons](https://github.com/tc39/ecma262/pull/3221#pullrequestreview-1735554031)  
  * [ ] [Michael Ficarra](https://github.com/tc39/ecma262/pull/3221#pullrequestreview-1784954743)  
<!--#endregion:todo-->

<!-- The following links are used throughout the README: -->

[Process]: https://tc39.es/process-document/
[Proposals]: https://github.com/tc39/proposals/
[Grammarkdown]: http://github.com/rbuckton/grammarkdown#readme
[Champion]: #status
[Prose]: #motivations
[Examples]: #examples
[API]: #api
[Specification]: https://rbuckton.github.io/proposal-regexp-modifiers

[Transpiler]: #todo
[Stage3ReviewerSignOff]: #todo
[Stage3EditorSignOff]: #todo
[Test262PullRequest]: https://github.com/tc39/test262/pull/3960
[Implementation1]: https://bugs.chromium.org/p/v8/issues/detail?id=12956
[Implementation2]: https://bugzilla.mozilla.org/show_bug.cgi?id=1899813
[Ecma262PullRequest]: https://github.com/tc39/ecma262/pull/3221
