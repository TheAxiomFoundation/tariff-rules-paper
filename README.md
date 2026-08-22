# Executable tariff law

This repository contains the working paper “Executable tariff law: deterministic derivations and conformance for the 2025–26 trade shock.” The manuscript source is `paper.qmd`; the committed publication artifact is `build/paper.pdf`.

## Build

Install [Quarto](https://quarto.org/) and run from the repository root:

```sh
quarto render paper.qmd
mv paper.pdf build/paper.pdf
```

Quarto renders `paper.pdf` at the repository root; the second command replaces the committed publication artifact at `build/paper.pdf`.

## License

The manuscript is licensed under the [Creative Commons Attribution 4.0 International License](LICENSE). Bundled fonts and other third-party materials retain their own licenses; see `fonts/SOURCES.md` and `_extensions/axiom/fonts/SOURCES.md`.
