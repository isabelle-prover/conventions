# Isabelle Guidelines for Notation #

- Notation can be introduced in Isabelle for both types and terms. 
Mixfix notation can be defined on the spot once they are defined, later with an explicit notation (`type_notation`, `notation`), or locally in an Isar proof (`write`).
This is documented in [isar-ref](https://isabelle.in.tum.de/dist/Isabelle2020/doc/isar-ref.pdf) §8.2 §8.3.

- Assigning correct priorities in mixfix declarations is crucial for avoiding syntactic ambiguities.
Prefer to use templates (like `infix`, `infixl`, `infixr` for binary operators)!

- Use print modes (documented in [isar-ref](https://isabelle.in.tum.de/dist/Isabelle2020/doc/isar-ref.pdf) §8.1.3)
  to define notation that is only meant for convenient `input`, or specific output scenarios (`ASCII`, `latex`).

- When introducing notation that you consider standard or folklore, 
  add a comment with a reference to some textbook, paper or Wikipedia entry to back your claim.
  If you invented a new notation, also add a comment stating that and explaining your choice.

- If you introduce new notation, put it into a bundle!

  - Bundles are documented in [isar-ref](https://isabelle.in.tum.de/dist/Isabelle2020/doc/isar-ref.pdf) §5.3. They can be either activated in a local theory context (`unbundle`), in an Isar proof body (`include`), in a proof refinement (`including`) and in a context specification (`includes`) (notably for `context` and long `theorem` statements).

  - An example can be found in `HOL-Anaylsis.Finite_Cartesian_Product` (`vec_syntax`, `no_vec_syntax`)

  - Only when the notation is specific enough (e.g. by a subscript) to rule out clashes with notation from other theories or future developments the notation can be set on the toplevel.

  - For syntax notations always provide both a bundle that enables (`CONCEPT_syntax`) and a bundle that disables (`no_CONCEPT_syntax`),
  e.g.:

  ```
  bundle timecredits_syntax
  begin
  notation
    timecredit_assn ("$")
  end

  bundle no_timecredits_syntax
  begin
  no_notation
    timecredit_assn ("$")
  end```
