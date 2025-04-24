## bib – Termux (Android)

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
