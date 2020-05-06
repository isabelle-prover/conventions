---
title: Commits
---

These conventions are adapted from the
[Lean prover commit conventions](https://github.com/leanprover-community/lean/blob/master/doc/commit_convention.md)
to fit Isabelle conventions.

## Format of the commit message

    <type>(<scope>) <subject>
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

``<scope>`` is a name of theory or a directory which contains changed files. For instance,
it could be

 - continued_fractions/Convergents
 - continued_fractions/
 - Groups

``<subject>`` has the following constraints:

 - Use imperative, present tense: "change" not "changed" nor "changes"
 - Do not capitalize the first letter
 - No dot(.) at the end

``<body>`` has the following constraints:

 - Just as in ``<subject>``, use imperative, present tense
 - Includes motivation for the change and contrasts with previous
   behavior

``<footer>`` is required in either of the following two situations:

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
