# Duel Math – 2-Player Greedy Game System

## 1. Core Mechanics

### Game Structure

* **2 Players:** Head-to-head competition
* **3 Rounds:** Best of three rounds wins the duel
* **8 Items:** Each with its own probability and multiplier
* **Bot Replacement:** AI fills in if a player is absent

### Round Flow

1. Both players place bets on any item.
2. System randomly selects one item using weighted probabilities.
3. Payouts are calculated according to item multipliers.
4. **Round Winner:** Player with higher net performance.
5. **Duel Winner:** Player who wins two or more rounds.

### Scoring

```
Net Performance = (Bet Amount × Multiplier) - Bet Amount
```

* **Round Winner:** Higher net performance
* **Duel Winner:** First to win two rounds

---

## 2. Mathematical Model

### Expected Value (EV)

```
EV = (Probability × Multiplier) - 1
```

Where:

* Probability = chance of item being selected
* Multiplier = payout ratio for that item

### House Edge

```
House Edge = 1 - (Sum of all Probability × Multiplier) / Number of Items
```

Where:

* Number of Items = 8 (total betting options)


## 3. Item System

### Final Multipliers

*(Target ≈ 9–10 % House Edge, 100 % total probability)*

| Item          | Probability | Multiplier | EV    | p × m    |
| ------------- | ----------- | ---------- | ----- | -------- |
| 1             | 30 %        | 3.6×       | 0 %   | 1.08     |
| 2             | 25 %        | 5.0×       | 0 %   | 1.25     |
| 3             | 15 %        | 7.0×       | 0 %   | 1.05     |
| 4             | 10 %        | 8.8×       | −12 % | 0.88     |
| 5             | 7 %         | 13.2×      | −8 %  | 0.92     |
| 6             | 5 %         | 19.8×      | −10 % | 0.99     |
| 7             | 2 %         | 27.5×      | −45 % | 0.55     |
| 8             | 1 %         | 44.0×      | −56 % | 0.44     |
| **Σ (p × m)** | 100 %       | —          | —     | **7.16** |

**Average return per $1 bet (uniform betting):**

```
R = 7.16 / 8 = 0.895
```

**House Edge:**

```
House Edge = 1 - 0.895 = 0.105 = 10.5 %
```


## 4. PvP Duel Examples

### Round 1

```
Player A: $100 on Item 1 (30 %, 3.6×)
Player B: $100 on Item 3 (15 %, 7×)
Outcome: Item 1 selected.
→ A wins $360 (+ $260)
→ B loses $100
Winner: A
```

### Round 2

```
Player A: $200 on Item 4 (10 %, 8.8×)
Player B: $150 on Item 6 (5 %, 19.8×)
Outcome: Item 6 selected.
→ A loses $200
→ B wins $2 970 (+ $2 820)
Winner: B
```

### Round 3

```
Player A: $300 on Item 8 (1 %, 44×)
Player B: $250 on Item 2 (25 %, 5×)
Outcome: Item 2 selected.
→ A loses $300
→ B wins $1 250 (+ $1 000)
Winner: B
```

**Duel Summary**

| Player | Round 1 | Round 2 | Round 3 | Net       |
| ------ | ------- | ------- | ------- | --------- |
| A      | +260    | −200    | −300    | −240      |
| B      | −100    | +2820   | +1000   | **+3720** |

🏆 **Duel Winner:** Player B

> Example illustrates variance; long-term averages converge to ~10 % house edge.


## 5. Comparison with Real Games

| Game              | House Edge |
| ----------------- | ---------- |
| European Roulette | 2.7 %      |
| American Roulette | 5.26 %     |
| **Duel System**   | **≈ 10 %** |


## 6. Bot AI System

| Bot        | Focus            | Target Items | Strategy     | Advantage vs User |
| ---------- | ---------------- | ------------ | ------------ | ----------------- |
| **Easy**   | High probability | 1–3          | Conservative | +2 %              |
| **Medium** | Mixed            | 1–5          | Balanced     | +5 %              |
| **Hard**   | High multiplier  | 3–8          | Aggressive   | +8 %              |

**EV Adjustment**
Baseline User EV = −10 %

```
Easy Bot EV = −8 %
Medium Bot EV = −5 %
Hard Bot EV = −2 %
```


## 7. Risk-Control & Fairness Practices

### 1️⃣ Zero-Positive EV Design

* Keep expected value of every item ≤ 0 (neutral or negative).
* Introduce "+EV" items only for short-term events or promotions.
* Ensures no player strategy can yield sustainable positive EV.

### 2️⃣ Dynamic Balancing Factor

* Periodically recalc Σ(p×m) from real play data.
* Rescale all multipliers by `target_return / actual_return`.
* Keeps overall house edge stable (~10 %) without visible changes to players.

### 3️⃣ Small Rake Mechanism

* Apply 1–2 % rake to total duel pot before payouts.
* Smooths variance and prevents temporary positive-EV drift from player clustering.
* Rake is added to the house reserve pool for long-term stability.



## 8. Key Metrics

| Metric                  | Value           |
| ----------------------- | --------------- |
| **House Edge**          | ~10 %           |
| **Average Return**      | 90 % per $1 bet |
| **User EV Range**       | −56 % to 0 %    |
| **Bot EV Range**        | −54 % to −2 %   |
| **Max Multiplier**      | 44×             |
| **Probability Range**   | 1 % – 30 %      |
| **Total Probabilities** | 100 %           |


**Duel Math v1.2 – Balanced Edition (Zero-Positive EV + Rake)**