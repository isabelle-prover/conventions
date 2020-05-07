---
title: Theory Documentation
---

Documentation is key for the long-term value of a development.
Without documentation, once a project loses its original maintainer(s), the project virtually dies due to inaccessibility.
In general, all comments must be written using Isabelle markdown (see [Isabelle reference manual](https://isabelle.in.tum.de/documentation.html)).

## References
Every project comes with a `.bib` containing the references that were used when developing the theories.
This file should be placed in the folder `document`.
Those references are then inserted at the appropriate places when documenting the theories (using the antiquation `@cite`).

## Header Documentation
Every file starts with:
- a comment declaring the author(s) of the file if there is more than one person working on the project
- the list of imports
- a file comment containing the general documentation
in this order.
Original authors should mark themselves with the `✐‹creator ...›` tag.
Additional (later) contributors should use the `✐‹contributor ...›` tag.

The file comment consists of the following sections:
- the title of the file followed by a summary of the content of the file
- main definitions (optional; can be covered in the summary)
- main theorems (optional; can be covered in the summary)
- notations (if notation is introduced)
- fact collections and bundles (if relevant fact collections or bundles are introduced)
- implementation notes (optional; description of important design decisions or interface features, including use of type classes and simp canonical form for new definitions)
- references (references to textbooks, papers, or Wikipedia pages)
- tags (a list of keywords that could be useful for search)

The following is an example of a file header:
```isabelle
✐‹creator "Kevin Kappelmann"›
✐‹contributor "Simon Wimmer"›
chapter ‹Continued Fractions›
theory Scratch
  imports HOL.Archimedean_Field "HOL-Library.Stream"
begin

paragraph ‹Summary›
text ‹We define generalised, simple, and regular continued fractions and
functions to evaluate their convergents. We follow the naming conventions from
@{cite wikicontinuedfractions} and @{cite wall2018analytic}.›

paragraph ‹Main Definitions›
text ‹
▪ Generalised continued fractions (gcfs)
▪ Simple continued fractions (scfs)
▪ (Regular) continued fractions ((r)cfs)
▪ Computation of convergents using the recurrence relation in
@{const convergents}.
▪ Computation of convergents by directly evaluating the fraction described by
the gcf in @{const convergents'}.
›

paragraph ‹Notations›
text ‹
▪ @{term "⌊x⌋"} is the floor for any ‹x› of an integral domain.
›

paragraph ‹Fact Collections›
text ‹
▪ ‹gcf_simps› contains simplification rules for gcfs
›

paragraph ‹Implementation Notes›
text ‹
▪ The most commonly used kind of continued fractions in the literature are
regular continued fractions. We hence just call them @{const continued_fractions}
in the library.
▪ We use streams from @{theory "HOL-Library.Stream"} to encode infinite sequences.
›

paragraph ‹Tags›
text ‹numerics, number theory, approximations, fractions›
```

## Theory-Body Documentation and Sectioning
Every theory should result in a human-readable file. For this, we document and section theories.
Regarding the former, all definitions and major theorems are accompanied by a text block (or comment).
- For definitions, the block should convey the mathematical meaning and motivation.
For clarity, minor technicalities need not be mentioned (e.g. divisions by zero)
- For major theorems, the block should address the importance and re-usability of the theorem.
- When referring to constants (`@const`), terms (`@term`), types (`@typ`), theorems (`@thm`) etc., antiquotations must be used. In particular, for constants, `@const` must be preferred over `@term`.

Moreover, the theory should be sectioned using the `chapter`, `section`, `subsection`, `paragraph`, etc. commands.
If a new section starts at the start of a theory, the corresponding sectioning command should go before the theory header.
Explanatory text that motivates and guides the user through the theory development should be added. 

Example:
```isabelle
paragraph ‹Generalised Continued Fractions›

text ‹
A ∗‹generalised continued fraction› (gcf) is a potentially infinite expression
of the form

\begin{equation*}
h+\cfrac{a_0}
  {b_0+\cfrac{a_1}
    {b_1+\cfrac{a_2}
      {b_2+\cfrac{a_3}
        {b_3+\dotsb}}}}
\end{equation*}
›

(* Above code produces:
                a₀
h + ---------------------------
                  a₁
      b₀ + --------------------
                    a₂
            b₁ + --------------
                        a₃
                  b₂ + --------
                      b₃ + ...
*)

text ‹where ‹h› is called the ∗‹head term› or ∗‹integer part›, the ‹a⇘is⇙› are
called the ∗‹partial numerators› and the ‹b⇘is⇙› the ∗‹partial denominators› of the
gcf. We store the sequence of partial numerators and denominators in a sequence
of @{term generalized_continued_fraction_pairs} ‹s›.
For convenience, one often writes ‹[h; (a⇩0, b⇩0), (a⇩1, b⇩1), (a⇩2, b⇩2), …]›.
›
definition "generalised_continued_fraction ≡ ..."
```


