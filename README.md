# Task 1 — Inconsistencies and duplicates

CSEN1095 Data Engineering

- **Name:** Muhamed Muhamed Muharam Mustafa
- **ID:** 58-22922

| File | |
|---|---|
| `task1.ipynb` | the cleaning, top to bottom, with outputs |
| `club_signups.csv` | the file we were given, unchanged |
| `club_signups_clean.csv` | the result: one row per student per club |

## What I did

`club_signups.csv` has 39 rows and is never edited: every fix is code in `task1.ipynb`. Looking first showed 13, 9 and 13 spellings of the 5 faculties, 3 cities and 5 clubs. I stripped and lower-cased them, mapped the rest with explicit dictionaries (Media Engineering and Technology → MET, Alex → Alexandria, El Giza → Giza, Debating → Debate, Soccer → Football), and asserted only canonical values remain. I removed extra spaces from names and title-cased them, and trimmed and lower-cased emails. I mapped the nine spellings of `fee_paid` to a boolean. `signed_up_at` mixed ISO dates with a slash format whose first part reaches 18 while the second is always 09, so the slash format is day/month; I parsed both into one datetime column. Removing the exact duplicates took 39 rows to 36. Dropping repeated sign-ups for the same student and club took 36 to 32; I kept the latest by `signed_up_at`, because each repeat is a newer version: in all four, the student came back to mark the fee as paid, so keeping the first would wrongly show them unpaid. Order matters: deduplicating before fixing club spellings still finds the 3 exact copies but only 2 of the 4 repeats, since Music/music and Debate/debate club look like different clubs, leaving 34 rows. Two different students are both called Mohamed Adel and even share an email. Both duplicate rules include `student_id`, so they were never merged; a name-based rule would have deleted 2 real sign-ups.
