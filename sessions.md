# Isabelle Community Sessions Conventions #


## Naming Conventions ##

- Sessions the AFP and community projects are named in capitalized Snake_Case, e.g. `Akra_Bazzi`. We follow this convention. 
  - Note that in the distribution session are named with capitalized words separated by hyphens, e.g. `HOL-Analysis`, `HOL-Library`.

- Theory names: capitalized Snake_Case, e.g. `Sepref_All_Examples`.

- If theories and sessions are named in this way, imports never need to need quotation marks, i.e. one can write `Akra_Bazzi.Akra_Bazzi` instead of `"Akra_Bazzi"`. Thus the latter form should never be used.

## Session Discipline

- One session per project is the norm.

- Each session must come with a `README.md` and `LICENSE` file.

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
 
## Folders and Theory Naming

Projects should be hierarchically structured using folders.
Theory names are generally captilised with underscores.
The theory name must describe the main content of the theory.
Example
```
Mathlib
│   README.md
│   LICENSE
│
└───Algebra
│   │   Monoids.thy
│   │   Groups.thy
│   │   ...
│   └───Continued_Fractions
│       │   Continued_Fractions_Basics.thy
│       │   Continued_Fractions_Recurrence.thy
│       │   Continued_Fractions_Limits.thy
│       │   ...
│ 
└───Topology
    │   ...
...
```

