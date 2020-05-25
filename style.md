---
title: Style
---

## General Rules

### Linting
- Lines must not be longer than 100 symbols (as indicated by the blue line in jEdit).
- Files should not be longer than 1500 lines. While this not a hard limit, exceeding this size limit should be seen as an opportunity to evaluate whether it can be sensibly split up.
- Punctuation (e.g. `,` or `.`) is followed by a space. Use spaces around infix operators and between binders (quantifiers, lambdas). If a line has to be broken it is often sensible to put the linebreaks around operators. For a specific operator, it is up to you whether to put it at the end of the line or the beginning of the new line but you should apply your choice consistently. 
- Use two spaces to indent. You can use an extra indent when a long line forces a break to suggest the break is artificial rather than structural.
- Use one blank line to separate top-level declarations such as theorems, definitions, datatype declarations, etc. You can group together several closely related top-level declarations by omitting the blank line. You may put two blank lines around contexts that are delimited by `begin` and `end`.

### "Do Nots"
- Do not use indexed access to fact collections, e.g. `algebra_simps(3)`.
- In procedural proofs, try to not apply tactics in the middle of a proof if they do not close a goal and do not give raise to a normal form.

## Comments
For comments that are not considered part of the literal document, e.g. TODO notes, use ML-style comments `(* ... *)`.
Comment delimiters `― ‹...›` are to be used for short inline comments, for example to clarify a proof step.
For broader comments, like motiviations for definitions, use the `text` command. See also [Theory Documentation](theory_documentation.md).

## Theorems and Definitions
The preferred method of stating assumptions is by using explicit `assumes` clauses;
however, this is just a suggestion.
You are free to state your assumptions using meta level implication if it reduces textual noise
or simplifies the proof body.

If you use `assumes`, the theorem name must always be followed by a linebreak.
Furthermore, the `show` must be on a separate line from the assumptions.
You can put multiple short assumptions in one line at a time.
Facts should be labelled with semantically meaningful names. If the fact is short enough, however, fact quoting should be preferred instead.
Here is a valid example:
```isabelle
theorem C_if_complicated_B_if_A:
    assumes A and complicated_if_A: "A ⟹  complicated B"
    and c_if_complicated: "complicated B ⟹ C"
    shows C
      using ‹A› oops
```

If you prove involved existential statements or case distinctions you should write down the theorem using `obtains`, e.g:
```isabelle
theorem empty_or_infinite_if_card_eq_0:
  assumes "card A = 0"
  obtains (empty) "A = {}" | (infinite) B where "B ⊆ A" "¬ finite B"
    oops
```

## Proofs
The `proof`, `next`, and `qed` commands are flushed to the left with respect to the current indentation block.
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
A `from` / `have` / `using` / `unfolding` / `by` combination can be put on the same line.
If you need more than two lines, then `from` and `have` should be aligned while the `using` / `unfolding` / `by` commands are aligned to one extra indentation with respect to the `have` block. 
If you have to break within one of the blocks, add another extra indentation.

When arguments themselves are long enough to require line breaks, use an additional indent for the new lines.

Here is an example:
```isabelle
lemma pigeonhole_if_infinite_domain:
  assumes inf_domain: "infinite A"
  and finite_range: "finite (f`A)"
  shows "∃ a ∈ A. infinite {a' ∈ A. f a' = f a}"
using finite_range inf_domain
proof (induction "f`A" arbitrary: A rule: finite_induct)
  case empty
  then show ?case by simp
next
  case (insert b F)
  ― ‹the pre-image of b›
  let ?Pb = "{a ∈ A. f a = b}"
  show ?case
  proof (cases "finite ?Pb")
    case True
    with ‹infinite A› have "infinite (A - ?Pb)"
      by simp
    moreover have "A - ?Pb = {a ∈ A. f a ≠ b}"
      by blast
    ultimately have "infinite {a ∈ A. f a ≠ b}"
      by simp
    from insert.IH[OF _ this] insert.hyps
    show ?thesis
      using rev_finite_subset
      by blast 
  next
    case False
    then have "?Pb ≠ {}" 
      by force
    with False show ?thesis
      by blast
  qed
qed
```

Facts that are crucial to the understanding of a step should be put in the `from` clause of a step.
Auxiliary facts can be put in the trailing using block or passed as tactic arguments.

### Calculations
Use calculation proofs when doing transitive reasoning. The transitive operator, `=` in the following example, must not be manually aligned:
```isabelle
lemma "((a::nat) + b) + c = c + (b + a)"
proof -
  have "(a + b) + c = (b + a) + c"  by simp
  also have "… = c + (b + a)" by simp
  finally show ?thesis by simp
qed
```

## Datatype and function definitions
While each equation of a function definition must be on a separate line, a datatype declaration may be put on a single line if it is short enough.
The separating `|` between several equations is either consistently put at the beginning of the line without indentation or at the end of the line.
By seperating the constructor respectively equation by one space, the usual indentation of two spaces is achieved.
The `where` command for a definition should be on the same line as the declaration, or, if this is not possible, it goes onto the next line with an extra indentation.
If the right-hand side of an equation has to be broken because it is too long, then it is shifted by one indentation plus one space (to account for the `"`) to the right.
Linebreaks within the right-hand side recursively add one indentation. 

Example:
```isabelle
datatype 'a list =
  Nil |
  Cons 'a "'a list"

function list_update :: "'a list ⇒ nat ⇒ 'a ⇒ 'a list" where
"list_update [] i v = []" |
"list_update (x # xs) i v = (
   case i of
     0 ⇒ v # xs |
     Suc j ⇒ x # list_update xs j v
   )"
```
or alternatively:
```isabelle
datatype 'a list =
  Nil
| Cons 'a "'a list"

function list_update :: "'a list ⇒ nat ⇒ 'a ⇒ 'a list" where
  "list_update [] i v = []"
| "list_update (x # xs) i v = (
     case i of
       0 ⇒ v # xs
     | Suc j ⇒ x # list_update xs j v
     )"
```

## Locales
The imports of a locale go on the same line as the locale declaration, or, if the line has to be broken, they are indented by one level.
Here, the `+`s that separate the imports always are at the end of the line.
The `fixes`, `defines`, and `assumes` of a locale are indented by one level as well.
The initial `begin` must always be followed by a blank line and `end` must be preceded by a blank line.
Here are two examples:
```isabelle
locale ex1 = import1 + import2 +
  fixes a b :: 'a
  fixes A :: "'a rel"
  assumes "sym A"
  assumes "(a, b) ∈ A"
begin

lemma "(b, a) ∈ A"
  oops

end
 

locale ex2 =
  import1 +
  this_is_a_very_long_import +
  fixes a :: 'a
begin

lemma "a ∈ UNIV"
  oops

end
```

