# Word Lists

This project takes several word lists and compiles them to a list of common words and a list of less common words.

## Usage

To use the word lists, `npm install @skedwards88/word_lists`.

You can import all of the words or a subset of words by length. For example `import {commonWords, uncommonWordsLen4} from "@skedwards88/word_lists";`. The exports are:

Export | Description
--- | ---
commonWords | All common words
commonWordsLen2 | All common words of length 2
commonWordsLen3 | All common words of length 3
commonWordsLen4 | All common words of length 4
commonWordsLen5 | All common words of length 5
commonWordsLen6 | All common words of length 6
commonWordsLen7 | All common words of length 7
commonWordsLen8plus | All common words of length 8+
uncommonWords | All uncommon words
uncommonWordsLen2 | All uncommon words of length 2
uncommonWordsLen3 | All uncommon words of length 3
uncommonWordsLen4 | All uncommon words of length 4
uncommonWordsLen5 | All uncommon words of length 5
uncommonWordsLen6 | All uncommon words of length 6
uncommonWordsLen7 | All uncommon words of length 7
uncommonWordsLen8plus | All uncommon words of length 8+

## Contributing

Does `compiled/commonWords.txt` include a word that you think is _not_ commonly known, or does `compiled/uncommonWords.txt` include a word that you think _is_ commonly known? Feel free to open a pull request to modify `compiled/notActuallyCommon.txt` or `compiled/notActuallyUncommon.txt`. Or, feel free to open an issue. The final word choice is up to the discretion of the repository owner.

## Development

### Raw word lists

`raw/wordnik.txt` is an opensource wordlist from [Wordnik](https://github.com/wordnik/wordlist). It contains ~200,000 entries, plus a few entries that were added as per user request.

`raw/wiki.txt` is the word frequency on Wikipedia, compiled by https://github.com/IlyaSemenov/wikipedia-word-frequency. It contains ~2.6 million entries, including non-English entries.

`raw/gutenberg.txt` is the 40,000 most common words on Project Gutenberg, as compiled in the April 16, 2006 [list by Wiktionary](https://en.wiktionary.org/wiki/Wiktionary:Frequency_lists#English).

`raw/movies.txt` is the 10,000 most common words from movies and TV, as compiled in the 2006 [list by Wiktionary](https://en.wiktionary.org/wiki/Wiktionary:Frequency_lists#English).

`LDNOOBW.txt` is the "list of dirty, naughty, obscene, and otherwise bad words" from [LDNOOBW](https://github.com/LDNOOBW/List-of-Dirty-Naughty-Obscene-and-Otherwise-Bad-Words), minus multi-word phrases, minus words not in `raw/wordnik.txt`, minus words that were subjectively deemed to be non-offensive due to a non-slang or scientific meaning, plus variations of words.

### Processed word lists

Files were processed into files that contain words that also exist in the Wordnik list but not the LDNOOBW word list.

`processed/wordnik.txt` is `raw/wordnik.txt` minus words from `LDNOOBW.txt`. `processed/wordnik_processor.py` is the script that generated this file.

`processed/gutenberg.txt` is `raw/gutenberg.txt` minus words that do not exist in `processed/wordnik.txt`. `processed/gutenberg_processor.py` is the script that generated this file.

`processed/movies.txt` is `raw/movies.txt` minus words that do not exist in `processed/wordnik.txt`. `processed/movies_processor.py` is the script that generated this file.

`processed/wiki.txt` is `raw/wiki.txt`, minus words that words that do not exist in `processed/wordnik.txt`. `processed/wiki_frequency_processor.py` is the script that generated this file.

### Compiled word lists

`compiled/commonWords.txt` consists of words that are on common to wordnik, wiki, and gutenberg AND words that are common to wordnik and movies. It omits words from `LDNOOBW.txt`. In addition, the list excludes the manually compiled `compiled/notActuallyCommon.txt` that were deemed subjectively not common and includes the manually compiled `compiled/notActuallyUncommon.txt` that were deemed subjectively not uncommon.

`compiled/uncommonWords.json` consists of all of the wordnik words that are not in `compiled/commonWords.txt`, minus words from `LDNOOBW.txt`.

Additionally, there are corresponding files for 2, 3, 4, 5, 6, 7, and 8+ letter words. For example, `compiled/uncommonWordsLen3.json` consists of all of the 3-letter words from `compiled/uncommonWords.json`.

These files were generated by `compiled/compile.py`.

To keep the package size smaller, only the compiled files are packaged. These are specified under the `files` key in `package.json`.

### Publishing

The `package.yml` workflow runs when a change is pushed to `main` or when the workflow is manually triggered. The workflow builds the files, bumps the package version, and publishes the package to npm.
