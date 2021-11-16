+++
title = "PIE Office: terminal based transliteration tool for ancient IE Languages"
date = "2020-09-21"
author = "Caio G"
authorTwitter = "silenus32" #do not include @
cover = ""
tags = ["scripts", "linguistics", "programming"]
description = "Release note on the `pieoffice` tool"
showFullContent = false
+++

# Introduction

As it is well known by people working with Ancient languages, it is generally hard to include in our texts textual samples written in the original scripts used in the source.
There are many ways for typing Ancient Greek, Latin with macrons, and Sanskrit in *devanāgarī*, but it requires learning a new keymap, which might take a while, and seems counterintuitive (particularly the *devanāgarī* mapping that is much more similar to a DVORAK keymap for the latin script).
Further, many local scripts do not come shipped in the main operational systems (Windows, MacOS and Linux) as a default choice, such as Luwian, Linear B, Cuneiform, Lydian, Avestan etc.
The common solution is to use transliteration schemes that arguably serve also as a way to grant access of the original text to a more general public without demanding learning a new writing system.

This solution is good enough, but I personally enjoy learning new systems and typesetting my texts to include both the source script and the romanization version, and I assume that other people interested on ancient languages do feel so themselves.
This is enough of a reason to play with programing for a while and develop *maybe-not-so-usefull* key mappings and transliteration tools.

# The pievim

Since 2017 I have been writing key mappings for my `vim` configuration, to the point that it covers 15 mappings for 14 languages (see the list on its [github page](https://github.com/caiogeraldes/pievim)).
I recently packed it as an easily installable plugin, so if you use vim and has `vim-plugged` installed, you can simply add the following lines to your `.vimrc` or other configuration file and run `PlugInstall`.
I guess I will take longer from now on to add new key mappings, so no need for rushing for updates.

```vim
call plug#begin('~/.vim/plugged')
Plug 'caiogeraldes/pievim'
" etc, etc
call plug#end()
```

The program is still a key mapping type of tool, so you must learn the mappings before typing fluently with it, but I did my best to program the simpler mapping I could.
Most of the mappings extend the rationale behind of Ancient Greek BETACODE and Sanskrit Harvard-Kyoto, but you can easily find the files in `autoload/ie/` to check my choices and edit them to your liking (keep in mind that if you change a mapping command, say `inoremap I ī` to  `inoremap ii ī` you should change the unmap command from `iunmap I` to `iunmap ii`).

# The PIE Office

Since a plugin for typing ancient IE languages in `vim` is extremely niche, I decided to convert the mappings to a *maybe-a-bit-more-useful* terminal tool, which I called `pieoffice`, available at the [Pypi repository](https://pypi.org/project/pieoffice/).
It follows the same principles of the `pievim`, but as a input > output terminal application.
If you have `pip` installed in your working environment, you can install it with:

```bash
pip install --user pieoffice
```

The update process is the same for other python modules installed by `pip` and you could install it system-wide without the flag `--user`.

The basic use is: `pieoffice convert <language> <text>`.
For example, if one would intend to convert "po-ro EQU-m 12" to Linear B script, one could simply call the following command to a terminal:

```bash
$ pieoffice convert linearb "po-ro EQU-m 12"
> 𐀡𐀫 𐂅 𐄐𐄈
```

It is simple to copy and paste such text from the terminal to the text editor of one's liking, so it is rather good for short conversions.
I still must implement the capability of reading piped information and text files for allowing conversion of longer texts, but be advised that you could import the language conversions schemes as Python modules and work with them from a python console, a `.py` script, a Jupyter Notebook etc.
The same result above could be attained by the following python script:

```python
import pieoffice.linearb as linb

text = "po-ro EQU-m 12" # which could also be a file etc

converted_text = linb.alpha_to_linearb(text)

print(text)
```

There are commands also for listing the languages available and the rules for each language, all documented in the help page of the script.


# Further additions

I would like to add transliteration schemes for Old Church Slavonic and more Indo-Iranian languages (abujidas are a bit harder to code), but it might take a while for me to do so.
Hitite is the next big challenge, so maybe in 2021.
If you feel like you could afford the time do any of this, please make a pull request, I would love to share the work involved in this project.
Besides adding new scripts it could be necessary to review some of the mappings to the languages I don't often use.
People working with these languages that feel that the transliteration scheme is unusual or plain wrong, please let me know or make a pull request.
Working with JSON or CSV databases could simplify the software quite a bit, so it might be something I do in the near future.

I would also like as I mentioned to allow the program to read files or pipes as input, but I might lack the time for such a thing in the near future.
Lastly, I plan to incorporate some of the functionalities of `pieoffice` to `pievim`, but just for funsies.


