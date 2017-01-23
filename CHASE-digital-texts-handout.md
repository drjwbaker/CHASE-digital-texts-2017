# CHASE Digital Texts Workshop, 3 March 2017, Courtauld Institute of Art, London

_____
## Schedule

- 11:00-11:30	Introduction (DK)
- 11:30-12:00	Shell: Basics (JB)
- 12:00-12:30	Shell: Counting (JB)
- 12:30-13:15	Lunch
- 13:15-14:00	Shell: Mining (JB)
- 14:00-15:00	Shell: Free Text (JB)
- 15:00-16:00	More with texts in and beyond the Shell (DK)
- 16:00-17:00	Supported self-directed learning / overflow!

_____
### Shell: Basics

**`pwd`** print working directory

**`ls`** list directory

- `-l`: list file information
- `-lh`: list human readable file information

**`cd`** change directory

______
### Shell: Interacting with Files

**`mkdir`** make directory

**`cat`** send file or files to output (in most cases, print to shell)

**`head`** output first parts of a file or files

**`tail`** output last parts of a file or files

**`mv`** rename or move a file or files. Syntax for renaming a file: `mv FILENAME NEWFILENAME`

**`cp`** copy a file or files. Syntax: `cp FILENAME NEWFILENAME`

**`>`** redirect output. Syntax with `cat`: `cat FILENAME1 FILENAME2 > NEWFILENAME`

**`rm`** remove a file or files. NB: *USE WITH EXTREME CAUTION!!!*

______
### Shell: Wildcards

**`?`** a placeholder for one character or number

**`*`** a placeholder for zero or more characters or numbers

**`[]`** defines a class of characters

*Examples*

- `foobar?`: matches seven character strings starting with `foobar` and ending with one character or number
- `foobar*`: matches strings starting with `foobar` ending with zero or more further characters or numbers
- `foobar*.txt`: matches strings starting with `foobar` and ending with `.txt`
- `[1-9]foobar?`: matches eight character strings starting that start with a number, have `foobar` after the number, and end with any character or number.

_____
### Shell: Counting and Mining

**`wc`** word count

- `-w`: count words
- `-l`: count lines
- `-c`: count characters (or `m` for Mac users)

**`grep`** global regular expression print

- `-c`: displays counts of matches for each file
- `-i`: match with case insensitivity
- `-w`: match whole words
- `-v`: exclude match
- `--file=FILENAME.txt`: use the file `FILENAME.txt` as the source of strings used in query

**`egrep`** pattern matching global regular expression print

- `--file=FILENAME.txt`: use the file `FILENAME.txt` as the source of strings used in query, this file may contain a regular expression

_____
#### Exercise

With the person next to you, select a word to search for and use what you have learnt do to the following:

- Search for all case sensitive instances of that word in the 'london' file. Print you results to the shell.
- Count all case sensitive instances of that word in both tsv files in this directory. Print you results to the shell.
- Count all case insensitive instances of that word in both tsv files in this directory. Print you results to the shell.
- Search for all case insensitive instances of that word in the 'london' file. Print you results to a new .tsv file. 
- Search for all case insensitive instances of that whole word in the 'london' file. Print you results to a new .tsv file.
- Compare the line counts of your tsv files.
- Open both files in a text editor (Notepad++, Atom, Kate, whatever you prefer) or Excel-like program to see the difference between searching strings and searching whole words using `grep`

______
### Shell: Free Text 

_____
### Option 1: A historical book


#### Grabbing a text, cleaning it up

*Work on this exercise with the person next to you*

Head to `.../digitext/text/`. We're going to work again with the `gulliver.txt` file we saw earlier.

First look at the file by typing `less -N gulliver.txt`. Use the down arrows and/or pageup/pagedown to look around the text. Note what the shell considers a line to be by the count on the left hand side. Hit `q` when you are down to return to the flashing command line.

We're going to start our work on cleaning this text by using the `sed` command. The command allows you to edit files directly.

Type `sed '9352,9714d' gulliver.txt > gulliver-nofoot.txt` and hit enter.

The command `sed` in combination with the `d` value will look at `gulliver.txt` and delete all values between the rows specified. The `>` action then prompts the script to this edited text to the new file specified.

Now type `sed '1,37d' gulliver-nofoot.txt > gulliver-noheadfoot.txt` and hit enter. This does the same as before, but for the header.

You now have a cleaner text. The next step is to prepare it even further for rigorous analysis.

We now use the `tr` command, used for translating or deleting characters. Type `tr -d [:punct:] < gulliver-noheadfoot.txt > gulliver-noheadfootpunct.txt` and hit enter.

This uses the translate command and a special syntax to remove all punctuation. It also requires the use of both the output redirect `>` we have seen and the input redirect `<` we haven't seen. 

Finally regularise the text by removing all the uppercase lettering. Type `tr [:upper:] [:lower:] < gulliver-noheadfootpunct.txt > gulliver-clean.txt` and hit enter.

Open the `gulliver-clean.txt` in a text editor. Note how the text has been transformed ready for analysis.

#### Pulling a text apart, counting word frequencies

We are now ready to pull the text apart.

Type `tr ' ' '\n' < gulliver-clean.txt > gulliver-linebyline.txt` and hit enter.

This uses the translate command again, this time to translate every blank space into `\n` which renders as a new line. Every word in the file will now have its own line.

This isn't much use, so to get a better sense of the data we need to use another new command called `sort`. Type `sort gulliver-linebyline.txt > gulliver-ordered.txt` and hit enter.

This script uses the `sort` command to rearrange the text from its original order into an alphabetical configuration. Open the file in a text editor and after scrolling past some blank space you will begin to see some numbers and finally words, or at least lots of copies of 'a'!

This is looking more useful, but we can go one step further. Type `uniq -c gulliver-ordered.txt > gulliver-final.txt` and hit enter.

This script uses `uniq`, another new command, in combination with the `-c` flag to both remove duplicate lines and produce a word count of those duplicates.

Note that these steps can be simplified by building 'pipes'. So...

`tr ' ' '\n' < gulliver-clean.txt | sort | uniq -c > gulliver-final.txt`

...would have done the line-by-line, sorting, and removal of duplicates in one go.

Either way we have now taken the text apart and produced a count for each word in it. This is data we can prod and poke and visualise, that can form the basis of our investigations, and can compare with other texts processed in the same way. And if we need to run a different set of transformation for a different analysis, we can return to `gulliver-clean.txt` to start that work

**Note: your final output will have two problems - not all punctuation will be removed and not all special characters have been handled correctly. Search online for why this might have happened (something about the `punct` command we used...)**

_____
### Option 2: A historical website

#### Grabbing a text, cleaning it up

*Work on this exercise with the person next to you*

Head to `.../digitext/text/`. We're going to work again with the `diary.html` file we saw earlier.

First look at the file by typing `less -N diary.html`. Use the down arrows and/or pageup/pagedown to look around the text. Note what the shell considers a line to be by the count on the left hand side. Hit `q` when you are down to return to the flashing command line.

We're going to start by using the `sed` command. The command allows you to edit files directly.

Type `sed '265,330d' diary.html > diary-nofoot.txt` and hit enter.

The command `sed` in combination with the `d` value will look at `diary.html` and delete all values between the rows specified. The `>` action then prompts the script to this edited text to the new file specified.

Now type `sed '1,221d' diary-nofoot.txt > diary-noheadfoot.txt` and hit enter. This does the same as before, but for the header.

You now have a cleaner text. The next step is to prepare it even further for rigorous analysis.

First we wil remove all the html tags. Type `sed -e 's/<[^>]*>//g' diary-noheadfoot.txt > diary-notags.txt`. Here we are using a regular expression (more on which at [http://data-lessons.github.io/library-data-intro/04-regular-expressions/](http://data-lessons.github.io/library-data-intro/04-regular-expressions/)) to find all valid html tags (anything within angle brackets) and delete them. This is a complex regular expression, do don't worry too much about how it works!

We now use the `tr` command, used for translating or deleting characters. Type `tr -d [:punct:] < diary-notags.txt > diary-notagspunct.txt` and hit enter.

This uses the translate command and a special syntax to remove all punctuation. It also requires the use of both the output redirect `>` we have seen and the input redirect `<` we haven't seen. 

Finally regularise the text by removing all the uppercase lettering. Type `tr [:upper:] [:lower:] < diary-notagspunct.txt > diary-clean.txt` and hit enter.

Open the `gulliver-clean.txt` in a text editor. Note how the text has been transformed ready for analysis.

#### Pulling a text apart, counting word frequencies

We are now ready to pull the text apart. This can be done by using 'pipes' which hold an output in memory before moving to the next. Type `tr ' ' '\n' < diary-clean.txt | sort | uniq -c | sort -r > diary-final.txt` and hit enter.

The first part of this uses the translate command again, this time to translate every blank space into `\n` which renders as a new line. Every word in the file will at this stage have its own line.

The second part uses the `sort` command to rearrange the text from its original order into an alphabetical configuration.

The third part uses `uniq`, another new command, in combination with the `-c` flag to remove duplicate lines and to produce a word count of those duplicates.

The fourth and final part sorts the text again by the counts of duplicates generated in step three.

We have now taken the text apart and produced a count for each word in it. This is data we can prod and poke and visualise, that can form the basis of our investigations, and can compare with other texts processed in the same way. And if we need to run a different set of transformation for a different analysis, we can return to `diary-clean.txt` to start that work

_____
### Where to go from here

Deborah S. Ray and Eric J. Ray, *Unix and Linux: visual quickstart guide*, 4th edition (2009).

- An invaluable (and not expensive) reference guide to using Unix shell commands - especially if you only use the command line sporadically!

*The Command Line Crash Course* [http://cli.learncodethehardway.org/book/](http://cli.learncodethehardway.org/book/) 'learn code the hard way'

- Good for reminders of the basics, especially if rote learning is your thing!

Al Sweigart, *Automate the Boring Stuff* [https://automatetheboringstuff.com/](https://automatetheboringstuff.com/)

- Practical programming for beginners based on scenarios such as batch renaming files or scrapping the web. Available as a book (£) or a website (free!)

Programming for Everybody (Python) [https://www.coursera.org/course/pythonlearn](https://www.coursera.org/course/pythonlearn) 

- A 10 week course that takes 2-4 hours per week. Python is popular in research programming as it is readable, relatively simple, and very powerful. This gives you some basics on which to build.

Programming Historian [http://programminghistorian.org/project-team](http://programminghistorian.org/project-team).

- The Programming Historian is an open, collaborative book aimed at providing programming lessons to historians. Although the examples are aimed to historians they should be applicable to most humanists.

Software Carpentry [https://software-carpentry.org](https://software-carpentry.org)

- Software Carpentry offers workshops and online tutorials on the basics of research computing. It is aimed at research scientists, but the lessons here on the Unix shell, Python, Git and GitHub (for version control), and R (for statistical analysis) are excellent introductions.

_____
### References

19th Century Books - Book Metadata - 01/09/2013. British Library (2014) DOI: [10.21250/DB21](https://dx.doi.org/10.21250/DB21)

James Baker and Ian Milligan, 'Counting and mining research data with Unix', *The Programming Historian* ([2014](http://programminghistorian.org/lessons/research-data-with-unix)

Ian Milligan and James Baker, 'Introduction to the Bash Command Line', *The Programming Historian* ([2014](http://programminghistorian.org/lessons/intro-to-bash))

William J. Turkel, 'Basic Text Analysis with Command Line Tools in Linux' ([15 June 2013](http://williamjturkel.net/2013/06/15/basic-text-analysis-with-command-line-tools-in-linux/). The section 'Shell: Free Text' is adapted from this and shared under a [Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported](http://creativecommons.org/licenses/by-nc-sa/3.0/).