# Heathkit SB-301 Restoration Plan

A restoration plan for the Heathkit SB-301 HF amateur receiver (1966–1970). It covers which parts fail with age, a phased restoration procedure, alignment, benchmarks and maintenance. Rev. 2 is checked against the original Heath assembly manual (595-946-01).

## Files

- [`sb301-restoration-plan.md`](sb301-restoration-plan.md) — source (pandoc markdown)
- [`sb301-restoration-plan.pdf`](sb301-restoration-plan.pdf) — rendered PDF

## Build

```sh
pandoc sb301-restoration-plan.md -o sb301-restoration-plan.pdf \
  --pdf-engine=xelatex -V mainfont="DejaVu Serif"
```

## Sources

- Heath Co., *Assembly and Operation of the Heathkit SSB Receiver Model SB-301*, 595-946-01. Free scan via W5RKL.
- AF6C, "Heathkit of the Month #36: SB-301", w6ze.org
- Heath mailing list archive and the Heathkit-Radios group on groups.io
