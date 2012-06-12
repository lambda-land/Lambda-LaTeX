## Description ##

A collection of LaTeX macro libraries used by the Lambda Group at Oregon State
University.  Probably of little interest to anyone else!

#### Files ####

+ **lambda.sty** - Generic math, language design, code, and meta-note macros.
  Include this in all of your papers.

+ **cc.sty** - Choice calculus macros. Depends on lambda.sty.

+ **vlc.sty** - Variational lambda calculus macros. Depends on lambda.sty and
  cc.sty. (Note: some non-backward compatible edits may still be made to this
  file, up through the submission of the VLC journal paper).


## Motivation ##

Our copy-paste reuse strategy for LaTeX macros is fast and flexible but
problematic when combining formalisms from multiple papers (for example, in
follow-up papers, grant proposals, presentations, and theses).  This is an
attempt to "canonize" some of our most widely used macros, so that they can be
shared and reused more easily.


## When to edit ##

*Don't directly modify these files in a non-backward compatible way!*

Old papers relying on these libraries should look exactly the same after
compiling them with and edits you make updates.

In general, prefer not to edit these libraries at all.  A good rule of thumb
would be to not add or edit a macro unless the change is needed in at least two
different papers.  Otherwise, add new commands locally or override existing
commands locally with `\renewcommand`.

If a macro does need to be edited, often it can be done in a backward
compatible way by introducing hook macros.  For example, consider the following
macro for declaring a new dimension A.

    \newcommand{\dimA}[2][a_1,a_2]{\DimIn[A]{#1}{#2}}

In some papers, we prefer the default tag names to be `a,b` rather than
`a_1,a_2`.  Rather than change the defaults directly, we can change the macro
to the following.

    \newcommand{\Atags}{a_1,a_2}
    \newcommand{\dimA}[2][\Atags]{\DimIn[A]{#1}{#2}}

Then in the papers that we want to change the defaults, we override `\Atags`.
    
    \renewcommand{\Atags}{a,b}

I have used this strategy extensively in combining our existing mass of
copy-pasted-edited macros into a mostly consistent whole.


## How to use ##

For each library you want to use, add a line like the following to your LaTeX
file: `\usepackage{lambda}`

The following gives two ways to install the libraries so that LaTeX will find
them when you compile the above command.

#### The fast and initially easy way: ####

1. Download the files. (Click the "Zip" button above.)
2. Copy them into the directory of your paper.

This will get you started but makes it more difficult to keep your libraries
up to date and in sync.

#### The more disciplined (better) way: ####

1. Install Git (if you haven't already).
2. Figure out where your LaTeX distribution looks for user-installed packages.
   * Linux: `~/texmf/tex/latex`
   * Mac: `~/Library/texmf/tex/latex`
   * Windows: ??? (If a Windows user figures this out, let me know.)
3. Create this directory and `cd` into it.
4. `git clone git://github.com/walkie/Lambda-LaTeX.git`

Then, each time you want to get the latest versions of the files:

1. `cd` into the git repository created by step 4 above.
2. `git pull`

This is the strategy you should use if you plan on editing the libraries
yourself, since then you can easily commit the changes back.  If you have a
GitHub account, I'll add you as a collaborator so you can commit your changes
directly.
