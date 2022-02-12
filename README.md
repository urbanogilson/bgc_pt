# Guia do Beej para Programação em C

Se você deseja apenas ler o guia, visite o site [Beej's Guide to C](https://beej.us/guide/bgc/).

Este repositório foi criado para que a tradução do livro para o Português esteja disponível para todos que quiserem alterar/corrigir/melhorar a tradução disponível.

## Dicionário

| Inglês | Português |
|-|-|
| string | cadeia de caracteres |
| loop | laço de repetição |

## Tradução

- [x] bgc_part_0100_boilerplate
- [x] bgc_part_0150_intro
- [ ] bgc_part_0200_var_stat
- [ ] bgc_part_0300_functions
- [ ] bgc_part_0400_pointers
- [ ] bgc_part_0500_arrays
- [ ] bgc_part_0600_strings
- [ ] bgc_part_0700_structs
- [ ] bgc_part_0725_io
- [ ] bgc_part_0750_typedef
- [ ] bgc_part_0800_pointers_2
- [ ] bgc_part_0850_malloc
- [ ] bgc_part_0900_scope
- [ ] bgc_part_1000_types_2
- [ ] bgc_part_1100_types_3
- [ ] bgc_part_1200_types_4
- [ ] bgc_part_1300_multifile
- [ ] bgc_part_1400_env
- [ ] bgc_part_1500_cpp
- [ ] bgc_part_1600_structs2
- [ ] bgc_part_1700_strings2
- [ ] bgc_part_1800_enum
- [ ] bgc_part_1900_ptrptr
- [ ] bgc_part_2000_bitwise
- [ ] bgc_part_2100_variadic
- [ ] bgc_part_2150_locale
- [ ] bgc_part_2200_unicode
- [ ] bgc_part_2300_exit
- [ ] bgc_part_2400_signal
- [ ] bgc_part_2500_vla
- [ ] bgc_part_2600_goto
- [ ] bgc_part_2700_typesv
- [ ] bgc_part_2800_arrays_2
- [ ] bgc_part_2900_jmp
- [ ] bgc_part_3000_inctype
- [ ] bgc_part_3100_complex
- [ ] bgc_part_3200_fixedint
- [ ] bgc_part_3300_time
- [ ] bgc_part_3400_threads
- [ ] bgc_part_3490_atomics
- [ ] bgc_part_3500_noreturn_align

---

# Beej's Guide to C

This is the source for Beej's Guide to C.

If you merely wish to read the guide, please visit the [Beej's Guide to
C](https://beej.us/guide/bgc/) website.

This is here so that Beej has everything in a repo and so translators
can easily clone it.

## Build Instructions

### Dependencies

* [Gnu make](https://www.gnu.org/software/make/) (XCode make works, too)
* [Python 3+](https://www.python.org/)
* [Pandoc 2.7.3+](https://pandoc.org/)
* XeLaTeX (can be found in [TeX Live](https://www.tug.org/texlive/))
* [Liberation fonts](https://en.wikipedia.org/wiki/Liberation_fonts) (sans, serif, mono)

Mac dependencies install (reopen terminal after doing this):

```
xcode-select --install                  # installs make
brew install python                     # installs Python3
brew install pandoc
brew install mactex                     # installs XeLaTeX
brew tap homebrew/cask-fonts
brew install font-liberation            # installs Liberation fonts
```

You might have to add something like this to your path to find `xelatex`:

```
PATH=$PATH:/usr/local/texlive/2021/bin/universal-darwin
```

### Build

1. Type `make` from the top-level directory.

   If you have Gnu Make, it should work fine.  Other makes might work as
   well.  Windows users might want to check out Cygwin.

2. Type `make stage` to copy all the build products and website to the
   `stage` directory.

3. There is no step three.

You can also `cd` to the `src` directory and `make`.

`make clean` cleans, and `make pristine` cleans to "original" state.

To embed your own fonts in the PDFs, see the `src/Makefile` for examples.

The `upload` target in the root `Makefile` demonstrates the build steps
for a complete release.  You'll need to change the `UPLOADDIR` macro in
the top-level `Makefile` to point to your host if you want to use that.
You're free to upload whatever versions you desire individually, as
well.

## Pull Requests

Please keep these on the scale of typo and bug fixes. That way I don't
have to consider any copyright issues when merging changes.

## TODO

* Copy code out
* Exercises
* Index
* C23