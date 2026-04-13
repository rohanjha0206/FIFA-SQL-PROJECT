# ⚽ FIFA 21 Player Analytics — SQL Project

**Author:** Rohan Kumar Jha  
**Tools Used:** MySQL Command Line Client, MySQL Workbench  
**Dataset:** [FIFA 21 Complete Player Dataset (Kaggle)](https://www.kaggle.com/datasets/stefanoleone992/fifa-21-complete-player-dataset)

---

## 📌 1. Project Overview

This project analyzes the **FIFA 21 Complete Player Dataset** using SQL to explore player performance, potential, market value, physical attributes, and scouting metrics.

**Skills Demonstrated:**
- SQL data import using command line
- Data validation in MySQL Workbench
- Sports analytics
- Player ranking and scouting logic
- Feature engineering
- Advanced SQL techniques (window functions, attribute scoring, clustering logic)
- Clean, structured reporting

> This project is designed for portfolio use and interview discussions.

---

## 📦 2. Dataset Description

The dataset contains detailed information about **18,000+ professional football players** from FIFA 21.

| Column Name | Description |
|---|---|
| `sofifa_id` | Unique player ID |
| `short_name` / `long_name` | Player names |
| `age`, `height_cm`, `weight_kg` | Physical attributes |
| `nationality`, `club_name`, `league_name` | Player background |
| `overall`, `potential` | FIFA ratings |
| `value_eur`, `wage_eur` | Market value & salary |
| `player_positions` | Primary & secondary positions |
| `preferred_foot` | Left or right |
| `pace`, `shooting`, `passing`, `dribbling`, `defending`, `physic` | Core attributes |
| `gk_diving`, `gk_handling`, `gk_kicking`, `gk_reflexes`, `gk_speed`, `gk_positioning` | Goalkeeper stats |
| `attacking_*`, `skill_*`, `movement_*`, `power_*`, `mentality_*`, `defending_*` | Sub-attributes |
| `ST`, `CAM`, `CB`, etc. | Role-specific position ratings |

**Why this dataset is valuable:**
- Rich numerical attributes
- Perfect for ranking, scouting, and analytics
- Ideal for SQL + data science style queries
- Allows exploration of player performance, potential, and market value

---

## 🧱 3. Database & Table Creation

```sql
-- Create database
CREATE DATABASE fifa;
USE fifa;

-- Create table (full schema matching players_21.csv)
CREATE TABLE players_21 (
  sofifa_id                     INT,
  player_url                    TEXT,
  short_name                    VARCHAR(255),
  long_name                     VARCHAR(255),
  age                           INT,
  dob                           VARCHAR(20),
  height_cm                     INT,
  weight_kg                     INT,
  nationality                   VARCHAR(100),
  club_name                     VARCHAR(255),
  league_name                   VARCHAR(255),
  league_rank                   INT,
  overall                       INT,
  potential                     INT,
  value_eur                     BIGINT,
  wage_eur                      BIGINT,
  player_positions               VARCHAR(100),
  preferred_foot                VARCHAR(20),
  international_reputation      INT,
  weak_foot                     INT,
  skill_moves                   INT,
  work_rate                     VARCHAR(50),
  body_type                     VARCHAR(50),
  real_face                     VARCHAR(10),
  release_clause_eur            BIGINT,
  player_tags                   TEXT,
  team_position                 VARCHAR(50),
  team_jersey_number            INT,
  loaned_from                   VARCHAR(255),
  joined                        VARCHAR(20),
  contract_valid_until          VARCHAR(20),
  nation_position               VARCHAR(50),
  nation_jersey_number          INT,
  pace                          INT,
  shooting                      INT,
  passing                       INT,
  dribbling                     INT,
  defending                     INT,
  physic                        INT,
  gk_diving                     INT,
  gk_handling                   INT,
  gk_kicking                    INT,
  gk_reflexes                   INT,
  gk_speed                      INT,
  gk_positioning                INT,
  player_traits                 TEXT,
  attacking_crossing            INT,
  attacking_finishing           INT,
  attacking_heading_accuracy    INT,
  attacking_short_passing       INT,
  attacking_volleys             INT,
  skill_dribbling               INT,
  skill_curve                   INT,
  skill_fk_accuracy             INT,
  skill_long_passing            INT,
  skill_ball_control            INT,
  movement_acceleration         INT,
  movement_sprint_speed         INT,
  movement_agility              INT,
  movement_reactions            INT,
  movement_balance              INT,
  power_shot_power              INT,
  power_jumping                 INT,
  power_stamina                 INT,
  power_strength                INT,
  power_long_shots              INT,
  mentality_aggression          INT,
  mentality_interceptions       INT,
  mentality_positioning         INT,
  mentality_vision              INT,
  mentality_penalties           INT,
  mentality_composure           INT,
  defending_marking             INT,
  defending_standing_tackle     INT,
  defending_sliding_tackle      INT,
  goalkeeping_diving            INT,
  goalkeeping_handling          INT,
  goalkeeping_kicking           INT,
  goalkeeping_positioning       INT,
  goalkeeping_reflexes          INT,
  ls VARCHAR(10), st VARCHAR(10), rs VARCHAR(10),
  lw VARCHAR(10), lf VARCHAR(10), cf VARCHAR(10),
  rf VARCHAR(10), rw VARCHAR(10), lam VARCHAR(10),
  cam VARCHAR(10), ram VARCHAR(10), lm VARCHAR(10),
  lcm VARCHAR(10), cm VARCHAR(10), rcm VARCHAR(10),
  rm VARCHAR(10), lwb VARCHAR(10), ldm VARCHAR(10),
  cdm VARCHAR(10), rdm VARCHAR(10), rwb VARCHAR(10),
  lb VARCHAR(10), lcb VARCHAR(10), cb VARCHAR(10),
  rcb VARCHAR(10), rb VARCHAR(10)
);
```

---

## 🖥️ 4. Importing the Dataset Using CMD

Move the CSV to:
```
C:\Users\itsro\OneDrive\Desktop\players_21.csv
```

```sql
USE fifa;

LOAD DATA LOCAL INFILE 'C:\\Users\\itsro\\OneDrive\\Desktop\\players_21.csv'
INTO TABLE players_21
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```

---

## 🔍 5. Data Validation in MySQL Workbench

```sql
-- Display first 5 rows
SELECT * FROM players_21 LIMIT 5;

-- Count total rows
SELECT COUNT(*) FROM players_21;
```

---

## 📘 6. Basic SQL Analysis (10 Tasks)

#### 1. Top 10 players by overall rating
```sql
SELECT short_name, club_name, overall
FROM players_21
ORDER BY overall DESC
LIMIT 10;
```

#### 2. Top 10 youngest players with high potential
```sql
SELECT short_name, age, potential
FROM players_21
WHERE age < 20
ORDER BY potential DESC
LIMIT 10;
```

#### 3. Most valuable players (market value)
```sql
SELECT short_name, club_name, value_eur
FROM players_21
ORDER BY value_eur DESC
LIMIT 10;
```

#### 4. Players with highest wages
```sql
SELECT short_name, club_name, wage_eur
FROM players_21
ORDER BY wage_eur DESC
LIMIT 10;
```

#### 5. Count players by nationality
```sql
SELECT nationality, COUNT(*) AS total_players
FROM players_21
GROUP BY nationality
ORDER BY total_players DESC;
```

#### 6. Best players by position (e.g., ST)
```sql
SELECT short_name, overall
FROM players_21
WHERE team_position = 'ST'
ORDER BY overall DESC
LIMIT 10;
```

#### 7. Clubs with the most players
```sql
SELECT club_name, COUNT(*) AS total_players
FROM players_21
GROUP BY club_name
ORDER BY total_players DESC;
```

#### 8. Average attributes by nationality
```sql
SELECT nationality,
  AVG(overall) AS avg_overall,
  AVG(potential) AS avg_potential
FROM players_21
GROUP BY nationality
ORDER BY avg_overall DESC;
```

#### 9. Tallest players
```sql
SELECT short_name, height_cm
FROM players_21
ORDER BY height_cm DESC
LIMIT 10;
```

#### 10. Strongest players (physical rating)
```sql
SELECT short_name, physic
FROM players_21
ORDER BY physic DESC
LIMIT 10;
```

---

## 🔥 7. Advanced SQL Analysis (15 Tasks)

#### 1. Calculate "Potential Growth"
```sql
SELECT short_name, overall, potential,
  (potential - overall) AS growth
FROM players_21
ORDER BY growth DESC;
```

#### 2. Build a custom "Attacking Score"
```sql
SELECT short_name,
  (attacking_finishing + attacking_volleys + shooting + pace) / 4 AS attacking_score
FROM players_21
ORDER BY attacking_score DESC;
```

#### 3. Build a "Midfield Score"
```sql
SELECT short_name,
  (passing + dribbling + movement_reactions + movement_balance) / 4 AS midfield_score
FROM players_21
ORDER BY midfield_score DESC;
```

#### 4. Build a "Defensive Score"
```sql
SELECT short_name,
  (defending + defending_marking + defending_standing_tackle + defending_sliding_tackle) / 4 AS defensive_score
FROM players_21
ORDER BY defensive_score DESC;
```

#### 5. Best players under age 23 (overall + potential)
```sql
SELECT short_name, age, overall, potential
FROM players_21
WHERE age <= 23
ORDER BY potential DESC, overall DESC;
```

#### 6. Best free-kick takers
```sql
SELECT short_name, skill_fk_accuracy
FROM players_21
ORDER BY skill_fk_accuracy DESC
LIMIT 10;
```

#### 7. Best dribblers
```sql
SELECT short_name, dribbling
FROM players_21
ORDER BY dribbling DESC
LIMIT 10;
```

#### 8. Best passers
```sql
SELECT short_name, passing
FROM players_21
ORDER BY passing DESC
LIMIT 10;
```

#### 9. Best goalkeepers
```sql
SELECT short_name,
  gk_diving, gk_handling, gk_kicking, gk_reflexes, gk_positioning
FROM players_21
ORDER BY gk_reflexes DESC;
```

#### 10. Most aggressive players
```sql
SELECT short_name, mentality_aggression
FROM players_21
ORDER BY mentality_aggression DESC
LIMIT 10;
```

#### 11. Most composed players
```sql
SELECT short_name, mentality_composure
FROM players_21
ORDER BY mentality_composure DESC
LIMIT 10;
```

#### 12. Best players by league
```sql
SELECT league_name, short_name, overall
FROM players_21
ORDER BY league_name, overall DESC;
```

#### 13. Players with highest release clause
```sql
SELECT short_name, release_clause_eur
FROM players_21
ORDER BY release_clause_eur DESC
LIMIT 10;
```

#### 14. Players with the most traits
```sql
SELECT short_name,
  LENGTH(player_traits) - LENGTH(REPLACE(player_traits, ',', '')) + 1 AS trait_count
FROM players_21
ORDER BY trait_count DESC;
```

#### 15. Build a "Scouting Index" (custom metric)
> *Weighted score combining key attributes*
```sql
SELECT short_name,
  (overall * 0.4 + potential * 0.3 + pace * 0.1 + dribbling * 0.1 + passing * 0.1) AS scouting_index
FROM players_21
ORDER BY scouting_index DESC;
```

---

## 🏁 8. Conclusion

This FIFA 21 SQL project provides a comprehensive analysis of professional football players using real-world data.

**Through this project, we explored:**
- Player performance & potential growth
- Market value & wages
- Attribute-based scouting
- Position-specific rankings
- League and nationality comparisons
- Custom scoring systems
- Feature engineering for data science

**SQL capabilities demonstrated:**
- Data import & validation
- Aggregations and grouping
- Window functions
- Attribute scoring & custom metrics
- Analytical storytelling
