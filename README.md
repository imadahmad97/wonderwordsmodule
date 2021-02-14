<p align="center">
  <img width="460" height="300" src="assets/main.gif">
</p>

<h1 align="center">Wonderwords</h1>
<p align="center">Generate random words and sentences with ease in python</p>
<p align="center">
  <img alt="PyPI - Downloads" src="https://img.shields.io/pypi/dm/wonderwords?style=for-the-badge">
  <img alt="Libraries.io SourceRank" src="https://img.shields.io/librariesio/sourcerank/pypi/wonderwords?style=for-the-badge">
  <img alt="PyPI - License" src="https://img.shields.io/pypi/l/wonderwords?style=for-the-badge">
</p>
<p align="center">
  <img alt="Python package build" src="https://github.com/mrmaxguns/wonderwordsmodule/workflows/Python%20package/badge.svg">
</p>
<p align="center">
  <a href="https://github.com/mrmaxguns/wonderwordsmodule">GitHub repository</a>
  | <a href="https://pypi.org/project/wonderwords">PyPI page</a>
  | <a href="https://wonderwords.readthedocs.io">Official Documentation</a>
</p>

***

Wonderwords is a python package useful for generating random words and
structured random sentences. It also comes with a colorful command line
interface for quickly generating random words. The latest version is available
[on GitHub](https://github.com/mrmaxguns/wonderwordsmodule) while the stable
version is available [on PyPI](https://pypi.org/project/wonderwords).

## Table of Contents

* [Installation](#installation)
* [Usage](#usage)
  * [The Wonderwords Python API](#the-wonderwords-python-api)
  * [The Wonderwords CLI](#the-wonderwords-cli)
* [Versioning](#versioning)
* [License](#license)
* [Contributing](#contributing)
* [Credits](#credits)

## Installation

To install the latest version of Wonderwords, use your favorite package manager
for the Python Package Index to install the ``wonderwords`` package. For example
with pip:

```bash
pip install wonderwords
```

To upgrade Wonderwords with pip use:

```bash
pip install --upgrade wonderwords
```

To verify that the installation worked, import Wonderwords in python:

```python
import wonderwords
```

If you get a `ModuleNotFound` error, make sure that you have installed
Wonderwords from the step above. For further issues,
[open a new issue from the GitHub page](https://github.com/mrmaxguns/wonderwordsmodule/issues/new/choose).

## Usage

This section will briefly describe Wonderwords useage. Since wonderwords has
a command line interface and python module, you will find two subsections.

### The Wonderwords Python API

The base random word generation class is the `RandomWord` class. You can
generate words with the `word` method:

```python
from wonderwords import RandomWord

r = RandomWord()

# generate a random word
r.word()

# random word that starts with a and ends with en
r.word(starts_with="a", ends_with="en")

# generate a random noun or adjective, by default all parts of speech are included
r.word(include_parts_of_speech=["nouns", "adjectives"])

# generate a random word between the length of 3 and 8 characters
r.word(word_min_length=3, word_max_length=8)

# generate a random word with a custom regular expression
r.word(regex=".*a")

# you can combine multiple filtering options
r.word(starts_with="ru", word_max_length=10, include_parts_of_speech=["verbs"])
```

You can also get a list of all words matching some criteria using the `filter`
method:

```python
# get a list of ALL words that start with "am"
r.filter(starts_with="am")

# you can use all the options found in the word method:
r.filter(ends_with="k", include_parts_of_speech=["verbs"], word_min_length=4)
```

You can also generate a random list of words with the `random_words` method.
This is much like the filter method, except you specify the amount of words
to return, and the words are randomly chosen. If there aren't enough words to
satisfy the amount, a `NoWordsToChooseFrom` exception is raised:

```python
# get a list of 3 random nouns
r.random_words(3, include_parts_of_speech=["nouns"])

# you can use all the options found in the word method
r.random_words(5, starts_with="o", word_min_length=10)

# if the amount of words you want to get is larger than the amount of words
# there are, a NoWordsToChooseFrom exception is raised:
r.random_words(100, starts_with="n", word_min_length=16)
# there are less than 100 words that are at least 16 letters long and start with
# n, so an exception is raised

# you can silence the NoWordsToChooseFrom exception and return all words even
# if there are less, by setting return_less_if_necessary to True
r.random_words(100, starts_with="n", word_min_length=16, return_less_if_necessary=True)
```

Generating random sentences is easy using the `RandomSentence` class:

```python
from wonderwords import RandomSentence

s = RandomSentence()

# Get a random bare-bone sentence
s.bare_bone_sentence()

# Get a random bare-bone sentence with a direct object
s.simple_sentence()

# Get a random bare-bone sentence with an adjective
s.bare_bone_with_adjective()

# Get a random sentence with a subject, predicate, direct object and adjective
s.sentence()
```

The full documentation with all information can be found at:
https://wonderwords.readthedocs.io

## The Wonderwords CLI

Wonderwords provides a command line interface, too, which can be used with the
`wonderwords` command. Usage:

```
usage: wonderwords [-h] [-w] [-f] [-l LIST] [-s {bb,ss,bba,s}] [-v]
                   [-sw STARTS_WITH] [-ew ENDS_WITH]
                   [-p {nouns,verbs,adjectives} [{nouns,verbs,adjectives} ...]]
                   [-min WORD_MIN_LENGTH] [-max WORD_MAX_LENGTH] [-r REGEX]
                   [-d DELIMITER]

optional arguments:
  -h, --help            show this help message and exit
  -w, --word, --random-word
                        generate a random word
  -f, --filter          filter a list of words matching the criteria specified
  -l LIST, --list LIST  return a list of words of a certain length
  -s {bb,ss,bba,s}, --sentence {bb,ss,bba,s}
                        return a sentence based on the structure chosen
  -v, --version         Print the version number and exit
  -sw STARTS_WITH, --starts-with STARTS_WITH
                        specify what string the random word(s) should start
                        with
  -ew ENDS_WITH, --ends-with ENDS_WITH
                        specify what string the random word(s) should end with
  -p {nouns,verbs,adjectives} [{nouns,verbs,adjectives} ...], --parts-of-speech {nouns,verbs,adjectives} [{nouns,verbs,adjectives} ...]
                        specify to only include certain parts of speech (by
                        default all parts of speech are included)
  -min WORD_MIN_LENGTH, --word-min-length WORD_MIN_LENGTH
                        specify the minimum length of the word(s)
  -max WORD_MAX_LENGTH, --word-max-length WORD_MAX_LENGTH
                        specify the maximum length of the word(s)
  -r REGEX, --regex REGEX, --re REGEX, --regular-expression REGEX
                        specify a python-style regular expression that every
                        word must match
  -d DELIMITER, --delimiter DELIMITER
                        Specify the delimiter to put between a list of words,
                        default is ', '
```

The basic commands are:

  * `-w`: generate a random word
  * `-f`: which works much like the `filter` function to return all words matching
    a certain criteria
  * `-l LIST`: get a list of `LIST` random words
  * `-s {bb,ss,bba,s}`: generate a random sentence:
    * `bb`: bare bone sentence
    * `ss`: simple sentence (bare bone sentence with direct object)
    * `bba`: bare bone sentence with adjective
    * `s`: generate a simple sentence with an adjective

# Versioning

During its early stages, Wonderwords didn't have a set versioning system and
therefore, versions before `v2.0.0-alpha` are in disarray. Starting with version
2 alpha, Wonderwords uses **sematic versioning**.

# License

Wonderwords is open source and is distributed under the MIT license. See LICENSE
for more details.

# Contributing

All contributions are welcome and we hope wonderwords will continue growing.
Start out by reading CONTRIBUTING.md for contributing guidelines and how to get
started.

# Credits

Wonderwords has been made possible thanks to the following works:

* `profanitylist.txt` from
  [RobertJGabriel/Google-profanity-words](https://github.com/RobertJGabriel/Google-profanity-words)
  under the
  [Apache-2.0 license](https://github.com/RobertJGabriel/Google-profanity-words/blob/master/LICENSE)
