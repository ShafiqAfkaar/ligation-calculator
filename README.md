# Ligation Calculator

A single-page calculator for setting up ligation, Gibson assembly, and homologous-recombination cloning reactions. Enter your vector and insert concentrations and lengths, pick a molar ratio, and it tells you how much of each to pipette.

**[Open the calculator →](https://YOUR-USERNAME.github.io/ligation-calculator/)**

No install, no dependencies, no build step. One HTML file that runs in any browser and works offline.

## What it does

- Calculates insert volume from vector volume, or from vector mass — whichever you'd rather hold fixed
- Molar ratio presets (1:1, 1:2, 1:3, 1:5) plus any custom ratio
- Reports the ng of DNA in each volume, not just the microlitres
- Optional make-up water: give it a total reaction volume and your enzyme/buffer volume and it works out the water
- Warns when a volume drops below 0.5 µL, where air-displacement pipettes get unreliable
- Shows what fraction of the reaction each component occupies
- Copies the whole scheme to your clipboard for a lab notebook
- Light and dark themes

## The formula

Molar amount is taken as proportional to length in base pairs, the standard bench approximation:

```
V_insert = R × (C_vector × V_vector) × L_insert / (C_insert × L_vector)
```

Where `R` is the molar ratio of insert to vector — for 1:3, `R = 3`.

In "vector mass" mode the vector volume is derived first as `V_vector = m_vector / C_vector`, then the same equation applies.

### What this ignores

Using length as a stand-in for molar mass ignores GC content and end modifications, which shift true molecular weight by a few percent. That is well within the tolerance of setting up a cloning reaction, but it is not a molarity measurement. If you need real molarity, measure it.

## Running it

**Online:** use the link above.

**Offline:** download `index.html` and open it. Everything is inlined — the only external request is the webfont, and the page falls back to a system stack without it. Nothing is uploaded anywhere; the calculation happens entirely in your browser.

## Origin

This started as a Python script that prompted for the same values on the command line. It became a web page so the numbers could be changed without retyping all six inputs and rerunning.

One behavioural change came out of the port. The original checked volumes with an `if/elif` chain, so when the insert volume was too small a vector volume that was *also* too small never got reported — you would fix one, rerun, and only then discover the second. Both are now checked independently and reported together.

## Contributing

Issues and pull requests welcome. It is one HTML file with no build step, so editing it is just editing it.

## License

MIT — see [LICENSE](LICENSE).
