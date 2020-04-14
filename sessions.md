# Isabelle Community Sessions Conventions #


## Naming Conventions ##

- Sessions in the distribution are named with hyphen separated capital words, e.g. `HOL-Analysis`, `HOL-Library`

- Other sessions -- in the AFP and community projects -- are named in Camel Case with underscores, e.g. `Akra_Bazzi`

- Theory names: Camel Case with underscores, e.g. `Sepref_All_Examples`

- Constants lower case (e.g. `prime`), Constructors capitalized (e.g. `Suc`, `Cons`, `Leaf`)

- Locales: too complicated for now

## Sessions Discipline

- one session per AFP entry/project is the norm

- additional "small sessions" are handy during development and may serve as entry points for sessions that want to base on an session not containing all the theories. Here is an example:

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
 




