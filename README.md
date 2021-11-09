<!--#region:intro-->
# Regular Expression Pattern Modifiers for ECMAScript

<!--#endregion:intro-->

<!--#region:status-->
## Status

**Stage:** 1  
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

- `(?imsx-imsx)` &mdash; Sets or unsets (using `-`) the specified RegExp flags starting at the current position until the next closing `)` or the end of the pattern.
- `(?imsx-imsx:subexpression)` &mdash; Sets or unsets (using `-`) the specified RegExp flags for the subexpression.

> NOTE: Certain flags cannot be modified mid-expression. These currently include `g` (global), `y` (sticky), and `d` (hasIndices).

> NOTE: The actual supported flags will be determined on a case-by-case basis.

> NOTE: This has no conflicts with existing syntax, as ECMAScript currently produces an error for this syntax in both `u` and non-`u` modes.

<!--#endregion:syntax-->

<!--#region:semantics-->
<!-- # Semantics -->


<!--#endregion:semantics-->

<!--#region:examples-->
# Examples

```js
const re1 = /^(?i)[a-z](?-i)[a-z]$/;
re1.test("ab"); // true
re1.test("Ab"); // true
re1.test("aB"); // false

const re2 = /^(?i:[a-z](?-i:[a-z]))$/;
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

* [ ] [Complete specification text][Specification].  
* [ ] Designated reviewers have [signed off][Stage3ReviewerSignOff] on the current spec text.  
* [ ] The ECMAScript editor has [signed off][Stage3EditorSignOff] on the current spec text.  

### Stage 4 Entrance Criteria

* [ ] [Test262](https://github.com/tc39/test262) acceptance tests have been written for mainline usage scenarios and [merged][Test262PullRequest].  
* [ ] Two compatible implementations which pass the acceptance tests: [\[1\]][Implementation1], [\[2\]][Implementation2].  
* [ ] A [pull request][Ecma262PullRequest] has been sent to tc39/ecma262 with the integrated spec text.  
* [ ] The ECMAScript editor has signed off on the [pull request][Ecma262PullRequest].  
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
[Test262PullRequest]: #todo
[Implementation1]: #todo
[Implementation2]: #todo
[Ecma262PullRequest]: #todo
