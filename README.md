# Spelling Bee (Trie-Based) — CS 351 Project 2

A completed implementation of a simplified **Spelling Bee** puzzle (in the style of the NYT game). The project focuses on building a **Trie** for fast dictionary operations and an inherited **SBTrie** class that manages game rules, scoring, and discovered words.

---

## Overview

You play with a **7-letter set**:
- 1 **central letter**
- 6 **other letters**

Your goal is to find as many valid words as possible from the currently loaded dictionary.

A valid word:
- is **4+ letters**
- **contains the central letter**
- uses only the 7 allowed letters (letters can repeat)
- exists in the dictionary
- has not been found previously

---

## Scoring + achievements

**Scoring**
- 4-letter word: **1 point**
- 5+ letters: **1 point per letter**
- **Pangram bonus**: **+7 points** if the word uses **all 7 letters**

**Achievements**
- **Pangram found**: you found at least one pangram
- **Bingo scored**: you found at least one word starting with **each** of the 7 letters (no bonus points)

---

## Project structure

This project is organized into three main files:

- `Trie.py` — generic trie for storing and searching words
- `SBTrie.py` — inherits from `Trie` and stores Spelling Bee game state
- `proj2<NetID>.py` — driver / interactive CLI (based on the provided starter)

> Note: `Trie` and `SBTrie` do **not** print anything. All user I/O happens in the driver script.

---

## Data structure design

### `Trie`
Stores a dictionary of words and supports:
- load words from file
- insert/search/remove
- clear
- get total count in **O(1)**
- list all stored words in sorted order (when needed)

### `SBTrie` (inherits from `Trie`)
`SBTrie`:
- uses the inherited trie as the **main dictionary** (“IS-A” relationship)
- contains a *second* trie for **found/discovered words** (“HAS-A” relationship)
- tracks current letters, score, pangram/bingo status, and found words

A key method is `sbWords(centralLetter, otherLetters)`, which lists all possible valid words for a letter set **without traversing the entire trie** (runtime requirement: proportional to the length of the longest valid word, not dictionary size).

---

## Interactive commands (CLI)

The driver runs an interactive menu with commands like:

1. Load a new dictionary (clears existing dictionary first)
2. Add to the existing dictionary
3. Enter a new 7-letter set (central + 6 others)
4. Show current letters
5. Attempt a word (prints points / total and tags Pangram/Bingo when achieved)
6. Show found words + totals
7. Show all possible Spelling Bee words (with lengths and Pangram marking)
8. Show help
9. Quit

Letter set input is forgiving:
- uppercase is converted to lowercase
- non-letters are ignored (e.g., `a-bcdefg` or `a,b,c,d,e,f,g`)

The set must end up as **7 unique letters** or the program reports `Invalid letter set`.

---

## How to run

1. Make sure you have Python 3.
2. Run the driver script:
   ```bash
   python3 proj2<NetID>.py
   ```
3. In the menu:
   - load a dictionary (command 1 or 2)
   - enter a letter set (command 3)
   - start guessing words (command 5)

---

## Sample letter sets

- Central: `c` — Others: `i k l p r y`
- Central: `i` — Others: `a c h n t y`
- Central: `f` — Others: `i x a b l e`

---

## Notes / constraints

- Python built-ins (lists, strings, tuples, dictionaries) are allowed.
- External data-structure classes (not written by you) are not used for the trie/game logic.
- Trie nodes avoid storing full prefix strings (store only what’s needed to traverse efficiently).
