# FIFA World Cup Data Dictionary

Source: [Kaggle – FIFA World Cup (abecklas)](https://www.kaggle.com/datasets/abecklas/fifa-world-cup). Covers the men's World Cups from 1930 to 2014.

## Files & relationships

| File | Grain | Rows |
|---|---|---|
| `WorldCups.csv` | One row per tournament | 20 |
| `WorldCupMatches.csv` | One row per match | 836 |

- `WorldCups.Year` ↔ `WorldCupMatches.Year`
- The source dataset's `WorldCupPlayers.csv` (player line-ups and match events) has been removed from this copy.

## WorldCups.csv

| Column | Type | Description |
|---|---|---|
| Year | int | Tournament year |
| Country | text | Host country |
| Winner | text | Champion |
| Runners-Up | text | 2nd place |
| Third | text | 3rd place |
| Fourth | text | 4th place |
| GoalsScored | int | Total goals in the tournament |
| QualifiedTeams | int | Number of teams in the finals |
| MatchesPlayed | int | Number of matches played |
| Attendance | int | Total tournament attendance |

## WorldCupMatches.csv

| Column | Type | Description |
|---|---|---|
| Year | int | Tournament year |
| Datetime | text | Kick-off local date/time, e.g. `13 Jul 1930 - 15:00` |
| Stage | text | Round, e.g. `Group A`, `Group 1`, `Round of 16`, `Quarter-finals`, `Semi-finals`, `Final`, plus several names for the third-place match |
| Stadium | text | Stadium name |
| City | text | Host city |
| Home Team Name | text | Home (first-listed) team |
| Home Team Goals | int | Full-time goals for the home team, including extra time |
| Away Team Goals | int | Full-time goals for the away team, including extra time |
| Away Team Name | text | Away (second-listed) team |
| Win conditions | text | Notes on extra time or penalties, e.g. `Italy win after extra time`; blank otherwise |
| Attendance | int | Match attendance (2 missing) |
| Half-time Home Goals | int | Home goals at half-time |
| Half-time Away Goals | int | Away goals at half-time |
| Referee | text | Referee, `SURNAME Firstname (NAT)` |
| Assistant 1 | text | First assistant referee, same format |
| Assistant 2 | text | Second assistant referee, same format |
| RoundID | int | Round identifier |
| MatchID | int | Match identifier (unique) |
| Home Team Initials | text | 3-letter FIFA code for the home team |
| Away Team Initials | text | 3-letter FIFA code for the away team |

## Data quality notes

- **Blank rows (removed):** the original `WorldCupMatches.csv` ended with 3,720 empty rows (`,,,…`). They have been deleted from this copy.
- **Duplicates (removed):** the original data listed 16 of the 2014 knockout matches twice: 852 match rows, but only 836 unique `MatchID`s. The copies have been deleted, so every `MatchID` is now unique, and match counts per year agree with `WorldCups.MatchesPlayed`.
- **Encoding:** mangled team, stadium and city names have been fixed. Examples: `C�te d'Ivoire` → `Côte d'Ivoire`, `rn">Republic of Ireland` → `Republic of Ireland`, `Malm�` → `Malmö`, `Stade V�lodrome` → `Stade Vélodrome`. Some referee names still have accented characters replaced by `�`, e.g. `Bj�rn KUIPERS (NED)`.
- **Inconsistent naming:** Iran appears as both `Iran` and `IR Iran` (both use `IRN`).
- **Historical names:** teams appear under the names they had at the time, e.g. `Germany FR`, `Soviet Union`, `Czechoslovakia`, `Yugoslavia`, `Zaire`.
- **Whitespace (cleaned):** leading and trailing spaces have been removed from `Datetime`, `City` and `Win conditions`.
- **Attendance (cleaned):** `WorldCups.Attendance` originally used `.` as a thousands separator (e.g. `3.386.810`). The dots have been removed, so it is now a plain integer.
