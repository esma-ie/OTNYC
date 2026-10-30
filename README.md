# OTNYC: Open TIMES New York City

OTNYC is an open energy-system model of New York City, for the IEA-ETSAP
TIMES model generator. It covers the city's buildings, transport and
electricity from 2010 to 2055. It is developed and maintained by Energy
Systems Modelling Analytics Ltd (ESMA), Galway, Ireland, and published
under an open licence (CC BY-SA 4.0).

> **Status: under redevelopment.** This repository holds the US EPA's
> COMET-NYC v16.0.1 as released (tag `comet-nyc-v16.0.1`) and the
> GAMS-ready export of its reference scenario, S1_NYC_REF (`dd/`). ESMA's
> redevelopment follows as later commits.

## Not a US EPA model

OTNYC is **not developed by, maintained by, reviewed by or endorsed by the
United States Environmental Protection Agency (US EPA).** It is an
independent redevelopment by ESMA.

The US EPA's **COMET-NYC** (City-based Optimization Model for Energy
Technologies, applied to New York City) is the starting point for that
redevelopment. Everything published in this repository after that starting
point is ESMA's work, and the US EPA bears no responsibility for it.
Results produced with OTNYC are not US EPA results and should not be
presented or cited as such. Nothing in this repository uses the US EPA's
name, seal or logo to suggest endorsement.

## Lineage and provenance

| | |
| --- | --- |
| Starting point | COMET-NYC, the US EPA's TIMES model of New York City, developed by the EPA Office of Research and Development (ORD) |
| COMET-NYC version | v16.0.1, published by EPA ORD on data.gov with v15.0.9 and background data ([DOI 10.23719/1532264](https://doi.org/10.23719/1532264)); the archive's SHA-256 is recorded with its import |
| Status of the starting point | US EPA data are in the US public domain by default, "unless otherwise specified" ([EPA data licence](https://pasteur.epa.gov/license/sciencehub-license.html)) |
| Redevelopment | ESMA Ltd, from 2026 |

COMET-NYC is documented in Kaplan, P.O., Z. Carroll, M. Pied, R. Chaffanjon
and K. Vaillancourt (2025), *Documentation for application of City-based
Optimization Model for Energy Technologies (COMET) to New York City to
support metropolitan-scale air, climate, and energy planning*, US EPA,
EPA/600/R-25/135 ([DOI 10.23719/1532264](https://doi.org/10.23719/1532264)).

How provenance is kept in this repository:

1. **The original first.** The first model commit holds the COMET-NYC
   v16.0.1 files exactly as released by the US EPA, unchanged. The commit
   message names the release and gives the SHA-256 checksum of the source
   archive, and the commit is tagged `comet-nyc-v16.0.1`. The EPA archive
   holds the Veda model twice, as `COMET_NYC_v16.0.1/` and as a
   values-only copy, `COMET_NYC_v16.0.1 - just numbers/`; both are kept,
   and nothing in the archive is left out. Workbook properties and
   external links are as the US EPA released them.
2. **ESMA's changes after it.** Every change ESMA makes follows as later
   commits, so `git diff comet-nyc-v16.0.1` shows exactly how OTNYC
   differs from the US EPA's original.
3. **GAMS-ready files with their origin.** Files exported from the Veda
   workbooks for GAMS are kept in `dd/<scenario>/`. `dd/README.md` records
   how each export was made: the source commit, the Veda version, the TIMES
   version targeted and the date.

## Licence

OTNYC as distributed here, and ESMA's contributions to it, are licensed
under the Creative Commons Attribution-ShareAlike 4.0 International licence
([`LICENSE`](LICENSE), [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)).
Material that originates from the US EPA remains in the US public domain;
this licence does not restrict any use of public-domain material that the
law allows.

When you use or adapt OTNYC:

- credit "OTNYC, Energy Systems Modelling Analytics Ltd (ESMA)" and the
  original COMET-NYC model by the US EPA Office of Research and
  Development;
- link to the CC BY-SA 4.0 licence and say whether you made changes;
- share your adaptations under the same licence (ShareAlike).

OTNYC is provided as is, without warranties of any kind (section 5 of the
licence).

## Running the model

OTNYC runs with the IEA-ETSAP TIMES model generator
([etsap-TIMES/TIMES_model](https://github.com/etsap-TIMES/TIMES_model),
GPL-3.0-or-later) under GAMS and an LP solver. The Veda workbooks can be
edited with Veda; the GAMS-ready files in `dd/` need only TIMES and GAMS.

OTNYC is also one of the test models for TIMES.jl
([esma-ie/TIMESjl](https://github.com/esma-ie/TIMESjl)), an open
translation of TIMES to Julia/JuMP that is developed and tested only on
openly licensed models.
