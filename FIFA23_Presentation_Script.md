# 🎤 Presentation Script — FIFA 23 Football Statistics EDA Project

> **How to use this script:** Each section is labelled with what's on screen in your notebook at that moment.
> Speak naturally — don't read word for word. Use this as your guide and talk in a conversational tone.
> Estimated total time: **10–12 minutes**

---

## OPENING — Before you start scrolling (0:00)

*Stand confidently, make eye contact, then begin.*

> "Good morning / afternoon everyone. My name is Sameer, and today I'll be presenting my mini project on **FIFA 23 Football Player Statistics Analysis** — an Exploratory Data Analysis project built using Python.
>
> Football is the most watched sport in the world, and behind every transfer decision, every squad selection, and every scouting report — there is data. So the idea behind this project was simple: take the official FIFA 23 player dataset, clean it up, and find meaningful patterns that could actually help someone — a club, a scout, or even a fantasy football player — make smarter decisions.
>
> Let me walk you through how I did that."

---

## SECTION: Project Summary (0:40)

*Scroll to the Project Summary markdown cell.*

> "So starting with the project summary — the dataset I used contains data on over **17,000 professional football players** from FIFA 23. Each player has around 29 attributes — things like their age, nationality, club, overall rating, potential, market value, wage, position, preferred foot, skill moves, and international reputation.
>
> My analysis focused on three main questions:
> — What drives a player's **overall rating**?
> — What determines a player's **market value**?
> — And which attributes can help identify **hidden talent** before they peak?
>
> The output is 10 visualisations, a correlation heatmap, and a set of recommendations — all of which I'll walk you through now."

---

## SECTION: Problem Statement (1:20)

*Point to the Problem Statement cell.*

> "The problem statement is straightforward — I wanted to **identify which variables influence player performance and market value**, and find patterns across nationality, position, age, and skill level using data analysis and visualisation.
>
> Think of it this way — if you were a football club with a limited budget, how do you know which 22-year-old to sign today who will be worth three times as much in two years? That's exactly the kind of question this analysis tries to answer."

---

## SECTION 1: Know Your Data (1:50)

*Run or show the `df.head()` output.*

> "Moving into Section 1 — Know Your Data. The first thing I always do before any analysis is just **look at the raw data**. Here I've imported the standard Python libraries — Pandas for data manipulation, NumPy for numerical operations, Seaborn and Matplotlib for visualisation.
>
> When I load the dataset and call `df.head()`, I can already see the columns — Name, Age, Nationality, Club, Overall, Potential, Value, Wage — and immediately notice something important: the **Value and Wage columns are stored as strings** with euro symbols and M or K suffixes. That's going to need cleaning before I can do any maths on them.

*Show `df.shape` output.*

> The dataset has **17,660 rows and 29 columns** — so we're working with a decently large, real-world dataset here, not a toy example.

*Show `df.info()` output.*

> And calling `df.info()` confirms the mixed data types — some columns are integers, some are objects, and a few floats. This already tells me where the wrangling work is going to be."

---

## SECTION 2: Understanding Your Variables (2:50)

*Show the variable description table.*

> "In Section 2, I documented every column properly. Rather than just knowing the names, I wanted to understand what each variable **means and how it's stored**.
>
> For example — **Overall** is a number from 43 to 91 representing a player's current ability. **Potential** is the maximum they could reach. **Special** is the sum of all individual attribute scores. **International Reputation** is rated 1 to 5.
>
> The target variables I focussed on for analysis were **Overall, Potential, and Value** — these three together tell the full story of a player: how good they are now, how good they could be, and what the market thinks they're worth."

---

## SECTION 3: Data Wrangling (3:30)

*Show the null values and the cleaning code.*

> "Section 3 is Data Wrangling — this is where I cleaned the dataset before visualising anything.

> First, I checked for **missing values**. The main nulls were in the Club column — 211 players without a club, which makes sense for free agents — and in the Release Clause column, which 1,151 players didn't have listed. Most importantly, the Loaned From column had nearly 17,000 nulls, but that's expected because most players aren't on loan. No rows needed to be dropped.

> I also confirmed there were **zero duplicate rows** in the dataset.

> The main cleaning tasks were:
> — The **Position** column had HTML span tags embedded in it — so I used a regex expression to extract just the position name like GK, CB, ST, and so on.
> — The **Value and Wage columns** had strings like €91M or €500K — I wrote a custom function to strip the symbols and convert M to millions and K to thousands, giving me clean float numbers to work with.
> — I also parsed **Height to centimetres** and **Weight to kilograms** from their string formats.
>
> After this, the data was fully clean and ready for analysis."

---

## SECTION 4: Visualisations (4:30)

*This is the longest section — spend the most time here.*

---

### Chart 1 — Overall Rating Distribution

*Show the histogram.*

> "Chart 1 is a histogram of player Overall ratings — this is the foundation of the whole analysis.
>
> What you can see is that the distribution is **roughly bell-shaped**, centred around a mean of about 66. The majority of players fall between 60 and 75. Very few — maybe the top 1% — reach above 85. That red dashed line is the mean.
>
> This tells us that elite players are genuinely rare, and that FIFA's rating scale does a good job of separating average professionals from world-class talent."

---

### Chart 2 — Top 10 Nationalities by Player Count

*Show the horizontal bar chart.*

> "Chart 2 looks at which countries produce the most players in professional football.
>
> **England tops the list with over 1,500 players**, followed by Germany and Spain. This reflects the size and depth of their domestic leagues — the Premier League, Bundesliga, and La Liga all have large squad sizes.
>
> But here's the interesting thing — having more players doesn't mean having better players. I'll show you that in the next chart."

---

### Chart 3 — Average Overall Rating by Nationality

*Show the bar chart.*

> "Chart 3 shows the **average quality** of players from each nation — only including nations with at least 50 players so the averages are statistically reliable.
>
> And what you see is that **England doesn't appear here** — despite having the most players overall, their average rating isn't high enough to make the top 10 for quality. Instead, nations like **Spain, France, Portugal, and Belgium** lead in average player quality.
>
> This tells us that some nations — particularly Spain and France — consistently produce elite-level talent through their academy systems. For a scout, this is exactly the kind of insight that tells you which talent pools to focus on."

---

### Chart 4 — Age Distribution

*Show the histogram.*

> "Chart 4 is the age distribution. Most players are between **18 and 28 years old**, with the peak around 21 to 23. The mean age is about 25.
>
> The distribution is right-skewed — meaning there's a long tail of older players, but very few remain professional above 35. Football is physically demanding and careers are short, and the data confirms this clearly."

---

### Chart 5 — Overall vs Potential (Scatter, coloured by Age)

*Show the scatter plot.*

> "Chart 5 is one of my favourites — it's a scatter plot of **Overall vs Potential, coloured by the player's age**.
>
> The red dashed diagonal line means a player has already reached their potential — their current rating equals their ceiling. Points **above** the line are players who still have room to grow.
>
> What you can clearly see is that **younger players** — the lighter, yellow dots — sit well above the diagonal. They have a big gap between where they are now and where they could be.
>
> **Older players** — the darker purple dots — cluster right along the diagonal. They've peaked.
>
> This is exactly what a talent scout would look for — a young player with high potential and a low current rating represents the best value for money."

---

### Chart 6 — Preferred Foot Distribution

*Show the pie + bar chart side by side.*

> "Chart 6 looks at preferred foot. This is a simple but revealing split — **77% of all professional footballers are right-footed** and only 23% are left-footed, which matches real-world statistics perfectly.
>
> But look at the bar chart on the right — **left-footed players actually have a slightly higher average Overall rating** than right-footed players.
>
> Why? Because left-footed players are rarer and therefore more in demand. Clubs specifically need them for left-back, left-wing, and left-midfield positions. So the best ones rise further and get better opportunities. It's a supply-and-demand effect visible directly in the data."

---

### Chart 7 — Weekly Wage vs Overall Rating

*Show the scatter plot.*

> "Chart 7 is the wage vs rating scatter plot — and this is one of the most economically interesting charts in the project.
>
> What you can see is not a straight line but an **exponential curve**. Players rated below 70 earn modest wages — typically under €10,000 per week. But once you cross the 80 rating threshold, wages shoot up dramatically — some players earning up to €450,000 per week.
>
> This means top-tier talent commands completely disproportionate pay. The curve also explains why clubs spend so aggressively in the transfer window — the difference between a rating 80 and a rating 85 player is massive in financial terms, not just performance terms."

---

### Chart 8 — Skill Moves × International Reputation Heatmap

*Show the heatmap.*

> "Chart 8 is a heatmap showing how **Skill Moves and International Reputation jointly affect average Overall rating**.
>
> Both axes go from 1 to 5 — Skill Moves on the Y axis, Reputation on the X. The darker red cells mean higher average ratings.
>
> The key insight is that **Reputation has a stronger effect than Skill Moves**. A player with 5-star reputation but only 3-star skills still has a very high average rating. Whereas 5-star skill moves alone, without the reputation, doesn't guarantee high ratings.
>
> This tells us that overall status and recognition — built through consistent performance over time — matters more to a player's rating than technical flair alone."

---

### Chart 9 — Average Overall Rating by Position

*Show the colour-coded bar chart.*

> "Chart 9 breaks down average ratings by field position — and I've colour-coded them: green for goalkeeper, blue for defenders, orange for midfielders, and red for attackers.
>
> **Goalkeepers have some of the highest average ratings** in the dataset — which makes sense because only truly elite goalkeepers make it to professional level. You don't see mediocre goalkeepers at top clubs.
>
> Central midfielders and centre-backs also perform well. Wide positions like wingers and fullbacks show slightly lower averages — not because those players are less talented, but because there's more depth and competition in those positions globally."

---

### Chart 10 — Correlation Heatmap

*Show the full correlation heatmap.*

> "And finally, Chart 10 — the correlation heatmap. This is the summary chart that ties everything together.
>
> I've looked at 11 numeric variables and plotted every pairwise correlation. The colour scale goes from blue — negative correlation — to red — strong positive correlation.
>
> The key findings here:
> — **Overall and Wage have a correlation of around 0.79** — the strongest relationship in the dataset. Better players earn significantly more.
> — **Overall and Value** are also strongly correlated at about 0.72.
> — **Special and Overall** are at 0.93 — almost perfectly correlated, which makes sense because Special is literally the sum of all attributes.
> — **Age and Value have a negative correlation** — older players are worth less on the market even if their current rating is still high.
> — **Age and Potential are negatively correlated** — confirming that the younger you are, the more room you have to grow.
>
> This heatmap is incredibly useful for machine learning — it tells us which features are the most predictive, and which ones are redundant and could cause multicollinearity."

---

## SECTION 5: Business Objective & Conclusion (9:30)

*Scroll to the final section.*

> "In Section 5 — the Business Objective — I translated all of these insights into actual recommendations.
>
> If I were advising a football club:
> — **Scout players aged 18 to 23** from France, Spain, or Brazil with a big Potential-to-Overall gap — that's your high-growth, low-cost investment window.
> — **Target players in the 75–80 Overall range** for wage efficiency — the exponential wage curve means you get much more performance per euro here than at the very top.
> — **Prioritise left-footed players** for wide positions — they're rarer, in higher demand, and statistically perform slightly better.
> — Use **International Reputation as a quick quality filter** when scouting large databases.
>
> And to summarise the whole project:
>
> We analysed over 17,000 players, cleaned messy real-world data, and produced 10 meaningful visualisations that reveal how player performance, age, nationality, position, and market value all interact with each other. The patterns we found are consistent, statistically grounded, and directly actionable."

---

## CLOSING (10:45)

> "That brings me to the end of my presentation.
>
> I hope this gave you a clear picture of how exploratory data analysis can turn raw sports data into real insights. Thank you so much for listening — I'm happy to take any questions."

---

## 💡 Tips For The Day

- **Don't memorise word for word** — understand each chart deeply and speak from that understanding.
- **Pause after showing each chart** — give the audience 2–3 seconds to look at it before you explain it.
- **Point to specific parts** of each chart when you mention numbers (e.g. point to the red line when saying "the mean is 66").
- **If someone asks a question you don't know**, say: *"That's a great point — the dataset doesn't cover that directly, but it would be an interesting extension to explore."*
- **Keep energy up during the heatmap** — it's the most data-dense chart, so slow down and be extra clear there.
