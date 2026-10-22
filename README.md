# Healthcare Analytics for Doctor Visits

> **Why do some people visit a doctor more often than others?**

I used Python and a real health survey of 5,190 adults to find out which things (illness, age, gender, chronic conditions, insurance) go along with more doctor visits. The whole analysis is explained step by step in a Jupyter Notebook, so it is easy to follow even if you are new to data analytics.

---

## Quick summary

- Only **about 1 in 5 people (20%)** visited a doctor in the 2-week period.
- **Sicker people visit much more.** Illness, days of reduced activity and a worse health score all point the same way.
- **Older people and women visit more** than younger people and men.
- **Private insurance made no difference** (20% vs 20%).


## About the data

- **Source:** an Australian health survey from 1977–78.
- **Size:** 5,190 people, 13 columns, no missing values, no duplicate rows.
- **Important:** `visits` counts doctor visits in the **past 2 weeks** only.

### What each column means

| Column | Meaning |
|---|---|
| `Unnamed: 0` | Row number (just an ID, not a health measurement) |
| `visits` | Number of doctor visits in the past 2 weeks |
| `gender` | male or female |
| `age` | Age in years divided by 100 (so 0.19 means 19 years) |
| `income` | Yearly income in tens of thousands of dollars (so 0.55 means about $5,500, in 1977–78 Australian dollars) |
| `illness` | Number of illnesses in the past 2 weeks (0 to 5) |
| `reduced` | Days of reduced activity because of illness in the past 2 weeks (0 to 14) |
| `health` | General health score from a questionnaire (0 to 12). **Higher means worse health.** |
| `private` | Has private health insurance (yes/no) |
| `freepoor` | Gets free government cover because of low income (yes/no) |
| `freerepat` | Gets free government cover because of old age, disability or veteran status (yes/no) |
| `nchronic` | Has a chronic condition that does **not** limit daily activity (yes/no) |
| `lchronic` | Has a chronic condition that **does** limit daily activity (yes/no) |

> I checked these meanings against the published documentation for this dataset (the `DoctorVisits` data in the R package `AER`). A few of them differ from the simplified student guide, for example `age`, `income`, `nchronic` and `lchronic`.

---

## Analysis process

1. **Load and check the data.** 5,190 rows, no missing values, no duplicates.
2. **Clean it.**
   - Turned `age` into real years (multiplied by 100).
   - Turned `income` into dollars (multiplied by 10,000).
   - Created a `visited` column: 100 if the person visited at least once, otherwise 0.
3. **Look at the big picture.** About 80% of people had zero visits, so averages are not very useful on their own.
4. **Compare groups.** Because most people had zero visits, I compared the **% of people who visited at least once** in each group. A higher bar means that group goes to the doctor more.
5. **Make charts** for every comparison.
6. **Write the conclusion**, including what the data cannot tell us.

---

## Key findings

| Question | What I found |
|---|---|
| How many people visited? | About **20%** visited at least once. The average was only 0.3 visits per person. |
| Does illness matter? | **7%** of people with no illnesses visited, rising to **42%** for people with 5 illnesses. |
| Does reduced activity matter? | **15%** with 0 days vs **64%** with 8–14 days of reduced activity. This was the strongest signal. |
| Does the health score matter? | **15%** for the best scores vs **44%** for the worst (6–12). |
| Does age matter? | **15%** of 15–24 year olds vs **30%** of people aged 65+. The rise is steady with age. |
| Does gender matter? | Women visited more than men: **24% vs 16%**. |
| Do chronic conditions matter? | A chronic condition that limits activity roughly doubled the rate: **35% vs 18%**. |
| Does private insurance matter? | No difference: **20% vs 20%**. |
| What about free government cover? | Free cover for old age, disability or veterans: **32% vs 17%**. Free low-income cover: **9%**, but this group has only 222 people, so I would not read much into it. |

---

##  Points to be considered

- **Patterns, not proof.** These results show which groups visit more, not what causes it.
- **Same 2 weeks.** Illness and doctor visits are measured in the same 2-week period, so they are tied together.
- **Age and illness overlap.** Older people are often sicker, so simple charts cannot fully separate the two.
- **Small group.** The free low-income group has only 222 people.
- **Old and uneven sample.** The survey is from 1977–78 and had more young and old people than a typical sample, so it may not match today's population.

---

## Tools used

- **Python 3**
- **pandas** for loading, cleaning and grouping the data
- **matplotlib** for charts
- **Jupyter Notebook** for code and explanations together
