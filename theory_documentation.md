# Theory Documentation

Documentation is key for the long-term value of a development.
Without documentation, once a project loses its original maintainer(s), the project virtually dies due to inaccessibility.
In general, all comments must be written using Isabelle markdown (see [Isabelle reference manual](https://isabelle.in.tum.de/documentation.html)).

## References
Every project comes with a `.bib` containing the references that were used when developing the theories.
This file should be place in the folder `document`.
Those references are then inserted at the appropriate places when documenting the theories.

## Header Documentation
Every file starts with:
- a comment declaring the author(s) of the file if there is more than one person workking on the project
- the list of imports
- a file comment containing the general documentation
in this order.

The file comment consists of the following sections:
- the title of the file followed by a summary of the content of the file
- main definitions (optional; can be covered in the summary)
- main theorems (optional; can be covered in the summary)
- notations (omitted only if no notation is introduced in this file)
- implementation Notes (optional; description of important design decisions or interface features, including use of type classes and simp canonical form for new definitions)
- references (references to textbooks, papers, or Wikipedia pages)
- tags (a list of keywords that could be useful for search)
When referring to constants and theorems, antiquotations must be used.

The following is an example of a file header:
```isabelle
✐‹creator "Kevin Kappelmann"›
chapter ‹Continued Fractions›

theory Scratch
imports Main
begin

paragraph ‹Summary›
text ‹We define generalised, simple, and regular continued fractions and
functions to evaluate their convergents. We follow the naming conventions from
@{cite wikicontinuedfractions} and @{cite wall2018analytic}.›

paragraph ‹Main Definitions›
text ‹
▸ Generalised continued fractions (gcfs)
▸ Simple continued fractions (scfs)
▸ (Regular) continued fractions ((r)cfs)
▸ Computation of convergents using the recurrence relation in
@{term "convergents"}.
▸ Computation of convergents by directly evaluating the fraction described by
the gcf in @{term convergents'}.
›

paragraph ‹Notations›
text ‹
▸ ⌊x⌋ is the floor for any x of an integral domain.
›

paragraph ‹Implementation Notes›
text ‹
▸ The most commonly used kind of continued fractions in the literature are
regular continued fractions. We hence just call them @{term continued_fractions}
in the library.
▸ We use sequences from @{theory Sequences} to encode potentially infinite
streams.
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

Moroever, the theory should be sectioned using the `chapter`, `section`, `subsection`, `paragraph`, etc. commands.
If a new section starts at the start of a theory, the corresponding sectioning command should go before the theory header.
Explanatory text that motivates and guides the user through the theory development should be added. 

Example:
```isabelle
paragraph ‹Generalised Continued Fractions›

text ‹
A ∗‹generalised continued fraction› (gcf) is a potentially infinite expression
of the form
›

text_raw ‹
                                a₀
                h + --------------------------
                                  a₁
                      b₀ + --------------------
                                    a₂
                            b₁ + --------------
                                        a₃
                                  b₂ + --------
                                      b₃ + ...
›

text ‹where ‹h› is called the ∗‹head term› or ∗‹integer part›, the ‹a⇩is› are
called the ∗‹partial numerators› and the ‹b⇩is› the ∗‹partial denominators› of the
gcf. We store the sequence of partial numerators and denominators in a sequence
of @{term generalized_continued_fraction_pairs} ‹s›.
For convenience, one often writes ‹[h; (a₀, b₀), (a₁, b₁), (a₂, b₂),...]›.
›
definition "generalised_continued_fraction ≡ ..."
```


