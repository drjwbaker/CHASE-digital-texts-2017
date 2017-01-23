# CHASE Digital Texts Workshop, 3 March 2017, Courtauld Institute of Art, London

_____
### Installation (to be completed before the session)

Windows users, see the section entitled 'Installing Git Bash' in the Programming Historian lesson [*Introduction to the Bash Command Line*](http://programminghistorian.org/lessons/intro-to-bash). OS X and Linux users, simply make sure you know how to find your 'Terminal'.

The data required for the lesson can be downloaded at: [https://github.com/drjwbaker/CHASE-digital-texts-2017/blob/master/digitext.zip?raw=true](https://github.com/drjwbaker/CHASE-digital-texts-2017/blob/master/digitext.zip?raw=true)

______
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
## Shell AM

Between now and 15:00 I will introduce you to programming by looking at how data can be manipulated, counted, and mined using the Unix shell, a command line interface to your computer and the files it has access to.

A Unix shell is a command-line interpreter that provides a user interface for the Linux operating system and for Unix-like systems (such as iOS). For Windows users, popular shells such as Cygwin or Git Bash provide a Unix-like interface (a command line interface preferable - to me at least - to Windows own flavour of command line).

I will cover a small number of basic commands (using Git Bash for Windows users, Terminal for iOS/Linux) for interrogating and abstracting from machine readable digital objects, in this case texts and metadata about texts. These commands constitute building blocks upon which more complex commands can be constructed to fit your data or project.

We'll be covering quite a lot but the key commands are in the handout for reference. We'll proceed in a follow my leader fashion. The format will be that I'll demo a command, you copy, and then we'll discuss the results. Stickies for when you get stuck or something doesn't appear to work.

______
### Shell: Basics

We will begin with the basics of navigating the Unix shell. We need to learn this before we can do anything interesting.

Start by opening your shell. When you run it, you will likely see a black window with a cursor flashing next to a dollar sign. This is our command line.

If, when opening a command window or at any other time today, you are unsure of where you are in a computer's file system, you can find out what directory you are in using `pwd` command, which stands for "print working directory", and hitting enter - which executes commands in the shell. Try typing `pwd` and hitting enter.

To orient ourselves, let's get a listing of what files are in this directory. Type `ls` and you will see a list of every file and directory within your current location.

You may want more information than just a list of files. You can do this by specifying various *flags* to go with our basic commands. These are additions to a command that provide the computer with a bit more guidance of what sort of output or manipulation you want.

If you type `ls -l` and hit enter the computer returns a long list of files that contains information similar to what you'd find in your finder or explorer: the size of the files in bytes, the date it was created or last modified, and the file name.

In everyday usage you will be more used to units of measurement like kilobytes, megabytes, and gigabytes. Luckily, there's another flag `-h` that when used with the -l option, use unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte in order to reduce the number of digits to three or less using base 2 for sizes.

Now `ls -h` won't work on its own. When you want to use two flags, you can just run them together. So, by typing `ls -lh` and hitting enter you receive an output in a human-readable format (note: that the order here doesn't matter).

You've now spent a great deal of time in your home directory. Let's go somewhere else. You can do that through the `cd` or Change Directory command. 

If you type `cd desktop` you are now on your desktop *note: for Windows users, the case of the file/directory doesn't matter. For Linux users like me, it does, and I believe that is the same for Mac people*. To double check, type `pwd` and you should see something that represents your desktop.

You'll note that this only takes you 'down' through your directory structure (as in into more nested directories). If you want to go back, you can type `cd ..`. This moves us 'up' one directory, putting us back where we started. If you ever get completely lost, the command `cd` will bring you right back to the home directory, right where you started.

Try exploring: move around the computer, get used to moving in and out of directories, see how different file types appear in the Unix shell. **TWO MINUTES**

Being able to navigate your file system using the bash shell is very important for using the Unix shell effectively. And as you become more comfortable, you'll soon find yourself skipping directly to the directory that you want.

_____
#### Summary

Within the Unix shell you can now:

- use the command `pwd` to find out where you are in on your computer
- use the command `ls` to list directory contents
- use flags `-l` and `-lh` to guide the output of the `ls` command
- use the command `cd` to move around your computer

On the handout, I've provided a bunch of other useful basic commands - copying, moving, deleting - which we don't need for today, but you will need if you take to working in this environment.

______
### Shell: Counting

Often you are presented with files about digital objects - say lists of books. A quick way to find out what is going on with them is to count their contents in some way. The Unix shell can be used to quickly generate counts from across files, something that is tricky to achieve using the graphical user interfaces of standard office suites.

In the Unix shell, use the `cd` command to navigate to the directory that contains our data: the `tabular` subdirectory of the `...digitext` directory. Remember, if at any time you are not sure where you are in your directory structure, type `pwd` and hit enter.

Type `ls -lh` and then hit enter. This prints, or displays, a list that includes a file and a subdirectory.

The file in this directory are two datasets that derive from metadata for nearly 50k 17th, 18th, and 19th century books digitsed by Microsoft in partnership with the British Library.

*Note: TSV files are those in which within each row the units of data (or cells) are separated by tabs. They are similar to CSV (comma seperated value) files were the values are separated by commas. The latter are more common but can cause problems with the kind of data we have, where commas can be found within the cells (though with the right encoding this can be overcome). Either way both can be read in simple text editors or in spreadsheet programs such as Libre Office Calc or Microsoft Excel.*

From here you can count the contents of the files.

The Unix command for counting is `wc`. Type `wc -w BLbooks-Paris.tsv` and hit enter. The flag `-w` combined with `wc` instructs the computer to print a word count, and the name of the file that has been counted, into the shell.

As was seen earlier today flags such as `-w` are an essential part of getting the most out of the Unix shell as they give you better control over commands.

If your reader request or piece of work is more concerned number of entries (or lines) than the number of words, you can use the line count flag. Type `wc -l BLbooks-Paris.tsv` and hit enter. Combined with `wc` the flag `-l` prints a line count and the name of the file that has been counted.

With these two flags, the most obvious thing we can use `wc` for is to quickly compare the shape of sources in digital format - for example word counts per page of a book, the distribution of characters per page across a collection of newspapers, the average line lengths used by poets. You can also use `wc` with a combination of wildcards and flags to build more complex queries.

Can you guess what the line `wc -l *.tsv` will do? Correct! This prints the line counts for `BLbooks-Paris.tsv` and `BLbooks-London.tsv`, offering a simple means of comparing these two sets of research data. Of course, it may be faster if you only have a handful of files to compare the line count for the two documents in Libre Office Calc, Microsoft Excel, or a similar spreadsheet program. But when wishing to compare the line count for tens, hundreds, or thousands of documents, the Unix shell has a clear speed advantage.

Moreover, as our datasets increase in size you can use the Unix shell to do more than copy these line counts by hand, by the use of print screen, or by copy and paste methods. Using the `>` redirect operator we saw earlier you can export our query results to a new file. Type `wc -l *.tsv > results/FOOBAR.txt` (or something like that, the last bit after `results/` could be anything!) and hit enter. This runs the same query as before, but rather than print the results within the Unix shell it saves the results as `FOOBAR.txt`. By prefacing this with `results/` the shelll is instructed to save the .txt file to the `results` sub-directory. To check this, navigate to the `results` subdirectory, hit enter, type `ls`, and hit enter again to see this file. Type `FOOBAR.txt` to see the file contents in the shell (as it is 10 lines or fewer in length, all the file contents will be shown here).

_____
## Shell PM

______
### Shell: Mining

The Unix shell can do much more than count the words and lines within a file. The `grep` command (meaning 'global regular expression print') is used to search across multiple files for specific strings of characters. It is able to do so much faster than the graphical search interface offered by most operating systems or office suites. And combined with the `>` operator, the `grep` command becomes a powerful research tool can be used to mine your data for characteristics or word clusters that appear across multiple files and then export that data to a new file. The only limitations here are your imagination, the shape of your data, and - when working with thousands or millions of files - the processing power at your disposal.

To begin using `grep`, first navigate to the `...digitext/tabular` directory. Here type `grep 1832 *.tsv` and hit enter. This query looks across all files in the directory that fit the given criteria (the .tsv files) for instances of the string, or character cluster, '1832'. It then prints them within the shell.

Press the up arrow once in order to cycle back to your most recent action. Amend `grep 1832 *.tsv` to `grep -c 1832 *.tsv` and hit enter. The shell now prints the number of times the string 1832 appeared in each `*.tsv file`. If you look at the output from the previous command, this tends to be refer to the date field of each book title.

Strings need not be numbers. `grep -c revolution *.tsv`, for example, counts the instances of the string `revolution` within the defined files and prints those counts to the shell. Run this, observe the output, and then amend it to `grep -ci revolution *.tsv`. This repeats the query, but prints a case insensitive count (including instances of both `revolution` and `Revolution`). Note how the count has increased. As before, cycling back and adding `> results/`, followed by a filename (ideally in .txt format), will save the results to a data file.

So far we have counted strings in file and printed to the shell or to file those counts. But the real power of `grep` comes in that you can also use it to create subsets of tabulated data (or indeed any data) from one or multiple files. Type `grep -i revolution *.tsv` and hit enter. This script looks in the defined files and prints any lines containing `revolution` (without regard to case) to the shell. `grep -i revolution *.tsv > results/FOOBAR-revolution.tsv` saves it to file.

However if we look at this file, it contains every instance of the string 'revolution' including as a single word and as part of other words such as 'revolutionary'. This perhaps isn't as useful as we thought... Thankfully, the `-w` flag instructs `grep` to look for whole words only, giving us greater precision in our search. Type `grep -iw revolution *.tsv > results/FOOBAR-revolution.tsv` and hit enter. This script looks in both of the defined files and exports any lines containing the whole word `revolution` (without regard to case) to the specified .tsv file. `wc -l *revolution` shows us the difference between them.

______
#### Exercise

With the person next to you, select a word to search for and use what you have learnt do to the following:

Search for all case sensitive instances of that word in the 'london' file. Print you results to the shell.

- `grep hero BLbooks-London.tsv`

Count all case sensitive instances of that word in both tsv files in this directory. Print you results to the shell.

- `grep -c hero *.tsv`

Count all case insensitive instances of that word in both tsv files in this directory. Print you results to the shell.

- `grep -ci hero *.tsv`

Search for all case insensitive instances of that word in the 'london' file. Print you results to a new .tsv file. 

- `grep -i hero BLbooks-London.tsv > new.tsv`

Search for all case insensitive instances of that whole word in the 'london' file. Print you results to a new .tsv file.

- `grep -iw hero BLbooks-London.tsv > new2.tsv`

Compare the line counts of your tsv files.

- `wc -l FILENAMES`

Open both files in a text editor (Notepad++, Atom, Kate, whatever you prefer) or Excel-like program to see the difference between searching strings and searching whole words using `grep`

______
#### Recap

Within the Unix shell you can now:

- use the `wc` command with the flags `-w` and `-l` to count the words and lines in a file or a series of files.
- use the redirector and structure `> subdirectory/filename` to save results into a subdirectory.
- use the `grep` command to search for instances of a string.
- use with `grep` the `-c` flag to count instances of a string, the `-i` flag to return a case insensitive search for a string, the `-v` flag to exclude a string from the results, and -w to return a whole word only search
- combine these commands and flags to build complex queries in a way that suggests the potential for using the Unix shell to count and mine your research data and research projects.

______
### Shell: Free Text

So far we have looked at how to use the Unix shell to manipulate, count, and mine tabulated data. Most data, especially digitised documents used in research, are much messier than book metadata. Nonetheless many of the same techniques can be applied to non-tabulated data, such as free text, we just need to think carefully about what it is we are counting and how we can get the best out of the Unix shell. 

Thankfully there are plenty of folks out there doing this sort of work and we can borrow what they do as an introduction to working with these more complex files. So for this exercise we're going to leap forward a little in terms of difficulty to an scenario where we won't learn about everything that is happening in detail or discuss at length each command. We're going to prepare and pull apart a text to show the potential of using the Unix shell in research. And where commands we've learnt about are used, I've left some of the figuring out to do to you - so please refer to your notes if you get stuck!

You have three options here:

- an example of hand transcribed text: Gulliver's Travels
- an example of text captured by an optical character recognition process: General Report on the Physiography of Maryland. A dissertation, etc. (Reprinted from Report of Maryland State Weather Service.) [With maps and illustrations.] 1898 (from [https://dx.doi.org/10.21250/db12](https://dx.doi.org/10.21250/db12))
- an example of a webpage: Piper's World (a GeoCities page from 1999 saved at archive.org)

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

We are now ready to pull the text apart. This can be done by using 'pipes' which hold an output in memory before moving to the next. Type `tr ' ' '\n' < gulliver-clean.txt | sort | uniq -c | sort -r > gulliver-final.txt` and hit enter.

The first part of this uses the translate command again, this time to translate every blank space into `\n` which renders as a new line. Every word in the file will at this stage have its own line.

The second part uses the `sort` command to rearrange the text from its original order into an alphabetical configuration.

The third part uses `uniq`, another new command, in combination with the `-c` flag to remove duplicate lines and to produce a word count of those duplicates.

The fourth and final part sorts the text again by the counts of duplicates generated in step three.

We have now taken the text apart and produced a count for each word in it. This is data we can prod and poke and visualise, that can form the basis of our investigations, and can compare with other texts processed in the same way. And if we need to run a different set of transformation for a different analysis, we can return to `gulliver-clean.txt` to start that work.

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

We have now taken the text apart and produced a count for each word in it. This is data we can prod and poke and visualise, that can form the basis of our investigations, and can compare with other texts processed in the same way. And if we need to run a different set of transformation for a different analysis, we can return to `diary-clean.txt` to start that work.

_____
### Option 3: A historical book (captured using Optical Character Recognition)

#### Grabbing a text, cleaning it up

*Work on this exercise with the person next to you*

Head to `.../digitext/text/`. We're going to work again with the `gulliver.txt` file we saw earlier.

First look at the file by typing `less -N gulliver.txt`. Use the down arrows and/or pageup/pagedown to look around the text. Note what the shell considers a line to be by the count on the left hand side. Hit `q` when you are down to return to the flashing command line.

We will start by using the `tr`, which is a command that can translate or delete characters. Type `tr -d [:punct:] < 000003160_01_text.json > 000003160_01_text-nopunct.txt` and hit enter.

This uses the translate command and a special syntax to remove all punctuation. It also requires the use of both the output redirect `>` we have seen and the input redirect `<` we haven't seen. 

Finally regularise the text by removing all the uppercase lettering. Type `tr [:upper:] [:lower:] < 000003160_01_text-nopunct.txt > 000003160_01_text-clean.txt` and hit enter.

Open the `000003160_01_text-clean.txt` in a text editor. Note how the text has been transformed ready for analysis.

#### Pulling a text apart, counting word frequencies

We are now ready to pull the text apart. This can be done by using 'pipes' which hold an output in memory before moving to the next. Type `tr ' ' '\n' < 000003160_01_text-clean.txt | sort | uniq -c | sort -r > 000003160_01_text-final.txt` and hit enter.

The first part of this uses the translate command again, this time to translate every blank space into `\n` which renders as a new line. Every word in the file will at this stage have its own line.

The second part uses the `sort` command to rearrange the text from its original order into an alphabetical configuration.

The third part uses `uniq`, another new command, in combination with the `-c` flag to remove duplicate lines and to produce a word count of those duplicates.

The fourth and final part sorts the text again by the counts of duplicates generated in step three.

We have now taken the text apart and produced a count for each word in it. This is data we can prod and poke and visualise, that can form the basis of our investigations, and can compare with other texts processed in the same way. And if we need to run a different set of transformation for a different analysis, we can return to `000003160_01_text-clean.txt` to start that work.

**Note: your final output will have one problem - not all the words counted are real words (see the words counted only 1 or 2 times). To better understand what has happened, search online to find out more about Optical Character Recognition of texts**

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

OCR text derived from digitised books published 1890 - 1899. ALTO XML. British Library (2014). DOI: [10.21250/db12](https://dx.doi.org/10.21250/db12)

19th Century Books - Book Metadata - 01/09/2013. British Library (2014). DOI: [10.21250/DB21](https://dx.doi.org/10.21250/DB21)

James Baker and Ian Milligan, 'Counting and mining research data with Unix', *The Programming Historian* ([2014](http://programminghistorian.org/lessons/research-data-with-unix)

Ian Milligan and James Baker, 'Introduction to the Bash Command Line', *The Programming Historian* ([2014](http://programminghistorian.org/lessons/intro-to-bash))

William J. Turkel, 'Basic Text Analysis with Command Line Tools in Linux' ([15 June 2013](http://williamjturkel.net/2013/06/15/basic-text-analysis-with-command-line-tools-in-linux/). The section 'Shell: Free Text' is adapted from this and shared under a [Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported](http://creativecommons.org/licenses/by-nc-sa/3.0/).