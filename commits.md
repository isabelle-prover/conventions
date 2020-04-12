# Isabelle Commit Guidelines #
These conventions are adapted from the
[lean commit conventions](https://github.com/leanprover-community/lean/blob/master/doc/commit_convention.md).

We are using the following convention for writing git-commit messages.
It is based on the one from AngularJS project([doc][angularjs-doc],
[commits][angularjs-git]).

[angularjs-git]: https://github.com/angular/angular.js/commits/master
[angularjs-doc]: https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#

## Format of the commit message

    <type>(<scope>): <subject>
    <NEWLINE>
    <body>
    <NEWLINE>
    <footer>

``<type>`` is:

 - feat (feature)
 - fix (bug fix)
 - doc (documentation)
 - style (formatting, missing semicolons, ...)
 - refactor
 - test (when adding missing tests)
 - chore (maintain, ex: travis-ci)
 - perf (performance improvement, optimization, ...)

``<scope>`` is a name of module or a directory which contains changed modules. For instance,
it could be

 - continued_fractions/Convergents
 - continued_fractions/
 - Groups

``<subject>`` has the following constraints:

 - use imperative, present tense: "change" not "changed" nor "changes"
 - do not capitalize the first letter
 - no dot(.) at the end

``<body>`` has the following constraints:

 - just as in ``<subject>``, use imperative, present tense
 - includes motivation for the change and contrasts with previous
   behavior

``<footer>`` is optional and may contain two items:

 - Breaking changes: All breaking changes have to be mentioned in
   footer with the description of the change, justification and
   migration notes
 - Referencing issues: Closed bugs should be listed on a separate line
   in the footer prefixed with "Closes" keyword like this:

    Closes #123, #456

Example
```
fix(continued_fractions): update assumption from convergency theorem

The convergency theorem does not require a field instance but more generally works
on any integral domain.

Closes #1337
```
