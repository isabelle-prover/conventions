# Isabelle Community Sessions Conventions #


## Naming Conventions ##

- Sessions in the distribution are named with capitalized words separated by hyphens, e.g. `HOL-Analysis`, `HOL-Library`

- Other sessions -- in the AFP and community projects -- are named in capitalized Snake_Case, e.g. `Akra_Bazzi`

- Theory names: capitalized Snake_Case, e.g. `Sepref_All_Examples`.

- If theories and sessions are named in this way, imports never need to need quotation marks, i.e. one can write `Akra_Bazzi.Akra_Bazzi` instead of `"Akra_Bazzi"`. Thus the latter form should never be used.

## Session Discipline

- One session per AFP entry/project is the norm

- Additional "small sessions" are handy during development and may serve as entry points for sessions that want to base on an session not containing all the theories. Here is an example:

```
session Project_Name = HOL +
  directories
    "Examples"
  theories
    Project_Main
    "Examples/Project_Name_All_Examples"

(* smaller sessions *)
session Project_Name_Entry in "Project_Name_Entry" = HOL +
  sessions
    Project_Name
  theories
    Project_Name.Project_Main
```
 




