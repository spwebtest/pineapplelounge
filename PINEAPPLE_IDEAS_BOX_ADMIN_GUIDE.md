# 🍍 Pineapple Ideas Box — Admin & Curation Guide

> **Private admin workflow documentation.** This guide is in a **public GitHub repository**. Do not put private spreadsheet URLs, edit links, email addresses, personal information, submission exports, or unpublished member responses here.

## Public suggestion form

**[🍍 Submit an Anonymous Game Idea](https://docs.google.com/forms/d/e/1FAIpQLSdqEXHXUoCfRU-o3IHCfmjkRUS4oNCgWa_YOkrYUXpjtjwqcA/viewform)**

The form is linked from [PINEAPPLE_MASTER_GAMES.md](PINEAPPLE_MASTER_GAMES.md). Members can submit ideas without supplying their names or email addresses; check Google Forms settings before claiming full anonymity.

## Where responses go

1. Open the private Google Sheets workbook linked to the form (from your own Google Drive).
2. **Form Responses 1** stores the raw form submissions. **Do not edit, delete, sort or rearrange raw response rows**, because the current sync uses their row numbers.
3. **Curated Ideas** is your working list. Each new submission is copied here automatically by the installed form-submit trigger.
4. If submissions do not appear, open **Extensions → Apps Script**, select **syncPineappleIdeas**, and click **Run**. Check the execution log for errors.

### Curated Ideas columns

| Column | Meaning | What to do |
|---|---|---|
| A — Source Row | Row number in raw responses | Leave unchanged |
| B — Date Submitted | Original submission time | Leave unchanged |
| C — Game | Game selected by member | Review |
| D — Original Idea | Member's words | Preserve |
| E — Extra Notes | Optional member comments | Preserve |
| F — Curated Idea | Your polished version | **Edit this** |
| G — Status | Review progress | **Select from dropdown** |
| H — Date Used | When idea was played | **Enter date when used** |
| I — Admin Notes | Internal planning notes | **Edit this** |

Status options: **New**, **Review**, **Approved**, **Used**, **Rejected**, **Duplicate**.

Suggested routine: filter Status = New → read the original → polish the Curated Idea → set Approved or Review → add notes → mark Used and record the date after playing. Keep one master list and filter by Game or Status as needed.

**Important:** Editing Curated Idea, Status or Admin Notes does not change the original submission. The sync adds missing rows; it does not rewrite already curated rows.

## Editing Google Form questions safely

Open the form in **edit mode** through Google Forms or Drive (not the public responder URL).

| Change | Difficulty | Script impact |
|---|---|---|
| Add/remove/reorder choices in **Which game?** dropdown | Easy | No change if question title stays the same |
| Add a new optional question | Easy | Form collects it, but current curated sync **will not copy it** until script is updated |
| Add a required question | Easy | New submissions must answer it; sync changes may be needed if you want to curate it |
| Reorder questions | Easy | Usually safe because sync matches headers by title |
| Rename **Which game?** | Caution | Update script's header matching first |
| Rename **What’s your idea?** | Caution | Update script's header matching first |
| Rename **Anything else you would like to add?** | Caution | May stop optional notes copying |
| Delete a question | Caution | Existing responses may remain in the sheet, but future data and sync expectations can change |

The current Apps Script finds the response columns by fragments of their headings: `timestamp`, `which game`, `what’s your idea`, and `anything else`. It is **not** a generic script that automatically imports every new question.

### Safest change process

1. Make a copy of the form and spreadsheet, or back up the Apps Script before major changes.
2. For a simple new game option, edit the existing dropdown without renaming the question.
3. For new, renamed or deleted questions, update the spreadsheet-bound Apps Script's `syncPineappleIdeas` mapping as needed.
4. Submit one test response using the public form link.
5. Check **Form Responses 1** and **Curated Ideas** for the correct values.
6. Check that the form-submit trigger still works. Run `installPineappleIdeasTrigger` once if it needs reinstalling.

### Managing Apps Script

The original standalone Apps Script created the form. The **spreadsheet-bound script**, accessed from the responses workbook via **Extensions → Apps Script**, contains:
- `setupPineappleIdeas`: creates/formats the Curated Ideas tab (usually only needed at setup).
- `syncPineappleIdeas`: copies new responses into the curated list.
- `installPineappleIdeasTrigger`: installs the automatic sync trigger (run once, not for every submission).

Avoid repeatedly running setup or altering the raw response structure without a backup.

## What about multiple answers for one game?

**Not implemented yet.** The current script makes **one curated row per form submission**, not one row per answer within a submission. If you later want 10 answers per round, decide whether these are ten members' responses, ten answers from one member, or ten answers curated into a game round before changing the form or script.

## Publishing approved ideas

Review and polish ideas privately first. Only copy approved game descriptions into [PINEAPPLE_MASTER_GAMES.md](PINEAPPLE_MASTER_GAMES.md) or the rules manual. Do not publish the raw response sheet or private admin notes.
