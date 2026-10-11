# Pineapple Games — Results Database

This directory is the canonical record of Pineapple game results.

## Files
- `games.json`: game definitions and scoring rules.
- `events.json`: individual games, weeks and races, with verified results and source notes.
- `players.json`: member identities and aliases, only as confirmed.

## Rules
1. Never invent missing scores, votes, dates or player identities.
2. Use `null` for unknown data; label unverified claims as `needs_verification`.
3. Store one event per week/race and one result per placement or answer.
4. Preserve historical entries; correct mistakes with a source note.
5. For Showdown, record poll totals and individual answers before calculating rankings.
6. For horse racing, record podium placements separately from elimination status.
7. All updates should be committed to GitHub for audit history.
8. This repository is public: do not store private member details or confidential data.

## Next
Reconcile historical Telegram screenshots and conversation records; add a Scores & Tallies page reading these JSON files. GitHub is the source of truth; the static website is read-only.
