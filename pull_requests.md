# Isabelle Community Pull Request Management

## Creating a Pull Request

We use a standard fork-and-branch workflow. See
https://blog.scottlowe.org/2015/01/27/using-fork-branch-git-workflow/
for a good introduction.

Here are some tips and tricks to make the process of contributing as smooth as possible.

1. Adhere to the guidelines described in this folder.
2. Discuss your contribution before and while you are working on it.
Create an issue to discuss your general ideas and questions.
For more detailed and longer conversations, you could also make use of [Isabelle's Zulip](https://isabelle.zulipchat.com/).
3. Create a pull request from a feature branch on your personal fork,
   as explained in the link above, or from a branch of the main repository if you have commit access.
4. If you have made a lot of changes/additions, make many PRs containing small, self-contained
   pieces. This helps you get feedback as you go along, and it is much easier to review. This is
   especially important for new contributors.
5. Answer the following three questions in your PR:
  1. What: What is this PR about?
  2. Why: Why is this PR useful/what is the problem you solve?
  3. How: How did you create the feature/solve the problem?
6. As for [commits](commits.md), bugs closed by the PR should be listed on a separate line
in the footer prefixed with "Closes".

## Code-Review Checklist
TODO: update for Isabelle. Taken from [lean code review](https://github.com/leanprover-community/mathlib/blob/master/docs/contribute/code-review.md)

Copy-paste into a comment when reviewing a pull request:
```
Check:

 * [ ] coding style
 * [ ] documentation
 * [ ] for tactics:
     * [ ] tests
     * [ ] efficiency (make sure at least it's not outrageously inefficient)
  * [ ] it fits the overall library design
```
