# bib (a CLI Bible reference tool)

bib is a CLI program that quickly prints Bible verses to the Terminal, using markdown files for the Bible generated by my [BibleGateway-to-Obsidian script](https://github.com/prestonharberts/biblegateway-to-obsidian).

> 🌟 **Included to download in this repo is the NET translation** 🌟 See Usage below. This is made possible by the [NET translation team's generous copyright](https://netbible.com/copyright/) which allows me to redistribute it for free to you all.

If you would like to use another translation, see Other Translations near the bottom of this page. Translation support may vary as this program relies on BibleGateway-to-Obsidian.

- [Features](#features)
- [Setup](#setup)
- [Usage](#usage)
  - [Example](#example)
  - [Copying text](#copying-text)
  - [Scaling demonstration](#scaling-demonstration)
  - [Random Bible verses](#random-bible-verses)
- [Other translations](#other-translations)
- [Todo](#todo)

## Features

- Verse-by-verse format
- Specified verse is shown in red
- Editorial headings are kept intact
- New paragraphs are shown with an arrow
- Ability to view multiple verses or a verse section
- All common book abbreviations are supported
- Certain translation show words in italic, and I put them in brackets here
- Hyphenated text to give the appearance of justified text alignment
- Works on a variety of terminal sizes

Also included is the program `bibr` (credit to [w1ldrabb1t](https://github.com/w1ldrabb1t)), that lets you randomly print a Bible verse to your terminal. See [Random Bible verses](#random-bible-verses) for more information.

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

Finally, move the included Bible folder or one generated by [BibleGateway-to-Obsidian](https://github.com/prestonharberts/biblegateway-to-obsidian) to the same folder you moved bib to. More instructions on using another translation can be found below in Other Translations.

## Usage

Here are some example usecases. By default, the previous and next 2 verses are also printed to show context. The specific verse you request is printed in red to stand out from the context verses.

> Both the full name of the book as well as abbreviations work with bib. All supported can be found [here (Logos)](https://www.logos.com/bible-book-abbreviations).

```bash
# this prints the entire Genesis 1 chapter
bib gen1

# this prints just Genesis 1:1 (and context verses Genesis 1:2-3)
bib gen1 1

# this prints the verses Genesis 1:1-2 (no context verses are printed)
bib gen1 1 2

# this prints John 3:16 (without any context verses)
bib -c john3 16
```

### Example

Here is an example of the program running with the included NET translation.

<p align=center><img src="https://github.com/user-attachments/assets/f2b1c09d-7df5-4035-ba93-d902ddf9cb21" width="512"></p>

### Copying text

Included in this repo is a program `bibcopy` that copies entire chapters at a time, reformats them, and lets me paste them into [Monkeytype](https://monkeytype.com/). It's formatted to be very minimal and looks like this in the NET translation:

<p align=center><img src="https://github.com/user-attachments/assets/573e279f-234e-463c-b559-f6b199ca468b" width="512"></p>

Support to automatically copy what you see with Bib isn't fully supported, but it would be done like this if you can remove the color codes that get introduced with my code. Just make sure to install `xclip`.

```bash
bib john3 16|xclip -sel clipboard
```

I recommend just running bib multiple times in a row similar to this, and then just copying the output from the terminal:

<p align=center><img src="https://github.com/user-attachments/assets/aec021e4-a29e-4674-afb0-52f3fb0f3bc5" width="512"></p>

### Scaling demonstration

One of my favorite features of this program and one that I spent a bit of time on is the "pseudo" text justification along with hyphenating words when a word goes off the screen, so it scales very well on various terminal widths. It catches a lot of edge cases that I painstakingly sought out and covered with regex, such as when character 80 of an 80-width terminal is `)` but is followed by a comma, it will hyphenate the word that is before the `)`. Below are some picture of what this bib looks like on different terminal sizes. 

<p align=center><img src="https://github.com/user-attachments/assets/52da7b37-f75b-4403-8c74-4ef9bb9ebf2b" width="768"></p>

### Random Bible verses

The included script bibr by [w1ldrabb1t](https://github.com/w1ldrabb1t) will randomly print a Bible verse to your terminal using bib. It does so by finding the last verse in a file, generating a number between 1 and x, and then calling bib.

To use, put bibr in the same directory as bib and the Bible folder, ideally in your PATH (see [Setup](#setup)).

Use the option `-c` to hide context verses like bib. There is also the option `-v` to enable verbose mode which will show the bib command it executes.

> Someday in the future, bibr will be a feature of bib and be run with `bib -r`.

<p align=center><img src="https://github.com/user-attachments/assets/c2765797-9e9e-43ed-8412-f58865dde872" width="512"></p>

A cool way to run this script and a fun way to find any [Issues](https://github.com/prestonharberts/bib/issues) is to run this:

```bash
for i in {1..1000}; do bibr; done
```

## Other Translations

If you would like to use another translation, please use my [BibleGateway-to-Obsidian script](https://github.com/prestonharberts/biblegateway-to-obsidian) to generate a new Bible (also be aware that not all translations will work with either bib or BibleGateway-to-Obsidian). Once it has, move only the Scripture folder to this repository, and rename it to `bible` (lowercase). Run the following from this folder to make the files compatible with this program:

```
chmod u+x ./bg2ob-to-bib
./bg2ob-to-bib
```

Now you can move the Bible folder to `~/Bin`, and bib is ready to be used.

## Todo

- [ ] Help menu [(1)](https://www.reddit.com/r/bash/comments/1j7qfl3/comment/mh3k4wv/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Make bibr an option in bib
- [x] Abbreviations list [(1)](https://www.reddit.com/r/bash/comments/1j7qfl3/comment/mh3k4wv/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [x] Add instructions if `Bin` path is different [(1)](https://www.reddit.com/r/bash/comments/1j7qfl3/comment/mh0m7pw/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [x] Symbolic link to script [(1)](https://www.reddit.com/r/commandline/comments/1j7qew9/comment/mh2lwgk/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Other language support [(1)](https://www.reddit.com/r/commandline/comments/1j7qew9/comment/mh39p9b/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Favorites [(1)](https://www.reddit.com/r/commandline/comments/1j7qew9/comment/mh67ax6/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Switch from markdown to XML [(1)](https://www.reddit.com/r/bash/comments/1j7qfl3/comment/mh44sjb/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
- [ ] Type `bib` to enter a console so you don't have to type bib for every verse you want
