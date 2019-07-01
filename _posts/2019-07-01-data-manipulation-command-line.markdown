---
layout: single
title:  "Data manipulation from the UNIX command line"
date:   2019-07-01 20:00:00 +0100
categories: analytics
header:
    overlay_image: /assets/images/data-cmd.jpeg
    show_overlay_excerpt: false
    overlay_filter: rgba(0, 73, 101, 0.3)
    teaser: /assets/images/data-cmd-teaser.jpeg
---

In this article I'm going to demonstrate various tools from the UNIX command line which can be used for effective data manipulation. This guide is written mainly for absolute beginners, but hopefully it will also provide useful information for seasoned data scientists and data engineers. 

## What is the Command line?

The UNIX command line (also called the UNIX shell) is a user interface which enables interaction with (Unix-like) operating systems using text-based commands. 

To run a command, you just type it in with the keyboard and then press the *ENTER* key. 

It is both an *interactive interpreter* (executes commands that you type in) and a *scripting language* (runs shell script from a file). To access the command line typically a *terminal emulator* program is used (Linux Console, Terminal, xterm, Konsole, iTerm2,...).

## Command line basics

The command line comes with various commands to navigate the file system, get information about the system and work with files.

### First steps

- **whoami** : Displays the name of the current user.
```bash
$ whoami
miroslav
```
- **hostname** : Displays the the current computer's host name and domain name.
```bash
$ hostname
HOME-PC
```
- **echo** *[string]* : Display a line of text.
```bash
$ echo hello
hello
```
- **history** : Displays the history of the commands typed in by the current user. *Note: You can also search the history by pressing the key combination CTRL+R.*

### Getting help

- **man** *[command]* : Opens the manual page for a specific command. Example usage:
```bash
$ man whoami
```
**To exit the manual press Q**

> This guide does not cover all of the existing options and features of the commands. To get all the details please use the ``` man ``` command above.

> Also this guide does not cover all the possible commands as this depends on what software is installed on the system.

### Navigation and file operations

- **pwd** : Display current directory location.
```bash
$ pwd
/home/miroslav/stuff/
```
- **cd** *[path]* : Change the current directory to the directory specified as *path*. Note that also relative paths can be used and also there are a few special symbols:
    * current directory: ``` . ```
    * parent directory: ``` .. ```
    * home directory: ``` ~ ```
    * Example:
```bash
$ cd ~/stuff
$ pwd
/home/miroslav/stuff/
```

- **ls** : List the contents of the current directory.
- **ls** *[path]* : List the contents of the specified directory.
```bash
$ ls ~/stuff
file1 file2 file3
```
- **ls -lf** : List the directory contents with details.
```bash
$ ls -lf ~/stuff
total 0
drwxr-xr-x    4 miroslav  staff   128 Jun 25 13:48 .
drwxr-xr-x+ 130 miroslav  staff  4160 Jun 25 13:48 ..
-rw-r--r--    1 miroslav  staff     0 Jun 25 13:48 file2
-rw-r--r--    1 miroslav  staff     0 Jun 25 13:48 file1
```
- **mkdir** *[path]* : Create a new directory in the specified path.
- **touch** *[path]* : Create a new empty file in the specified path.
- **cp** *[source]* *[target]* : Copy a file or a folder (with the ``` -r ``` switch) from the *source* to *target*. Relative paths also work here just like in the ```cd ``` command. Note there is an additional symbol called the wildcard ``` * ``` which is useful for selecting multiple files.
```bash
$ cp file8.txt stuff/
$ cp -r stuff2 stuff/
$ cp -r *.txt texts/
```
- **mv** *[source]* *[target]* : Move a file or rename from the *source* to *target*. This command also supports relative paths just like ``` cp ```.
```bash
$ mv file8.txt stuff/
$ mv file9.txt file10.txt
```

- **find** *[directory]* *[options]* : Search for files in the directory.
```bash
$ find ./stuff/ -name file*
./stuff//files.txt
./stuff//file2.txt
./stuff//file1.txt
./stuff//file4.txt
```

- **rm** *[path]* : Delete a file. For deleting directories use the ``` -r ``` switch.
```bash
$ rm file8.txt
$ rm -r stuff2/
```
> **Warning:** There is no recycle bin, so be careful when deleting files and directories.

### Reading files

- **cat** *[file]* : Display the whole content of a file. This command can also be used to concatenate multiple files and creating new files.
```bash
$ cat file1.txt
file1 text
$ cat file1.txt file2.txt
file1 text
file2 text
```

- **cat** > *[file]* : Cat can also be used to type in a new file. To exit the editor press **CTRL + C**
```bash
$ cat > newfile.txt
hello
hi
hola
```

- **head** *[file]* : Displays lines at the beginning of the file. Number of lines can be specified with the ``` -n ``` option.
```bash
$ head -n 2 file8.txt
line1
line2
```
- **tail** *[file]* : Displays lines at the end of the file. Number of lines can be specified with the ``` -n ``` option.
- **less** *[file]* : View contents of a file one page at a time. Allows forward and backward scrolling through the file as well as searching in the file. Ideal for opening very large files that do not fit into memory. You can use the arrow keys to scroll. **To exit press Q**.

## Advanced usage

- **wget** *[url]* : Download a file from an url address.

``` bash
$ wget https://ocw.mit.edu/ans7870/6/6.006/s08/lecturenotes/files/t8.shakespeare.txt
--2019-06-25 14:39:24--  https://ocw.mit.edu/ans7870/6/6.006/s08/lecturenotes/files/t8.shakespeare.txt
Resolving ocw.mit.edu (ocw.mit.edu)... 104.125.20.72
Connecting to ocw.mit.edu (ocw.mit.edu)|104.125.20.72|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5458199 (5.2M) [text/plain]
Saving to: ‘t8.shakespeare.txt’

t8.shakespeare.txt  100%[===================>]   5.21M  10.7MB/s    in 0.5s    

2019-06-25 14:39:25 (10.7 MB/s) - ‘t8.shakespeare.txt’ saved [5458199/5458199]
```

- **tar** *[options]* *[archive]* *[directory]*: Tar is the standard archiving utility in Unix-like operating systems. Depending on the type of compression there are various options to use. The most common are:
    * **create gzip archive** : ```-cvzf```
    * **create bzip archive** : ```-cvjf```
    * **extract gzip archive** e.g. file.tar.gz : ```-xvzf```
    * **extract bzip archive** e.g. file.tar.bz2 : ```-xvjf```

- **tar examples:** In the first line the *to_archive/* directory is compressed into *archive.tar.gz*. In the second line the file is extracted.
``` bash
$ tar -cvzf archive.tar.gz to_archive/
$ tar -xvzf archive.tar.gz
```

- **grep** *[expression]* *[file]* : Processes files line by line and returns the lines where the expression term has been matched. The main strength of the tool is the support for [Regular Expressions](https://en.wikipedia.org/wiki/Regular_expression). You can play around with Regular Expressions on [Regex 101](https://regex101.com/).
```
$ grep 'princess' t8.shakespeare.txt
    And leave eighteen. Alas, poor princess,
    And here the bracelet of the truest princess
    Teach you our princess English?
    Shall be call'd queen, but princess dowager
    An aged princess; many days shall see her,
    Holds hand with any princess of the world.
    The best I had, a princess wrought it me-
    Kent. Kind and dear princess!
    ...
```

- **|** : The pipe operator is used to chain output from one command to the input of another command or program. Example search for files and directories with a specific name:
``` bash
$ ls | grep stuff
stuff1
stuff2
```

- **>** : The redirect operator is used to pass the output to either a file or stream. Single arrow indicates that you wish to overwrite the file if it exists, while the double arrows ``` >> ``` are used to append to an existing file. 
```bash
$ ls > files.txt
```

- **wc** *[options]* *[file]* : Counts the number of lines ``` -l ```, characters ``` -m ``` or words ``` -w ``` in a file.
```bash
$ wc -l t8.shakespeare.txt
  124456 t8.shakespeare.txt
$ wc -m t8.shakespeare.txt
 5458199 t8.shakespeare.txt
$ wc -w t8.shakespeare.txt
  901325 t8.shakespeare.txt
```

- **bc** : Command line calculator. To exit the program type ``` exit ```.
```bash
$ bc
123+333
456
exit
```

- **seq** *[range]* : Generate a sequence of numbers.
```bash
$ seq 6
1
2
3
4
5
6
```

- **sort** *[file]* : Rearrange the lines in a text file so that they are sorted, numerically and alphabetically.
```bash
$ sort data.txt
apples
bananas
kiwis
oranges
pears
```

- **uniq** : Returns unique lines from the sorted input. The command can be used to display all the unique lines ``` -u ``` or duplicate lines ``` -d ``` from a file.
```bash
$ sort data.txt | uniq -u
bananas
kiwis
oranges
$ sort data.txt | uniq -d
apples
pears
```

- **cut** *[options]* *[file]* : Select columns from output of a program. It is possible to use bytes ``` -b ```, columns ``` -c ```, field number ``` -f ``` or a specific delimiter ``` -d ```. In the first example below ``` 2- ``` means cut everything from the second byte until the end of line. In the second example there is the opposite ``` -2 ``` cut everything from the beginning to the second byte.
```bash
$ cut -b 2- data.txt
pples
ranges
ears
iwis
ananas
$ cut -b -2 data.txt
ap
or
pe
ki
ba
```

- **comm** *[file1]* *[file2]* : Compare two sorted files and write to standard output: the lines that are common, plus the lines that are unique.
```bash
$ comm file1.txt file2.txt
file1 text
            file2 text
```

- **cmp** *[file1]* *[file2]* : Compares two files byte by byte and helps to find out if two files are identical.
```bash
$ cmp file1.txt file2.txt
file1.txt file2.txt differ: char 5, line 1
```

- **diff** *[file1]* *[file2]* : Diff stands for difference. This command is used to display the differences in the files by comparing the files line by line.
```bash
$ diff file1.txt file2.txt
1c1
< file1 text
---
> file2 text
```

- **paste** *[options]* *[file1]* *[file2]* : Used to join files horizontally (parallel merging) by outputting lines consisting of lines from each file. A delimiter can be specified with the ``` -d ``` flag.
```bash
$ paste file1.txt file2.txt
id  value
10  12
$ paste -d "," file1.txt file2.txt
id,value
10,12
```

- **split** *[options]* *[file]* : Split file into specified chunks.
```bash
$ split -b 20M output.log
```

## Awk

- **awk** *[options]* '*[code]*' *[file]* : Awk is a pattern-directed scanning and processing language.

Awk is a standard tool on every UNIX system. It is very useful for text-processing tasks and other scripting needs. The syntax of the language is similar to the C programming language, but without mandatory semicolons, manual memory management, or static typing. 

It excels at text processing. It can be used from the command line or as a stand-alone scripting language.

> In this guide I'm going to show only a few useful features of this language. For a more complete tutorial please visit the [Awk Tutorial](http://www.grymoire.com/Unix/Awk.html).

> A very quick introduction to the Awk language can also be found here: [https://learnxinyminutes.com/docs/awk/](https://learnxinyminutes.com/docs/awk/).

In the command line the Awk code needs to be placed between quote characters ``` ' ' ```.

**Example:** *Print words from a file which are longer than 5 characters*

```bash
$ cat words.txt
brown
tree
craftsmanship
book
beautiful
existence
ministerial
computer
town

$ awk 'length($1) > 5' words.txt
craftsmanship
beautiful
existence
ministerial
computer
```

AWK is a **line oriented language**. It divides a file into lines and line is broken up into a sequence of fields. These fields can be accessed using the variables like: ``` $1 ``` which represents the first field, ``` $2 ``` the second and so on. 
The ``` $0 ``` variable refers to the line.

The ``` length() ``` function above is also a part of the language. There are many useful built-in functions and variables.
In the example below, the built-in variable ``` NR ``` contains the current line which is being processed.

**Example:** *Return every second line from a file*

```bash
$ awk 'NR % 2 == 0 {print}' words.txt
tree
book
existence
computer
```

**Example:** *Print line numbers for each line in a file using the NR variable*

```bash
$  awk '{print NR, $0}' words.txt
1 brown
2 tree
3 craftsmanship
4 book
5 beautiful
6 existence
7 ministerial
8 computer
9 town
```

**Example:** *Search for a pattern*


```bash
$ awk 'match($0, /^[c,b]/)' words.txt
brown
craftsmanship
book
beautiful
computer
```

The ``` match() ``` function above is another useful built-in function which also supports regular expressions.
Match takes 2 parameters. The first one ``` $0 ``` represents the current line of text.
The second parameter is the regular expression ``` /^[c,b]/ ``` which matches with the characters ``` c ``` or ``` b ``` if they are at the beginning of the line.

**Example:** *Number of lines from two files*

```bash
$ awk 'END {print NR}' words.txt words2.txt
36
```

``` BEGIN ``` and ``` END ``` are special patterns in the language which are executed before and after every line has been processed. The example above demonstrates the use of ``` END ```. It will print only once after all lines have been processed and returns 36 which is actually the number of lines in both files together.

**Example:** *Using BEGIN to create a header*

```bash
$ awk 'BEGIN {print "id,name"}' users.txt
id,name
1,John
2,Tom
3,Jane
```

**Example:** *Replacing text with Awk*
```bash
$ echo "Hello John" | awk '{$2="Miroslav"; print $0}'
Hello Miroslav
```

In the example above we have reassigned the ``` $2 ``` (second field) with our own word and printed the result. We can do this with any file and even define complex rules for replacement.

**Example:** *Replacing the field separator*

```bash
$ echo "one,two,three" | awk '$1=$1' FS="," OFS=":"
one:two:three
```

The above example uses two additional parameters: 
* ``` FS ``` which tells Awk what is the field separator in the input data. (Alternatively ``` -F"," ``` could have been used)
* ``` OFS ``` which is the output field separator.

> Note that the default field separator in Awk is whitespace and using the FS and OFS parameters we can change it to whatever we want.

**Example:** *Using Awk to calculate fields*

```bash
$ echo "2,4,6" | awk -F"," '{print $1 * 2, $2 * 3, $3 * 4}' OFS="," 
4,12,24
```

The example above shows how Awk can deal with numerical text data and do some calculations with it.
The text ``` "2,4,6" ``` is split by the ``` , ``` and then each field is multiplied by a different number.
* The first field ``` $1 ``` contains 2 and the calculation is 2 * 2 = 4
* Second field ``` $2 ``` contains 4 and the calculation is 4 * 3 = 12
* Third field ``` $3 ``` contains 6 and the calculation is 6 * 4 = 24

Please take a while to understand this concept as it is very useful for working with large CSV files which might be too big to do this calculation in Excel.

> To learn about CSV files please check [https://en.wikipedia.org/wiki/Comma-separated_values](https://en.wikipedia.org/wiki/Comma-separated_values).

## Sed

- **sed** *[options]* '*[code]*' *[file]* : Stream editor.

Sed is another standard UNIX command line tool. The name stands for stream editor and it can perform various functions on files like, search, find and replace, insert or delete. The most common usage is substitution of text in files (by using special patterns) without even opening them.

> For a more detailed tutorial please check the [Sed Tutorial](http://www.grymoire.com/Unix/Sed.html).

**Example:** *Substitution of word in a file*

```bash
$ cat fruit.txt
apples are great

$ sed 's/apples/oranges/' fruit.txt
oranges are great
```

Here the ``` s ``` specifies the substitution operation. The ``` / ``` are delimiters. The text ``` apples ``` is the search pattern and the text ``` oranges ``` is the replacement string.

**Example:** *Replacing the Nth occurrence*

```bash
$ cat fruit.txt
apple apple apple apple
$ sed 's/apple/orange/3' fruit.txt
apple apple orange apple
```
**Example:** *Replacing all the occurrences*

```bash
$ cat fruit.txt
apple apple apple apple
$ sed 's/apple/orange/g' fruit.txt
orange orange orange orange
```

The ``` g ``` parameter means global as oposed to the previous example where we used ``` 3 ``` to substitute only the 3rd occurrence.

**Example:** *Add parentheses around a word*

```bash
$ sed 's/apple/(&)/3' fruit.txt
apple apple (apple) apple
```

**Example:** *Add a prefix to a word*

```bash
$ sed 's/apple/pine&/3' fruit.txt
apple apple pineapple apple
```

The ``` & ``` pattern represents the current match and in the examples we are using it to add parentheses and a prefix.

**Example:** *Keeping part of the match*

```bash
$ echo abcd123 | sed 's/\([a-z]*\).*/\1/'
abcd
```

The ``` \1 ``` means the first remembered pattern. Sed has up to nine remembered patterns.
We can use that to remove duplicate words.

**Example:** *Remove duplicated words*

```bash
$ echo "hello hello world" | sed 's/\([a-z]*\) \1/\1/'
hello world
```

## Practical one-liners

In this section I am going to show a few practical command combinations which should fit into a single line.

**Example:** *Combine multiple CSV files which have the same header*

```bash
$ head -2 file1.txt > all.txt; tail -n +3 -q file*.txt >> all.txt
```

Explanation: The first part saves the header to the file ``` all.txt ```. Then all the files are concatenated into the file by using the ``` tail ``` command to skip the header.

**Example:** *Filtering a CSV using Awk*

```bash
$ awk -F"," '/text/' source.csv > filtered.csv
```

Explanation: The command above will output only those lines from ``` source.csv ``` to ``` filtered.csv ``` where the term ``` text ``` was found.

**Example:** *Count observations in a CSV file based on condition on a specific column*

```bash
$ awk -F"," '$5 > 40' all.csv | wc -l
1857
```

Explanation: In the example above, we are counting the lines in the CSV file where the value in the 5th column is higher than 40.

**Example:** *Add a new column to a CSV file*

```bash
$ cat data.csv
model,type,price
A,basic,10
B,extended,22
C,premium,45

$ awk -F"," '{ if(NR == 1) {print $0,"price_doubled"} else {print $0,$3 * 2}}' OFS="," data.csv > newdata.csv

$ cat newdata.csv
model,type,price,price_doubled
A,basic,10,20
B,extended,22,44
C,premium,45,90
```

Explanation: In this example a new column named ``` price_doubled ``` is calculated by multiplying the ``` price ``` column ```$3``` by 2. The conditional statement ``` if(NR == 1) ``` in the Awk code makes sure that the header value ``` price_doubled ``` is printed in the first line and the values are calculated in the ``` else ``` block on the next lines. The new column is added to the original data. The resulting CSV is then stored as ``` newdata.csv ```.

## Basic Shell scripting

A shell script is a file containing code designed to be run by the command line interpreter. From this point of view, the command line can be viewed as an interpreter of the scripting language. Writing shell scripts is very useful for automation of repeating sequences of commands and also for writing small programs.

A script is basically a plain text file containing code which is directly executable in the command line. No compilation to an executable file format is needed as the file is basically interpreted line by line by the shell.

> The default shell in Linux, Mac OSX and other Unix-like systems is called **Bash** and many times the language used is called **Bash** as well. The terms **"shell script"** and **"bash script"** are often used interchangeably. To find out more please check here: [https://en.wikipedia.org/wiki/Bash_(Unix_shell)](https://en.wikipedia.org/wiki/Bash_(Unix_shell)).

> A quick introduction to Bash can be found here: [https://learnxinyminutes.com/docs/bash/](https://learnxinyminutes.com/docs/bash/).

### Basics of Bash

> Bash is the worst scripting language except for all the others :)

### Shebang

This is a special identifier at the very first line in the file which is there for the operating system to recognize that a file is a bash script and not just some plain text document. There are many different ways to define the shebang. The most portable ways are the following:

```bash
#!/usr/bin/env sh
```
or
```bash
#!/usr/bin/env bash
```

> More about shebang here: [http://en.wikipedia.org/wiki/Shebang_(Unix)](http://en.wikipedia.org/wiki/Shebang_(Unix))

### Comments

Comments are lines of text that will be ignored by the interpreter. They are useful for documenting the code or including additional information for the readers of the script. Also the shebang is actually a comment. Here is an example script that contains just comments:

```bash
#!/usr/bin/env bash

# hello there! welcome to my script!
# this is another comment
```

When the example above is executed nothing will be printed out on the screen.

### Hello, World!

Typically the first step in learning a new programming language is the obligatory *"Hello, World!"* program. This program prints the text ``` Hello, World! ``` to the screen.

First step is to create a new file ``` hello.sh ``` with the following code:

```bash
#!/usr/bin/env bash
echo "Hello, World!"
```

Before the script can be run it has to be set as executable with the following command:

```bash
$ chmod +x hello.sh
```

> Note: This is needed for all the scripts that you create to make them executable.

After that it can be executed by simply calling the name of the file in the command line:

```bash
$ ./hello.sh
Hello, World!
```

### Variables and the if statement

```bash
#!/usr/bin/env bash
Name="Miro"

if [ "$Name" == "Tom" ]
then
    echo "Your name is Tom."
else
    echo "Your name isn't Tom. It's $Name."
fi
```

The above example shows multiple features of bash scripts:
* Creating a new variable ``` Name="Miro" ```. This is also called a naked variable and there should be no spaces around ``` = ```.
* The ``` if ``` statement is used for conditional logic. In this example the condition is seen in the brackets ``` [ $Name == "Tom" ] ```.
* If the condition is **true** then ``` echo "Your name is Tom" ``` is executed.
* If the condition is **false** the ``` else ``` part ``` echo "Your name isn't Tom. It's $Name" ``` is executed.
* In bash the ``` if ``` statement needs to be ended with a ``` fi ``` keyword.

Try changing the value of ``` Name="Miro" ``` above to ``` "Tom" ``` to see the other result.

> Note the space and quote positions in the above script. Misplacing a space or a quote might cause the script to stop working. Many times these bugs are hard to spot.

### Loops

Loops are a useful construct for repeating certain statements for multiple times. Otherwise the command would have to be copy-pasted many times and that would result in code which is very hard to maintain. Below are few examples how to use loops with variables which increment on each iteration.

```bash
#!/usr/bin/env bash
# range based loop
for a in {1..3}
do
    echo "$a"
done

# traditional for loop
for ((b=1; b <= 3; b++))
do
    echo $b
done

# while loop with condition; -lt means "less than"
c="0"
while [ $c -lt 4 ]
do
    echo $c
    c=$[$c+1] # increment the c variable
done

# infinite while loop with a break condition
d="0"
while [ true ]
do
    echo $d
    d=$[$d+1] # increment the d variable
    if [ $d -gt 3 ] # if d is greater than 3
    then
        break # breaks out of the infinite loop
    fi
done
```

### Functions

The code can be organized into executable functions. These can be called the same way as the built in commands. The example below shows a custom function which multiplies it's parameter by 3 and prints the result to the screen.
A function can also return a result by using the ``` return ``` statement.
Note that function parameters are referenced to as ``` $1 ```, ``` $2 ```, ``` $3 ``` and so on.

```bash
#!/usr/bin/env bash

function multiply_and_print ()
{
    result=$[$1 * 3]
    echo "The result is $result"
    return $result
}

multiply_and_print 10
```

### Useful scripts

The constructs mentioned above are the basis on which more useful and complex scripts can be built. 

**Example:** *Reading user input*

```bash
#!/usr/bin/env bash
echo "Enter Your Name"
read name
echo "Welcome $name"
```

**Example:** *Test if file exists*

```bash
#!/usr/bin/env bash
filename=$1
if [ -f "$filename" ]
then
    echo "File exists"
else
    echo "File does not exist"
fi
```
Note that in this case ``` $1 ``` refers to the argument given to the script from the command line e. g. ``` ./check_file.sh myfile.txt ```.

**Example:** *Enumerate files in the current directory*

```bash
#!/usr/bin/env bash

i=0
for FILE in $PWD/*; do
   i=$[$i + 1]
   echo "$i: $FILE"
done
```

Here ``` $PWD ``` is a special built in variable which is similar to the ``` pwd ``` command.

### Example: Address Book

```bash
#!/usr/bin/env bash

# The file to save the data
DATA="address-book.txt"

# Input the name, address and phone number
echo -n "Name of person: " 
read name
echo -n "Address: "
read address
echo -n "Phone number: "
read phone

# Ask user for confirmation
echo "Save the new contact:"
echo -e "$name ; $address ; $phone \n"
echo -n "y/n: "
read answer

if [ "$answer" == "y" ] 
then
    echo "$name ; $address ; $phone" >>$DATA
else
    echo "The contant was not saved."
fi
```

The example above is a simple script which asks the user for new contact information. After entering the details the user can confirm or decline a new entry into the Address book. If the user chooses ``` y ``` the entry is appended into the file ``` address-book.txt ```.

## Conclusion

I believe that the examples provided in this guide will be a good starting point to those people who want to know more about the command line, Awk, Sed and Shell scripting. I hope this guide gives you some useful information and also inspires you to use the command line as a useful tool for many data related tasks.
