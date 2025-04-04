# bib (a CLI Bible reference tool)

bib is a CLI program that quickly prints Bible verses to the Terminal, using markdown files for the Bible generated by my [BibleGateway-to-Obsidian script](https://github.com/prestonharberts/biblegateway-to-obsidian).

> 🌟 **Included to download in this repo is the NET translation** 🌟 See Usage below. This is made possible by the [NET translation team's generous copyright](https://netbible.com/copyright/) which allows me to redistribute it for free to you all.

If you would like to use another translation, see Other Translations near the bottom of this page. Translation support may vary as this program relies on BibleGateway-to-Obsidian.

- [Features](#features)
- [Setup](#setup)
- [Usage](#usage)
  - [Example](#example)
- [Other features](#other-features)
  - [User configuration](#user-configuration)
  - [Printing multiple verses](#printing-multiple-verses)
  - [Copying text](#copying-text)
  - [Scaling demonstration](#scaling-demonstration)
  - [Searching with bibs](#searching-with-bibs)
  - [Random verses with bibr](#random-verses-with-bibr)
- [Other translations](#other-translations)
- [Termux](#termux)
- [Todo](#todo)

## Features

- Verse-by-verse format
- Specified verse is shown in red
- Editorial headings are kept intact
- New paragraphs are shown with an arrow
- Ability to view multiple verses or a verse section
- All common book abbreviations are supported
- Interactive CLI mode lets you just type book, chapter, and verse without having to type bib
- Certain translation show words in italic, and I put them in brackets here
- Hyphenated text to give the appearance of justified text alignment
- Works on a variety of terminal sizes

Also included with bib are 2 programs `bibs` and `bibr` by [w1ldrabb1t (GitHub)](https://github.com/w1ldrabb1t)

- bibs lets you search for words and phrases in the Bible and prints found results with bib. See [Searching with bibs](#searching-with-bibs).
- bibr randomly print a Bible verse to your terminal using bib. See [Random verses with bibr](#random-verses-with-bibr).

## Setup

I recommend putting this script in your PATH so that it can be called anywhere. I made a Bin folder in my user directory, moved bib to it, and added this line to my `.bashrc`:

```bash
export PATH=/home/$USER/Bin/:$PATH
```

As long as you move it to a folder in PATH, it is fine. You do not have to use the folder I use above.

Next, give execution privileges to bib. Using my folder as an example:

```bash
chmod u+x ~/Bin/bib
```

Finally, move the included Bible folder to the same folder you moved bib to. More instructions on using another translation can be found below in Other Translations.

## Usage

Here are some example usecases. By default, the previous and next 2 verses are also printed to show context. The specific verse or verses you request are printed in red to stand out from the context verses.

> Full names and abbreviations of books work in bib. Most of the common abbreviations found [here (Logos)](https://www.logos.com/bible-book-abbreviations) are supported. For the list of supported abbreviations in this script, run `bib -a`.

```bash
# this prints the entire Genesis 1 chapter
bib gen1

# this prints Genesis 1:1 (and context verses Genesis 1:2-3)
bib gen1 1

# this prints Genesis 1:1 (no context verses)
bib gen1 1 -n

# this prints Genesis 1:3-4 (and context verses Genesis 1-2 and 5-6)
bib gen1 3 4

# this prints Genesis 1:3-4 (no context verses)
bib gen1 3 4 -n
```

Any of the following formats also work thanks to extensive input formatting, and capital letters make no difference either:

```bash
# my preferred way to type into bib
bib 1cor13 4 7

# other supported formats
bib 1 Corinthians 13:4-7
bib 1st Corinthians 13:4-7
bib 1cor13:4-7
bib 1cor13:4 7
bib 1cor13 4-7
bib 1 cor 13:4-7
bib 1 cor 13:4 7
bib 1 cor 13 4-7
bib 1 cor 13 4 7
```

Verses from the same book can also be listed together with commas without having to retype the book name over again (commas and hyphens can still be replaced with spaces here):

```bash
bib matt 2:1, 28:18-20, 1:1-17, 8:5-10, 21:43
```

If you want to enter into a interactive prompt similar to Python, just run `bib` by itself, and you can enter any Bible reference without having to type bib over again. History is also supported and is stored in `~/.bib_history`.

The example from earlier would appear like this in the interactive mode:

```bash
# enter into bib interactive mode
bib

# type Bible references
>>> gen1
>>> gen1 1
>>> gen1 1 2
>>> john3 16 -n
```

### Example

Here is an example of the program running with the included NET translation in script mode and interactive mode.

<p align=center><img src="https://github.com/user-attachments/assets/d4323219-5edd-454a-9e71-02f65fa8fb0c" width="800"></p>

## Other features

### User configuration

Open bib in a text editor, and at the top are several options you can change, including the following:

- What character to use to show a new paragraph is starting
- Whether to show context verses by default
  - Enabling context by default lets you type `-n` to hide context verses
  - Disabling context by default lets you type `-c` to show context verses
- Whether to use `less` or `cat` to print bib output

### Printing multiple verses

Multiple verses can be strung together in a single line, and all of it will print, one by one. Add the context flags `-n`/`-c` after every verse you want to remove or show context verses for, or use `-N`/`-C` to hide or show all context for all verses for the current command.

This feature works in both the interactive and non-interactive modes, and the only limitation is that all books with numbers (1 Cor.) cannot have a space between the number and the book title.

```bash
>>> phil4 13 1john4 18 19 heb12 7
# different formats are also supported
>>> phil 4:13 1john 4 18-19 heb12 7
# this will run bib by itself without entering into the prompt
bib phil 4:13 1john 4 18-19 heb12 7

# hide context verses for only phil4 13
>>> phil4 13 1john4 18 19 heb12 7
>>> phil4 13 -n 1john4 18 19 heb12 7

# hide all context verses for all selected verses
>>> phil4 13 1john4 18 19 heb12 7 -N
>>> -N phil4 13 1john4 18 19 heb12 7
```

### Copying chapters

Included in this repo is a program `bibc` that copies entire chapters at a time, reformats them, and lets me paste them into [Monkeytype](https://monkeytype.com/). It's formatted to be very minimal and looks like this in the NET translation:

<p align=center><img src="https://github.com/user-attachments/assets/573e279f-234e-463c-b559-f6b199ca468b" width="450"></p>

Support to automatically copy what you see with Bib isn't fully supported, but it would be done like this if you can remove the color codes that get introduced with my code. Just make sure to install `xclip`.

```bash
bib john3 16|xclip -sel clipboard
```

I recommend just running bib multiple times in a row similar to this, and then just copying the output from the terminal:

<p align=center><img src="https://github.com/user-attachments/assets/180d111b-c2d2-4bcd-8813-116f6625074c" width="450"></p>

### Scaling demonstration

One of my favorite features of this program and one that I spent a bit of time on is the automatic hyphenation of words that go off the screen to give the text body a "pseudo" justified text alignment look, so it scales very well on various terminal widths. It catches a lot of edge cases that I painstakingly sought out and covered with regex, such as when character 80 of an 80-width terminal is `)` but is followed by a comma, it will hyphenate the word that is before the `)`. Below are some picture of what this bib looks like on different terminal sizes. 

<p align=center><img src="https://github.com/user-attachments/assets/52da7b37-f75b-4403-8c74-4ef9bb9ebf2b" width="800"></p>

### Searching with bibs

The included script bibs by [w1ldrabb1t](https://github.com/w1ldrabb1t) lets you search for a word or phrase in the Bible, and it will print the results one at a time to your terminal using bib. Multiple word phrases should be placed in quotation marks.

<p align=center><img src="https://github.com/user-attachments/assets/cf03e2f0-eb82-4daa-8f4c-2ac5e6bd09a0" width="450"></p>

### Random verses with bibr

The included script bibr by [w1ldrabb1t](https://github.com/w1ldrabb1t) will randomly print a Bible verse to your terminal using bib. It does so by finding the last verse in a file, generating a number between 1 and x, and then calling bib.

To use, put bibr in the same directory as bib and the Bible folder, ideally in your PATH (see [Setup](#setup)).

Use the options `-n` to hide context verses in bib and `-N` to hide all context for all verses if you select multiple in one line. There is also the option `-v` to enable verbose mode which will show the bib command it executes.

> Someday in the future, bibr will be a feature of bib and be run with `bib -r`.

<p align=center><img src="https://github.com/user-attachments/assets/c2765797-9e9e-43ed-8412-f58865dde872" width="450"></p>

A cool way to run this script and a fun way to find any [Issues](https://github.com/prestonharberts/bib/issues) is to run this:

```bash
for i in {1..1000}; do bibr; done
```

## Other Translations

If you would like to use another translation, please use my [BibleGateway-to-Obsidian script](https://github.com/prestonharberts/biblegateway-to-obsidian) to generate a new Bible (also be aware that not all translations will work with either bib or BibleGateway-to-Obsidian). Once it has, move only the Scripture folder to this repository, and rename it to `bible` (lowercase).

Make sure you have `perl` and `cpan` are installed on your computer using your respective package manager, then run the following:

```bash
# if first time opening just press enter to all prompts cpan will ask for
cpan
install Module::Build
install File::Rename
```

Now, run the following from this project's folder to make the files compatible with bib:

```
chmod u+x ./bg2ob-to-bib
./bg2ob-to-bib
```

Now you can move the Bible folder to `~/Bin`, and bib is ready to be used.

## Termux

This script also works in Termux for Android. Later on I explain how to set up the Termux:Widgets feature to have an app shortcut on my homescreen that opens bib in interactive mode for convenience.

First, install Termux. I choose to install Termux, Termux:Styling, and Termux:Widget from [F-Droid](https://f-droid.org/).

Once Termux has been installed, enter into the app and wait until the app sets itself up. Then, install the following dependencies:

```bash
pkg install git bash ncurses ncurses-utils jq coreutils
```

Run the following to clone the project:

```bash
git clone https://github.com/prestonharberts/bib
```

You should be able to `cd bib` to go into the folder and run `./bib` to launch my program. Try entering some Bible verses.

Now, run `cd ~` to go back to the home folder, and run `vi .bashrc` to add some settings to Bash. Paste into the file my recommended PATH, alias, and prompt string settings.

- With the PATH settings, bib can be called anywhere.
- Aliases are shortened ways to run commonly used commands. With these you can clear the screen with `c` and exit the terminal with `q`. These are also implemented into bib.
- The PS1 (prompt string 1) line changes the input field to look like my preferred layout with some color.

```bash
# PATH
if ! [[ "$PATH" =~ "$HOME/.local/bin:$HOME/bin:$HOME/bib:" ]]; then
    export PATH="$HOME/.local/bin:$HOME/bin:$HOME/bib:$PATH"
fi

# aliases
alias c='clear'
alias q='exit'

# prompt string
PS1='\[\e]0;\W\a\][\[\033[01;34m\]android \W\[\033[00m\]] $ '
```

### Termux:Widget

This section will put an app icon on your homescreen to quickly open bib with one tap. In Termux, run `mkdir ~/.shortcuts` to create a folder in your home directory that we'll use to put the script. Then (if you ran git clone earlier in the default home directory), run the following to copy the program to the shortcuts folder:

```bash
cp ~/bib/bib ~/bib/bible ~/.shortcuts
```

I recommend editing `~/.shortcuts/bib` by searching for `| less` and putting a `#` before every `|` of that search so you don't need to scroll through chapters with keys, but so you can swipe with your finger like any other app. You can then also hide the Termux extra key bar by pressing Volume Up+Q on your phone's keyboard.

I also recommend changing the first few lines of code in bib to look like this so the arrow symbol for new paragraphs appears as a pilcrow sign:

```bash
#PARAGRAPH_MARKER="↓"
PARAGRAPH_MARKER="¶"
```

Now, you can add a Termux widget to your homescreen from your phone's widget menu, and select bib. If you want it to appear as Bible instead of bib, move the script in shortcuts to be a new name with this command, and then add it again to your homescreen:

```bash
mv ~/.shortcuts/bib ~/.shortcuts/Bible
```

### Termux bg2ob-to-bib

If you want to use the bg2ob-to-bib program from Termux, you need to run `cpan` and then enter the following to install the rename tool I use in the script:

```bash
install Module::Build
install File::Rename
```

## Todo

- [ ] Help menu [(1)](https://www.reddit.com/r/bash/comments/1j7qfl3/comment/mh3k4wv/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Make bibr an option in bib
- [x] Abbreviations list [(1)](https://www.reddit.com/r/bash/comments/1j7qfl3/comment/mh3k4wv/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [x] Add instructions if `Bin` path is different [(1)](https://www.reddit.com/r/bash/comments/1j7qfl3/comment/mh0m7pw/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [x] Symbolic link to script [(1)](https://www.reddit.com/r/commandline/comments/1j7qew9/comment/mh2lwgk/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Other language support [(1)](https://www.reddit.com/r/commandline/comments/1j7qew9/comment/mh39p9b/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Favorites [(1)](https://www.reddit.com/r/commandline/comments/1j7qew9/comment/mh67ax6/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Switch from markdown to XML [(1)](https://www.reddit.com/r/bash/comments/1j7qfl3/comment/mh44sjb/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [x] Type `bib` to enter a console so you don't have to type bib for every verse you want
- [x] Allow console mode to take options
- [x] Finish writing Termux setup guide
