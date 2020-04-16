# Isabelle Style Guidelines #
These conventions are adapted from the
[mathlib naming convention](https://github.com/leanprover-community/mathlib/edit/master/docs/contribute/style.md).
to fit for Isabelle conventions.

## General Rules
- Lines must not be longer than 80 (TODO or 100?) characters
- Files must not be longer than 1000.
- Use spaces around infix operators and binders (quantifiers). Put them before a line break rather
than at the beginning of the next line.
- Use two spaces to indent. You can use an extra indent when a long line
forces a break to suggest the break is artificial rather than
structural
- Use a blank line to separate theorems and definitions.
This can be omitted, for example, to group together a number of
short definitions, or to group together a definition and notation.

## Comments
Use comment delimiters `― ‹...›` to provide comments that should not be part
of the general documentation (e.g. TODO notes).

## Theorems and Definitions
The preferred method of stating assumptions is by using explicit `assume` clauses.
You can put multiple short assumptions in one line at a time.
Preferably, you should label facts with semantically meaningful names;
numerals are fine for intermediate facts.
Here are some valid examples:

```isabelle
theorem assumes ha: A and b_of_a: "A ⟹ B" and c_of_b: "B ⟹ C" shows C
oops

theorem assumes A "A ⟹ B" "B ⟹ C" shows C
oops

theorem assumes ha: A
  and b_of_a: "A ⟹ B"
  and c_of_b: "B ⟹ C"
  shows C
oops
```

The `proof`, `next`, and `end` commands are flushed to the left with respect to the current indentation block.
```isabelle
theorem nat_add_comm: "(n :: nat) + m = m + n"
proof (induction n)
  case 0
  then show ?case sorry
next
  case (Suc n)
  then show ?case sorry
qed
```
A "from" / "have" / "using" / "unfolding" / "by" combination can be put on the same line.
You can also put each of these blocks in a new line if the text is too long, but add an extra indentation in that case.
If you have to break within one of the blocks, add another extra indentation.

If the "by" justification takes more than a single line, keep the "by" on the same
line as the "have" and then begin the justification indented on the next line.
If you already had to break due to another block, put the by in a new line too.

When arguments themselves are long enough to require line breaks, use an additional indent for the new lines.

Here is an example:
```isabelle
lemma pigeonhole_infinite: assumes inf_domain: "infinite A"
  and finite_range: "finite (f`A)"
  shows "∃ a ∈ A. infinite {a' ∈ A. f a' = f a}"
using finite_range inf_domain
proof (induction "f`A" arbitrary: A rule: finite_induct)
  case empty
  then show ?case by simp
next
  case (insert b F)
  note IH = ‹⋀A. ⟦F = f`A; infinite A⟧
    ⟹ ∃ a ∈ A. infinite {a' ∈ A. f a' = f a}›
  ― ‹the pre-image of b›
  let ?Pb = "{a ∈ A. f a = b}"
  show ?case
  proof (cases "finite ?Pb")
    case True
    with ‹infinite A› have "infinite (A - ?Pb)" by simp
    moreover have "A - ?Pb = {a ∈ A. f a ≠ b}" by blast
    ultimately have "infinite {a ∈ A. f a ≠ b}" by simp
    from IH[OF _ this] insert.hyps show ?thesis by
      (blast intro: rev_finite_subset)
  next
    case False
    then have "?Pb ≠ {}" by force
    with False show ?thesis by blast
  qed
qed
```

Facts that are crucial to the understand of a step should be put in the from clause of a step.
Auxiliary facts can be put in the trailing using block or passed as tactic arguments.

### Calculations
Use calculation proofs when doing transitive reasoning. Example:
```isabelle
theorem add_comm: "(n :: nat) + m = m + n"
proof (induction n)
  case 0
  show ?case using add_zero zero_add by simp
next
  case (Suc n)
  have "Suc n + m = Suc (n + m)" by (fact succ_add)
  also have "... = Suc (m + n)" using Suc.IH by clarify
  also have "... = Suc m + n" by (fact succ_add[symmetric])
  also have "... = m + Suc n" by (fact succ_add_eq_add_succ)
  finally show ?case by clarify
qed
```

------
Copyright (c) 2020. All rights reserved.
Released under Apache 2.0 license as described in the file LICENSE.

Modified by: Kevin Kappelmann

Original author: Jeremy Avigad
