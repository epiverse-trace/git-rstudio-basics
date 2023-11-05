---
title: Ignoring Things
teaching: 5
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Configure Git to ignore specific files.
- Explain why ignoring files can be useful.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I tell Git to ignore files I don't want to track?

::::::::::::::::::::::::::::::::::::::::::::::::::

<!--

## previous

previously

Git is the Version control software for PLAIN text files that works offline and online

now

Git is the Version control software for multiple PLAIN text files in a single project that works offline and online

Paste new files of summative assessment (link to Drive folder) to project folder.

git status

::::::::::::::::: checklist

### Good practice box

- When using git, some cases we can ignore non-plain files

- But above all, we do need to ignore Regenerable Files (ones that are a product of plain text files) like HTML, PDF, PNG

- Files you'll typically want to ignore: .DS_store, Excel file

- List of pre-made gitignore files for many different languages: https://github.com/github/gitignore 

:::::::::::::::::::::::::::

Opportunity to practice how to create an .gitignore file by using Rstudio check list

Configuración de proyecto, según principios sobre buenas prácticas en computación científica (ref)
* Tratar datos originales como “solo lectura”
* Todo lo generado por scripts debe ser “descartable” y capaz de regenerarse a partir de los mismos scripts
adaptado de: https://talesofr.wordpress.com/2017/12/12/a-minimal-project-tree-in-r/ 

::::::::::::::::: testimonial

### TESTIMONIAL

Refer also to the section of “What Not to Put Under Version Control” from the following manuscript by G. Wilson et al. 2017 Good Enough Practices in Scientific Computing (swcarpentry.github.io), 

https://swcarpentry.github.io/good-enough-practices-in-scientific-computing/#what-not-to-put-under-version-control

which enphazise, among other notes, in: 
version control systems are optimized for plain text files; 
avoid raw data, since it should not change;
avoid intermediate files or results that can be re-generated from raw data and software.


:::::::::::::::::::::::::::::

What happens when we run the Rmd file? it generates new files

edit .gitignore file

git add specific files

::::::::::::::::::::::::::::::::: challenge

### Exercise!

Let’s solve this question
Click here https://www.menti.com/alcraf5dm9kp 

::::::::::::::::: hint

### HINT (`hint`)

...

::::::::::::::::::::::

::::::::::::::::: solution

### SOLUTION (`solution`)

...

::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::

a good commit message (evaluate if this can go in 04-changes.md)

::::::::::::::::: checklist

### Good practice box

- Start with an infinitive verb. 

  - It recalls an specific action.


- Keep commit messages short

  - GitHub suggests no more than 50 characters for the first line

  - Then you can add more context lines below


:::::::::::::::::::::::::::

Edit the Rmd file

::::::::::::::::::::::::::::::::: challenge

### Exercise!

- In breakout rooms

- Modify three different types of information in the Rmd file
  - Replace the PNG figure
  - Erase the text “US” in the list of countries
  - Replace the input file for the drop US country

- By turns, each member have to share it screen and choose to make only one of these modifications.

- If there are more than 3 people, modifications can be repeated

- When finished, share your commit messages in the Google Doc file

::::::::::::::::: hint

### HINT (`hint`)

...

::::::::::::::::::::::

::::::::::::::::: solution

### SOLUTION (`solution`)

...

::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::

::::::::::::::::: checklist

### Good practice box

- Make atomic commits

- What is atomic or not atomic?

  - it is not about quantity of changes, but one unit of change

- “Stage chunk” in Rstudio helps to make atomic commits, even if you change a lot of lines!


:::::::::::::::::::::::::::


## episode starts here

-->

What if we have files that we do not want Git to track for us,
like backup files created by our editor
or intermediate files created during data analysis?
Let's create a few dummy files:

```bash
$ mkdir results
$ touch a.csv b.csv c.csv results/a.out results/b.out
```

and see what Git says:

```bash
$ git status
```

```output
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	a.csv
	b.csv
	c.csv
	results/

nothing added to commit but untracked files present (use "git add" to track)
```

Putting these files under version control would be a waste of disk space.
What's worse,
having them all listed could distract us from changes that actually matter,
so let's tell Git to ignore them.

We do this by creating a file in the root directory of our project called `.gitignore`:

```bash
$ nano .gitignore
$ cat .gitignore
```

```output
*.csv
results/
```

These patterns tell Git to ignore any file whose name ends in `.csv`
and everything in the `results` directory.
(If any of these files were already being tracked,
Git would continue to track them.)

Once we have created this file,
the output of `git status` is much cleaner:

```bash
$ git status
```

```output
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

The only thing Git notices now is the newly-created `.gitignore` file.
You might think we wouldn't want to track it,
but everyone we're sharing our repository with will probably want to ignore
the same things that we're ignoring.
Let's add and commit `.gitignore`:

```bash
$ git add .gitignore
$ git commit -m "Ignore data files and the results folder"
$ git status
```

```output
On branch main
nothing to commit, working tree clean
```

As a bonus, using `.gitignore` helps us avoid accidentally adding files to the repository that we don't want to track:

```bash
$ git add a.csv
```

```output
The following paths are ignored by one of your .gitignore files:
a.csv
Use -f if you really want to add them.
```

If we really want to override our ignore settings,
we can use `git add -f` to force Git to add something. For example,
`git add -f a.csv`.
We can also always see the status of ignored files if we want:

```bash
$ git status --ignored
```

```output
On branch main
Ignored files:
 (use "git add -f <file>..." to include in what will be committed)

        a.csv
        b.csv
        c.csv
        results/

nothing to commit, working tree clean
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Ignoring Nested Files

Given a directory structure that looks like:

```bash
results/data
results/plots
```

How would you ignore only `results/plots` and not `results/data`?

:::::::::::::::  solution

## Solution

If you only want to ignore the contents of
`results/plots`, you can change your `.gitignore` to ignore
only the `/plots/` subfolder by adding the following line to
your .gitignore:

```output
results/plots/
```

This line will ensure only the contents of `results/plots` is ignored, and
not the contents of `results/data`.

As with most programming issues, there
are a few alternative ways that one may ensure this ignore rule is followed.
The "Ignoring Nested Files: Variation" exercise has a slightly
different directory structure
that presents an alternative solution.
Further, the discussion page has more detail on ignore rules.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Including Specific Files

How would you ignore all `.csv` files in your root directory except for
`final.csv`?
Hint: Find out what `!` (the exclamation point operator) does

:::::::::::::::  solution

## Solution

You would add the following two lines to your .gitignore:

```output
*.csv           # ignore all data files
!final.csv      # except final.csv
```

The exclamation point operator will include a previously excluded entry.

Note also that because you've previously committed `.csv` files in this
lesson they will not be ignored with this new rule. Only future additions
of `.csv` files added to the root directory will be ignored.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Ignoring Nested Files: Variation

Given a directory structure that looks similar to the earlier Nested Files
exercise, but with a slightly different directory structure:

```bash
results/data
results/images
results/plots
results/analysis
```

How would you ignore all of the contents in the results folder, but not `results/data`?

Hint: think a bit about how you created an exception with the `!` operator
before.

:::::::::::::::  solution

## Solution

If you want to ignore the contents of
`results/` but not those of `results/data/`, you can change your `.gitignore` to ignore
the contents of results folder, but create an exception for the contents of the
`results/data` subfolder. Your .gitignore would look like this:

```output
results/*               # ignore everything in results folder
!results/data/          # do not ignore results/data/ contents
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Ignoring all data Files in a Directory

Assuming you have an empty .gitignore file, and given a directory structure that looks like:

```bash
results/data/position/gps/a.csv
results/data/position/gps/b.csv
results/data/position/gps/c.csv
results/data/position/gps/info.txt
results/plots
```

What's the shortest `.gitignore` rule you could write to ignore all `.csv`
files in `result/data/position/gps`? Do not ignore the `info.txt`.

:::::::::::::::  solution

## Solution

Appending `results/data/position/gps/*.csv` will match every file in `results/data/position/gps`
that ends with `.csv`.
The file `results/data/position/gps/info.txt` will not be ignored.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Ignoring all data Files in the repository

Let us assume you have many `.csv` files in different subdirectories of your repository.
For example, you might have:

```bash
results/a.csv
data/experiment_1/b.csv
data/experiment_2/c.csv
data/experiment_2/variation_1/d.csv
```

How do you ignore all the `.csv` files, without explicitly listing the names of the corresponding folders?

:::::::::::::::  solution

## Solution

In the `.gitignore` file, write:

```output
**/*.csv
```

This will ignore all the `.csv` files, regardless of their position in the directory tree.
You can still include some specific exception with the exclamation point operator.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## The Order of Rules

Given a `.gitignore` file with the following contents:

```bash
*.csv
!*.csv
```

What will be the result?

:::::::::::::::  solution

## Solution

The `!` modifier will negate an entry from a previously defined ignore pattern.
Because the `!*.csv` entry negates all of the previous `.csv` files in the `.gitignore`,
none of them will be ignored, and all `.csv` files will be tracked.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Log Files

You wrote a script that creates many intermediate log-files of the form `log_01`, `log_02`, `log_03`, etc.
You want to keep them but you do not want to track them through `git`.

1. Write **one** `.gitignore` entry that excludes files of the form `log_01`, `log_02`, etc.

2. Test your "ignore pattern" by creating some dummy files of the form `log_01`, etc.

3. You find that the file `log_01` is very important after all, add it to the tracked files without changing the `.gitignore` again.

4. Discuss with your neighbor what other types of files could reside in your directory that you do not want to track and thus would exclude via `.gitignore`.

:::::::::::::::  solution

## Solution

1. append either `log_*`  or  `log*`  as a new entry in your .gitignore
2. track `log_01` using   `git add -f log_01`
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- The `.gitignore` file tells Git what files to ignore.

::::::::::::::::::::::::::::::::::::::::::::::::::


