---
title: Theorem Attributes
---

Attributes modify theorems in various ways in Isabelle.
Most of the important ones simply add some sort of tag to the theorem that will be picked up by other tools.
The most common and important ones in Isabelle/HOL are the ones that declare that a theorem should be used by Isabelle's general-purpose automation:
`simp`, `intro`, `dest`, `elim`, and `iff`.

- `simp` states that a theorem should be used as a rewrite rule (possibly a conditional one) by the simplifier.
This affects methods such as `simp`, `auto`, `force`, `fastforce` that make use of the simplifier.

- Theorems tagged with `intro`, `dest`, `elim` are used by the *classical reasoner*.
This affects methods such as `auto`, `blast`, `force`, `fastforce`.

– `iff` can be applied to theorems stating a logical equivalence and declares that the theorem should be used both by the simplifier and by the classical reasoner.

For more details on this and other attributes, see the [isar-ref](https://isabelle.in.tum.de/dist/doc/isar-ref.pdf).

Anyone developing a theory will have to make the choice of which theorems to declare as `simp`, `intro` etc.
These choices can have significant consequences, not only for that theory itself, but also for any work that imports it:
Well-chosen attributes can make proof automation much smoother with goals disappearing ‘magically’ after applying `auto`.
Poorly chosen attributes, on the other hand, can slow down the automation or even make it loop indefinitely.
Even the former -- ‘goals disappearing magically’ -- has the downside that proofs may become more difficult to read and maintain
since it can become unclear which rules are being applied.
The provers also have heuristics and search depth thresholds,
so a proof that works at the very edge of the search threshold may break in a future version of Isabelle.

Choosing attributes well takes experience, so the general advice is:
Do not declare something as `simp`/`intro`/etc. unless you are sure that it is a good idea.
As for more specific guidelines:

- Good automation rules should generally perform relatively obvious steps that do not *surprise* the user.
- Classical rules and conditional `simp` rules typically involve some sort of backtracking.
If this backtracking sends the automation down a wrong path, it can slow them down significantly.
- Anyt unconditional equation where the left-hand side should clearly be rewritten to the right-hand side should probably be a simp rule (e.g. `x + 0 = x`).
- This also applies for conditional equations as long as the tradeoff between how complicated the precondition, how often the rule can apply syntactically, and how often the rule will actually apply works out (e.g. `x ≠ 0 ⟹ a * x = b * x ⟷ a = b`).
- For distributivity rules of the form `f (g x) = g (f x)` or `f (g x) (g y) = g (f x y)`, it is not immediately clear which way around they should be applied.
These *can* be turned into simp rules, but the choice of whether `f` (resp. `g`) should be ‘pulled out’ or ‘pushed in’ should be consistent for *all* simp rules involving `f` (resp. `g`).
- The left-hand side of a simp rule should always be fully simplified already; otherwise, it might not get picked up.
For instance, a rule like `length (x # xs) = length ys` might never be applied because the simplifier rewrites `length (x # xs) = length xs + 1` first.
- Good `simp` rules are essential for making the proof automation experience smoother.
Whenever you introduce a new constant, try to prove relevant simple `simp` rules.
- Classic rules (`iff`, `intro` etc.) are not *as* important as `simp` rules.
Especially if the reasoning step encoded in the rule is a conceptually nontrivial one (i.e. one that a detailed paper proof would mention),
it is usually better to apply it explicitly in a proof rather than relying on the automation to do it.

There are various other ‘theorem collections’ with corresponding attributes that work similarly, but have more specific purposes.
Examples are `continuous_intros`, `tendsto_intros`, `derivative_intros`.
There is no central documentation for these, but the general rule here is that if these concepts are relevant to your work, you should prove corresponding theorems with the corresponding attribute.
For example, if you define a new real-valued function, you should prove that it is continuous and declare that theorem as `continuous_intros` etc.
