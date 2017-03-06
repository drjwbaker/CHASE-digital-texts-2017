## Appendix: Extra sessions in the final hour


### What is a line?

An issue from the exercises is what makes a new line in a file. The answer is that it depends on your computer's operating system (OS).

Line ending is marked by a special, non-displayable sequence:
- Mac CR carriage return \r
- *nix LF linefeed \n
- Windows CRLF carriage return linefeed \r\n

Thus, Windows files of the same content are **always** bigger than their Mac or *nix equivalents because each line ends with two bytes instead of one.

In normal working when files are processed on your machine only this difference in indicating line ending is of no consequence. Indeed, your colleagues probably have similar machines to you, so sharing files with them should not lead to problems. But if you publish your files, or use files from outside sources, you may encounter problems. The most likely symptom is to see your file's contents as one long string of text, all apparently one line. This is not the case, it is just that the program you've used to open the file does not recognise the line ending used. You can convert line endings in many ways, some programs will do it for you, or building on your work today in the Shell Free Text exercise Option 1 in which you used the `tr` command to convert spaces to new lines. In this case the new lines are represented by the *nix form of `\n`. Similarly you can convert the new lines to or from any combination as you  require.

> *nix stand to UNIX and all variants such as Linux.  
> The Mac OS is based on UNIX, which makes the change in line ending marker very annoying. 


### Encoding

**ASCII** American Standard Code for Information Interchange  
**UTF-8** Unicode (or Universal Coded Character Set) Transformation Format – 8-bit

In this additional session I gave a bit of a history lesson on ASCII and other means of encoding characters; how do computers represent internally the characters that we understand. In effect though, this is not relevant to current research except for describing the problems previously encountered when trying to work with languages other than the north American English used by the developers of many modern computer systems. All that matters for our purposes is that all the problems are solved by using utf-8.

UTF-8 allows all special characters, all diacritics modifications of basic characters and all languages to be represented in a space-efficient form. Use it for all your materials!

Here's a simple example of how a punctuation character can go awry even in a straight forward English text. 

**Sample text: Kipling’s Serving Men**

> I KEEP six honest serving-men  
(They taught me all I knew);  
Their names are What and Why and When  
And How and Where and Who.  
I send them over land and sea,  
I send them east and west;  
But after they have worked for me,  
I give them all a rest.  

> I let them rest from nine till five,  
For I am busy then,  
As well as breakfast, lunch, and tea,  
For they are hungry men.  
But different folk have different views;  
I know a person small—  
She keeps ten million serving-men,  
Who get no rest at all!

> She sends'em abroad on her own affairs,  
From the second she opens her eyes—  
One million Hows, two million Wheres,  
And seven million Whys!

In utf-8 `eyes—` renders correctly.  
The dash is an em-dash not a hyphen.  
In Windows, with a default UK locale, you’ll see `eyesâ€”`.
*Locale* is the jargon for the localisation of a machine, For example, the same physical machine can be configured for a US keyboard or a UK keyboard. In which case the letters remain in the same locations, but 

Looking at the sample tabular data from the exercise you can see many examples of the benefit of using UTF-8.

Consider this line from the BLBooks-London metadata file, and as selected when searching for *revolution*:

~~~~
BLbooks-London.tsv:014808580	|||	und			DALTON, Henry Robert Samuel.		שמעו זאת; or, the Mountain Mystery; an apocalypse proclaiming openly the deep secret of the Universe ... in its practical relation to the great social revolution, now impending over the nations of the world, as predicted by men of wisdom from early times. [In verse.] [electronic resource]		London : Remington & Co., 1878.					lsidyv34761f85
~~~~

You can see that the title includes Hebrew characters. To the computer they are just other members of the set of characters defeind by utf-8 and are useda nd displayed the same as any other. No special processing is required. They can even be mixed in the same string of text.

Or at least you will see the Hebrew characters assuming your system has been configured to display them!
