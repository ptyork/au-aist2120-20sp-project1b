# Project 1b: Word Mirror 

This is a simple little utility with a twist. I can't really think of a useful purpose for this particular script in real life, but the general concept of parsing and modifying a file word-by-word is VERY useful. Regardless, the goal is to reverse the letters of each individual word in a given input file. 

The script, `rorrim.py`, should: 

1. Open the file specified as the first argument to the script (see below)
2. Read the file one line at a time (i.e., for line in file)
3. Split the contents of each line into words (no argument passed to split so you split on whitespace)
4. Iterate over each word
    4a. Mirror the word
    4b. Append the translated word (and a blank space)to a string
5. Print the mirrored string to the screen

## CONSIDERATIONS

1. If a "word" is empty or just whitespace, return nothing.

2. When translating a "word", be careful to check for punctuation and deal with that correctly. Especially words followed by periods, commas, etc. But also words starting or ending with quotation marks. Pay attention to periods, question marks, exclamation points, commas, quotation marks, semi-colons, and dashes. E.g.:
    - battle, ==> elttab,
        * __not__ ,elttab
    - "rejoicing ==> "gniciojer
        * __not__ gniciojer"
    - tribulation," ==> noitalubirt,"
        * __not__ ",noitalubirt

3. If a "word" is __JUST__ punctuation (like em dash "--"), then just return the word untranslated.

## HINTS 

1. The "arguments" to a python program are in the sys.argv list. The first element in the list is the name of the script and the rest are any additional words (arguments) added to the end. [See here for explanation](https://www.tutorialspoint.com/python/python_command_line_arguments.htm). The code needed may look as follows:
```
import sys

filename = sys.argv[1]
```

2. For consideration #2 above, you might start off your to_piglatin function by creating prefix and suffix strings. Start each as an empty string. Then "move" each punction character from the beginning of the word to the prefix string and any from the end to the suffix string. Then at the end, concatenate and return prefix + word + suffix. For example, the first part (moving the prefix characters) may look similar to:
```
    punctuation_chars = '.?!,\'"():;-'
    prefix = ''
    while len(word) > 0 and word[0] in punctuation_chars:
        prefix = prefix + word[0]
        word = word[1:]
```

## REQUIRED IMPLEMENTATION NOTES 

1. You MUST abstract your most useful logic by creating a function named `mirror_me` that takes a word and returns the reversed version (properly handling the punctuation issue outlined above). This function should be "called" as your step 4a above, which will make the main script much cleaner. In other words, the main part of your script should open the file, loop through each line, split the line into words, and iterate over the words, and the following function MUST be defined in your script and called to reverse each individual word: 

``` 
        def mirror_me(word): 
          ... REVERSE THE WORD ...
          return word
``` 

2. You MUST modify kennedy.txt, replacing John F. Kennedy's name with your own. JUST edit and save the file using VS code or another text editor. No Python code required here.

3. You MUST then mirror `kennedy.txt` and redirect the output to `backwards_kennedy.txt`. In other words, you should run `python rorrim.py kennedy.txt > backwards_kennedy.txt`. This mirrored file should be in your final submission. __DO NOT WRITE TO A FILE INSIDE OF YOUR SCRIPT. ONLY READ AND PRINT. WRITING OCCURS HERE BY REDIRECTING OUTPUT.__

Note: If you do output redirection in Windows Powershell (the default shell for VS Code), it outputs writes the file using Unicode, which can cause issues. Use a standard Command Prompt (cmd.exe) if running this in Windows. Should not have any issues on Mac or Linux (and thus Mimir).

When done, be sure to test the heck out of this and then submit the __project1 directory__ in Mimir.

## OPTIONAL CHALLENGES 

1. If the original word was title case, make the reversed word title case, as well. In other words "Kennedy" would become "Ydennek".

2. Create a second version of the script, rorrim2.py. This version should import the mirror_me function from rorrim (`from rorrim import mirror_me`). Instead of asking for a file name and reading the text from the file, instead read in the text line-by-line from sys.stdin. This should allow you to run it interactively AND to pipe in text from another command (e.g., `type kennedy.txt | python rorrim2.py`). 

3. Instead of mirroring the words, scramble them. In other words, use every letter, but randomly. This is challenging, but doable. You will need to use the randint() function from the random module. Hint: consider converting each word to a list of characters and then "pop()" a letter from a random location in the word until all characters are used. Assuming your list of characters in called word, something like `ch = word.pop(randint(0,len(word)))` might be useful code here.
