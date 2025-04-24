## bib – Other Translations

To use a different translation, generate a new Bible with my [BibleGateway-to-Obsidian script](https://github.com/prestonharberts/biblegateway-to-obsidian) (Note: not all translations are compatible with bib or BibleGateway-to-Obsidian). Once generated, move only the `Scripture` folder into the `bin` folder in this repository and rename it to `bible` (lowercase).

Make sure you have `perl` and `cpan` are installed on your computer using your respective package manager, then run the following:

```bash
# if first time opening just press enter to all prompts cpan will ask for
cpan
install Module::Build
install File::Rename
```

Now, run the following from this project's folder to make the files compatible with bib:

```
cd bin
chmod u+x ./bg2ob-to-bib
./bg2ob-to-bib
```

Finally, move the Bible folder to the same folder as bib, and run bib to verify that it's working.
