# NFL Color Rush, 2015–2017: A Data Project

A hand-verified dataset and short data story about the NFL's Color Rush promotion, the one-color alternate uniforms worn on Thursday Night Football. It asks what 32 games, sourced audience figures, and a uniform log can and cannot tell us about audiences and accessibility.

**Live data story:** https://claude.ai/artifact/C6Jf4McrptxKEN1vVBoA9U

## Headline findings

- **Network drives audience size.** NFL Network-only games drew roughly 5–8M viewers. CBS or NBC simulcasts drew roughly 10–22M. Any uniform effect has to be measured within one group.
- **Averages move with the schedule.** Simulcast games averaged 15.9M in 2016 and 13.8M in 2017 (about −13%). 2017 also changed networks, the streaming partner, and matchups. NFL Network-only games averaged 6.7M (2015), 6.1M (2016), and 7.1M (2017) on only 3–4 games per season.
- **The documented accessibility failure was one game.** The 2015 Bills at Jets game paired all red with all green, and colorblind viewers could not tell the teams apart. The NFL said afterward that its TV test had not accounted for color blindness. For 2016 it consulted color-blindness experts, and many games put one team in white. Of the 23 games with any sourced uniform detail so far, 15 had a team in white.
- **Causal claims are not supported.** Every Thursday game after 2015 was a Color Rush game, so there is almost no clean control group.

## What's in this project

| File | What it is |
|---|---|
| `NFL_Color_Rush_Expanded_Dataset.xlsx` | The dataset (15 sheets, listed below) |
| `cvd_separation.py` | Helper that fills color-distance columns on `Accessibility_Audit` from jersey hex codes (normal, deuteranopia, protanopia) |
| `color-rush-project.html` | The data story page, built from the workbook |

### Workbook sheets

| Sheet | Purpose | Status |
|---|---|---|
| `START_HERE` | Scope, caveats, how to read blanks | Complete |
| `Game_Log_2015_2017` | 32 Thursday games: teams, scores, networks, viewership | Verified; viewership sourced for 30 of 32 |
| `Viewership_Context` | Package-level audience averages | Partial |
| `Evidence_Claims` | Findings with confidence labels and links | Ongoing |
| `Sources` | Source list | Ongoing |
| `Accessibility_Audit` | Per-game uniform detail and CVD scoring scaffold | Uniform detail for 23 of 32; **all scores blank** |
| `Audit_Rubric` | 1–5 scoring scale, procedure, calibration anchor | Complete |
| `Sentiment_Coding`, `Search_Log`, `Reliability_Check`, `Sentiment_Protocol`, `Pilot_Tally` | Reddit sentiment collection protocol and pilot tracking | Built; **no data collected** |
| `Broadcast_Criticism` | Sourced broadcaster and network-executive criticism | 2 rows |
| `Merchandise_Research` | Jersey sales | **Empty:** no verified public series |
| `Matched_Control_Games` | Non-Color Rush Thursday games | 5 candidates; strength and market fields blank |

Blank cells mean not verified or not collected, not zero.

## Data quality notes

- **Home/away and scores were corrected.** The original game log had home and away teams swapped on all 32 rows, the 2017-10-19 Chiefs–Raiders score reversed (the Raiders won 31–30), and the 2017-11-30 Washington score wrong (14, not 6). All 32 rows now match nflverse results.
- **The log has 32 games, not 33.** One row, the 2017 Thanksgiving Giants–Washington game, is not a verified Color Rush game because Thanksgiving games were exempt per Wikipedia. Treat it as a control unless uniforms are verified.
- **Viewership is secondary.** Figures are Nielsen TV viewers and household ratings as reported by Sports Media Watch and NBC press releases, not pulled from Nielsen directly. A few are reported only through later comparison articles; each row has a source link and a note. Network types differ, so compare within type.
- **Uniform facts are partly secondary.** 2015 uniforms are verified from AP. Many 2016–2017 rows rely on Wikipedia, ESPN, and team sites and are marked `partial`.

## Reproducing the checks

1. Download `games.csv` from the nflverse `nfldata` repository (`data/games.csv` on GitHub).
2. Filter to seasons 2015–2017, regular season, `weekday == "Thursday"`, and compare date, away/home team, and scores with `Game_Log_2015_2017`.
3. To compute color distances, add jersey hex codes on `Accessibility_Audit` and run:

   ```
   python cvd_separation.py NFL_Color_Rush_Expanded_Dataset.xlsx
   ```

   It simulates deuteranopia and protanopia (Machado et al. 2009, severity 1.0) and writes CIE76 distances. These are a cross-check on human scores, not a replacement: they cover jersey color only and have no validated thresholds.

## Limitations

- No causal estimate of Color Rush on ratings. There is almost no control group, and network, streaming, and matchup quality change alongside the uniforms.
- No jersey sales data. If a proxy is used, such as a Wayback Machine best-seller rank, it should be labeled as rank, not sales.
- Fan sentiment is unmeasured. The Reddit protocol is ready, but the pilot has not been run.
- Broadcaster criticism is anecdotal. One on-air case (Al Michaels, 2016) and one network-executive statement (Fox's Bill Wanger, April 10, 2018, secondhand).
- Accessibility scores are an ordinal research measure, not a clinical or accessibility standard.

## Next steps

1. Score the accessibility audit from uniform photos using a CVD simulator, with a second reviewer on about 10 games.
2. Run the 50–100 comment Reddit pilot with the thread cap and strata in `Pilot_Tally`, then expand.
3. Add team-strength, star-absence, and market fields to the control games, and add more controls.
4. Source on-air broadcaster quotes beyond the two found.

## Main sources

AP (2015 and 2016 Color Rush coverage), NPR (Nov. 13, 2015), ESPN (Nov. 2, 2017), Sports Media Watch, NBC Sports Group press releases, nflverse game results, Wikipedia (Color Rush overview), Awful Announcing, theScore. Full links are on the `Sources` and `Evidence_Claims` sheets.

## License

Not yet chosen. Add one before publishing, and check each source's terms before redistributing quoted material.
