# Ligation Calculator

[![License: MIT](https://img.shields.io/badge/License-MIT-0f62fe.svg)](LICENSE)
[![No dependencies](https://img.shields.io/badge/dependencies-none-009d9a.svg)](#running-it)
[![Live demo](https://img.shields.io/badge/demo-GitHub%20Pages-8a3ffc.svg)](https://shafiqafkaar.github.io/ligation-calculator/)

A single-page calculator for setting up ligation, Gibson assembly, and homologous-recombination cloning reactions. Enter your vector and insert concentrations and lengths, pick a molar ratio, and it tells you how much of each to pipette.

**[Open the calculator →](https://shafiqafkaar.github.io/ligation-calculator/)**

No install, no dependencies, no build step, no account. One HTML file that runs in any browser and keeps working offline.

## Why

Everyone doing molecular cloning does this arithmetic, and most people do it in their head or in a spreadsheet they rebuilt from scratch. Getting the molar ratio wrong wastes a day; pipetting 0.3 µL and pretending it was accurate wastes a week. This does the calculation and tells you when the answer is not pipettable.

## What it does

- Calculates insert volume from **vector volume** or from **vector mass** — whichever you'd rather hold fixed
- Molar ratio presets (1:1, 1:2, 1:3, 1:5) plus any custom ratio
- Reports the **nanograms** of DNA in each volume, not just the microlitres
- Optional **make-up water**: give it a total reaction volume and your enzyme/buffer volume and it works out the water
- **Warns below 0.5 µL**, where air-displacement pipettes stop being trustworthy
- Shows what fraction of the reaction each component occupies
- Copies the finished scheme to your clipboard for a lab notebook
- Light and dark themes, works on a phone at the bench

## The formula

Molar amount is taken as proportional to length in base pairs, the standard bench approximation:

```
V_insert = R × (C_vector × V_vector) × L_insert / (C_insert × L_vector)
```

`R` is the molar ratio of insert to vector — for 1:3, `R = 3`.

In **vector mass** mode the vector volume is derived first, as `V_vector = m_vector / C_vector`, and then the same equation applies.

### What this ignores

Using length as a stand-in for molar mass ignores GC content and end modifications, which shift true molecular weight by a few percent. That sits well inside the tolerance of setting up a cloning reaction, but it is not a molarity measurement. If you need real molarity, measure it.

The 0.5 µL threshold is a rule of thumb for air-displacement pipettes, not a specification. Check your own pipette's accuracy at the low end of its range.

## Running it

**Online** — use the link above.

**Offline** — download `index.html` and open it. All the CSS and JavaScript are inlined; the page falls back to system fonts without a network and stays fully functional.

**On privacy** — nothing you type is transmitted, stored, or logged. There is no server, no analytics, no cookies, no `localStorage`. The calculation happens entirely in your browser, so it is fine to use with unpublished data. To be precise about the one exception: the page requests its typefaces from Google Fonts, so Google sees the IP address of anyone loading it. That is the only outbound request in the file, it carries none of your input, and deleting the three `<link>` tags in the `<head>` removes it at the cost of the typography.

A `Content-Security-Policy` is declared in the document head — `default-src 'none'` with a narrow allowlist — so the page cannot make network calls or load third-party scripts even if it were modified to try.

**On a lab computer** — copy `index.html` onto a USB stick. It needs no network, no Python, and no admin rights to run.

## Origin

This began as a Python script that prompted for the same values on the command line. It became a web page so the numbers could be adjusted without retyping all six inputs and rerunning.

One behavioural change came out of the port. The original checked volumes with an `if/elif` chain, so when the insert volume was too small a vector volume that was *also* too small never got reported — you would fix one, rerun, and only then discover the second. Both are now checked independently and reported together.

## Contributing

Issues and pull requests welcome, particularly from anyone who has been bitten by a ratio convention that differs from the one used here.

There is no build step and no toolchain: `index.html` is the whole program. Clone it, open it in a browser, edit it, refresh. If you change the calculation, please say in the PR which protocol or kit manual you are matching.

## Citing

If this saved you some time and you want to point at it, there is a [`CITATION.cff`](CITATION.cff) — GitHub renders a "Cite this repository" button from it.

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, put it on your lab's intranet.
