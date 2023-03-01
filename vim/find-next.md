# Find next and replace same words

## How do I change same words quickly?

In vs code, I do the job with cmd + d. Is there any way to do the same thing using vim?

> *cgn

- **\***: start a search for the word under the cursor (g* if you don’t want the word boundaries)
- **c**: change
- **gn**: the next match

With the combination of this command and the dot command(.), I can repeatedly replace same words.

## Caveat

Once you replaced same words and then you want to replace another word, you need to type **\*** again. Otherwise, you would keep searching for the previous word that you don't intend.

## References

- [Select multiple words, one at a time, then replace them all](https://vi.stackexchange.com/questions/27812/select-multiple-words-one-at-a-time-then-replace-them-all)
- [Vim Find Next](https://vimtricks.com/p/vim-find-next/)
