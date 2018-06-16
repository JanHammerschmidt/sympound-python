# sympound-python

This library is an implementation of the [SymSpellCompound](https://github.com/wolfgarbe/SymSpell) algorithm in Python. It was initially forked from [rcourivaud/symspellcompound](https://github.com/rcourivaud/symspellcompound) although most of the code has been rewritten.

# Installation

```
pip install sympound
```

# Documentation

If you want a quick complete example, see [example.py](example.py).

### Creating the sympound object

The first step is to create an `sympound` object, the constructor takes two main arguments:
- `distancefun` is a function that will be used to compute the distance between two strings. It takes two arguments (the two strings to compare). You typically want to use a function computing the [Damerau-Levenshtein distance](https://en.wikipedia.org/wiki/Damerau%E2%80%93Levenshtein_distance), but you can get more creative and use keyboard distances.
- `maxDictionaryEditDistance` is the maximum distance that will be pre-computed. Increasing this parameter will return more suggestions, but also make the memory print much larger

### adding dictionaries

Then some dictionaries can be added through the `load_dictionary` function, typically taking a file path as argument. The format of the dictionary is typically either a list of words (one per line), or a list of word and frequency (separated by a space). See [example-dict2.txt](example-dict2.txt) for an example.

A lot of computations happen at this stage and adding a large dictionary can easily take more than one minute, so we provide two functions to save the analyzed ductionaries as a pickle: `save_pickle` and `load_pickle`, both taking a file path as argument. Note that the pickled is gzipped.

### Lookup

Once the dictionaries are loaded, you can get suggestions for a string by calling `lookup_compound(str, edit_distance_max)`, where `str` is the string you want to analyze and `edit_distance_max` is the maximum distance you want suggestions for.

The function returns a sorted list of `SuggestItem`s, containing three fields:
- `term` being the suggested fixed string
- `distance` being the distance with the original string
- `count` being the frequency if given in the dictionary

# Copyright

The code is Copyright Esukhia, 2018, and is distributed under the [MIT License](LICENSE).