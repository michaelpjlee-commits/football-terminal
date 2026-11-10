# Liverpool refresh — picked up 10 Nov 2026

Today in this task is Tuesday 10 November 2026, the international break after 10 Premier League games. Liverpool are 4th on 18 points (W5 D3 L2), 14 scored, 10 conceded. Last league game: Crystal Palace 1–3 Liverpool, 8 Nov.

This note is what is already in the branch, and what is still open. Do not treat the open items as done.

## Done in this branch

Checked against at least two of: ESPN match summaries (`site.api.espn.com`, `totalShots` / `shotsOnTarget`), the Premier League stats API (`footballapi.pulselive.com`, season `841`, Opta `total_scoring_att` = 160, `ontarget_scoring_att` = 47), and the FBref 2026/27 Liverpool Premier League page (160 shots, 47 on target, opponent 129 shots and 35 on target).

### Team Style (`data/lfc-extras.json`, Liverpool only)

Old file: updated 28 Oct, 8 league games, through Brighton on 25 Oct. Now: updated 10 Nov, 10 league games, through Palace on 8 Nov. Other clubs’ style objects were not changed.

| Figure | Old (8 games) | New (10 games) |
| --- | --- | --- |
| Shots / on target | 123 / 39 (15.4 on target 4.9 a game) | 160 / 47 (16.0 / 4.7 a game) |
| Possession | 53.3% | 52.9% |
| Corners | 38 | 52 |
| Passes / accurate | 3,677 / 3,060 | 4,491 / 3,712 |
| Crosses | 139 | 194 |
| Long balls | 404 | 513 |
| Tackles won | 78 | 93 |
| Interceptions | 65 | 89 |
| Fouls | 110 | 146 |
| Shots faced / on target | 100 / 25 | 129 / 35 |
| Goals for / against | 11 / 8 | 14 / 10 |
| Headed shots | 13 | 21 |
| Shots in the box / outside | 71 / 52 | 103 / 57 |
| Set-piece goals | 1 (the penalty) | 2 (penalty plus Mac Allister’s 40' set-piece header at Palace) |
| Open-play goals counted in `open` | 9 | 11 |
| Fast-break goals | 1 | 2 (Isak 89' at Palace) |
| Late goals scored / conceded (76'+) | 2 / 1 | 3 / 2 (Isak 89'; Nketiah 90+5' pen) |
| Early goals (0–15') | 2 | 2 (unchanged) |
| Own goals | 1 | 1 (unchanged) |

4-2-3-1 record in the same file: was P8 W4 D3 L1, 11–8. Now P10 W5 D3 L2, 14–10. FBref lists that shape in all 10 league games.

### Shots — why the old figure was wrong

The Team Style shots number is not calculated in the page. It is `style.Liverpool.shots` in `data/lfc-extras.json`, which was the sum of ESPN’s box-score field `totalShots` (the stat labelled SHOTS) for Liverpool’s league matches.

That field is the right one. Summed through Palace it is 160, which matches Opta `total_scoring_att` (160) and FBref’s squad shot total (160). On target matches too (47). Blocked shots in Opta are 57, and 47 on target + 56 off target + 57 blocked = 160, so `totalShots` includes blocked shots rather than replacing them.

The page showed 123 because the file stopped after Brighton (25 Oct): 123 + Arsenal (1 Nov, 17) + Crystal Palace (8 Nov, 20) = 160. No change was made to the display formula (`shots / games`). The shot-zone parser used for the two new matches was checked against the stored GW1 and GW8 shot lists (0 mismatches on zone, outcome and minute) and the new matches’ event counts match ESPN `totalShots` and `shotsOnTarget` for both teams.

A scraped premierleague.com club page showed “Shots 94”. That does not match the Premier League stats API for the same season (160). 94 was not used.

### Shots tab, line-ups, formation tracker

GW9 (Liverpool 0–1 Arsenal, 1 Nov, Anfield) and GW10 (Crystal Palace 1–3 Liverpool, 8 Nov, Selhurst Park) were added under `lfc`, with ESPN commentary shots, goals, cards, subs and both XIs. Liverpool’s tactics line-up board reads this list, so those two games are selectable. No performance-score rows (`perf`) were added.

### Managers (current-season duel only)

Andoni Iraola’s game list in `cur.Liverpool` gained:

- 1 Nov, Arsenal, 0–1, Premier League
- 4 Nov, Fenerbahce, 2–3, Champions League league phase
- 8 Nov, Crystal Palace, 3–1, Premier League

Other managers’ logs were not changed. The all-time managers page was not changed.

### Injuries, and the Squad / Overview lines that read them

The live squad sheet (published Google Sheet) still had Szoboszlai as Available, 100%, with empty news, after 8 apps, 7 starts, 571 minutes, 1 goal, 1 assist. `applyLfcAvail` in `index.html` overwrites that only while the feed still says Available:

- Status: Injured. Chance left blank (not 0%).
- News: knee, off at 69' at Palace on 8 Nov, Iraola said he was not 100% at full time, a doubt for Hungary (BBC, 9 Nov). No confirmed club return date. Next league game is Man Utd at home, 22 Nov.

Same function, only while the feed text is still the old wording:

- Gravenberch: sheet said “Foot injury” and Doubt, 75%. News now says heel, day to day, missed Arsenal, Fenerbahce and Palace. The 75% was left as the player-feed figure.
- Frimpong, Bradley, Leoni, Ekitiké: still Injured with chance 0. News replaced only where it still said “Unknown return”, from Liverpool FC.com quotes (Iraola, Sep/Oct) and, for Frimpong’s possible 22 Nov return, Liverpool.com on 10 Nov.

Once the sheet itself catches up, the override does not apply.

### Strongest XI

Per-90 ratings were not recomputed. The GW1–8 table is unchanged. “Available now” uses those same ratings, drops Szoboszlai (20.3) and brings in Barcola (16.5): 212.2 (95.2%) becomes 219.2 (98.3%). The note says Muñoz is available and Gravenberch is only a doubt. The old note said Szoboszlai (hamstring) and Muñoz (knee, 25%) were both out. That Muñoz line was out of date: he played at Palace.

Chart.js script tags in the head of `index.html` were not edited.

## Still to do

Browser check of the running page was started and not finished, so none of the tabs below were clicked through. Syntax of the page script was checked with `node --check` only.

### Overview

The live sheet already has Liverpool 4th, 18 points, 14 for, 10 against, form L W W L W, after GW10 (Palace still marked provisional on the sheet). xG on that sheet is 15.87 for and 13.19 against. premierleague.com’s club page showed xG 15.82. The sheet value was left. This branch does not change overview numbers except the injury count, which will include Szoboszlai once the override runs. The saved snapshot inside `index.html` is still 20 Oct 2026 (7 games, Liverpool 5th on 12 points). It is only used when the live sheet fails. It was not updated, because it holds every club.

### Latest News

`data/news/all.json` already had Liverpool headlines through 10 Nov 2026, including the BBC line “Szoboszlai a doubt for Nations League conclusion” (9 Nov). Not edited.

### Squad

Live sheet already has 10-game counting stats. Compared with FBref and left as they are, because they are what the page loads and they were not identical:

- Minutes are within about 1–9 of FBref (for example Szoboszlai 571 vs 572, Muñoz 455 vs 459, Nyoni 223 vs 230, Ngumoha 202 vs 209).
- Goals for the players checked match (Isak 7, Wirtz 1, Mac Allister 1, Gakpo 1, Szoboszlai 1, Muñoz 2).
- Assists do not: Wirtz is 5 on the sheet and 3 on FBref. Muñoz is 1 on the sheet and 0 on FBref. No second source was pulled for assists, so the sheet values stayed.
- There is no shots column on the Premier League squad table. FBref player shots (not shown on the page): Isak 25, Wirtz 23, Mac Allister 17, Gakpo 17, Szoboszlai 15, Muñoz 13, Barcola 12, Van Dijk 6. Do not add a column unless the layout change is wanted. Sortable squad headers were not touched.

### Team Style — still open

- Passes 4,491 (sum of ESPN match `totalPasses`) vs Opta `total_pass` 4,526. Accurate passes 3,712 vs Opta 3,742. Crosses 194 vs Opta 193. Tackles won 93 vs Opta `won_tackle` 91. Interceptions 89 vs Opta 101. The file keeps the ESPN sums so they add up from the stored matches. The interception gap is the one that matters.
- Possession 52.9% is the ESPN average (Opta’s possession sum was 528.5, which is 52.85% a game).
- Radar ranks still compare this 10-game Liverpool profile with every other club frozen at 8 games (25 Oct). Those clubs were left unchanged on purpose. Ranks and “plays most like” will be off until the other 19 clubs are rebuilt the same way.
- `matches_counted` is still 80. It was not changed.

### Shots tab

GW9 and GW10 maps are in the file, but the page was not opened. GW9 has a Wirtz free-kick that hit the bar, zoned `long_l` (the commentary says a difficult angle and long range on the left). Worth a look on the pitch graphic. No `perf` rows, so Performance scan says there are no scores for those two matches.

### Fixtures

Live sheet already has GW1–GW10 results, including Palace 1–3 on 8 Nov (status “Full time (provisional)”), and the next fixture Liverpool v Man Utd, Sunday 22 Nov, 16:30. Not edited. Cup reports for Chelsea (28 Oct) and Fenerbahce (4 Nov) were already linked. Snapshot fallback is still 20 Oct, same caveat as Overview.

### Injuries

Override is written, not clicked through. Jaros is still “Knee injury - Unknown return date” on the sheet. He was not in the Liverpool FC.com or Liverpool.com pieces used here, so he was left. Van Dijk withdrew from the Netherlands squad (Sky, 9 Nov). That was not treated as a club injury.

### Stats

Team stats on the sheet already say 10 played, 14 goals, xG 15.87, xGA 13.19, 4 clean sheets, 25 yellow cards, 1 red. FBref’s squad total is 27 yellow cards. Opta `total_yel_card` is 25, which matches the sheet, so 25 was left. The Premier League stats tab does not show a shots row. Shots for this club are on Team Style.

### Managers

Only Iraola’s current log was extended. The historical ladder, head-to-heads and GW1–8 ratings table were not rebuilt. Strongest XI strength for GW9 (Nyoni started, Szoboszlai came on at 59') and GW10 was not calculated, because the bonus-point per-90 ratings were not available again.

### Sources not finished

- Fantasy Premier League `bootstrap-static` returned 403, so player status was taken from the published sheet (which is fed by that API) plus BBC, Liverpool FC.com and Liverpool.com.
- FBref HTML returned 403 from this machine. The FBref numbers used are from the page text already retrieved (standard stats, shooting, the match log of possession and formation). Per-match FBref shot logs were not re-downloaded.
- Local click-through of Overview, Latest News, Squad, Team Style, Shots, Strongest XI, Managers, Fixtures, Injuries and Stats, on the running page, is still to do.
