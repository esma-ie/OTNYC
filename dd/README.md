# OTNYC: GAMS-ready files

`dd/<scenario>/` holds what the TIMES model generator needs to run a
scenario without Veda: `<scenario>.run`, the `*.dd` files it includes,
`cplex.opt` and `times2veda.vdd`. Nothing else from the Veda export is kept,
and nothing was edited by hand.

| | |
| --- | --- |
| Source workbooks | tag `comet-nyc-v16.0.1`: COMET-NYC v16.0.1 as released by the US EPA, unchanged (the Veda model `COMET_NYC_v16.0.1/`) |
| Exported with | Veda2 v5.0.0.0 (DD export of the Veda case `S1_NYC_REF`) |
| Exported | 30 Oct 2026, by ESMA |
| TIMES version targeted | v4.9.7 ([etsap-TIMES/TIMES_model](https://github.com/etsap-TIMES/TIMES_model) @ `d9a6a25`) |
| Scenarios | `s1_nyc_ref`: S1_NYC_REF, the reference scenario of COMET-NYC |
| Checksums | `manifest.json`: every file with its size and SHA-256 |

The files are byte-exact (`.gitattributes`: no line-ending conversion), so
the checksums in `manifest.json` hold on every platform. TIMES.jl's
reference harness pins this folder by the SHA-256 of `manifest.json`.
`manifest.json` is kept exactly as written at the import; its `from` and
`imported` fields record where the export was checked before it was added
here.

## Checks made before publication (30 Oct 2026)

- The Veda model the export was made from was a clone of this repository at
  tag `comet-nyc-v16.0.1`. Of its 283 tracked files, 278 were byte-identical
  to the tag (SHA-256). The other five: Veda's own settings in
  `COMET_NYC_v16.0.1/AppData/` (`Cases.json`, `Groups.json`,
  `Settings.json`, `FrontEndFormFormSettings.json`), which Veda rewrites
  when cases are defined, and `SubRES_TMPL/SubRES_TechREF_Trans.xlsx`, which
  had been re-saved: every cell of its three sheets, formulas and cached
  values, is identical to the tag; only the file's packaging differs. Veda
  also wrote two synchronisation logs in `SyncLogs/`.
- Every file is complete. `tradeparam.dd` holds a header and no data block,
  as Veda writes it for a scenario file with no records (OTNYC has no
  trade parameters). `base.dd` holds the timeslice tree, `TS_GROUP` and
  `TS_MAP`.
- The case compiles and preprocesses under TIMES v4.9.7 @ `d9a6a25` (GAMS
  54.6.1, run up to the SOLVE statement): normal completion and no
  domain-violation records. The TIMES quality checks report, as for every
  OTNYC scenario:
  - 50 `*07 SEVERE ERROR` "Defective sum of FX and UP FLO_SHAREs in Group":
    process `TPELCCR11` in regions R2-R6, vintages 2012-2055, group
    `TPELCCR11_NRGI`, whose only share is an UP share of 0.12056 for
    `TRNELC`. TIMES auto-relaxes these shares in preprocessing
    (`pp_qafs.mod`, v4.9.7) and the run continues. The data are as the US
    EPA released them.
  - 47 `*01 WARNING` "Demand: DEM commodity with missing COM_PROJ
    Projection".
- Not yet solved here. A GAMS/CPLEX reference run follows in TIMES.jl's
  reference suite ([esma-ie/TIMESjl](https://github.com/esma-ie/TIMESjl)).

The other scenarios of the EPA release (S2_NYC_REF_IRA, S3_NYC_REF_IRA_LSR,
S4_NYC_REF_IRA_LSR_CLPCA, S4a_NYC_REF_IRA_LSR_CLPCA,
S4b_NYC_REF_IRA_LSR_CLPCA, S5_NYC_NZ50) were exported and checked in the
same way on 30 Oct 2026, with the same results, and can be added to `dd/`
later.

## Running a scenario

With GAMS and the TIMES source (v4.9.7) on the include path, from
`dd/<scenario>/`:

    gams <scenario>.run idir1=<path to TIMES_model> lp=cplex

The run file uses REDUCE YES, as Veda wrote it. Any LP solver GAMS offers
can replace CPLEX.
