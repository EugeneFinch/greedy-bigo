# Duel Math – 2-Player Greedy Game System

## 1. Core Mechanics

### Game Structure
- **2 Players**: Head-to-head competition  
- **3 Rounds**: Best of three rounds wins the duel  
- **8 Items**: Each with its own probability and multiplier  
- **Bot Replacement**: AI fills in if a player is absent  

### Round Flow
1. Both players place bets on any item.  
2. System randomly selects one item using weighted probabilities.  
3. Payouts are calculated according to item multipliers.  
4. **Round Winner**: Player with higher *net performance*.  
5. **Duel Winner**: Player who wins two or more rounds.  

### Scoring
```
Net Performance = (Bet Amount × Multiplier) - Bet Amount
```

- **Round Winner:** Higher net performance  
- **Duel Winner:** First to win two rounds  


## 2. Mathematical Model

### Expected Value (EV)
```
EV = (Probability × Multiplier) - 1
```
Where:
- Probability = chance of item being selected
- Multiplier = payout ratio for that item

### House Edge
```
House Edge = 1 - (Sum of all Probability × Multiplier) / Number of Items
```
Where:
- Number of Items = 8 (total betting options)  


## 3. Item System

### Final Multipliers  
*(Target: ~9–10 % House Edge, 100 % total probability)*

| Item | Probability | Multiplier | EV | p × m |
|------|--------------|-------------|----|--------------------|
| 1 | 30 % | 3.5× | +5 % | 1.05 |
| 2 | 25 % | 5.0× | +25 % | 1.25 |
| 3 | 15 % | 7.0× | +5 % | 1.05 |
| 4 | 10 % | 9.0× | −10 % | 0.90 |
| 5 | 7 % | 14.0× | −2 % | 0.98 |
| 6 | 5 % | 20.0× | 0 % | 1.00 |
| 7 | 2 % | 30.0× | −40 % | 0.60 |
| 8 | 1 % | 45.0× | −55 % | 0.45 |
| **Sum (p × m)** | 100% | — | — | **7.28** |

**Average return per $1 bet (uniform betting):**
```
R = 7.28 / 8 = 0.91
```

**House Edge:**
```
House Edge = 1 - 0.91 = 0.09 = 9%
```


## 4. PvP Duel Examples

### Round 1
```
Player A: $100 on Item 1 (30%, 3.5×)
Player B: $100 on Item 3 (15%, 7×)
Outcome: Item 1 selected.
→ A wins $350 (+$250)
→ B loses $100
Winner: A
```

### Round 2
```
Player A: $200 on Item 4 (10%, 9×)
Player B: $150 on Item 6 (5%, 20×)
Outcome: Item 6 selected.
→ A loses $200
→ B wins $3,000 (+$2,850)
Winner: B
```

### Round 3
```
Player A: $300 on Item 8 (1%, 45×)
Player B: $250 on Item 2 (25%, 5×)
Outcome: Item 2 selected.
→ A loses $300
→ B wins $1,250 (+$1,000)
Winner: B
```

**Duel Summary**
| Player | Round 1 | Round 2 | Round 3 | Net |
|---------|----------|----------|----------|------|
| A | +250 | −200 | −300 | −250 |
| B | −100 | +2850 | +1000 | **+3750** |

🏆 **Duel Winner:** Player B  

> This example illustrates variance; long-term averages converge to a 9 % house edge.

---

## 5. Comparison with Real Games
| Game | House Edge |
|-------|-------------|
| European Roulette | 2.7 % |
| American Roulette | 5.26 % |
| **Duel System** | **≈ 9 %** |

---

## 6. Bot AI System

### Bot Types
| Bot | Focus | Target Items | Strategy | Advantage vs User |
|------|--------|----------------|------------|-------------------|
| **Easy** | High-probability | 1–3 | Conservative | +2 % |
| **Medium** | Mixed | 1–5 | Balanced | +5 % |
| **Hard** | High-multiplier | 3–8 | Aggressive | +8 % |

### EV Adjustment
Baseline User EV = −9%

```
Easy Bot EV = −7%
Medium Bot EV = −4%
Hard Bot EV = −1%
```

---

## 7. Key Metrics

| Metric | Value |
|---------|--------|
| **House Edge** | ~9% |
| **Average Return** | 91% per $1 bet |
| **User EV Range** | −55% to +25% (per item) |
| **Bot EV Range** | −47% to +33% |
| **Max Multiplier** | 45× |
| **Probability Range** | 1% – 30% |
| **Total Probabilities** | 100% |

---

## 8. Optional Extensions
- **Variance analysis** – compute σ² of payouts to tune risk.
- **Provably Fair RNG** – hash-seeded roll for transparency.
- **Risk cap** – optional payout limit per round.

