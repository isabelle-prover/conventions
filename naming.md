# Isabelle Naming Conventions #
These conventions are adapted from the
[mathlib naming convention](https://github.com/leanprover-community/mathlib/edit/master/docs/contribute/naming.md)
to fit for Isabelle conventions.

## General Conventions ##

Identifiers are generally lower case with underscores. For the most
part, we rely on descriptive names. Often the name of theorem simply
describes the conclusion:

- `succ_ne_zero`
- `mul_zero`
- `mul_one`
- `sub_add_eq_add_sub`
- `le_iff_lt_or_eq`

If only a prefix of the description is enough to convey the meaning,
the name may be made even shorter:

- `neg_neg`
- `pred_succ`

Sometimes, to disambiguate the name of theorem or better convey the
intended reference, it is necessary to describe some of the
hypotheses. The word "of" is used to separate these hypotheses:

- `lt_of_succ_le`
- `lt_of_not_ge`
- `lt_of_le_of_ne`
- `add_lt_add_of_lt_of_le`

Sometimes abbreviations or alternative descriptions are easier to work
with. For example, we use `pos`, `neg`, `nonpos`, `nonneg` rather than
`zero_lt`, `lt_zero`, `le_zero`, and `zero_le`.

- `mul_pos`
- `mul_nonpos_of_nonneg_of_nonpos`
- `add_lt_of_lt_of_nonpos`
- `add_lt_of_nonpos_of_lt`

Sometimes the word "left" or "right" is helpful to describe variants
of a theorem.

- `add_le_add_left`
- `add_le_add_right`
- `le_of_mul_le_mul_left`
- `le_of_mul_le_mul_right`

We can also use the word "self" to indicate a repeated argument:

- `mul_inv_self`
- `neg_add_self`

## Axiomatic Descriptions ##

Some theorems are described using axiomatic names, rather than
describing their conclusions.

- `*_def`  (for unfolding a definition)
- `refl`
- `irrefl`
- `symm`
- `trans`
- `antisymm`
- `asymm`
- `congr`
- `comm`
- `assoc`
- `left_comm`
- `right_comm`
- `mul_left_cancel`
- `mul_right_cancel`
- `inj`  (injective)

## Names for Symbols ##

- `imp`: implication
- `forall`
- `exists`
- `ball`: bounded forall
- `bex`: bounded exists

## Introduction and Elimination Rules ##

- `*I`: introduction rule
- `*E`: elimination rule

------
Copyright (c) 2020. All rights reserved.
Released under Apache 2.0 license as described in the file LICENSE.
Modified by: Kevin Kappelmann
Original author: Jeremy Avigad
